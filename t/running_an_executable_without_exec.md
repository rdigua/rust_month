Running an executable without exec

Jan 12, 2020

27 minute read

-   [os](https://fasterthanli.me/tags/os)
-   [assembly](https://fasterthanli.me/tags/assembly)
-   [linux](https://fasterthanli.me/tags/linux)
-   [rust](https://fasterthanli.me/tags/rust)

This article is part 2 of the series  [Making our own executable packer](https://fasterthanli.me/blog/2020/whats-in-a-linux-executable/):

[](https://fasterthanli.me/blog/2020/whats-in-a-linux-executable/)

Previously (Part 1)

What's in a Linux executable?

[](https://fasterthanli.me/blog/2020/position-independent-code/)

Next up (Part 3)

Position-independent code

In part 1, we've looked at three executables:

-   `sample`, an assembly program that prints “hi there” using the  `write`  system call.
-   `entry_point`, a C program that prints the address of  `main`  using  `printf`
-   The  `/bin/true`  executable,  _probably_  also a C program (because it's part of GNU coreutils), and which just exits with code 0.

We noticed that  `entry_point`  printed different addresses when run with GDB, but always the same address when run directly.

What happens if we run it ourselves?

Let's make  `elk`, the binary crate, our command-line “Executable & Linker Kit”, also execute the binary after it's parsed it.

```rust
// in `elk/src/main.rs`
use std::{env, error::Error, fs};

fn main() -> Result<(), Box<dyn Error>> {
    let input_path = env::args().skip(1).next().expect("usage: elk FILE");
    let input = fs::read(&input_path)?;

    println!("Analyzing {:?}...", input_path);

    let file = match delf::File::parse_or_print_error(&input[..]) {
        Some(f) => f,
        None => std::process::exit(1),
    };
    println!("{:#?}", file);

    println!("Executing {:?}...", input_path);
    use std::process::Command;
    let status = Command::new(input_path).status()?;
    if !status.success() {
        return Err("process did not exit successfully".into());
    }

    Ok(())
}

```

Let's run it a few times to compare:

```shell
$ cargo b -q && ./target/debug/elk ./samples/entry_point
Analyzing "./samples/entry_point"...
File {
    type: Dyn,
    machine: X86_64,
    entry_point: 00001040,
}
Executing "./samples/entry_point"...
main is at 0x5571c34e9139
$ cargo b -q && ./target/debug/elk ./samples/entry_point
# (cut)
main is at 0x55f7a0f27139
$ cargo b -q && ./target/debug/elk ./samples/entry_point
# (cut)
main is at 0x5605a2753139
$ cargo b -q && ./target/debug/elk ./samples/entry_point
# (cut)
main is at 0x5565093aa139

```

Mhh,  `main`  has different addresses every time. It seems like the address is always  `0x...139`  though.

Okay, so maybe C is doing funky stuff. Let's go back to something simpler - our  `hello`  program, written in assembly.

Things don't make much sense here either.

Sure, GDB and elk agree: the entry point  _is_  `0x00401000`.

```shell
$ cargo b -q && ./target/debug/elk ./samples/hello
Analyzing "./samples/hello"...
File {
    type: Exec,
    machine: X86_64,
    entry_point: 00401000,
}
Executing "./samples/hello"...
hi there
$ gdb -ex starti ./samples/hello
Starting program: /home/amos/ftl/elk/samples/hello

Program stopped.
0x0000000000401000 in _start ()

```

But  `0x401000`  is 4.004 Mib! And our executable is only 8.68 KiB!

Where  _is_  our code in the executable file, even?

Just like  `nasm`  transformed our assembly code into an object file before,  `ndisasm`  can do the reverse option: it can  _disassemble_  an X86 binary back into (somewhat) readable assembly.

We don't know where our code is in  `./samples/hello`, so.. let's just try to disassemble the  _whole file_.

```shell
$ ndisasm ./samples/hello | less
00000000  7F45              jg 0x47
00000002  4C                dec sp
00000003  46                inc si
00000004  0201              add al,[bx+di]
00000006  0100              add [bx+si],ax
00000008  0000              add [bx+si],al
0000000A  0000              add [bx+si],al
0000000C  0000              add [bx+si],al
0000000E  0000              add [bx+si],al
00000010  0200              add al,[bx+si]
(cut)

```

Okay, well… I recognize the  `7F 45 4C 46`  part - that's the ELF magic! It really is disassembling the whole file..

So if we want to find our actual code… we need to look for a  `syscall`  right?

Oh look, there's one at  `0x1019`!

```shell
0000100C  0000              add [bx+si],al
0000100E  00BA0900          add [bp+si+0x9],bh
00001012  0000              add [bx+si],al
00001014  B80100            mov ax,0x1
00001017  0000              add [bx+si],al
00001019  0F05              syscall ; 🎉
0000101B  48                dec ax
0000101C  31FF              xor di,di
0000101E  B83C00            mov ax,0x3c
00001021  0000              add [bx+si],al

```

This.. doesn't look quite right, though. I don't remember doing additions before  `syscall`. There's another one at  `0x1023`, but that's it.

Let's look at  `ndisasm`'s manual:

```
$ man ndisasm

NAME
       ndisasm - the Netwide Disassembler, an 80x86 binary file disassembler

SYNOPSIS
       ndisasm [ -o origin ] [ -s sync-point [...]] [ -a | -i ] [ -b bits ] [ -u ] [ -e hdrlen ] [ -p vendor ] [ -k
       offset,length [...]] infile

```

Huh…  `-b bits`? What's that?

```
$ man ndisasm
(cut)
       -b bits
           Specifies 16-, 32- or 64-bit mode. The default is 16-bit mode.

```

Ah. So  `ndisasm`  defaults to disassembling code as 16-bit. Well, it's a testament to how long NASM has been around I guess (since October 1996!), but I'm fairly sure we want 64-bit mode.

```
$ ndisasm -b 64 ./samples/hello | less
00000FFF  00BF01000000      add [rdi+0x1],bh
00001005  48BE002040000000  mov rsi,0x402000
         -0000
0000100F  BA09000000        mov edx,0x9
00001014  B801000000        mov eax,0x1
00001019  0F05              syscall
0000101B  4831FF            xor rdi,rdi
0000101E  B83C000000        mov eax,0x3c
00001023  0F05              syscall
00001025  0000              add [rax],al
00001027  0000              add [rax],al
00001029  0000              add [rax],al
0000102B  0000              add [rax],al

```

AhAH! What have we here… It's  _most_  of our assembly code, except it's missing the  `mov rdi, 1`.

Well, the second instruction starts at  `0x00001005`, maybe if we ask  `ndisasm`  to start at  `0x00001000`  we'll get a different result?

```
$ man ndisasm
(cut)

       -k offset,length
           Specifies that length bytes, starting from disassembly offset offset, should be skipped over without
           generating any output. The skipped bytes still count towards the calculation of the disassembly offset.

```

Interesting! Let's go:

```
$ ndisasm -b 64 -k 0,$((0x1000)) ./samples/hello | head
00000000  skipping 0x1000 bytes
00001000  BF01000000        mov edi,0x1
00001005  48BE002040000000  mov rsi,0x402000
         -0000
0000100F  BA09000000        mov edx,0x9
00001014  B801000000        mov eax,0x1
00001019  0F05              syscall
0000101B  4831FF            xor rdi,rdi
0000101E  B83C000000        mov eax,0x3c
00001023  0F05              syscall

```

Heyyyy that's better!

![](https://fasterthanli.me/img/common/bear.svg)What did we learn?

Using  `ndisasm`, we were able to disassemble the  `hello`  executable and obtain  `hello.asm`  (more or less). It defaults to 16-bit mode so we have to specify  `-b 64`.

The offset at which we start disassembling matters, as x86 instructions are variable-length. In our case, it started at  `0x1000`  into the file.

I can't help but notice something interesting - our code is at  `0x1000`  into the file, and the entry point was  `0x401000`. Coincidence? I think not.

Note that  `ndisasm`  will happily disassemble standard input if we pass  `-`  as a file name. So we can use another program to do our cutting:

```shell
$ dd if=./samples/hello skip=$((0x1000)) bs=1 count=$((0x25)) | ndisasm -b 64 -
37+0 records in
37+0 records out
37 bytes copied, 8,191e-05 s, 452 kB/s
00000000  BF01000000        mov edi,0x1
00000005  48BE002040000000  mov rsi,0x402000
         -0000
0000000F  BA09000000        mov edx,0x9
00000014  B801000000        mov eax,0x1
00000019  0F05              syscall
0000001B  4831FF            xor rdi,rdi
0000001E  B83C000000        mov eax,0x3c
00000023  0F05              syscall

```

In fact, we could even read the code from rust and pipe it to  `ndisasm`. Let's do that!

![](https://fasterthanli.me/img/common/bear-glasses.svg)Cool bear's hot tip

We're making  `hello`-specific modifications to  `elk`  for now. We'll fix it later.

Pinky promise.

```rust
// in `elk/src/main.rs`

fn main() -> Result<(), Box<dyn Error>> {
    // omitted: analysis part

    println!("Disassembling {:?}...", input_path);
    let code = &input[0x1000..];
    // disassemble at most 0x25 bytes
    let code = &code[..std::cmp::min(0x25, code.len())];
    ndisasm(code)?;

    Ok(())
}

fn ndisasm(code: &[u8]) -> Result<(), Box<dyn Error>> {
    use std::{
        io::Write,
        process::{Command, Stdio},
    };

    let mut child = Command::new("ndisasm")
        .arg("-b")
        .arg("64")
        .arg("-")
        .stdin(Stdio::piped())
        .stdout(Stdio::piped())
        .spawn()?;
    child.stdin.as_mut().unwrap().write_all(code)?;
    let output = child.wait_with_output()?;
    println!("{}", String::from_utf8_lossy(&output.stdout));

    Ok(())
}

```

And then we get this:

```rust
cargo b -q && ./target/debug/elk ./samples/hello
Analyzing "./samples/hello"...
File {
    type: Exec,
    machine: X86_64,
    entry_point: 00401000,
}
Disassembling "./samples/hello"...
00000000  BF01000000        mov edi,0x1
00000005  48BE002040000000  mov rsi,0x402000
         -0000
0000000F  BA09000000        mov edx,0x9
00000014  B801000000        mov eax,0x1
00000019  0F05              syscall
0000001B  4831FF            xor rdi,rdi
0000001E  B83C000000        mov eax,0x3c
00000023  0F05              syscall

```

Neat!

So, now we have some executable code in memory somewhere.

And while  `elk`  is running  `elk's`  code is  _also_  in memory somewhere - being executed.

Could we.. maybe.. find a way to jump from  `elk's`  code to  `sample's`  code?

We've already seen  [how to bind Win32 APIs](https://fasterthanli.me/blog/2019/making-our-own-ping-2/). The short version is that if you have a pointer that's the address of a function, you can just cast it to a function pointer, and call it. Just like that:

```rust
// in `elk/src/main.rs`

unsafe fn jmp(addr: *const u8) {
    let fn_ptr: fn() = std::mem::transmute(addr);
    fn_ptr();
}

```

That's it! That's all there is to it.

So, logically, we should be able to just do that:

```rust
// in `elk/src/main.rs`
fn main() -> Result<(), Box<dyn Error>> {
    // omitted: everything else

    println!("Executing {:?} in memory...", input_path);
    let entry_point = code.as_ptr();
    println!("Entry point: {:?}", entry_point);
    unsafe {
        jmp(entry_point);
    }

    Ok(())
}

```

Easy! Eaasy. This series will be so short. I don't even need to check the result, I'm sure this will just work. Unless it doesn't. But it'll work! I guarantee it.

Ok, I can tell you don't believe me, so just to convince you, let's run it:

```rust
cargo b -q && ./target/debug/elk ./samples/hello
Analyzing "./samples/hello"...
(cut)

Executing "./samples/hello" in memory...
Entry point: 0x5586c7d35ac0
[1]    14095 segmentation fault (core dumped)  ./target/debug/elk ./samples/hello

```

Okay well. I give up. There. You can finish the series yourself.

![](https://fasterthanli.me/img/common/bear-glasses.svg)Cool bear's hot tip

Psssst!

Not all memory is the same.

What's that cool bear? Not all memory is the same? Sure it is! It's just bytes. Doesn't matter what the physical memory modules are, they all behave the same way, just with different performance characteristics. I can tell that this should work because THOSE ARE THE SAME BYTES THE PROCESSOR WAS RUNNING EARLIER.

And I know it's valid machine code because I just disassembled it and it gave me the original assembly, more or less.

![](https://fasterthanli.me/img/common/bear-glasses.svg)Cool bear's hot tip

Think about security.

Mhhhh. How would security get in the way of what we're trying to do…

Let's say we take our  `entry_point.c`  program. If we have a local variable, we can read from it and write to it, right?

```c
// in `elk/samples/entry_point.c`

#include <stdio.h>

int main() {
    printf("main is at %p\n", &main);
    int numb = 13;
    printf("numb is at %p\n", &numb);
    numb = 127;
    printf("wrote to numb, now = %d\n", numb);
}

```

```shell
$ gcc entry_point.c -o entry_point
$ ./entry_point
main is at 0x55a990a01149
numb is at 0x7ffedf17a274
wrote to numb, now = 127

```

Right! It appears to be stored somewhere completely different from  `main`  though

-   44 terabytes apart in the address space. I don't have 44 terabytes of RAM so… there must be different.. areas?

![](https://fasterthanli.me/img/running-an-executable-without-exec/memory-areas.png)

Of course, this isn't to scale. That next diagram isn't to scale either - you have to imagine the purple and yellow areas being much, much thinner. But this is pretty much what  `entry_point`'s address space looks like - from what I gather.

![](https://fasterthanli.me/img/running-an-executable-without-exec/memory-areas-linear.png)

What if we allocate memory with  `malloc`? And what about constants?

```c
// in `elk/samples/entry_point.c`

#include <stdio.h>
#include <stdlib.h>

const int cons = 29;

int main() {
    printf("main is at %p\n", &main);
    int numb = 13;
    printf("numb is at %p\n", &numb);
    void *aptr = malloc(sizeof(int));
    printf("cons is at %p\n", &cons);
    printf("aptr is at %p\n", aptr);
    free(aptr);
}

```

```shell
$ gcc entry_point.c -o entry_point
$  ./entry_point
main is at 0x5593c22b5169
numb is at 0x7ffeb6f9a80c
cons is at 0x5593c22b8048
aptr is at 0x5593c39386b0

```

Huh. So we have something like:

![](https://fasterthanli.me/img/running-an-executable-without-exec/memory-areas-linear2.png)

Can we write to those? Let's try writing to a constant:

```c
// in `elk/samples/entry_point.c`

#include <stdio.h>
#include <stdlib.h>

const int cons = 29;

int main() {
    int *cons_addr = (int *) &cons;
    printf("cons = %d\n", *cons_addr);
    printf("writing to cons...\n");
    // note: `cons = 31` doesn't compile
    *cons_addr = 31;
    printf("cons = %d\n", *cons_addr);
}

```

```shell
$ gcc entry_point.c -o entry_point
$ ./entry_point
cons = 29
writing to cons...
[1]    2598 segmentation fault (core dumped)  ./entry_point

```

Ah. It appears we can't - the program crashes if we try that.

Can we write to  `main`?

```c
// in `elk/samples/entry_point.c`

#include <stdio.h>
#include <stdlib.h>

int main() {
    int *main_addr = (int *) &main;
    printf("main = %x\n", *main_addr);
    printf("writing to main...\n");
    *main_addr = 0xABCD;
    printf("cons = %x\n", *main_addr);
}

```

```shell
$ gcc entry_point.c -o entry_point
$ ./entry_point
main = e5894855
writing to main...
[1]    2848 segmentation fault (core dumped)  ./entry_point

```

Read-only too. Makes sense that they're in the same area then!

What if we store some x86 binary in a constant? Since it seems to be in the same area as  `main`, maybe it'll execute from there?

We know that this assembly:

```x86asm
    xor rdi, rdi
    mov eax, 0x3c
    syscall

```

Corresponds to this in binary:

```raw
4831FF
B83C000000
0F05

```

So we can do this:

```
#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>

const char *instructions = "\x48\x31\xFF\xB8\x3C\x00\x00\x00\x0F\x05";

int main() {
    printf("        main @ %p\n", &main);
    printf("instructions @ %p\n", instructions);
    void (*f)(void) = (void*) instructions;
    printf("jumping...\n");
    f();
    printf("after jump\b");
}

```

```shell
$ gcc entry_point.c -o entry_point
$ ./entry_point
        main @ 0x5648dfe6d149
instructions @ 0x5648dfe6e004
jumping...
[1]    3978 segmentation fault (core dumped)  ./entry_point

```

Well, that still doesn't work. Apparently  `0x1000`  bytes make all the difference.

At this point, we have a  _pretty strong_  suspicion that all memory is not, in fact, the same, and that we have different memory areas with different.. permissions?

![](https://fasterthanli.me/img/running-an-executable-without-exec/memory-areas2.png)

Maybe there's a way to inspect that at runtime, let's do some research… mhh,  [what do we have here](https://linux.die.net/man/1/pmap):

```raw
Name

pmap - report memory map of a process

Synopsis

pmap [ -x | -d ] [ -q ] pids...
pmap -V

Description

The pmap command reports the memory map of a process or processes.

```

Interesting!

Our programs are too short-lived though - we won't have time to run  `pmap`  before they exit. We could get them to sleep or wait for user input… or we could just use gdb!

```shell
$ gdb ./entry_point
(gdb) starti
Starting program: /home/amos/ftl/elk/samples/entry_point

Program stopped.
0x00007ffff7fd4100 in _start () from /lib64/ld-linux-x86-64.so.2
(gdb) info proc
process 4086
cmdline = '/home/amos/ftl/elk/samples/entry_point'
cwd = '/home/amos/ftl/elk/samples'
exe = '/home/amos/ftl/elk/samples/entry_point'

```

So now, if we run  `pmap`  on process  `4086`…

```shell
$ pmap 4086
4086:   /home/amos/ftl/elk/samples/entry_point
0000555555554000      4K r---- entry_point
0000555555555000      4K r-x-- entry_point
0000555555556000      4K r---- entry_point
0000555555557000      8K rw--- entry_point
00007ffff7fce000     12K r----   [ anon ]
00007ffff7fd1000      4K r-x--   [ anon ]
00007ffff7fd2000      8K r---- ld-2.30.so
00007ffff7fd4000    124K r-x-- ld-2.30.so
00007ffff7ff3000     32K r---- ld-2.30.so
00007ffff7ffc000      8K rw--- ld-2.30.so
00007ffff7ffe000      4K rw---   [ anon ]
00007ffffffde000    132K rw---   [ stack ]
ffffffffff600000      4K --x--   [ anon ]
 total              348K

```

We were right!

I recognize our  `0x55555555....`  addresses, and our  `00007ffff7f.....`  addresses from before. And there are permissions!

Let's keep running the program in GDB:

```shell
(gdb) c
Continuing.
        main @ 0x555555555149
instructions @ 0x555555556004
jumping...

Program received signal SIGSEGV, Segmentation fault.
0x0000555555556004 in ?? ()

```

So:

-   `main`  is in the  `0x0000555555555000`  4K area, which is  `r+x`  (readable and executable)
-   `instructions`  is in the  `0000555555556000`  4K area, which is  `r`  (readable, but  _not_  executable)

This explains everything! I think! Thanks cool bear!

![](https://fasterthanli.me/img/common/bear-glasses.svg)Cool bear's hot tip

You're welcome, pay it forward.

We can see in  `pmap`'s output that those areas have  `entry_point`  as a value in the  `Mapping`  column. And that makes sense! The executable is mapped directly in memory - we discussed this in  [Reading files the hard way - Part 2](https://fasterthanli.me/blog/2019/reading-files-the-hard-way-2/).

I'm not super fond of the way  `pmap`  shows this information though. Maybe we can find another way to get it?

```shell
$ man 5 proc
(cut)

    /proc/[pid]/maps
              A file containing the currently mapped memory regions and their access permissions.  See mmap(2) for some further information about memory mappings.

```

That looks promising, let's give it a shot!

```shell
$ cat /proc/4086/maps
address                   perms offset  dev   inode                      pathname
555555554000-555555555000 r--p 00000000 08:01 3291229                    /home/amos/ftl/elk/samples/entry_point
555555555000-555555556000 r-xp 00001000 08:01 3291229                    /home/amos/ftl/elk/samples/entry_point
555555556000-555555557000 r--p 00002000 08:01 3291229                    /home/amos/ftl/elk/samples/entry_point
555555557000-555555558000 r--p 00002000 08:01 3291229                    /home/amos/ftl/elk/samples/entry_point
555555558000-555555559000 rw-p 00003000 08:01 3291229                    /home/amos/ftl/elk/samples/entry_point
555555559000-55555557a000 rw-p 00000000 00:00 0                          [heap]
7ffff7dcb000-7ffff7df0000 r--p 00000000 08:01 800108                     /usr/lib/libc-2.30.so
7ffff7df0000-7ffff7f3d000 r-xp 00025000 08:01 800108                     /usr/lib/libc-2.30.so
7ffff7f3d000-7ffff7f87000 r--p 00172000 08:01 800108                     /usr/lib/libc-2.30.so
7ffff7f87000-7ffff7f88000 ---p 001bc000 08:01 800108                     /usr/lib/libc-2.30.so
7ffff7f88000-7ffff7f8b000 r--p 001bc000 08:01 800108                     /usr/lib/libc-2.30.so
7ffff7f8b000-7ffff7f8e000 rw-p 001bf000 08:01 800108                     /usr/lib/libc-2.30.so
7ffff7f8e000-7ffff7f94000 rw-p 00000000 00:00 0
7ffff7fce000-7ffff7fd1000 r--p 00000000 00:00 0                          [vvar]
7ffff7fd1000-7ffff7fd2000 r-xp 00000000 00:00 0                          [vdso]
7ffff7fd2000-7ffff7fd4000 r--p 00000000 08:01 795305                     /usr/lib/ld-2.30.so
7ffff7fd4000-7ffff7ff3000 r-xp 00002000 08:01 795305                     /usr/lib/ld-2.30.so
7ffff7ff3000-7ffff7ffb000 r--p 00021000 08:01 795305                     /usr/lib/ld-2.30.so
7ffff7ffc000-7ffff7ffd000 r--p 00029000 08:01 795305                     /usr/lib/ld-2.30.so
7ffff7ffd000-7ffff7ffe000 rw-p 0002a000 08:01 795305                     /usr/lib/ld-2.30.so
7ffff7ffe000-7ffff7fff000 rw-p 00000000 00:00 0
7ffffffde000-7ffffffff000 rw-p 00000000 00:00 0                          [stack]
ffffffffff600000-ffffffffff601000 --xp 00000000 00:00 0                  [vsyscall]

```

Interesting - there's a device number and an inode number in there. We can use  `ls`  to check that we're indeed talking about the same file:

```shell
$ ls -i ./entry_point
3291229 ./entry_point

```

It is!

So, the file is mapped.. and then a process is created with multiple memory mappings, and then it's started. All good so far.

Quick question: what happens if we remove the file that's currently mapped?

Right now, we can use  `debugfs`  to print the path of the file that corresponds to inode  `3291229`:

```shell
$ sudo debugfs -R "ncheck 3291229" /dev/sda1
debugfs 1.45.4 (23-Sep-2019)
Inode   Pathname
3291229 /home/amos/ftl/elk/samples/entry_point

```

What if we remove it?

```shell
$ rm entry_point

```

Huh, that worked. What do the memory maps look like now?

```shell
$ cat /proc/4086/maps | head -3
555555554000-555555555000 r--p 00000000 08:01 3291229                    /home/amos/ftl/elk/samples/entry_point (deleted)
555555555000-555555556000 r-xp 00001000 08:01 3291229                    /home/amos/ftl/elk/samples/entry_point (deleted)
555555556000-555555557000 r--p 00002000 08:01 3291229                    /home/amos/ftl/elk/samples/entry_point (deleted)

```

Still the same! But the kernel knows (the kernel always knows) that the file was deleted.

So, if we compile  `entry_point.c`  again:

```shell
$ gcc entry_point.c -o entry_point
$ ls -i ./entry_point
3291247 ./entry_point

```

It gets a different inode! And if we fire off a second gdb instance on the new executable and compare their mappings, we get:

```shell
$ diff --unified /proc/{4086,5199}/maps | bat

```

![](https://fasterthanli.me/img/running-an-executable-without-exec/diff-maps.png)

![](https://fasterthanli.me/img/common/bear-glasses.svg)Cool bear's hot tip

In at least  `bash`  and  `zsh`  (and probably others), the  `a{b,c,d}e`  syntax is expanded to  `abe ace ade`.

The  [bat utility](https://crates.io/crates/bat)  is a rust reimagining of the  `cat`  utility, which you can grab with  `cargo install bat`. We use it here only for color.

So that's how it's legal to delete an executable that is currently running under Linux. The same thing is  _way_  illegal on Windows. Renaming a running Windows executable is okay though. I guess their memory mapping strategy is different!

Back to our regularly-scheduled instruction fiddling. So we have the right instructions in memory, but we need to make that memory  **executable**. Just like we need to  `chmod +x`  a file before running it from the shell or something.

We can do that with  `mprotect`:

```shell
$ man mprotect
NAME
       mprotect — set protection of memory mapping

SYNOPSIS
       #include <sys/mman.h>

       int mprotect(void *addr, size_t len, int prot);

```

So far so good - an address, a length, and some flags. We've got  `PROT_READ`,  `PROT_WRITE`, and  `PROT_EXEC`. Like a good Unix C function, it returns  `0`  on success,  `-1`  on error.

![](https://fasterthanli.me/img/common/bear-glasses.svg)Cool bear's hot tip

In C,  `size_t`  is an integral data type (ie., it stores integers) of the same bit-width as a pointer. So, on 32-bit,  `size_t`  is 4 bytes, on 64-bit,  `size_t`  is 8 bytes.

C has  `size_t`  (unsigned) and  `ssize_t`  (signed), Rust has  `usize`  and  `isize`.

Cool, let's get going:

```c
// in `elk/samples/entry_point.c`

#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>

#include <sys/mman.h>
#include <errno.h>

const char *instructions = "\x48\x31\xFF\xB8\x3C\x00\x00\x00\x0F\x05";
const size_t instructions_len = 10;

int main() {
    printf("        main @ %p\n", &main);
    printf("instructions @ %p\n", instructions);

    printf("making instructions executable...\n");
    int ret = mprotect(
        (void*) instructions, // addr
        instructions_len,     // len
        PROT_READ | PROT_EXEC // prot
    );
    if (ret != 0) {
        printf("mprotect failed: error %d\n", errno);
        return 1;
    }

    void (*f)(void) = (void*) instructions;
    printf("jumping...\n");
    f();
    printf("after jump\b");
}

```

Now this is starting to look like a  _real_  C program, low-cost error handling and all.

```shell
$ gcc entry_point.c -o entry_point
$ ./entry_point
./entry_point
        main @ 0x55f68b710169
instructions @ 0x55f68b711008
making instructions executable...
mprotect failed: error 22

```

Ah. Error 22 happens to be  `EINVAL`, and  `mprotect`'s man page notes:

```shell
ERRORS
(cut)
       The mprotect() function may fail if:

       EINVAL The addr argument is not a multiple of the page size as returned by sysconf().

```

Page size eh. Okay, I'll byte. I mean bite! Let's assume pages are 4KiB - because that's what they usually end up being unless large pages is enabled (we saw that in “Reading files the hard way”), that means we need our address to end in  `000`.

It's time… for some bit manipulation.

If we have a bit string, like so;

```raw
101011110000

```

We can use the  `binary NOT`  operator on it, and get:

```raw
~ 101011110000
--------------
= 010100001111

```

All the bits were flipped!

We can also  `binary AND`  two bit strings, like so:

```raw
  11110000
& 10101010
----------
= 10100000

```

So, what we want to do is take an address and strip the 3 rightmost nibbles.

![](https://fasterthanli.me/img/common/bear-glasses.svg)Cool bear's hot tip

A  [nibble](https://en.wikipedia.org/wiki/Nibble)  is the  _extremely cute_  name for a half-byte.

Remember that bytes are represented with two hexadecimal characters, like so:  `00`,  `FF`, etc. A nibble is represented with only one!

```raw
We have: 0x55f68b711008
We want: 0x55f68b711000

```

The  `binary AND`  operation is essentially “keep only the bits set in both operands”, so if we had something like:

```raw
// we're using hexadecimal notation now,
// we were using binary notation before.

  55F68B711008 
& FFFFFFFFF000 (this value is called a mask)
--------------
  55F68B711000
           ^^^ those are all zero now

```

But I don't want to write a value like  `0xFFFFFFFFF000`  by hand. That's too many Fs! Even when writing the explanation, I didn't feel like it - I just used vim visual mode and replace commands to make sure everything aligned right.

I'm also fairly sure it's not the correct mask anyway. The correct mask on 32-bit would be  `0xFFFF_F000`  - eight nibbles, four bytes, 32 bits - and the correct mask on 64-bit would be  `0xFFFF_FFFF_FFFF_F000`  - sixteen nibbles, eight bytes, 64 bits.

So, we got it wrong. And even though, as mentioned previously, we don't care at all about ELF32, we still care about writing as few Fs as possible. However, we can simply take  `0xFFF`  and inverse it with a  `binary NOT`  - and then we'll get the proper mask.

Thus, we get:

```
      55F68B711008 
&            ~ FFF
------------------
      55F68B711008 
& FFFFFFFFFFFFF000
------------------
      55F68B711000

```

Awesome! Let's put all that into practice, shall we:

```c
// in `elk/samples/entry_point.c`

#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>

#include <sys/mman.h>
#include <errno.h>

const char *instructions = "\x48\x31\xFF\xB8\x3C\x00\x00\x00\x0F\x05";

int main() {
    printf("        main @ %p\n", &main);
    printf("instructions @ %p\n", instructions);

    size_t region = (size_t) instructions;
    region = region & (~0xFFF);
    printf("        page @ %p\n", region);

    printf("making page executable...\n");
    int ret = mprotect(
        (void*) region,       // addr
        0x1000,               // len - now the size of a page (4KiB)
        PROT_READ | PROT_EXEC // prot
    );
    if (ret != 0) {
        printf("mprotect failed: error %d\n", errno);
        return 1;
    }

    void (*f)(void) = (void*) instructions;
    printf("jumping...\n");
    f();
    printf("after jump\b");
}

```

```shell
$ gcc entry_point.c entry_point
$ ./entry_point
        main @ 0x564b8c654169
instructions @ 0x564b8c655004
        page @ 0x564b8c655000
making page executable...
jumping...
$ 

```

It didn't segfault! IT DIDN'T SEGFAULT! Let's walk through it with  `ugdb`:

```shell
$ ugdb ./entry_point
(gdb) catch syscall exit
(gdb) start
(gdb) c
(for some reason, there was a temporary breakpoint somewhere else)
Catchpoint 1 (call to syscall exit)
(gdb) bt
#0  0x000055555555600e in ?? ()   
#1  0x0000555555555238 in main ()

```

![](https://fasterthanli.me/img/running-an-executable-without-exec/ugdb-executing-instructions.png)

Everything seems in order!  `main`  did call our code, which doesn't correspond to any known symbol, so GDB just shows it as  `??`.

The disassembly panel (top-left) shows garbage, because the catchpoint stopped execution  _right after_  the  `syscall`  instruction. It's trying to make sense of whatever data happens to be  _after_  our  `instructions`  constant, as if it was code.

Phew.

Okay.

## And now, the real thing

It's time to execute a real ELF file. But first - we've seen that parts of the executable are mapped into memory. How does the OS know which parts to map where, which ones to make executable, etc.?

Thanks to…  **program headers**.

Remember in our ELF header diagram from last time we had fields like “Program header offset”, “Number of program headers” and “Size of program header entry”?

Ok, I'll pull it up - it's the yellow bits here:

![](https://fasterthanli.me/img/whats-in-a-linux-executable/elf64-header.png)

Well, in the ELF file, at the proper offset, there's a bunch of these:

![](https://fasterthanli.me/img/running-an-executable-without-exec/elf64-program-header.png)

I'll confess - I made that diagram pretty early on, when I was still writing the previous article. And it didn't fully click until I wrote this entire article.

Now that we've examined the memory map for a running process, and messed with it in a bunch of ways, every field on that diagram makes sense. Except for physical address, which I'm fairly sure is deprecated?

Let's get parsing!

I won't re-explain any of the parsing tricks we saw in  [the previous article](https://fasterthanli.me/blog/2020/whats-in-a-linux-executable/)  - feel free to go back to it for reference.

```rust
// in `elf/src/lib.rs`

#[derive(Debug, Clone, Copy, PartialEq, Eq, TryFromPrimitive)]
#[repr(u32)]
pub enum SegmentType {
    Null = 0x0,
    Load = 0x1,
    Dynamic = 0x2,
    Interp = 0x3,
    Note = 0x4,
}

impl_parse_for_enum!(SegmentType, le_u32);

```

We'll only need  _one_  additional trick - just like we used  `derive-try-from-primitive`  for enums, we'll use  [enumflags2](https://crates.io/crates/enumflags2)  for bitflags for which each flag is an enum variant.

```shell
$ cargo add enumflags2
      Adding enumflags2 v0.6.2 to dependencies

```

Usage is simple enough. If we derive  `BitFlags`  on an enum with an integer representation, like so:

```rust
use enumflags2::*;

#[derive(Debug, Clone, Copy, PartialEq, Eq, BitFlags)]
#[repr(u32)]
pub enum SegmentFlag {
    Execute = 0x1,
    Write = 0x2,
    Read = 0x4,
}

```

Then we can use the  `enumflags2::BitFlags<SegmentFlag>`  type as… a set of flags, that we can OR (`|`) and AND (`&`) and NOT (`!`). There's also a  `from_bits`  method that maps the integer value to our Rust type, and a  `bits`  method to convert back to the integer value:

```rust
#[cfg(test)]
mod tests {
    #[test]
    fn try_bitflag() {
        use super::SegmentFlag;
        use enumflags2::BitFlags;

        // this is a value we could've read straight from an ELF file
        let flags_integer: u32 = 6;
        // this is how we parse it. in practice, it's less verbose,
        // because of type inference.
        let flags = BitFlags::<SegmentFlag>::from_bits(flags_integer).unwrap();
        assert_eq!(flags, SegmentFlag::Read | SegmentFlag::Write);
        assert_eq!(flags.bits(), flags_integer);

        // this does not correspond to any flags
        assert!(BitFlags::<SegmentFlag>::from_bits(1992).is_err());
    }
}

```

Just like for non-bitflag enums before, we'll make a macro to help parse bitflags:

```rust
// in `delf/src/parse.rs`

#[macro_export]
macro_rules! impl_parse_for_enumflags {
    ($type: ident, $number_parser: ident) => {
        impl $type {
            pub fn parse(i: parse::Input) -> parse::Result<enumflags2::BitFlags<Self>> {
                use nom::{
                    combinator::map_res,
                    error::{context, ErrorKind},
                    number::complete::$number_parser,
                };
                let parser = map_res($number_parser, |x| {
                    enumflags2::BitFlags::<Self>::from_bits(x).map_err(|_| ErrorKind::Alt)
                });
                context(stringify!($type), parser)(i)
            }
        }
    };
}

```

It's very similar to our previous macro, except:

-   we return a  `BitFlags<Self>`
-   we use  `.map_err`  rather than  `.ok_or`  because  `from_bits`  returns a  `Result<T, E>`, not an  `Option<T>`.

And now we can invoke it on  `SegmentFlag`, and define our  `ProgramHeader`  struct:

```rust
// in `delf/src/lib.rs`

impl_parse_for_enumflags!(SegmentFlag, le_u32);

pub struct ProgramHeader {
    pub r#type: SegmentType,
    pub flags: BitFlags<SegmentFlag>,
    pub offset: Addr,
    pub vaddr: Addr,
    pub paddr: Addr,
    pub filesz: Addr,
    pub memsz: Addr,
    pub align: Addr,
    pub data: Vec<u8>,
}

#[derive(Debug)]
pub struct File {
    // omitted: existing fields
    pub program_headers: Vec<ProgramHeader>,
}

```

![](https://fasterthanli.me/img/common/bear-glasses.svg)Cool bear's hot tip

Why own a copy of  `data`  if it's already in the input?

Well, this way the returned  `delf::File`  isn't tied to the lifetime of the input, and, who knows, maybe we can change the contents of segments later…

We can also implement a neat little  `Debug`  formatter:

```rust
// in `delf/src/lib.rs`

use std::ops::Range;

impl ProgramHeader {
    /**
     * File range where the segment is stored
     */
    pub fn file_range(&self) -> Range<Addr> {
        self.offset..self.offset + self.filesz
    }

    /**
     * Memory range where the segment is mapped
     */
    pub fn mem_range(&self) -> Range<Addr> {
        self.vaddr..self.vaddr + self.memsz
    }
}

impl fmt::Debug for ProgramHeader {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(
            f,
            "file {:?} | mem {:?} | align {:?} | {} {:?}",
            self.file_range(),
            self.mem_range(),
            self.align,
            // the default Debug formatter for `enumflags2` is a bit
            // on the verbose side, let's print something like `RWX` instead
            &[
                (SegmentFlag::Read, "R"),
                (SegmentFlag::Write, "W"),
                (SegmentFlag::Execute, "X")
            ]
            .iter()
            .map(|&(flag, letter)| {
                if self.flags.contains(flag) {
                    letter
                } else {
                    "."
                }
            })
            .collect::<Vec<_>>()
            .join(""),
            self.r#type,
        )
    }
}

```

Next up, we need to solve a tiny little problem - so far we've been parsing the ELF file from start to finish. But the program headers may be anywhere - we need to be reading from the specific offset in the ELF header.

Since our input is a slice, we can simply use sub-slicing syntax:

```rust
// in `delf/src/lib.rs`

impl File {
    // note: there are some fields we don't store or use for now, so let's
    // quiet down that warning for a moment.
    #[allow(unused_variables)]
    pub fn parse(i: parse::Input) -> parse::Result<Self> {
        let full_input = i;

        // omitted: rest of parser

        use nom::combinator::map;
        // some values are stored as u16 to save storage, but they're actually
        // file offsets, or counts, so we want them as `usize` in rust.
        let u16_usize = map(le_u16, |x| x as usize);

        // ph = program header, sh = section header
        let (i, (ph_offset, sh_offset)) = tuple((Addr::parse, Addr::parse))(i)?;
        let (i, (flags, hdr_size)) = tuple((le_u32, le_u16))(i)?;
        let (i, (ph_entsize, ph_count)) = tuple((&u16_usize, &u16_usize))(i)?;
        let (i, (sh_entsize, sh_count, sh_nidx)) = tuple((&u16_usize, &u16_usize, &u16_usize))(i)?;

        // `chunks()` divides a slice into chunks of equal size - perfect, as we know the entry size.
        let ph_slices = (&full_input[ph_offset.into()..]).chunks(ph_entsize);
        let mut program_headers = Vec::new();
        for ph_slice in ph_slices.take(ph_count) {
            let (_, ph) = ProgramHeader::parse(full_input, ph_slice)?;
            program_headers.push(ph);
        }

        let res = Self {
            machine,
            r#type,
            entry_point,
            program_headers,
        };
        Ok((i, res))
    }
}

```

All that's left is to implement  `ProgramHeader::parse`

```rust
// in `delf/src/lib.rs`

impl ProgramHeader {
    fn parse<'a>(full_input: parse::Input<'_>, i: parse::Input<'a>) -> parse::Result<'a, Self> {
        use nom::sequence::tuple;
        let (i, (r#type, flags)) = tuple((SegmentType::parse, SegmentFlag::parse))(i)?;

        let ap = Addr::parse;
        let (i, (offset, vaddr, paddr, filesz, memsz, align)) = tuple((ap, ap, ap, ap, ap, ap))(i)?;

        let res = Self {
            r#type,
            flags,
            offset,
            vaddr,
            paddr,
            filesz,
            memsz,
            align,
            // `to_vec()` turns a slice into an owned Vec (this works because u8 is Clone+Copy)
            data: full_input[offset.into()..][..filesz.into()].to_vec(),
        };
        Ok((i, res))
    }
}

```

I want to talk about the double sub-slicing trick we just used above for a minute.

When we have a  `start`  and a  `length`, we'd normally have to write this:

```rust
let sub = &full[start..start+length];

```

![](https://fasterthanli.me/img/running-an-executable-without-exec/double-subslice-1.png)

However, we can just as well write this:

```rust
let sub = &full[start..][..length];

```

![](https://fasterthanli.me/img/running-an-executable-without-exec/double-subslice-2.png)

And then we don't have to add anything, or mention  `start`  twice. It's particularly handy here because our start has to be converted from an  `Addr`  into an  `usize`.

Alright! Does any of this even work?

Again, we can use  `elk`  to check - since it's always going to build with our latest  `delf`  changes, as it refers to it by path.

```shell
$ cargo b -q && ./target/debug/elk ./samples/hello
cargo b -q && ./target/debug/elk ./samples/hello
Analyzing "./samples/hello"...
File {
    type: Exec,
    machine: X86_64,
    entry_point: 00401000,
    program_headers: [
        file 00000000..000000e8 | mem 00400000..004000e8 | align 00001000 | R.. Load,
        file 00001000..00001025 | mem 00401000..00401025 | align 00001000 | R.X Load,
        file 00002000..00002009 | mem 00402000..00402009 | align 00001000 | RW. Load,
    ],
}
Disassembling "./samples/hello"...
(cut)

```

Works pretty nicely! We can see that  `samples/hello`  is mapped pretty simply in memory - three contiguous 4KiB sections mapped with different access rights: first read-only, then read+execute, then read+write.

That means we don't need to hardcode the disassembly address anymore. Where we had:

```rust
// in `elk/src/main.rs`
// in `main()`

    println!("Disassembling {:?}...", input_path);
    let code = &input[0x1000..];
    let code = &code[..std::cmp::min(0x25, code.len())];
    ndisasm(code)?;

```

We can simply have:

```rust
// in `elk/src/main.rs`
// in `main()`

    println!("Disassembling {:?}...", input_path);
    let code_ph = file
        .program_headers
        .iter()
        .find(|ph| ph.mem_range().contains(&file.entry_point))
        .expect("segment with entry point not found");

    ndisasm(&code_ph.data[..], file.entry_point)?;

```

Above, I've added an  `offset`  parameter to the  `ndisasm()`  function so that the addresses displayed in the disassembly are accurate:

```rust
// in `elk/src/main.rs`

fn ndisasm(code: &[u8], origin: delf::Addr) -> Result<(), Box<dyn Error>> {
    use std::{
        io::Write,
        process::{Command, Stdio},
    };

    let mut child = Command::new("ndisasm")
        .arg("-b")
        .arg("64")
        .arg("-o")
        .arg(format!("{}", origin.0))
        .arg("-")
        .stdin(Stdio::piped())
        .stdout(Stdio::piped())
        .spawn()?;
    child.stdin.as_mut().unwrap().write_all(code)?;
    let output = child.wait_with_output()?;
    println!("{}", String::from_utf8_lossy(&output.stdout));

    Ok(())
}

```

Let's give it a shot:

```rust
$ cargo b -q && ./target/debug/elk ./samples/hello

Analyzing "./samples/hello"...
File {
    type: Exec,
    machine: X86_64,
    entry_point: 00401000,
    program_headers: [
        file 00000000..000000e8 | mem 00400000..004000e8 | align 00001000 | R.. Load,
        file 00001000..00001025 | mem 00401000..00401025 | align 00001000 | R.X Load,
        file 00002000..00002009 | mem 00402000..00402009 | align 00001000 | RW. Load,
    ],
}
Disassembling "./samples/hello"...
00401000  BF01000000        mov edi,0x1
00401005  48BE002040000000  mov rsi,0x402000
         -0000
0040100F  BA09000000        mov edx,0x9
00401014  B801000000        mov eax,0x1
00401019  0F05              syscall
0040101B  4831FF            xor rdi,rdi
0040101E  B83C000000        mov eax,0x3c
00401023  0F05              syscall

```

Awesome!

Now let's execute it. We know from earlier that before we do that, we must make the memory executable. In C, we used  `mprotect`  to do it.

Now, there is a  [libc crate](https://crates.io/crates/libc)  that does contain  `mprotect`, and the relevant  `PROT_`  constants… but that's no fun! We already did the low-level drudgery once. Right now, I want something nice in my life.

A cozy, safe abstraction.

And we can have that! The  [region crate](https://crates.io/crates/region)  allows us to do exactly that (and in a cross-platform manner, to boot).

```shell
$ cargo add region
      Adding region v2.1.2 to dependencies

```

```rust
// in `elk/src/main.rs`
// in `main()`

    println!("Executing {:?} in memory...", input_path);

    use region::{protect, Protection};
    let code = &code_ph.data;
    unsafe {
        protect(code.as_ptr(), code.len(), Protection::ReadWriteExecute)?;
    }

    let entry_offset = file.entry_point - code_ph.vaddr;
    let entry_point = unsafe { code.as_ptr().add(entry_offset.into()) };
    println!("       code  @ {:?}", code.as_ptr());
    println!("entry offset @ {:?}", entry_offset);
    println!("entry point  @ {:?}", entry_point);
    unsafe {
        jmp(entry_point);
    }

    Ok(())

```

Alright. Well.

This is it right? We can run the executable without  `exec`? We did the thing?

Let's find out.

```shell
$  cargo b -q && ./target/debug/elk samples/hello
Analyzing "samples/hello"...
File {
    type: Exec,
    machine: X86_64,
    entry_point: 00401000,
    program_headers: [
        file 00000000..000000e8 | mem 00400000..004000e8 | align 00001000 | R.. Load,
        file 00001000..00001025 | mem 00401000..00401025 | align 00001000 | R.X Load,
        file 00002000..00002009 | mem 00402000..00402009 | align 00001000 | RW. Load,
    ],
}
Disassembling "samples/hello"...
00401000  BF01000000        mov edi,0x1
00401005  48BE002040000000  mov rsi,0x402000
         -0000
0040100F  BA09000000        mov edx,0x9
00401014  B801000000        mov eax,0x1
00401019  0F05              syscall
0040101B  4831FF            xor rdi,rdi
0040101E  B83C000000        mov eax,0x3c
00401023  0F05              syscall

Executing "samples/hello" in memory...
       code  @ 0x561828e69000
entry offset @ 00000000
entry point  @ 0x561828e69000

```

Fuck.

I'm pretty sure  `hello`  was supposed to print something.

```shell
$ ./samples/hello
hi there

```

Yes, yes, it was. What the heck is happening. We didn't even get a segfault!

Is it even running our code? Let's use  `ugdb`  to find out:

```shell
$ ugdb ./target/debug/elk ./samples/hello
(gdb) break jmp
(gdb) start

```

![](https://fasterthanli.me/img/running-an-executable-without-exec/exec-1.png)

So far so good. Does it actually jump to the right place?

```shell
(gdb) stepi
(gdb) stepi

```

![](https://fasterthanli.me/img/running-an-executable-without-exec/exec-2.png)

It does!

But it.. doesn't… print “hi there”.

We got more detective work to do.

This article is part 2 of the series  [Making our own executable packer](https://fasterthanli.me/blog/2020/whats-in-a-linux-executable/):

[](https://fasterthanli.me/blog/2020/whats-in-a-linux-executable/)

Previously (Part 1)

What's in a Linux executable?

[](https://fasterthanli.me/blog/2020/position-independent-code/)

Next up (Part 3)

Position-independent code

This article was made possible thanks to my patrons: Aurora, Brian, Chad Morrow, Corey, Fernando, Geert Depuydt, Geoff Cant, Geoffroy Couprie, Henry Goffin, Ignacio Vergara, Jane Lusby, Jesús Higueras, Jonathan Knapp, Justin Gerhardt, Jérémy Gtld, Lina Cambridge, Lucien Greathouse, Makoto Nakashima, Mara Bos, Maximilian, Mayfield Reynolds, Michael Alyn Miller, Nicolas Goy, o0Ignition0o, Pascal, Raphael Gaschignard, Romain Ruetschi, Ryszard Sommefeldt, Sean Bryant, Sebastian Zimmer, Seth Stadick, Someone, Stefano Probst, Ted Mielczarek, Zaki, and Тим Маринин.

If you liked this article, please support my work on Patreon!

[![](https://fasterthanli.me/img/patreon/mark-white.png)Become a Patron](https://www.patreon.com/bePatron?u=47556)