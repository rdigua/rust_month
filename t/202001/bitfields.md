
# [Bitfields Forever: Why we need a C-compatible Rust Crate](https://immunant.com/blog/2020/01/bitfields/)

By  [Daniel Kolsoi](https://immunant.com/authors/daniel-kolsoi)

## What Are Bitfields?

The C programming language is a product of a time where it was important to use as few resoures as possible. Memory was measured in kilobytes rather than gigabytes as we do today. Bitfields offer a handy way to reduce memory usage. However, bitfields aren’t just a relic of yesteryear’s computer programming; they remain frequently used today. Some domains, like embedded hardware, still require programmers to be frugal with memory. Projects like Nginx as well as many Linux kernel modules also improve reduce memory usage this way. Moreover, some hardware interfaces expect bits to be laid out in a particular format.

So, how do bitfields actually work? The idea is that if you have multiple integers values you have to keep track of but know that they wouldn’t use all possible values in the integer type, you can compact them together by assigning a maximum bit size to the integer. For example, suppose we’d like to write a very contrived compact date  `struct`  in C:

```c
struct Date {
    unsigned char day: 5;
    unsigned char month: 4;
    signed short year: 15;
} __attribute__((packed));

```

We use 5 bits of space for  `day`  because that’s the minimum size (`2 ^ 5 = 32`) to store the largest number of days in any given month (31). Similarly, we give  `month`  4 bits to minimally represent 12 months. Finally, we give  `year`  enough bits to be able to represent the current year (and then some!) and make it signed to signify the era. This should give us a nice three-byte  `struct`[1](https://immunant.com/blog/2020/01/bitfields/#fn:1).

Clang can helpfully confirm our  `struct`  is laid out as expected:

```bash
clang -Xclang -fdump-record-layouts date.c

```

```c
*** Dumping AST Record Layout
     0 | struct Date
 0:0-4 |   unsigned char day
 0:5-8 |   unsigned char month
1:1-15 |   signed short year
       | [sizeof=3, align=1]

```

The bitfields  `day`  and  `month`  share the first byte, but the last bit of  `month`  straddles the second byte followed by  `year`  taking up the remainder of the last two bytes.

## Translation Requirements

The goal of  [C2Rust](https://github.com/immunant/c2rust)  is to translate any standard C code into Rust. To translate bitfields from C, we therefore require drop-in compatible bitfield support. Since the Rust ecosystem revolves around sharing code in libraries (called crates), we decided to look at the few most promising crates to see what was available. Unfortunately, we found that not all of them provided byte compatibility with equivalent C structures which C2Rust must ensure so that its output is FFI compatible with the original C input. Section 6.7.2.1 of the C standard states that you cannot take pointers to bitfields. This is because pointers can only refer to whole bytes, not individual bits. However, since a  `struct`  may contain a mix of bitfields and non-bitfields, we must still be able to take pointers (and references) to non-bitfield fields. Although a softer requirement, most of the crates did provide an abstraction layer so that users didn’t have to think about or manage bitfield boilerplate directly.

In summary, our crate requirements are as follows:

1.  ABI compatibility with C
2.  Able to take pointers to non-bitfields
3.  Abstraction layer with minimal boilerplate

Here is an overview of the 3rd party crates we looked at and how they stacked up to our requirements:

### The`rust-bitfield`Crate

The  [rust-bitfield](https://github.com/dzamlo/rust-bitfield)  crate provides a nifty  `bitfield!`  macro_rules macro:

```rust
bitfield!{
    struct Date(MSB0 [u8]);
    u32;
    get_day, set_day: 4, 0;
    get_month, set_month: 8, 5;
    get_year, set_year: 23, 9;
}

fn main() {
    let mut date = Date([0, 0, 0]);

    date.set_day(7);
    date.set_month(1);
    date.set_year(2020);

    assert_eq!(date.get_day(), 7);
    assert_eq!(date.get_month(), 1);
    assert_eq!(date.get_year(), 2020);
}

```

We liked that the bit specification was easy to read and that you could specify most or least significant bit ordering. However, since the  `struct`  must be backed by a byte array, there are no directly addressible non-bitfield fields, let alone pointers to them(`#2`). Another issue we had was that  `macro_rules!`  macros are hard to format automatically. Passing them into our  [refactoring tool](https://github.com/immunant/c2rust/tree/master/c2rust-refactor)  would cause them to be formatted unexpectedly. This is because the refactorer has to re-print source code to file and does not know what the expected format of the non-standard macro is. The nice thing about this approach is that it abstracts the complexity of bitfields behind helper methods(`#3`).

### The`packed_struct`Crate

The feature-packed  [packed_struct](https://github.com/hashmismatch/packed_struct.rs)  crate:

```rust
#[derive(PackedStruct)]
#[packed_struct(bit_numbering="msb0")]
pub struct Date {
    #[packed_field(bits="0..=4")]
    day: u8,
    #[packed_field(bits="5..=8")]
    month: u8,
    #[packed_field(bits="9..=23", endian="msb")]
    year: i16,
}

fn main() {
    let mut date = Date { day: 0, month: 0, year: 0 };

    date.day = 7;
    date.month = 1;
    date.year = 2020;

    assert_eq!(date.day, 7);
    assert_eq!(date.month, 1);
    assert_eq!(date.year, 2020);
}

```

We really wanted to use this crate. It seems to have a ton of neat configuration options, e.g., you can turn bitfields into enums. And more importantly, it uses actual fields rather than an internal byte representation, unlike  `rust-bitfield`.

A big problem we had with it was usability. It seems to be  [very particular](https://github.com/hashmismatch/packed_struct.rs/issues/39)  about the type signatures you provide to it, and the compiler errors weren’t that helpful. It took half an hour to figure out how to get the above example compiling after fiddling around with its  `Integer`  type[2](https://immunant.com/blog/2020/01/bitfields/#fn:2). And we’re still not sure why  `year`  needs its endianness explicitly specified when the  `struct`  already has a default. This crate may just still require a lot of macro polish. However, the biggest problem we had with this crate was that the generated  `struct`s are not byte compatible with their C counterparts(`#1`).  `Date`, in the above example, is four bytes large! Instead, there’s a helper method to build a correctly sized byte array from scratch. On the plus side, the derive macro and  `struct`  attributes seemed like a great approach in general.

### The`bindgen`Crate

The  [bindgen](https://github.com/rust-lang/rust-bindgen)  crate emits Rust  `struct`s based on C code for interoperability and therefore is a bit closer to what we need in  `C2Rust`  than the previous two crates. Running the C date example through bindgen would get you the following, trimmed for brevity:

```rust
#[repr(C)]
pub struct __BindgenBitfieldUnit<Storage, Align> {
    storage: Storage,
    align: [Align; 0],
}
impl<Storage, Align> __BindgenBitfieldUnit<Storage, Align>
where
    Storage: AsRef<[u8]> + AsMut<[u8]>,
{
    pub fn get_bit(&self, index: usize) -> bool {
        // ...
    }
    pub fn set_bit(&mut self, index: usize, val: bool) {
        // ...
    }
    pub fn get(&self, bit_offset: usize, bit_width: u8) -> u64 {
        // ...
    }
    pub fn set(&mut self, bit_offset: usize, bit_width: u8, val: u64) {
        // ...
    }
}
#[repr(C, packed)]
pub struct Date {
    pub _bitfield_1: __BindgenBitfieldUnit<[u8; 4usize], u16>,
}

impl Date {
    pub fn day(&self) -> ::std::os::raw::c_uchar {
        unsafe { ::std::mem::transmute(self._bitfield_1.get(0usize, 5u8) as u8) }
    }
    pub fn set_day(&mut self, val: ::std::os::raw::c_uchar) {
        unsafe {
            let val: u8 = ::std::mem::transmute(val);
            self._bitfield_1.set(0usize, 5u8, val as u64)
        }
    }

    // ...
}

```

Note that the amount of boilerplate can quickly balloon(`#3`). Despite this, the above is a really neat approach because the  `align`  field treats the alignment as if it were an actual field that can be customized through generics.  `#1`  is satisfied because byte compatability is maintained. Furthermore, it’s very clever that consecutive bitfields are combined into a single byte array. Lastly,  `#2`  is satisfied because the  `Date`  `struct`  has concrete fields which could have pointers taken to them if needed.

### Honorable Mention: The`bitvec`Crate

Unfortunately, we didn’t catch wind of this crate when we first researched existing bitfield support, so we never did a thorough evaluation of it. It seems to have existed in some capacity at that point, though. Check out this  [blog post](https://myrrlyn.net/blog/misc/bitfields-in-rust)  to learn more.

It appears to have the same problem as  `rust-bitfield`  insofar that bitfields are backed by a byte array. Therefore it doesn’t meet requirement  `#2`. Bits are read in a novel way though. A generic load method reads from (and another writes to) the backing bytes like so:

```rust
bitvec[10..23].load::<u16>().unwrap();

```

Here the index represents bits, not bytes. A big advantage  `bitvec`  does have over  `rust-bitfield`  and  `packed_struct`  is that it seems to still be actively developed as of this writing.

## Our Approach: The`c2rust-bitfields`Crate

Learning from the first three of the above crates, we tried to find a middle ground which could satisfy all of our requirements:

```rust
#[repr(C, align(1))]
#[derive(BitfieldStruct)]
struct Date {
    #[bitfield(name = "day", ty = "libc::c_uchar", bits = "0..=4")]
    #[bitfield(name = "month", ty = "libc::c_uchar", bits = "5..=8")]
    #[bitfield(name = "year", ty = "libc::c_short", bits = "9..=23")]
    day_month_year: [u8; 3]
}

fn main() {
    let mut date = Date {
        day_month_year: [0; 3]
    };

    date.set_day(7);
    date.set_month(1);
    date.set_year(2020);

    assert_eq!(date.day(), 7);
    assert_eq!(date.month(), 1);
    assert_eq!(date.year(), 2020);
}

```

We are ABI compatible with C(`#1`) because we use a  `struct`  format with actual fields and combine adjacent bitfields into a single byte array field. This format also allows for pointers (and references) to be taken of non-bitfield fields, satisfying  `#2`. Lastly,  `#3`  is satisfied by having method generation boilerplate automatically derived from the macro with very little of it user-facing.

The way this works is two-fold. Firstly, a transparent  `c2rust-bitfields-derive`  crate exports the  `BitfieldStruct`  derive macro which handles all of the attribute parsing and method generation. These generated methods assume the existence of a  `FieldType`  trait which is implemented for all integer types as well as  `bool`. It allows the generated code to determine whether a bitfield type is signed, what is its total number of bits, and also provides internal getters and setters[3](https://immunant.com/blog/2020/01/bitfields/#fn:3). Secondly, the  `c2rust-bitfields`  crate re-exports  `BitfieldStruct`  and provides the  `FieldType`  trait and implementations.

Originally, this project only consisted of the  `c2rust-bitfield`  crate containing the derive macro code. We then realized that we did not support booleans. So we added the  `FieldType`  trait which enabled us to write more generic code over both integer and boolean types. However, the gotcha was that proc macro crates can only export proc macros and nothing else. And so we had to split the crate in two to account for this limitation (which might be removed in the future). Both crates are available on  [crates.io](https://crates.io/search?q=c2rust-bitfields).

### Bitfields in the Wild: Nginx

Adding bitfield support to C2Rust was necessary to successfully translate and compile Nginx in Rust. One Nginx  `struct`  with bitfields looks like this in C:

```c
typedef struct {
    ngx_file_t file;
    off_t offset;
    ngx_path_t *path;
    ngx_pool_t *pool;
    char *warn;
    ngx_uint_t access;
    unsigned log_level:8;
    unsigned persistent:1;
    unsigned clean:1;
    unsigned thread_write:1;
} ngx_temp_file_t;

```

Rather than the last four fields being four unsigned ints in size(16 bytes on many platforms), it only needs to occupy two bytes. And when transpiled into Rust, it looks like this:

```rust
#[repr(C)]
#[derive(BitfieldStruct, Clone, Copy)]
pub struct ngx_temp_file_t {
    pub file: ngx_file_t,
    pub offset: off_t,
    pub path: *mut ngx_path_t,
    pub pool: *mut ngx_pool_t,
    pub warn: *mut libc::c_char,
    pub access: ngx_uint_t,
    #[bitfield(name = "log_level", ty = "libc::c_uint", bits = "0..=7")]
    #[bitfield(name = "persistent", ty = "libc::c_uint", bits = "8..=8")]
    #[bitfield(name = "clean", ty = "libc::c_uint", bits = "9..=9")]
    #[bitfield(name = "thread_write", ty = "libc::c_uint", bits = "10..=10")]
    pub log_level_persistent_clean_thread_write: [u8; 2],
    pub _pad: [u8; 6],
}

```

Interestingly, there are 6 trailing bytes for padding. This is necessary to be equivalent to the original C  `struct`. But the resulting struct is still 8 bytes(`16 - 2 - 6 = 8`) smaller than if bitfields were not used.

## Possible Crate Improvements (PRs Welcome!)

1.  Big Endian architectures are not currently supported. They currently produce a hard compiler error.
    
2.  We currently only support the inclusive range format  `..=`  for the  `bits`  attribute param. This means specifying a single bit looks like  `7..=7`. We could support a single-digit value or an alternative  `bit`  attribute param. The exclusive range  `..`  could also be supported.
    

## First-Class Bitfield Support in Rust?

Josh Triplett  [recently mentioned](https://youtu.be/l9hM0h6IQDo?t=1132)  that the FFI working group is looking to explore Rust support for bitfields. A syntax for this might simply use attributes:

```rust
#[repr(C, packed)]
struct Date {
    #[bits(5)] day: libc::c_uchar,
    #[bits(4)] month: libc::c_uchar,
    #[bits(15)] year: libc::c_short,
}

fn main() {
    let mut date = Date {
        day: 0,
        month: 0,
        year: 0,
    };

    date.day = 7;
    date.month = 1;
    date.year = 2020;

    assert_eq!(date.day, 7);
    assert_eq!(date.month, 1);
    assert_eq!(date.year, 2020);
    assert_eq!(std::mem::size_of::<Date>(), 3);
}

```

# What’s Next?

As we continue to develop C2Rust, we’d love to hear what you want to see translated next. Drop us a line at  [team@immunant.com](mailto:team@immunant.com)  and let us know! If you have legacy C code you need modernized and translated, the team here at Immunant is here to help. We are available for consulting and contracting engagements ranging from one-time support to full-service code modernization.

----------

1.  The packed attribute is used to ensure the bytes are consecutive without any padding in between.  [↩︎](https://immunant.com/blog/2020/01/bitfields/#fnref:1)
    
2.  Not shown in the example since we figured out a simpler version.  [↩︎](https://immunant.com/blog/2020/01/bitfields/#fnref:2)
    
3.  Technically, trait methods can’t be private. But users are not expected to use any of them, so we consider them internal.  [↩︎](https://immunant.com/blog/2020/01/bitfields/#fnref:3)
    

----------

[Rust](https://immunant.com/tags/rust)[c2rust](https://immunant.com/tags/c2rust)[transpiler](https://immunant.com/tags/transpiler)[bitfields](https://immunant.com/tags/bitfields)

2101 Words

2020-01-27 00:00 -0800