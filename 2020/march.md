# March 2020

## rust





### nalgebra，Rust线性代数库

nalgebra，Rust线性代数库，包含变换和静态或动态大小的矩阵。WASM中使用效果良好。

[Doc.rs链接](https://docs.rs/nalgebra/0.20.0/nalgebra/)：https://docs.rs/nalgebra/0.20.0/nalgebra/

[Github链接](https://github.com/rustsim/nalgebra)：https://github.com/rustsim/nalgebra

# Rust: assert_cmd

可以簡單驗證指令回傳值的庫

[Read more](https://bit.ly/3dB8dWg)

### 在 no_std 中使用async/await

在最近的nightly版本中，你可以在使用no_std时使用async/await了。

### ttf-parser v0.5

ttf-parser，一个高级，安全，零分配的TrueType字体解析器。现在v0.5，支持可变字体和C API。

[Github](https://github.com/RazrFalcon/ttf-parser)

### doc.rs 现在允许选择 build 目标平台

例如  `winapi`  只有两个目标平台：`x86_64-pc-windows-msvc`  和  `i686-pc-windows-msvc`  ，那就可以这样配置：

```
[package.metadata.docs.rs]
# This also sets the default target to `x86_64-pc-windows-msvc`
targets = ["x86_64-pc-windows-msvc", "i686-pc-windows-msvc"]

```

详情：[https://blog.rust-lang.org/2020/03/15/docs-rs-opt-into-fewer-targets.html](https://blog.rust-lang.org/2020/03/15/docs-rs-opt-into-fewer-targets.html)

# Rust 1.42.0 發佈了！

增加了 Subslice patterns

```
fn foo(words: &[&str]) {
    match words {
        [] => println!("empty slice!"),
        [one] => println!("one element: {:?}", one),
        [one, two] => println!("two elements: {:?} {:?}", one, two),
        _ => println!("I'm not sure how many elements!"),
    }
}

```

新巨集 matches!

```
// Using a match expression:
match self.partial_cmp(other) {
    Some(Less) => true,
    _ => false,
}
// Using the `matches!` macro:
matches!(self.partial_cmp(other), Some(Less))

let foo = 'f';
assert!(matches!(foo, 'A'..='Z' | 'a'..='z'));
let bar = Some(4);
assert!(matches!(bar, Some(x) if x > 2));

```

其它功能詳見

[Read more](https://bit.ly/2Wbae5w)

### Web 框架常备的  `Sessions`  库

`Sessions`  库可以为自定义会话后端系统提供基础的内存和文件系统支持。

特性如下：

-   Async/await
    
-   Easy custom Store
    
-   Stores the values in a Map<String, Value> based on serde_json
    

使用示例：

```
let store = Arc::new(CustomStore::new());

let id = format!("id.{}", 0);                   // Generates an UID
let store = store.clone();
let session = store.get(&id).await.unwrap();    // Fresh Session

session.id().unwrap();                          // ""
session.status().unwrap();                      // SessionStatus::Created
session.state().unwrap();                       // State

session.set::<usize>("counter", 0).unwrap();    // None
session.set("number", 233).unwrap();            // None
session.get::<usize>("counter").unwrap();       // Some(0)
session.get::<u32>("number").unwrap();          // Some(233)

session.save().await;                           // Ok(())

```

GitHub 地址：https://github.com/trek-rs/sessions


# Rust: 實時3D Nbody模擬

![](https://i.imgur.com/XJmuiPU.png)

http://bit.ly/2VNlVyV

### Firecracker: serverless 应用的轻量级虚拟化

详情：  [https://blog.acolyer.org/2020/03/02/firecracker/](https://blog.acolyer.org/2020/03/02/firecracker/)

## git-trim：一个用于修剪用Rust编写的合并的本地/远程分支git工具。

![](https://github.com/foriequal0/git-trim/raw/master/images/logo.png)

`git-trim`自动修剪合并或消失的git远程跟踪分支。

按常规的操作，Git的PR工作流程有些繁琐。但现在只需键入`git trim`并按下y一次键就足够了。

![](https://github.com/foriequal0/git-trim/raw/master/images/3-git-trim-in-action.png)

![](https://github.com/foriequal0/git-trim/raw/master/images/4-after.png)

这就是`git-trim`。它知道分支是否合并到默认基础分支中，或者是否被拒绝。甚至`push --delete`在您需要时忘记删除远程分支时也可以。

前往GitHub仓库了解更多：[https://github.com/foriequal0/git-trim](https://github.com/foriequal0/git-trim)


---
++++++
---

## learning

#### 博文：Macros vs Rename

[Macros vs Rename](https://rust-analyzer.github.io/blog/2020/03/30/macros-vs-rename.html)

#### 用Github workflow cross-compiling 多个Linux版本的rust可执行文件。

[用Github workflow cross-compiling 多个Linux版本的rust可执行文件](https://gist.github.com/FedericoPonzi/873aea22b652572f5995f23b86543fdb)

#### 自己动手写Web Assembly解析器（2）

[Let’s Write a Web Assembly Interpreter (Part 2)](https://medium.com/@richardanaya/lets-write-a-web-assembly-interpreter-part-2-6c430f3f4bfd)

#### 自己动手写Web Assembly解析器（1）

[Let’s Write a Web Assembly Interpreter (Part 1)](https://medium.com/@richardanaya/lets-write-a-web-assembly-interpreter-part-1-287298201d75)

### 上海科技大学GeekPie社团 WorkShop#7「关于Rust你需要了解的…」

#rust #workshop

B站视频回放地址：

-   [https://www.bilibili.com/video/BV1ti4y1b7xy/](https://www.bilibili.com/video/BV1ti4y1b7xy/)

三份 PPT 下载地址：

-   [https://c-t.work/s/74b9dcf657be4d](https://c-t.work/s/74b9dcf657be4d)
-   [https://cowtransfer.com/s/c98f417a076d48](https://cowtransfer.com/s/c98f417a076d48)  密码shanghaitech
-   [https://c-t.work/s/37a60fd0da9041](https://c-t.work/s/37a60fd0da9041)  密码shanghaitech

### 两篇关于「K-Rust ： Rust 可执行形式语义」的论文

#rust #paper

-   上科大宋老师：  [https://arxiv.org/abs/1804.10806](https://arxiv.org/abs/1804.10806)
-   Cyber Security Lab , NTU ：  [https://arxiv.org/abs/1804.07608](https://arxiv.org/abs/1804.07608)

### 使用no_std crate开发webAssembly

#rust #wasm

推荐阅读，使用no_std的 crate 开发webAssembly，通过开发web模拟器来实现嵌入式图形库举例说明。

[Read More](https://rahul-thakoor.github.io/using-no-standard-library-crates-with-webassembly/)

### 如何在Android设备上运行rust应用

#rust #android

[Read More](https://krupitskas.github.io/posts/quest-dev-part-2/)

### Rust 项目常用的 GitHub Actions

#rust #ci #cd

[@svartalf](https://twitter.com/svartalf)开发了一个网站，列举了rust项目常用的一些GitHub Action。

[Repo](https://actions-rs.github.io/)

### Rust编写操作系统系列：async/await

在本文中，我们将探讨协作式多任务处理以及Rust的async/await功能。

这篇[博客文章链接](https://os.phil-opp.com/async-await/)：https://os.phil-opp.com/async-await/

### PingCAP：使用 Go 工具快速在线查找 Rust 程序瓶颈

在线分析大型 Rust 应用程序很困难，目前常见的分析器无法胜任该工作。来自 PingCAP 官博的分享，介绍了他们在工程上是如何使用 go 工具分析 Rust 程序性能瓶颈的。详情请看原文：https://pingcap.com/blog/quickly-find-rust-program-bottlenecks-online-using-a-go-tool/

![](https://download.pingcap.com/images/blog/find-rust-program-bottlenecks-online-using-go-tool.png)

### 通过开发一个 JIRA 来学习 Rust

测试驱动的 Rust 学习项目，适合有其他语言编程经验的 Rust 新手. 在这个项目中，你可以通过一系列测试驱动的练习以及阅读材料来学习如何构建一个 JIRA，并在此过程中学习 Rust.

详情：[https://github.com/LukeMathWalker/build-your-own-jira-with-rust](https://github.com/LukeMathWalker/build-your-own-jira-with-rust)

### 对于国内程序员来说, 即能练习英文又能学习Rust, 是不是很Cool.

作者很努力的录制了大量Rust基础学习教程, 拼命代码例子进行讲解, 也可以练习听力, 推荐给大家:  [https://egghead.io/lessons/rust-integer-types-in-rust](https://egghead.io/lessons/rust-integer-types-in-rust)

### AWS的程序员: 马克·布鲁克, 写了一篇关于他最近2年使用Rust的一些心得

文章链接:  [http://brooker.co.za/blog/2020/03/22/rust.html](http://brooker.co.za/blog/2020/03/22/rust.html)

#### Actix中如何通过RustLS应用TLS和SNI(server name identification)

https://stephanheijl.com/rustls_sni.html

### 一篇分析Rust内存安全的论文

Rust是否可以实现内存安全的承诺？

[论文](https://arxiv.org/abs/2003.03296)

### Rust安全指南文档

文档的目的是进行安全的应用程序开发建议，同时利用Rust语言提供的各种可能性。

[指南](https://anssi-fr.github.io/rust-guide/)

### 一份Rust中`Option`和Haskell中`Maybe`的速查表

这是针对那些希望快速在`Option`值上找到相应函数名称的人。例如，对于Rust，在特定情况下使用哪一个？是`or_else`，`unwrap_or`还是`unwrap_or_else`？

[速查表](https://notes.iveselov.info/cheatsheet-rust-option-vs-haskell-maybe)

### 用Rust重写 Dropbox 同步引擎核心功能

Dropbox是最实用且免费的文件同步、备份、共享云存储软件, 同步引擎是桌面电脑上 Dropbox 文件夹背后的魔法，也是 Dropbox 最古老、最重要的代码之一。用Rust来对它进行重写, 足以展现出Rust强大的能力.

这篇文本[https://dropbox.tech/infrastructure/rewriting-the-heart-of-our-sync-engine](https://dropbox.tech/infrastructure/rewriting-the-heart-of-our-sync-engine)  详细说明了重写Dropbox同步引擎的过程, 值得大家阅读.

### Rust中的引用

Rust中的引用允许你使用值但不获取其所有权, 理解引用对于Rust使用者来说非常重要. 这里有一篇文章, 对引用解释的比较通俗易懂. 推荐给大家.  [https://blog.thoughtram.io/references-in-rust/](https://blog.thoughtram.io/references-in-rust/)

### 是优化？不是优化？关于对 COW 的深入思考

文章从 Copy-On-Write 的概念入手，探讨了 C++ 中的 COW，和 Rust 中的 COW 的设计。然后做了简单的性能评测，以及解释了 Rust 中的睿智设计。推荐阅读。

https://oribenshir.github.io/afternoon_rusting/blog/copy-on-write

### staticvec - 静态 Vec

静态 Vec 的意思就是非动态分配内存的 Vec。使用了预先分配的一定容量的内存。 它使用 const generics，基于一个 array 实现。

https://github.com/slightlyoutofphase/staticvec

### Out of the Box Dynamic Dispatch

Llogiq 大佬新出的文章。摸索出了一种小技巧，可以不使用 Box 指针来实现同样的动态分派。值得学习。

https://llogiq.github.io/2020/03/14/ootb.html

### Rust for gopher

😊给 Gopher 的一段 Rust 简单介绍，相信你会喜欢上 Rust 的！

视频地址请戳：https://youtu.be/eQjPvsmfIts

Reddit 上参与讨论：https://www.reddit.com/r/golang/comments/fgy1fo/a_short_introduction_to_rust_for_programmers/

### 关于 Rust 复杂结构体初始化的讨论

Rust 的复杂结构的初始化是比较头疼的问题。 目前有几种流行的解决方法，例如  `pub fn new（）`约定和  `builder`模式。在这篇博文中，我们将对它们进行比较，并介绍一种新的模式 -  `Init Struct Pattern`。

查看博客原文：https://xaeroxe.github.io/init-struct-pattern/

### 【博客】我对 Rust 和 .NET 的探索

作者从事于用 Rust 促进 .NET 开发的工作，现在他们的项目有点快成形的意思了但还有很多问题，所以他决定和社区的人介绍一下他们的工作并交流一下.

项目现在还没取好名字，也暂不开源，主要两部分组成：

-   将 rustc 中的 LLVM bitcode 转化为 .NET 程序集（assembly）的编译器
-   为其他 .NET 程序集聚合 Rust bindings 的工具，这样就可以用 Rust 代码来调用 .NET 库了.

这样一来 Rust 代码就可以调用 .NET 代码了，反过来也一样.

下面是一个 Rust 函数，它将一串数字的字符串字面量转化为一个 .NET 字符，然后再对其调用  `System.Int32.TryParse()`

```
fn int_tryparse_out_parm() -> bool {
    let s = "30579";
    let s_clr = System::Text::Encoding::UTF8().GetString_1(s.as_bytes());
    let mut result = 0;
    let b = System::Int32::TryParse_2(&s_clr, &mut result);
    return b && (result == 30579);
}

```

详情：[https://ericsink.com/entries/dotnet_rust.html](https://ericsink.com/entries/dotnet_rust.html)

### Evokit ：用于搜索的神经网络进化机器学习系统

详情：[https://github.com/etsy/Evokit](https://github.com/etsy/Evokit)

### Bottlerocket ： 基于 Linux 的操作系统

这个操作系统几乎所有新部件都是用 Rust来构建的.

详情：[https://github.com/bottlerocket-os/bottlerocket](https://github.com/bottlerocket-os/bottlerocket)


### 【视频】Rust NYC: Jon Gjengset - 让 unsafe 代码变得简单易懂

详情：[https://www.youtube.com/watch?v=QAz-maaH0KM](https://www.youtube.com/watch?v=QAz-maaH0KM)

### 对 Rust build pattern 的新思考 - Init Struct Pattern

文章浅显易懂，有一些有价值的思考，推荐阅读：

https://xaeroxe.github.io/init-struct-pattern/

### 一本关于Rust初学者的书

[@snoyberg](https://twitter.com/snoyberg)和[Miriam Snoyman](https://twitter.com/LambdaMom/)正在写一本关于Rust的书，现在可以填写[表单](https://docs.google.com/forms/d/e/1FAIpQLSeBgnFFXK22-HqP9rub59oHI4pZ1rAdBdsxRAJ23GyEAAd6eQ/viewform)申请试读。

[Read More](https://docs.google.com/forms/d/e/1FAIpQLSeBgnFFXK22-HqP9rub59oHI4pZ1rAdBdsxRAJ23GyEAAd6eQ/viewform)

# Rust: Nannou 更新了 WebGPU

Nannou是Rust的開源，創新的程式框架。

自發布以來，今天標誌著該項目最大的里程碑之一-版本0.13的發布。

WebGPU是一個GPU使用的跨平台標準

WebGPU正在所有主要瀏覽器中實現

代表以後Nannou也可以利用瀏覽器來畫出各種畫面

文章裡有例子

http://bit.ly/32Squtg

### Serverless + Rust 的尝试

I lightly documented my experience with Rust serverless using Cloudflare Workers.

TL;DR There is a lot of promise, but the overall state of Rust on serverless is pretty immature. This is likely to change in the next 12 months.

UPDATE: For Cloudflare workers you can access the Workers KV API directly using wasm_bindgen. This improves performance significantly. A full example can be found here: https://github.com/jRiest/the-best-goats/

reddit: https://www.reddit.com/r/rust/comments/fdmzyh/serverless_rust_i_tried_it_with_cloudflare_workers/

### 半小时学习 Rust

Rust 学起来不是很难么？半小时怎么可能...让我们一起来看看这位小哥写的博客，30 分钟速览 Rust 语法的概要，博客地址：https://fasterthanli.me/blog/2020/a-half-hour-to-learn-rust/

## [【Rust每周一知】Rust为什么会有String和&str？](https://rust.cc/article?id=08bc71ca-7aa1-4fce-93aa-614712430c66)

[洋芋](https://rust.cc/blog_with_author?author_id=207704d2-4f5e-4219-a631-6ab4ab4d8929)  发表于  2020-03-05 09:38

Tags：rust，每周一知

本文是Amos博客文章[“Working with strings in Rust”](https://fasterthanli.me/blog/2020/working-with-strings-in-rust/)的翻译。

人们选择Rust编程语言时总会遇到一个问题：为什么会有两种字符串类型？为什么会出现String和&str？

Amos在其另一篇文章["declarative-memory-management"](https://fasterthanli.me/blog/2019/declarative-memory-management)中部分回答了这个问题。但是在本文中又进行了一些实验，看看是否可以为Rust的做法“辩护”。文章主要分为C和Rust两大部分。

首先是C语言部分：

-   print程序示例
-   UTF-8编码
-   print程序处理UTF-8编码
-   传递字符串

### C语言的print程序示例

让我们从简单C程序开始，打印参数。

```
// in `print.c`

#include <stdio.h> // for printf

int main(int argc, char **argv) {
    for (int i = 0; i < argc; i++) {
        char *arg = argv[i];
        printf("%s\n", arg);
    }

    return 0;
}

```

```
$ gcc print.c -o print
$ ./print "ready" "set" "go"
./print
ready
set
go

```

好的！很简单。程序使用的是标准的`C11`主函数签名，该签名用`int`定义参数个数（`argc`，参数计数），和用`char**`或`char *[]`“字符串数组”定义参数（`argv`，参数向量）。然后，使用`printf`格式说明符`%s`将每个参数打印为字符串，其后跟`\n`换行符。确实，它将每个参数打印在自己的行上。

在继续之前，请确保我们对正在发生的事情有正确的了解。修改以上的程序，使用`%p`格式说明符打印指针！

```
// in `print.c`

int main(int argc, char **argv) {
    printf("argv = %p\n", argv); // new!
    for (int i = 0; i < argc; i++) {
        char *arg = argv[i];
        printf("argv[%d] = %p\n", i, argv[i]); // new!
        printf("%s\n", arg);
    }

    return 0;
}

```

```
$ gcc print.c -o print
$ ./print "ready" "set" "go"
argv = 0x7ffcc35d84a8
argv[0] = 0x7ffcc35d9039
./print
argv[1] = 0x7ffcc35d9041
ready
argv[2] = 0x7ffcc35d9047
set
argv[3] = 0x7ffcc35d904b
go

```

好的，`argv`是一个地址数组，在这些地址上有字符串数据。像这样：

![rust-string-argv1](https://raw.githubusercontent.com/lesterli/blockchain/master/images/rust_string_argv1.png)

`printf`的`%s`格式符怎么知道什么时候停止打印？因为它只获得一个地址，而不是起始地址和结束地址，或者起始地址和长度。让我们尝试自己打印每个参数：

```
// in `print.c`

#include <stdio.h> // printf

int main(int argc, char **argv) {
    for (int i = 0; i < argc; i++) {
        char *arg = argv[i];
        // we don't know where to stop, so let's just print 15 characters.
        for (int j = 0; j < 15; j++) {
            char character = arg[j];
            // the %c specifier is for characters
            printf("%c", character);
        }
        printf("\n");
    }

    return 0;
}

```

```
$ gcc print.c -o print
$ ./print "ready" "set" "go"
./printreadys
readysetgoCD
setgoCDPATH=.
goCDPATH=.:/ho

```

哦哦～我们的命令行参数相互“渗入”。让我们尝试将我们的程序通过管道`xxd`传输到一个十六进制的转储程序中，以查看发生了什么事：

```
$ # note: "-g 1" means "show groups of one byte",
$ # xxd defaults to "-g 2".
$ ./print "ready" "set" "go" | xxd -g 1
00000000: 2e 2f 70 72 69 6e 74 00 72 65 61 64 79 00 73 0a  ./print.ready.s.
00000010: 72 65 61 64 79 00 73 65 74 00 67 6f 00 43 44 0a  ready.set.go.CD.
00000020: 73 65 74 00 67 6f 00 43 44 50 41 54 48 3d 2e 0a  set.go.CDPATH=..
00000030: 67 6f 00 43 44 50 41 54 48 3d 2e 3a 2f 68 6f 0a  go.CDPATH=.:/ho.

```

啊啊！它们确实彼此跟随，但是两者之间有一些区别：这是相同的输出，用`^^`进行注释的位置是分隔符：

```
00000000: 2e 2f 70 72 69 6e 74 00 72 65 61 64 79 00 73 0a  ./print.ready.s.
          .  /  p  r  i  n  t  ^^ r  e  a  d  y  ^^ 

```

似乎每个参数都由值0来终止。确实，C具有以null终止的字符串。因此，我们可以“修复”我们的打印程序：

```
#include <stdio.h> // printf

int main(int argc, char **argv) {
    for (int i = 0; i < argc; i++) {
        char *arg = argv[i];
        // note: the loop condition is gone, we just loop forever.
        // well, until a 'break' at least.
        for (int j = 0;; j++) {
            char character = arg[j];

            // technically, we ought to use '\0' rather than just 0,
            // but even `gcc -Wall -Wextra -Wpedantic` doesn't chastise
            // us, so let's just go with it.
            if (character == 0) {
                break;
            }
            printf("%c", character);
        }
        printf("\n");
    }

    return 0;
}

```

```
$ gcc print.c -o print
$ ./print "ready" "set" "go"
./print
ready
set
go

```

一切都更好！虽然，我们也需要修复图：

![rust-string-argv2](https://raw.githubusercontent.com/lesterli/blockchain/master/images/rust_string_argv2.png)

> 提示：可能已经注意到，当我们的打印程序超出参数范围时，`CDPATH=.:/ho`也会显示出来。那是（一部分）环境变量！这些都在GNU C库glibc中程序参数旁边。但是具体细节不在本文讨论范围之内，需要查看制作自己的可执行打包程序系列。

好的！现在我们完全了解发生了什么，让我们做一些更有趣的事情：将参数转换为大写。因此，如果我们运行`./print hello`，它应该打印HELLO。我们也将跳过第一个参数，因为它是程序的名称，现在对我们而言这并不是很有趣。

```
#include <stdio.h> // printf
#include <ctype.h> // toupper

int main(int argc, char **argv) {
    // start from 1, skips program name
    for (int i = 1; i < argc; i++) {
        char *arg = argv[i];
        for (int j = 0;; j++) {
            char character = arg[j];
            if (character == 0) {
                break;
            }
            printf("%c", toupper(character));
        }
        printf("\n");
    }

    return 0;
}

```

```
$ gcc print.c -o print
$ ./print "hello"
HELLO

```

好的！太好了！在我看来功能齐全，可以发货了。出于谨慎考虑，让我们运行最后一个测试：

```
$ gcc print.c -o print
$ ./print "élément"
éLéMENT

```

哦～我们真正想要的是“ÉLÉMENT”，但显然，我们还没有弄清正在发生的一切。好的，也许现在大写字母太复杂了，让我们做些简单的事情：打印每个字符并用空格隔开。

```
// in `print.c`

#include <stdio.h> // printf

int main(int argc, char **argv) {
    for (int i = 1; i < argc; i++) {
        char *arg = argv[i];
        for (int j = 0;; j++) {
            char character = arg[j];
            if (character == 0) {
                break;
            }
            // notice the space following `%c`
            printf("%c ", character);
        }
        printf("\n");
    }

    return 0;
}

```

```
$ gcc print.c -o print
$ ./print "élément"
  l   m e n t 

```

不好了。这不会做，根本不会做。让我们回到最后一个行为良好的版本，该版本仅打印每个字符，中间没有空格，并查看输出的实际内容。

```
// in main
// in for
// in second for
            printf("%c", character); // notice the lack of space after `%c`

```

```
$ gcc print.c -o print
$ ./print "élément" | xxd -g 1
00000000: c3 a9 6c c3 a9 6d 65 6e 74 0a                    ..l..ment.
          ^^^^^    ^^^^^

```

如果正确阅读此信息，则“é”不是一个`char`，实际上是2个`char`。好像...很奇怪。

让我们快速编写一个`JavaScript`程序，并使用`Node.js`运行它：

```
// in `print.js`

const { argv, stdout } = process;

// we have to skip *two* arguments: the path to node,
// and the path to our script
for (const arg of argv.slice(2)) {
    for (const character of arg) {
        stdout.write(character);
        stdout.write(" ");
    }
    stdout.write("\n");
}

```

```
$ node print.js "élément"
é l é m e n t

```

啊! 好多了！`Node.js`能正确转换为大写吗？

```
// in `print.js`

const { argv, stdout } = process;

for (const arg of argv.slice(2)) {
    stdout.write(arg.toUpperCase());
    stdout.write("\n");
}

```

```
$ node print.js "élément"
ÉLÉMENT

```

它可以。让我们看一下十六进制转储：

```
$ node print.js "élément" | xxd -g 1
00000000: c3 89 4c c3 89 4d 45 4e 54 0a                    ..L..MENT.
          ^^^^^    ^^^^^

```

虽然`Node.js`程序行为与预期相同，但我们可以看到，`É`也与其他字母不同，“c3 a9”的大写字母对应为“c3 89”。

C程序没有正常工作，因为它将“c3”和“a9”独立对待，它应将其看作一个单一的“Unicode值”。为什么将“é”编码为“c3 a9”？现在是时候进行快速的UTF-8编码入门了。

### 快速的UTF-8入门

“abcdefghijklmnopqrstuvwxyz”，“ABCDEFGHIJKLMNOPQRSTUVWXYZ”和“123456789”以及“!@＃$％^＆*()”等字符都有对应的数字值。例如，“A”的数字值是65。为什么会这样呢？这是个惯例，计算机只知道数字，而我们经常使用字节作为最小单位，因此很久以前人们决定，如果一个字节的值为65，则它表示字母“A”。

由于ASCII是7位编码，因此它具有128个可能的值：0到127（含0）。但是在现代机器上，一个字节为8位，因此还有“另外”128个可能的值。大家都以为。我们可以在其中填充“特殊字符”：

![rust-string-cp437](https://raw.githubusercontent.com/lesterli/blockchain/master/images/rust_string_cp437.png)

不只是ASCII，而是ASCII加我们选择的128个字符。当然有很多语言，因此并非每种语言的非ASCII字符都可以容纳这些额外的128个值，因此对于那些大于127的值，有几种替代的解释。这些解释被称为“代码页”。上面的图片是Codepage 437，也称为CP437，OEM-US，OEM 437，PC-8或DOS Latin US。

如果不关心大写字母，那么对于法语这样的语言来说已经足够了。但是对所有东欧语言，这是不够的，甚至一开始没覆盖亚洲语言。因此，日本想出了自己的办法，他们用日元符号代替了ASCII的反斜杠，并用上划线代替了波浪号，并引入了双字节字符，因为有128个额外的字符对他们来说还不够。

对于使用小字母的语言，人们使用诸如Windows-1252之类的代码页已有多年了，西方世界中的大多数文本仍然有点像ASCII，也称为“扩展ASCII”。但是最终，世界集体开始整理他们的事务，并决定采用UTF-8，该UTF-8：

-   看起来像ASCII字符的ASCII（未扩展），并且使用相同的空格。
-   允许更多的字符，多字节序列。

在这之前人们会问：两个字节还不够吗？（或者是两个双字节字符的序列？），当然也可以是四个字节，但是最终，由于诸如紧凑性之类的重要原因，并为使大多数C程序保持half-broken而不是完全不可用，采用了UTF-8。

除了微软。他们做了，但感觉太少，太迟了。内部一切仍然是UTF-16。RIP。

那么，ASCII加多字节字符序列，它如何工作？相同的基本原理，每个字符都有一个值，因此在Unicode中，“é”的数字是“e9”，我们通常这样写“U+00E9”。0xE9是十进制，其大于127，所以它不是ASCII 233，而我们需要做多字节编码。

UTF-8如何进行多字节编码？使用位序列！

-   如果一个字节以110开头，则意味着我们需要两个字节
-   如果一个字节以1110开头，则意味着我们需要三个字节
-   如果一个字节以11110开头，则意味着我们需要四个字节
-   如果一个字节以10开头，则表示它是多字节字符序列的延续。

因此，对于具有“U+00E9”的“é”，其二进制表示形式为“11101001”，并且我们知道我们将需要两个字节，因此我们应该具有以下内容：

![string-utf8-encoding1](https://raw.githubusercontent.com/lesterli/blockchain/master/images/string_utf8_encoding1.png)

我们可以看到两个字节的UTF-8序列为我们提供11位存储空间：第一个字节为5位，第二个字节为6位。我们只需要8位，因此我们从右到左填充它们，首先是最后6位：

![string-utf8-encoding2](https://raw.githubusercontent.com/lesterli/blockchain/master/images/string_utf8_encoding2.png)

然后是剩下的2位：

![string-utf8-encoding3](https://raw.githubusercontent.com/lesterli/blockchain/master/images/string_utf8_encoding3.png)

其余的位填充零：

![string-utf8-encoding4](https://raw.githubusercontent.com/lesterli/blockchain/master/images/string_utf8_encoding4.png)

大功告成！0b11000011是0xC3和0b10101001是0xA9。与我们之前看到的相对应：“é”是“c3 a9”。

### 返回C的print程序

所以C程序，如果要真正分离字符，则必须进行一些UTF-8解码。我们仍然可以尝试自己做。

```
// in `print.c`

#include <stdio.h> // printf
#include <stdint.h> // uint8_t

void print_spaced(char *s) {
    // start at the beginning
    int i = 0;

    while (1) {
        // we're going to be shifting bytes around,
        // so treat them like unsigned 8-bit values
        uint8_t c = s[i];
        if (c == 0) {
            // reached null terminator, stop printing
            break;
        }

        // length of the sequence, ie., number of bytes
        // that encode a single Unicode scalar value
        int len = 1;
        if (c >> 5 == 0b110) {
            len = 2;
        } else if (c >> 4 == 0b1110) {
            len = 3;
        } else if (c >> 3 == 0b11110) {
            len = 4;
        }

        // print the entire UTF-8-encoded Unicode scalar value
        for (; len > 0; len--) {
            printf("%c", s[i]);
            i++;
        }
        // print space separator
        printf(" ");
    }
}

int main(int argc, char **argv) {
    for (int i = 1; i < argc; i++) {
        print_spaced(argv[i]);
        printf("\n");
    }

    return 0;
}

```

没有讨论String和&str。关于Rust字符串处理的文章却没有Rust代码，而且已经花了大约十分钟！

程序有效吗？

```
$ gcc print.c -o print
$ ./print "eat the rich"
e a t   t h e   r i c h 

```

```
$ ./print "platée de rösti"
p l a t é e   d e   r ö s t i 

```

```
$ ./print "23€ ≈ ¥2731"
2 3 €   ≈   ¥ 2 7 3 1 

```

```
$ ./print "text 🤷 encoding"
t e x t   🤷   e n c o d i n g

```

好吧，我不知道每个人都在抱怨什么，UTF-8超易实现，只花了我们几分钟时间，而且100％正确，符合标准，永远适用于所有输入，并且始终做正确的事。是吗？反例来了，考虑以下字符串：

```
$ echo "noe\\u0308l"
noël

```

这只是法国的圣诞节！当然，我们的程序可以解决此问题，而且不会费力：

```
$ ./print $(echo "noe\\u0308l")
n o e ̈ l 

```

哦哦～事实上，U+0308是“组合解析”，是“仅在前一个字符上打两个点”。实际上，如果需要，我们可以打更多的东西（以增加圣诞节的欢呼声）：

> 提示：显示单个“形状”的多个标量值的组合被称为“字素簇”，了解更多有关内容阅读Henri Sivonen的文章  ["🤦🏼‍♂️".length == 7](https://hsivonen.fi/string-length/)。

> 另外，由于作者Amos是法国人，整篇文章都带有Latin-1偏爱。了解更多有关内容阅读Manish Goregaokar的文章[Breaking Our Latin-1 Assumptions](https://manishearth.github.io/blog/2017/01/15/breaking-our-latin-1-assumptions/)。

因此，也许我们的程序并未实现UTF-8编码的所有微妙之处，但是我们已经接近了。我们现在暂时不考虑字符的组合，而将重点放在Unicode标量值上。我们想要的是：

-   解码我们的输入，将其从UTF-8转换为一系列Unicode标量值（我们将选择uint32_t）
-   将标量值转换为大写对应值
-   重新编码为UTF-8
-   打印到控制台

因此，让我们从一个decode_utf8函数开始。我们将只处理2个字节的序列：

```
// in `upper.c`

#include <stdio.h> // printf
#include <stdint.h> // uint8_t, uint32_t
#include <stdlib.h> // exit

void decode_utf8(char *src, uint32_t *dst) {
    int i = 0;
    int j = 0;

    while (1) {
        uint8_t c = src[i];
        if (c == 0) {
            dst[j] = 0;
            break; // null terminator
        }

        uint32_t scalar;
        int len;

        if (c >> 3 == 0b11110) {
            fprintf(stderr, "decode_utf8: 4-byte sequences are not supported!\n");
            exit(1);
        } if (c >> 4 == 0b1110) {
            fprintf(stderr, "decode_utf8: 3-byte sequences are not supported!\n");
            exit(1);
        } else if (c >> 5 == 0b110) {
            // 2-byte sequence
            uint32_t b1 = (uint32_t) src[i];
            uint32_t b2 = (uint32_t) src[i + 1];
            uint32_t mask1 = 0b0000011111000000;
            uint32_t mask2 = 0b0000000000111111;

            scalar = ((b1 << 6) & mask1) | ((b2 << 0) & mask2);
            len = 2;
        } else {
            // 1-byte sequence
            scalar = (uint32_t) c;
            len = 1;
        }
        dst[j++] = scalar;
        i += len;
    }
}

int main(int argc, char **argv) {
    uint32_t scalars[1024]; // hopefully that's enough
    decode_utf8(argv[1], scalars);

    for (int i = 0;; i++) {
        if (scalars[i] == 0) {
            break;
        }
        printf("U+%04X ", scalars[i]);
    }
    printf("\n");

    return 0;
}

```

```
$ gcc upper.c -o upper
$ ./upper "noël"
U+006E U+006F U+00EB U+006C 

```

从逻辑上讲，U+00EB应该是“ë”的代码位置，确实是的！

它的全名是“带Diaeresis的拉丁文小写字母E”。因此，现在我们只需要进行反向转换即可！

```
// in `upper.c`

void encode_utf8(uint32_t *src, char *dst) {
    int i = 0;
    int j = 0;

    while (1) {
        uint32_t scalar = src[i];

        if (scalar == 0) {
            dst[j] = 0; // null terminator
            break;
        }

        if (scalar > 0b11111111111) {
            fprintf(stderr, "Can only encode codepoints <= 0x%x", 0b11111111111);
            exit(1);
        }

        if (scalar > 0b1111111) { // 7 bits
            // 2-byte sequence

            uint8_t b1 = 0b11000000 | ((uint8_t) ((scalar & 0b11111000000) >> 6));
            //           2-byte marker              first 5 of 11 bits

            uint8_t b2 = 0b10000000 | ((uint8_t) (scalar & 0b111111));
            //           continuation               last 6 of 11 bits  

            dst[j + 0] = b1;
            dst[j + 1] = b2;
            j += 2;
        } else {
            // 1-byte sequence
            dst[j] = (char) scalar;
            j++;
        }

        i++;
    }
}

// omitted: decode_utf8

int main(int argc, char **argv) {
    uint32_t scalars[1024]; // hopefully that's enough
    decode_utf8(argv[1], scalars);

    for (int i = 0;; i++) {
        if (scalars[i] == 0) {
            break;
        }
        printf("U+%04X ", scalars[i]);
    }
    printf("\n");

    uint8_t result[1024]; // yolo
    encode_utf8(scalars, result);

    printf("%s\n", result);

    return 0;
}

```

```
$ gcc upper.c -o upper
$ ./upper "noël"
U+006E U+006F U+00EB U+006C 
noël

```

太棒了！现在，我们需要的只是某种转换表！从小写的代码位置到大写的对应值。我们将编写足以支持法语的内容：

```
#include <ctype.h> // toupper

int main(int argc, char **argv) {
    uint32_t scalars[1024]; // hopefully that's enough
    decode_utf8(argv[1], scalars);

    for (int i = 0;; i++) {
        if (scalars[i] == 0) {
            break;
        }
        printf("U+%04X ", scalars[i]);
    }
    printf("\n");

    // this is the highest codepoint we can decode/encode successfully
    const size_t table_size = 0b11111111111;
    uint32_t lower_to_upper[table_size];
    // initialize the table to just return the codepoint unchanged
    for (uint32_t cp = 0; cp < table_size; cp++) {
        lower_to_upper[cp] = cp;
    }
    // set a-z => A-Z
    for (int c = 97; c <= 122; c++) { // ha.
        lower_to_upper[(uint32_t) c] = (uint32_t) toupper(c);
    }

    // note: nested functions is a GNU extension!
    void set(char *lower, char *upper) {
        uint32_t lower_s[1024];
        uint32_t upper_s[1024];
        decode_utf8(lower, lower_s);
        decode_utf8(upper, upper_s);
        for (int i = 0;; i++) {
            if (lower_s[i] == 0) {
                break;
            }
            lower_to_upper[lower_s[i]] = upper_s[i];
        }
    }
    // set a few more
    set(
        "éêèàâëüöïÿôîçæœ",
        "ÉÊÈÀÂËÜÖÏŸÔÎÇÆŒ"
    );

    // now convert our scalars to upper-case
    for (int i = 0;; i++) {
        if (scalars[i] == 0) {
            break;
        }
        scalars[i] = lower_to_upper[scalars[i]];
    }

    uint8_t result[1024]; // yolo
    encode_utf8(scalars, result);

    printf("%s\n", result);

    return 0;
}

```

```
$ gcc upper.c -o upper
$ ./upper "Voix ambiguë d'un cœur qui, au zéphyr, préfère les jattes de kiwis"
U+0056 U+006F U+0069 U+0078 U+0020 U+0061 U+006D U+0062 U+0069 U+0067 U+0075 U+00EB U+0020 U+0064 U+0027 U+0075 U+006E U+0020 U+0063 U+0153 U+0075 U+0072 U+0020 U+0071 U+0075 U+0069 U+002C U+0020 U+0061 U+0075 U+0020 U+007A U+00E9 U+0070 U+0068 U+0079 U+0072 U+002C U+0020 U+0070 U+0072 U+00E9 U+0066 U+00E8 U+0072 U+0065 U+0020 U+006C U+0065 U+0073 U+0020 U+006A U+0061 U+0074 U+0074 U+0065 U+0073 U+0020 U+0064 U+0065 U+0020 U+006B U+0069 U+0077 U+0069 U+0073 
VOIX AMBIGUË D'UN CŒUR QUI, AU ZÉPHYR, PRÉFÈRE LES JATTES DE KIWIS

```

### 传递字符串

首先，是C程序，C很容易！只需使用`char *`。

```
// in `woops.c`

#include <stdio.h>

int len(char *s) {
    int l = 0;
    while (s[l]) {
        l++;
    }
    return l;
}

int main(int argc, char **argv) {
    char *arg = argv[1];
    int l = len(arg);
    printf("length of \"%s\" = %d\n", arg, l);
}

```

```
$ # we're back into the parent of the "rustre" directory
$ # (in case you're following along)
$ gcc woops.c -o woops
$ ./woops "dog"
length of "dog" = 3

```

看到？简单！没什么`String/&str`。回到现实。首先，这实际上不是字符串的长度。它是使用UTF-8对其进行编码所需的字节数。因此，例如：

```
$ ./woops "née"
length of "née" = 4

$ ./woops "🐈"
length of "🐈" = 4

```

我们不会花费一半的文章来实现UTF-8解码器和编码器，只是感到惊讶的是，我们无法正确地计算字符数。而且，那不是现在困扰我的事情。现在困扰我的是，编译器没有采取任何措施阻止我们执行此操作：

```
#include <stdio.h>

int len(char *s) {
    s[0] = '\0';
    return 0;
}

int main(int argc, char **argv) {
    char *arg = argv[1];
    int l = len(arg);
    printf("length of \"%s\" = %d\n", arg, l);
}

```

```
$ gcc woops.c -o woops
$ ./woops "some user input"
length of "" = 0

```

`len()`是正确的，将通过单元测试。通过它执行完成时，字符串的长度是零。如果没有人愿意去看`len`函数本身，例如，如果它在第三方库中，或更糟的是在专有的第三方库中，那么调试将很有趣。当然，C有`const`：

```
int len(const char *s) {
    s[0] = '\0';
    return 0;
}

```

但它不会通过编译：

```
woops.c: In function ‘len’:
woops.c:4:10: error: assignment of read-only location ‘*s’
    4 |     s[0] = '\0';
      |    

```

修改下：

```
int len(const char *s) {
    char *S = (void *) s;
    S[0] = '\0';
    return 0;
}

```

现在它再次通过编译，运行它，它会默默地覆盖我们的输入字符串，就像之前一样。

接下来是Rust程序部分：

-   print程序
-   错误处理
-   迭代
-   传递字符串转换成大写
-   索引

### print程序

让我们看看实现打印参数，Rust程序是怎样实现的：

```
$ cargo new rustre
     Created binary (application) `rustre` package
$ cd rustre

```

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");
    println!("{}", arg.to_uppercase());
}

```

以上内容的说明：`std::env::args()`返回一个`Iterator`字符串。`skip(1)`忽略程序名称（通常是第一个参数），`next()`获取迭代器中的下一个元素（第一个“实际”）参数。可能有下一个参数，也可能没有。如果没有，`.expect(msg)`通过停止程序打印`msg`。如果有，就有了一个`Option<String>`！

```
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.01s
     Running `target/debug/rustre`
thread 'main' panicked at 'should have one argument', src/libcore/option.rs:1188:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace.

```

好的！因此，当我们不传递参数时，运行程序会有如上输出。让我们传递一些测试字符串：

```
$ cargo run --quiet -- "noël"
NOËL
$ cargo run --quiet -- "trans rights"
TRANS RIGHTS
$ cargo run --quiet -- "voix ambiguë d'un cœur qui, au zéphyr, préfère les jattes de kiwis"
VOIX AMBIGUË D'UN CŒUR QUI, AU ZÉPHYR, PRÉFÈRE LES JATTES DE KIWIS
$ cargo run --quiet -- "heinz große"
HEINZ GROSSE

```

一切都测试了！最后一个特别酷，用德语的“ß”，确实是“ss”的连字。好吧，这很复杂，但这就是要点。

### 错误处理

因此Rust的行为就像字符串是UTF-8一样，这意味着它必须在某个时刻解码我们的命令行参数，意味着这可能会失败。但是，只在没有参数的情况下看到错误处理，而对于参数无效的UTF-8则看不到错误处理。什么是无效的UTF-8？好吧，我们已经看到“é”被编码为“c3 e9”，所以可以这样工作：

```
$ cargo run --quiet -- $(printf "\\xC3\\xA9")
É

```

我们已经看到一个双字节的UTF-8序列具有：

-   在第一个字节中指示它是一个双字节的序列（前三个位，110）
-   在第二个字节中指示它是多字节序列的延续（前两个位10）

如果我们开始读取一个双字节的序列，然后突然停止怎么办？如果我们传入了C3，但未传入A9呢？

```
$ cargo run --quiet -- $(printf "\\xC3")
thread 'main' panicked at 'called `Result::unwrap()` on an `Err` value: "\xC3"', src/libcore/result.rs:1188:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace.

```

查看错误堆栈信息。

```
$ RUST_BACKTRACE=1 cargo run --quiet -- $(printf "\\xC3")
thread 'main' panicked at 'called `Result::unwrap()` on an `Err` value: "\xC3"', src/libcore/result.rs:1188:5                                                
stack backtrace:
(cut)
  13: core::result::unwrap_failed
             at src/libcore/result.rs:1188
  14: core::result::Result<T,E>::unwrap
             at /rustc/5e1a799842ba6ed4a57e91f7ab9435947482f7d8/src/libcore/result.rs:956
  15: <std::env::Args as core::iter::traits::iterator::Iterator>::next::{{closure}}
             at src/libstd/env.rs:789
  16: core::option::Option<T>::map
             at /rustc/5e1a799842ba6ed4a57e91f7ab9435947482f7d8/src/libcore/option.rs:450
  17: <std::env::Args as core::iter::traits::iterator::Iterator>::next
             at src/libstd/env.rs:789
  18: <&mut I as core::iter::traits::iterator::Iterator>::next
             at /rustc/5e1a799842ba6ed4a57e91f7ab9435947482f7d8/src/libcore/iter/traits/iterator.rs:2991
  19: core::iter::traits::iterator::Iterator::nth
             at /rustc/5e1a799842ba6ed4a57e91f7ab9435947482f7d8/src/libcore/iter/traits/iterator.rs:323
  20: <core::iter::adapters::Skip<I> as core::iter::traits::iterator::Iterator>::next
             at /rustc/5e1a799842ba6ed4a57e91f7ab9435947482f7d8/src/libcore/iter/adapters/mod.rs:1657
  21: rustre::main
             at src/main.rs:2
(cut)

```

基本上是这样：

-   在`main()`
-   我们调用`Iterator`的`.next()`
-   最后调用`Result`的`.unwrap()`
-   此时panicked

这意味着只有当我们尝试将参数作为String获取时，它才会出现panic。如果我们将其作为`OsString`，就不会panic：

```
fn main() {
    let arg = std::env::args_os()
        .skip(1)
        .next()
        .expect("should have one argument");
    println!("{:?}", arg)
}

```

```
$ cargo run --quiet -- hello
"hello"
$ cargo run --quiet $(printf "\\xC3")
"\xC3"

```

但是它没有`.to_uppercase()`方法。因为它是一个`OsString`，它是一系列字节。C程序如何处理无效的UTF-8输入？

```
$ ../upper $(printf "\\xC3")
U+00C0 U+0043 U+0044 U+0050 U+0041 U+0054 U+0048 U+003D U+002E U+003A U+002F U+0068 U+006F U+006D U+0065 U+002F U+0061 U+006D U+006F U+0073 U+002F U+0072 U+0075 U+0073 U+0074 U+003A U+002F U+0068 U+006F U+006D U+0065 U+002F U+0061 U+006D U+006F U+0073 U+002F U+0067 U+006F U+003A U+002F U+0068 U+006F U+006D U+0065 U+002F U+0061 U+006D U+006F U+0073 U+002F U+0066 U+0074 U+006C U+003A U+002F U+0068 U+006F U+006D U+0065 U+002F U+0061 U+006D U+006F U+0073 U+002F U+0070 U+0065 U+0072 U+0073 U+006F U+003A U+002F U+0068 U+006F U+006D U+0065 U+002F U+0061 U+006D U+006F U+0073 U+002F U+0077 U+006F U+0072 U+006B 
ÀCDPATH=.:/HOME/AMOS/RUST:/HOME/AMOS/GO:/HOME/AMOS/FTL:/HOME/AMOS/PERSO:/HOME/AMOS/WORK

```

答案是：不好。实际上一点也不好。UTF-8解码器首先读取C3，然后读取下一个字节（是空终止符），结果应为“à”。但它不再停下来，而是读完参数末尾，直接进入环境块，找到第一个环境变量。现在，在这种情况下，这似乎很温和。但是如果该C程序被用作Web服务器的一部分，并且其输出直接显示给用户怎么办？如果第一个环境变量不是`CDPATH`，而是  `SECRET_API_TOKEN`怎么办？那将是一场灾难。

但如果命令行参数是无效的UTF-8，Rust程序就会尽早panic。如果想优雅地处理这种情况怎么办？可以使用`OsStr::to_str`，它返回一个`Option`值。

```
fn main() {
    let arg = std::env::args_os()
        .skip(1)
        .next()
        .expect("should have one argument");

    match arg.to_str() {
        Some(arg) => println!("valid UTF-8: {}", arg),
        None => println!("not valid UTF-8: {:?}", arg),
    }
}

```

```
$ cargo run --quiet -- "é"
valid UTF-8: é
$ cargo run --quiet -- $(printf "\\xC3")
not valid UTF-8: "\xC3"

```

精彩。我们学到了什么？

在Rust中，只要你不明确地用`unsafe`，类型`String`的值永远是有效的UTF-8。如果尝试使用无效的UTF-8构建`String`，则会出现错误。一些程序，像`std::env::args()`会隐藏错误处理，因为错误的情况非常少。但它仍然会检查错误，并会检查是否发生错误，因为这样做是安全的。

相比之下，C没有字符串类型。它甚至没有真正的字符类型。char是一个ASCII字符加上一个附加位，实际上，它只是一个带符号的8位整数：`int8_t`。绝对不能保证`char *`其中的任何内容都是有效的UTF-8。没有与`char *`关联的编码，只是内存中的地址。也没有关联的长度，计算其长度涉及找到空终止符。空终止字符也是一个严重的安全问题，更不用说NUL是有效的Unicode字符，因此以空字符结尾的字符串不能表示所有有效的UTF-8字符串。

### 迭代 Iteration

我们将如何用空格分隔字符？

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");

    for c in arg.chars() {
        print!("{} ", c);
    }
    println!()
}

```

```
$ cargo run --quiet -- "cup of tea"
c u p   o f   t e a 

```

很简单！让我们尝试使用非ASCII字符：

```
$ cargo run --quiet -- "23€ ≈ ¥2731"
2 3 €   ≈   ¥ 2 7 3 1 
$ cargo run --quiet -- "memory safety 🥺 please 🙏"
m e m o r y   s a f e t y   🥺   p l e a s e   🙏 

```

一切似乎都很好。如果我们要打印Unicode标量值的数字而不是它们的字形，该怎么办？

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");

    for c in arg.chars() {
        print!("{} (U+{:04X}) ", c, c as u32);
    }
    println!()
}

```

```
$ cargo run --quiet -- "aimée"
a (U+0061) i (U+0069) m (U+006D) é (U+00E9) e (U+0065)

```

酷！如果我们想显示其为UTF-8编码怎么办？我的意思是打印单个字节？

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");

    for b in arg.bytes() {
        print!("{:02X} ", b);
    }
    println!()
}

```

```
$ cargo run --quiet -- "aimée"
61 69 6D C3 A9 65 

```

有我们的"c3 a9"！很简单。目前为止，我们还没对类型的担心，在我们的Rust程序中还没有一个`String`或`&str`。所以，让我们去寻找麻烦。

### 传递字符串转换成大写

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");

    println!("upp = {}", uppercase(arg));
    println!("arg = {}", arg);
}

fn uppercase(s: String) -> String {
    s.to_uppercase()
}

```

```
$ cargo build --quiet
error[E0382]: borrow of moved value: `arg`
 --> src/main.rs:8:26
  |
2 |     let arg = std::env::args()
  |         --- move occurs because `arg` has type `std::string::String`, which does not implement the `Copy` trait
...
7 |     println!("upp = {}", uppercase(arg));
  |                                    --- value moved here
8 |     println!("arg = {}", arg);
  |                          ^^^ value borrowed here after move

error: aborting due to previous error

For more information about this error, try `rustc --explain E0382`.
error: could not compile `rustre`.

```

哦，上帝，编译器来了。问题在于我们将arg传入`uppercase()`，然后又再次使用它。我们可以先打印arg，然后再调用uppercase()。那行得通吗？可以。但是，假设我们就是需要先调用`uppercase`呢？

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");

    println!("upp = {}", uppercase(arg.clone()));
    println!("arg = {}", arg);
}

fn uppercase(s: String) -> String {
    s.to_uppercase()
}

```

```
$ cargo run --quiet -- "dog"
upp = DOG
arg = dog

```

但是这有点愚蠢。为什么我们需要克隆arg？只是传入`uppercase`，我们不需要在内存中有第二个拷贝。现在在内存中，我们有：

-   arg（“dog”）
-   arg的拷贝，我们传入`uppercase()`（“dog”）
-   uppercase()返回值（“DOG”）

我猜这是`&str`存在的意义吧？让我们尝试一下：

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");

    println!("upp = {}", uppercase(arg));
    println!("arg = {}", arg);
}

fn uppercase(s: &str) -> String {
    s.to_uppercase()
}

```

```
cargo run --quiet -- "dog"
error[E0308]: mismatched types
 --> src/main.rs:7:36
  |
7 |     println!("upp = {}", uppercase(arg));
  |                                    ^^^
  |                                    |
  |                                    expected `&str`, found struct `std::string::String`
  |                                    help: consider borrowing here: `&arg`

```

根据编译器的提示修改：

```
println!("upp = {}", uppercase(&arg));

```

```
$ cargo run --quiet -- "dog"
upp = DOG
arg = dog

```

为了使其更接近于C代码，我们应该：

-   分配一个“目标”
-   传递“目标”到`uppercase()`
-   `uppercase()`遍历每个字符，将其转换为大写，并将其附加到"目标"

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");

    let mut upp = String::new();
    println!("upp = {}", uppercase(&arg, upp));
    println!("arg = {}", arg);
}

fn uppercase(src: &str, dst: String) -> String {
    for c in src.chars() {
        dst.push(c.to_uppercase());
    }
    dst
}

```

```
$ cargo run --quiet -- "dog"
error[E0308]: mismatched types
  --> src/main.rs:14:18
   |
14 |         dst.push(c.to_uppercase());
   |                  ^^^^^^^^^^^^^^^^ expected `char`, found struct `std::char::ToUppercase`

```

> ToUppercase，该结构由char上的to_uppercase方法创建，返回一个迭代器，该迭代器生成char的大写等效项。

迭代器，知道这一点，我们可以使用`for x in y`：

```
fn uppercase(src: &str, dst: String) -> String {
    for c in src.chars() {
        for c in c.to_uppercase() {
            dst.push(c);
        }
    }
    dst
}

```

```
$ error[E0596]: cannot borrow `dst` as mutable, as it is not declared as mutable
  --> src/main.rs:15:13
   |
12 | fn uppercase(src: &str, dst: String) -> String {
   |                         --- help: consider changing this to be mutable: `mut dst`
...
15 |             dst.push(c);
   |             ^^^ cannot borrow as mutable

```

让我们看一下`String::push`的声明：

```
pub fn push(&mut self, ch: char)

```

因此`dst.push(c)`与`String::push(&mut dst, c)`完全相同。根据编译器建议修改：

```
fn uppercase(src: &str, mut dst: String) -> String {
	...
}

```

```
$ cargo run --quiet -- "dog"
upp = DOG
arg = dog

```

`uppercase`没有返回值呢？

```
fn uppercase(src: &str, mut dst: String) {
    for c in src.chars() {
        for c in c.to_uppercase() {
            dst.push(c);
        }
    }
}

```

```
cargo run --quiet -- "dog"
error[E0382]: borrow of moved value: `upp`
  --> src/main.rs:10:26
   |
7  |     let upp = String::new();
   |         --- move occurs because `upp` has type `std::string::String`, which does not implement the `Copy` trait
8  |     uppercase(&arg, upp);
   |                     --- value moved here
9  | 
10 |     println!("upp = {}", upp);
   |                          ^^^ value borrowed here after move

```

我们需要让upp可变地借用。

```
fn main() {
    let arg = std::env::args()
        .skip(1)
        .next()
        .expect("should have one argument");

    let mut upp = String::new();
    // was just `upp`
    uppercase(&arg, &mut upp);

    println!("upp = {}", upp);
    println!("arg = {}", arg);
}

// was `mut dst: String`
fn uppercase(src: &str, dst: &mut String) {
    for c in src.chars() {
        for c in c.to_uppercase() {
            dst.push(c);
        }
    }
}

```

```
$ cargo run --quiet -- "dog"
upp = DOG
arg = dog

```

现在又可以使用了！可增长的字符串，这是否意味着我们可以预分配合理大小的String，然后将其重新用于多个uppercase 调用？

### 索引

C允许我们直接索引，Rust允许我们这样做吗？

```
fn main() {
    for arg in std::env::args().skip(1) {
        for i in 0..arg.len() {
            println!("arg[{}] = {}", i, arg[i]);
        }
    }
}

```

```
$ cargo run --quiet -- "dog"
error[E0277]: the type `std::string::String` cannot be indexed by `usize`
 --> src/main.rs:4:41
  |
4 |             println!("arg[{}] = {}", i, arg[i]);
  |                                         ^^^^^^ `std::string::String` cannot be indexed by `usize`
  |
  = help: the trait `std::ops::Index<usize>` is not implemented for `std::string::String`

```

我们不可以。我们可以先将其转换为Unicode标量值数组，然后对其进行索引：

```
fn main() {
    for arg in std::env::args().skip(1) {
        let scalars: Vec<char> = arg.chars().collect();
        for i in 0..scalars.len() {
            println!("arg[{}] = {}", i, scalars[i]);
        }
    }
}

```

```
$ cargo run --quiet -- "dog"
arg[0] = d
arg[1] = o
arg[2] = g

```

是的，行得通！老实说，这样比较好，因为我们只需要解码一次UTF-8字符串，然后我们就可以进行随机访问了。这可能就是为什么它没有实现`Index<usize>`的原因。

有趣的事情：`Index<Range<usize>>`。

```
fn main() {
    for arg in std::env::args().skip(1) {
        let mut stripped = &arg[..];
        while stripped.starts_with(" ") {
            stripped = &stripped[1..]
        }
        while stripped.ends_with(" ") {
            stripped = &stripped[..stripped.len() - 1]
        }
        println!("     arg = {:?}", arg);
        println!("stripped = {:?}", stripped);
    }
}

```

```
$ cargo run --quiet -- "  floating in space   "
     arg = "  floating in space   "
stripped = "floating in space"

```

> String是堆分配的，因为它是可增长的。而&str可以从任何地方引用数据：堆，栈，甚至程序的数据段。

`&str`，它是不同的，它指向相同的内存区域，只是在不同的偏移量处开始和结束。实际上，我们可以使其成为一个函数：

```
fn main() {
    for arg in std::env::args().skip(1) {
        let stripped = strip(&arg);
        println!("     arg = {:?}", arg);
        println!("stripped = {:?}", stripped);
    }
}

fn strip(src: &str) -> &str {
    let mut dst = &src[..];
    while dst.starts_with(" ") {
        dst = &dst[1..]
    }
    while dst.ends_with(" ") {
        dst = &dst[..dst.len() - 1]
    }
    dst
}

```

而且效果也一样。不过，这似乎很危险。如果原始字符串的内存被释放怎么办？

```
fn main() {
    let stripped;
    {
        let original = String::from("  floating in space  ");
        stripped = strip(&original);
    }
    println!("stripped = {:?}", stripped);
}

```

```
$ cargo run --quiet -- "  floating in space   "
error[E0597]: `original` does not live long enough
 --> src/main.rs:5:26
  |
5 |         stripped = strip(&original);
  |                          ^^^^^^^^^ borrowed value does not live long enough
6 |     }
  |     - `original` dropped here while still borrowed
7 |     println!("stripped = {:?}", stripped);
  |                                 -------- borrow later used here

```

在Rust中？编译器将检查所有的"恶作剧"。

最后，String用范围索引，很酷，但是`..`是字符范围吗？

```
fn main() {
    for arg in std::env::args().skip(1) {
        println!("first four = {:?}", &arg[..4]);
    }
}

```

```
$ cargo run --quiet -- "want safety?"
first four = "want"
$ cargo run --quiet -- "🙈🙉🙊💥"
first four = "🙈"

```

字节范围。我以为所有Rust字符串都是UTF-8？但是使用切片，我们可以得到部分多字节序列，或无效的UTF-8？假如：

```
fn main() {
    for arg in std::env::args().skip(1) {
        println!("first two = {:?}", &arg[..2]);
    }
}

```

```
$ cargo run --quiet -- "🙈🙉🙊💥"
thread 'main' panicked at 'byte index 2 is not a char boundary; it is inside '🙈' (bytes 0..4) of `🙈🙉🙊💥`', src/libcore/str/mod.rs:2069:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace.

```

那太好了。它会panic，这是安全的事情。

### 结束语

无论如何，这篇文章已经很长了。希望它对Rust中的字符串处理有足够的介绍，以及Rust为什么同时具有String和&str。

答案当然依旧是安全性，正确性和性能。

在我们编写的最后一个Rust字符串操作程序时，确实遇到了障碍，但是它们主要是编译时错误或panic。我们没有一次：

-   从无效地址读取
-   写入无效的地址
-   忘了释放东西
-   覆盖了其他一些数据
-   需要一个额外的工具来告诉我们问题出在哪里

而且，加上令人惊叹的编译器信息以及社区，这就是Rust的美。

### 几个小技巧让你的 Rust 代码性能

不用改动代码，只通过几个技巧就能提高你的 Rust 项目运行速度，比如在 `Cargo.tom` 文件中  `[profile.release]`  下根据情况更改一些字段或许就可以提升你的项目性能：

-   `lto = "fat"`
-   `codegen-units = 1`
-   `target-cpu = "native"`
-   ...

详细介绍：[https://deterministic.space/high-performance-rust.html](https://deterministic.space/high-performance-rust.html)

### Rust blog：近期以及未来的模式匹配改进

Rust 官方博客介绍了即将了即将应用于stable Rust 的模式匹配新特性

#### Subslice 模式匹配，[head, tail @ ..]

`..`  意味着可变间隔，例如

```
fn recover_attrs_no_item(&mut self, attrs: &[Attribute]) -> PResult<'a, ()> {
    let (start, end) = match attrs {
        [] => return Ok(()),
        [x0] => (x0, x0),
        [x0, .., xn] => (x0, xn),
    };
    let msg = if end.is_doc_comment() {
        "expected item after doc comment"
    } else {
        "expected item after attributes"
    };
    let mut err = self.struct_span_err(end.span, msg);
    if end.is_doc_comment() {
        err.span_label(end.span, "this doc comment doesn't document anything");
    }
    if let [.., penultimate, _] = attrs {
        err.span_label(start.span.to(penultimate.span), "other attributes here");
    }
    Err(err)
}

```

其中  `[x0, .., xn]`  就表示匹配第一个以及最后一个元素而忽略中间的所有元素.

另一种用法是可以将subslice约束为一个变量，比如如果我们希望某个函数除了最后一个参数之外的参数不能为  `...`  那么可以这样写：

```
match &*fn_decl.inputs {
    ... // other arms
    [ps @ .., _] => {
        for Param { ty, span, .. } in ps {
            if let TyKind::CVarArgs = ty.kind {
                self.err_handler().span_err(
                    *span,
                    "`...` must be the last argument of a C-variadic function",
                );
            }
        }
    }
}

```

这里的  `ps @ ..`  就表示忽略参数的最后的一个元素而将剩下的元素转化为 变量  `ps`

其他还有

-   Nested OR-patterns
-   Bindings after @
-   Combining by-move and by-ref bindings

详情：  [https://blog.rust-lang.org/inside-rust/2020/03/04/recent-future-pattern-matching-improvements.html](https://blog.rust-lang.org/inside-rust/2020/03/04/recent-future-pattern-matching-improvements.html)

---
++++++
---

## strory

### 社区决定取消Rust LATAM 2020

在过去的几周中，密切监视着'新型冠状病毒肺炎'的情况，并就此情况进行了一些内部讨论。 衷心告知，我们决定取消Rust LATAM 2020。

详细通知[https://rustlatam.org/index.html#cancel-en](https://rustlatam.org/index.html#cancel-en)

### 【Rust日报】2020-03-16 Rust动态

-   AWS 在其博客中介绍了该团队最新的开源项目 Bottlerocket。 据介绍，Bottlerocket 是一种新的基于 Linux 的开源操作系统， 用于在虚拟机或裸机主机上运行容器，主要采用 Rust 代码编写， 并且仅包含运行容器的基本软件。
    
    Bottlerocket 支持 Docker 镜像和其他开放容器倡议 （Open Container Initiative，OCI）支持的平台。 同时，Bottlerocket 依赖于镜像模型，而不是程序包更新系统。
    
    [https://aws.amazon.com/cn/blogs/aws/bottlerocket-open-source-os-for-container-hosting/](https://aws.amazon.com/cn/blogs/aws/bottlerocket-open-source-os-for-container-hosting/)
    
-   sheeit：一个速度飞快的网页版电子表格引擎，支持上千个用户同时编辑上百万个表格单元。  
    [https://github.com/wilfredwee/sheeit](https://github.com/wilfredwee/sheeit)
    
    sheeit依靠四大核心技术支持：
    
    -   支持上千个并发读（和很多写）操作
    -   所有类型的数据操作都非常快
    -   计算公式只有在必要的时候才被激活校验
    -   各种公式计算高速并行同时进行
-   async-graphql v1.0.0 已发布，支持所有GraphQL特性，欢迎试用。
    
    [https://github.com/sunli829/async-graphql](https://github.com/sunli829/async-graphql)
    
-   ripgrep v12.0.0 正式发布 ripgrep是一个按照正则表达式模式搜索当前目录的行搜索工具 v12.0.0主要是修复bug和提高搜索性能，并增加了一点小的新功能。  
    [https://github.com/BurntSushi/ripgrep/releases/tag/12.0.0](https://github.com/BurntSushi/ripgrep/releases/tag/12.0.0)
    
-   最新GitHub最活跃10大编程语言排名Rust名列第4！  
    [https://learnworthy.net/10-most-active-programming-languages-in-github/](https://learnworthy.net/10-most-active-programming-languages-in-github/)
    
    ```
    1. JavaScript  
    2. Python
    3. Java
    4. Rust
    5. PHP
    6. C#
    7. C++
    8. TypeScript 
    9. Ruby
    10. Shell
    11. C
    
    ```
    
-   2020 Rust Conference开始征集发言，教程和论文  
    [https://blog.rust-lang.org/2020/03/10/rustconf-cfp.html](https://blog.rust-lang.org/2020/03/10/rustconf-cfp.html)
    
    RustConf2020将于2020年8月20-21日举办，有意发言或发表论文的请尽快申请。 论文征集开放截止日期是2020年4月5日星期一。  
    [RustConf2020论文征集网站](https://cfp.rustconf.com/events/rustconf-2020)
    
-   Rust游戏编程月报2020年2月期  
    [https://rust-gamedev.github.io/posts/newsletter-007/](https://rust-gamedev.github.io/posts/newsletter-007/)
    
-   五年了，我还在学Rust编程！？！！？！  
    WHAT！？！？(歪帽黑人脑袋顶上好多问好和感叹号) ，Rust语言很强大，也很有趣，不断完善，各种异步函数。。。  
    哈哈哈～～～五年了，我还在学RUST！  
    [https://llogiq.github.io/2020/03/07/learning.html](https://llogiq.github.io/2020/03/07/learning.html)
    

---
++++++
---

## wasm

### 系列博文：实现一个WebAssembly解释器

随着 WebAssembly 越来越火热，medium 上的一位博主开始撰写系列博文，使用 Rust 实现 WebAssembly 解释器，原文请看：https://medium.com/@richardanaya/lets-write-a-web-assembly-interpreter-part-1-287298201d75  ![](https://cdn.nlark.com/yuque/0/2020/png/439468/1585241405654-f49520c5-4c81-4002-8b27-64165dc52bad.png?x-oss-process=image/resize,w_746)

reddit 上参与讨论：https://www.reddit.com/r/rust/comments/foqoxd/lets_write_a_web_assembly_interpreter_part_1/

# Rust: 實際使用Wasm

文章一開始講解了wasm的優缺點 像是是32位開頭而不是64位 指標與介面類型之類的一些基本內容仍然是WIP狀態

下面介紹各種名詞

-   wasm –“機器碼”。設計用於可移植，快速且易於執行的bytecode。
-   wasi –“系統調用”。用於執行基本系統任務（主要是I/O）的API。
-   編譯器- rustc, clang, emscripten等
-   wasmer – wasmer.io上的人製作的直譯器/JIT
-   wasmtime –直譯器/JIT 不同的人做的
-   wapm –與npm類似的軟件包管理器
-   WASI – WebAssembly系統接口，一種POSIX-y API， 為非Web平台上的wasm程式提供系統介面。
-   Cranelift –用Rust編寫的編譯器和JIT後端。在概念上類似LLVM。

詳細請看文章

[Read more](https://bit.ly/38NGnme)

### Yew Form

Yew Form，它是Yew的HTML表单的模型绑定器。支持：

-   Rust结构体和HTML表单控件之间的双向绑定
-   使用Keats验证器（https://github.com/Keats/validator）进行验证
-   支持通过`#[derive(Model)]`定义结构体

[Demo](http://chronogears.com/yew-form/)

## Yew v0.13发布

Yew是使用Rust＆WebAssembly构建客户端Web应用程序的框架。

在[此版本](https://github.com/yewstack/yew/releases/tag/0.13.0)中，增加了对使用[Rust与Web Assembly Working Group](https://rustwasm.github.io/)的基础`web-sys`插件构建Web应用程序的支持。我们也已经开始为事件监听器集成`gloo`插件（也来自rust / wasm工作组）。

此版本中的另一个重大变化是对`Component`属性指定方式的更新。对于上下文，Yew 在使用“ JSX”样式语法声明组件时允许在**编译时**属性检查。在此版本之前，默认情况下将属性视为可选属性，并且如果要按要求将struct字段注释为struct属性，则可以使用宏属性对其进行注释（忘记传递必需的属性会导致编译错误）。对于此版本，我们翻转了默认行为。默认情况下，将属性视为必要的属性，如果使用此类注释，则将其视为可选属性。新语法利用了[Rust 1.34中](https://blog.rust-lang.org/2019/04/11/Rust-1.34.0.html#custom-attributes-accept-arbitrary-token-streams)发布的[令牌自定义属性](https://blog.rust-lang.org/2019/04/11/Rust-1.34.0.html#custom-attributes-accept-arbitrary-token-streams)，如下所示：

```
#[derive(Clone, Properties)]
struct Props {
  #[prop_or(3)],
  countdown: usize,

  #[prop_or_else(Callback::noop)]
  on_click: Callback<()>,

  #[prop_or(true)]
  display: bool,

  #[prop_or_default]
  highlight: bool,

  // implicitly required
  required: MyRequiredValue,

  #[prop_or_default]
  opt_value: Option<Value>,

  // implicitly required
  opt_required: Option<Value>,
}

```

详细发布文档：[https://github.com/yewstack/yew/releases/tag/0.13.0](https://github.com/yewstack/yew/releases/tag/0.13.0)

---
++++++
---

## game

# 有人用rust做了一個wasm遊戲引擎 Oxygengine

今天還有做了Asset browser

[Read more](https://bit.ly/2WNp6r5)

### wasm-tetris - Rust 写的 Tetris 克隆

俄罗斯方块啦，网页上运行的。

https://github.com/ha-shine/wasm-tetris

### Rust Gamedev newletter

#rust #gamedev

[@ozkriff](https://twitter.com/ozkriff)正在创建Rust Gamedev 的newsletter，欢迎各位参与共享，下面是一些issue，你可以找到你感兴趣的解决它。

[Repo](https://github.com/rust-gamedev/rust-gamedev.github.io/issues)

---
++++++
---

---
++++++
---

## story

#### dbcrossbar 0.3.1: 开源大表数据复制工具即将发布新版本

dbcrossbar 0.3.1: Copy large tables between BigQuery, PostgreSQL, RedShift, CSV, S3, etc. (preview release, uses async Rust)

【[作者-emk](https://www.reddit.com/user/emk/)】

大家好，Faraday公司非常慷慨的开源了其表数据复制工具[`dbcrossbar`](https://www.dbcrossbar.org/)。 一年多以来，这个开源工具已经在很多地方被重度用于生产系统，已经到了可以值得勇敢的Rust开发人员认真审视的时候了。 （已经知道未来在Version 1.0还将会有更重大的信息披露）

你可以使用`dbcrossbar`将CSV裸数据快速的导入PostgreSQL，或者将PostgreSQL数据库中的表 在BigQuery里做一个镜像表来做分析应用。`dbcrossbar`提供了各种[常用流行的数据（库）](https://www.dbcrossbar.org/dbcrossbar_guide_0.generated.svg)  的驱动程序，设计目标是用来可以高效的操作大约1GB到500GB范围大小的数据集的。 （更牛的地方是用在计算机集群中去分发不同的数据拷贝）由于`dbcrossbar`使用多个异步的`Rust Streams`'流'和  [`backpressure`](https://ferd.ca/queues-don-t-fix-overload.html)来控制数据流， 所以整个数据复制过程完全不需要写临时文件。在工具程序内部，`dbcrossbar`把一个数据表表达成多个CSV数据流， 这样就避免了用一个大的CSV文件去存整个表的内容的情况，同时也可以使得应用云`buckets`更高效。

`dbcrossbar`支持常用的纯量数据类型，外加数组，JSON，GeoJSON和UUID等， 并且可以在不同类型的数据库之间转换这些类型，还可以通过`--where`命令行选项 做条件过滤，它可以overwrite覆盖写操作数据表，append添加写，甚至可以 (对PostgreSQL和BigQuery)做UPSERT（Update or Insert into a table)操作。 它知道怎么自动的来回将PostgreSQL的表定义转换成BigQuery的表定义。

Rust的异步功能已经在这个开源项目中被证明了Rust是一种超级牛的编程语音。虽然可以预见的 还会在正在进行的开发中遇到各种各样的问题和挑战，但是Rust语言的`ownership and borrowing`  严格规定已经证明可以使同时使用异步功能函数和线程混用而很少出错。同时Rust语言保证了 高超的运行性能。特别需要鸣谢[`u/burntsushi`](https://www.reddit.com/u/burntsushi/)  提供了CSV的`Rust`语言库，以及Rust语言社区提供的各种非得好用和优秀的开源软件包， 那些需要感谢的人名单的确是满满的一长串。

欢迎提交`bug`和代码库的`PR`，具体的指南和安装手册可以看[dbcrossbar的官方网站](https://www.dbcrossbar.org/)。 有问题欢迎骚扰！

### 今晚(2020-03-28)，上海科大Rust线上活动

[活动链接](https://mp.weixin.qq.com/s/ljKJAuHk7cCpnJ4cgbHOuQ)：https://mp.weixin.qq.com/s/ljKJAuHk7cCpnJ4cgbHOuQ

### Rust文档团队，再见

Rust文档团队不再存在。

[博客文章链接](https://blog.rust-lang.org/inside-rust/2020/03/27/goodbye-docs-team.html)：https://blog.rust-lang.org/inside-rust/2020/03/27/goodbye-docs-team.html

# rustc-dev-guide簡介

編譯器對您的程式碼做了什麼？

編譯器是如何做到的？

這其中包含了一大堆問題

-   如何平衡編譯器速度，編譯器記憶體使用、速度、大小、穩定性/正確性等問題？
-   編譯過程的包含哪些階段？如何將它們組合在一起？
-   泛型在編譯過程中會發生什麼？
-   在編譯過程中執行會何種優化？
-   增量編譯如何運作？
-   rustc是否支持並行編譯？

如果您了解編譯器並希望加入rustc-dev-guide

我們歡迎您的貢獻，並期待您的參與！

[Read more](https://bit.ly/2UGVQ2h)

### 【博客】Rust：未来网络世界的系统级编程语言

详情：[https://www.publish0x.com/rhyzom/rust-a-systems-programming-language-for-tomorrows-networked-xzexrk](https://www.publish0x.com/rhyzom/rust-a-systems-programming-language-for-tomorrows-networked-xzexrk)

### MEUSE: 私有的 Cargo crate 注册表

详情：[https://github.com/mcorbin/meuse](https://github.com/mcorbin/meuse)

### regex crate 的发展计划

详情：[https://github.com/rust-lang/regex/issues/656](https://github.com/rust-lang/regex/issues/656)

### TWiR 330

Rust社区很多更新内容，可以查看[详细信息](https://this-week-in-rust.org/blog/2020/03/17/this-week-in-rust-330/)。

BTW：TWiR正在寻找新的维护者。

### `All Hands`  回顾

【来自 Rust 官博的消息】原定于 3 月 16 日至 20 日在希腊塞萨洛尼基举行的 Rust All Hands 活动在 1 月被取消。“All Hands” 是本年度大家最喜欢的活动之一，对于我们今年无法举办该活动，我们感到非常失望。为了保持透明并记录未来事件，我们对发生的事情，所学到的知识以及所有人的未来进行了回顾。

阅读更多请看：https://blog.rust-lang.org/inside-rust/2020/03/18/all-hands-retrospective.html

### 2020 RustConf CFP (Call For Proposals) 正式启动

你有什么关于 Rust 想要分享的吗? 想要谈谈 Rust 的 学习和使用 Rust 的经验吗？或者想深入讲解 Rust 的一个方面? 亦或是有其他的想法？我们都欢迎你的提议！[RustConf 2020 CFP 官网](https://cfp.rustconf.com/events/rustconf-2020)现已上线并接受提议.

详情：[https://cfp.rustconf.com/events/rustconf-2020](https://cfp.rustconf.com/events/rustconf-2020)

### 关于Rust的预测

#rust

[@pauldix](https://twitter.com/pauldix)是InfluxDB的CTO，他在 2014 年的预测是：许多用 Java 编写的基础结构项目将在 Go 中重写。2020年的预测许多在Go编写的基础设施项目将在Rust中重写。点击下面的链接参与讨论。

[Read More](https://twitter.com/pauldix/status/1234563709957296131)

### 考虑使用Rust

越来越多的公司正在考虑是否应该将Rust添加到其技术栈中，这个演讲希望可以帮助做出决定。

[YouTube](https://youtu.be/DnT-LUQgc7s)

### timetill.rs 项目

timetill.rs 是一个社区项目，致力于收集来自世界各地的 Rust 会议。 Timetill.rs 是一个开放项目，社区中的任何人都可以参与。

详情请看：https://timetill.rs/#/

---
++++++
---

## gui

## 编写Rust的 Neovim 客户端

以下是Neovim的简单图形用户界面。在可能的情况下，可以进行一些图形上的改进，但其功能应类似于终端用户界面。

![](https://github.com/Kethku/neovide/raw/master/assets/BasicScreenCap.png)

标准的全功能Neovim GUI。除此之外，还有一些视觉效果：

![](https://github.com/Kethku/neovide/raw/master/assets/Ligatures.png)

![](https://github.com/Kethku/neovide/raw/master/assets/AnimatedCursor.gif)

表情符号支持

![](https://github.com/Kethku/neovide/raw/master/assets/Emoji.png)

前往Github仓库获取源代码：[https://github.com/Kethku/neovide](https://github.com/Kethku/neovide)

---
++++++
---

## db


---
++++++
---

## web

### `h2`  v0.2.1 版本更新

`h2`  是基于 tokio 的 HTTP/2.0 客户端和服务器实现。github 地址：https://github.com/hyperium/h2

### 用 Rust 写的 NATS 监控 web app

Rust warp web框架写的后端。NATS[https://nats.io/]

> NATS.io is a simple, secure and high performance open source messaging system for cloud native applications, IoT messaging, and microservices architectures.

https://github.com/sphqxe/NATS-WebUI

### Cloudsmith 支持直接上传 Cargo 包到他们的云平台

可以直接使用 cargo publish 上传。

构建私源( a private ‘single source of truth’ )的几个优点，他写了：

-   Can be managed, secured and controlled in a systematic way
-   Is available to teams and individuals within the organization anywhere in the world via a ‘web-scale’ cloud infrastructure
-   Can be distributed on a commercial/licensed basis if necessary on the same basis
-   Supports assets all common languages and formats (Rust and Cargo being just one of dozens of supported formats)

https://blog.cloudsmith.io/2020/03/09/announcing-native-cargo-uploads-in-cloudsmith/
---
++++++
---

## tools


#### geo, geo-types, 和 geo-json 新版本发布！

[geo](https://docs.rs/geo),  [geo-types](https://docs.rs/geo-types), 和  [geojson](https://docs.rs/geo-types)  新版本发布，现在已经更新到crates.io.

有不少non-breaking的更新，添加了不少新的功能特征：

-   增加了大量的一级文档，同时加了很多扩展型的例子，特别是很多crate库中geo生态中 相互操作性的例子文档。
-   更多的`LineString`  iterators，允许`Points`  和  `Coordinates`做mutable iteration操作。
-   一些新的算法，特别是在Chamberlain-Duquette领域
-   `geojson`  和  `geo`  类型的  `From`  和  `TryFrom`实现。
-   `geojson`  类型除了增加了[quick_collection](https://docs.rs/geojson/0.18.0/geojson/fn.quick_collection.html)  功能之外，允许任意合法的GeoJSON类型转换成`geo-types`的`Geometrycollection`。 这曾经是很多程序员的痛点，因为在很多地方都要搞boilerplate，现在牺牲一点点性能就可以获得极大的便利性。
-   现在RDP and Visvalingam-Whyatt simplification算法都可以直接返回简化了点地理几何索引`indices`。 这个对很多FEI用户非常有用，因为不同的几何坐标系类型之间彼此常常是不能直接MAP在一起的，往往需要重建自己的 简单几何坐标类型，重新编译本地的原生类型。如果你现在拿到这些索引，哈，简单多了！

这些新版库还包含了很大一部分各种各样的小改进，大部分都是文档类的，但愿任意被新用户轻松掌握；`geo`生态已经有 了很多专业领域的crates了（比如`coordinate projection`  和  `transformation, shapefiles, gpx, polylines`等等） 要把这些专业领域的库都能很好的掌握的揉和起来应用不简单，这些新的功能更新就是要让应用更加简单方便容易。

#### cargo-feature - Don't suffer from adding or removing feature

https://github.com/Riey/cargo-feature

只需要敲入下面的代码：

```
cargo feature serde +derive

```

不需要再像下面这样手工输入：

```
[dependencies]
serde = "1"

```

或

```
[dependencies]
serde = { version = "1", features = ["derive"] }

```

#### Rust analyser 每周更新changelog

https://rust-analyzer.github.io/thisweek/2020/03/23/changelog-17.html

https://rust-analyzer.github.io/manual.html

### tide-validator - tide 框架数据校验中间件

#rust #crate

tide-validator 是一个tide的数据校验中间件，刚开发出来没多久，作者希望能得到code review。

[Repo](https://github.com/bnjjj/tide-validator)

### Rust lifetime 可视化插件

[这片文章](https://rufflewind.com/2017-02-15/rust-move-copy-borrow)介绍了用可视化方式展示rust借用、生命周期、Clone等，文章中介绍了一些符号的作用，如果以后我们在尝试理解生命周期并给别人讲述时，都使用这套规则，那么理解成本将会降低很多。

Jeff Walker在这一片文章[Rust Lifetime Visualization Ideas](https://blog.adamant-lang.org/2019/rust-lifetime-visualization-ideas/)中表示这种图形虽然美观且易懂，但是并不适合在编辑器里展示，因为它占用的空间太大了，并且在现实编码情况下，这种展示方式可能变得相当复杂。

文章中介绍了Paul Daniel Faria为Atom编辑器开发了一个rust lifetime可视化插件原型，可以通过选中变量，查看它的生命周期范围并高亮展示，但是这种展示方式并不清晰，要通过开发者自己去识别，脑力成本有点高。所以开发一款美观、直观、且使用的Rust lifetime可视化插件确实是个难活。

作者通过对vscode代码截图，然后用图片编辑工具添加了他认为比较好的展示方式，最后总结了一款Rust lifetime可视化插件应该具备哪些要素，并鼓励开发者参考他的想法尝试开发。

[Graphical depiction of ownership and borrowing in Rust](https://rufflewind.com/2017-02-15/rust-move-copy-borrow)

[Rust Lifetime Visualization Ideas](https://blog.adamant-lang.org/2019/rust-lifetime-visualization-ideas/)

[Rust lifetime plugin for atom](https://github.com/Nashenas88/borrow_visualizer_prototype)


### 使用`absolution`，摆脱`syn`

absolution，用于在令牌树上进行操作的过程宏工具。

[Github](https://github.com/Manishearth/absolution)

### Rust实现的top工具比较

除了top外，一些可能会使用的基于终端的系统监视工具，包括ytop，bottom，zenith。

[文章](https://www.wezm.net/v2/posts/2020/rust-top-alternatives/)

### 超棒的 Rust 浏览器搜索扩展

该扩展可以让你直接在地址栏即时搜索 Rust 文档，crates.io 上相关的库，Rust 内建方法甚至 Rust 官方书籍等等。使用方法相当简单，在浏览器地址栏输入  `rs`，然后按空格，这个插件就会被启用，接着你就可以搜索🔍你需要的内容了！

目前支持 Chrome、Firefox 浏览器，安装地址：https://rust-search-extension.now.sh/。该项目源码 GitHub 地址：https://github.com/folyd/rust-search-extension。

![](http://q691wklq3.bkt.clouddn.com/demonstration.gif)

### ripgrep 12 更新

ripgrep是一种面向行的搜索工具，这个版本是 ripgrep 的一个重要版本，其中包含许多错误 修复，一些重要的性能改进和一些次要的新功能。

仓库地址：https://github.com/BurntSushi/ripgrep

### Rust Search Extension : 最好用的 Rust 搜索插件

![demonstration.gif](https://i.loli.net/2020/03/18/ueTEJtiNMdKWrV5.gif)

地址：[https://rust-search-extension.now.sh/](https://rust-search-extension.now.sh/)

### pkgar - Redox 上的包管理工具（以及包格式）

作者最近在设计 redox 上的包格式。它应该具有如下优点：

1.  原子性
2.  经济性
3.  快速
4.  最小化
5.  可重定位（可装在任何目录下）
6.  安全

详细请阅读原文。

https://www.redox-os.org/news/pkgar-introduction/

### 更紧凑的`Cow`

相对于`std::borrow::Cow`，`beef::Cow`在内存上更紧凑。

```
use beef::Cow;

let borrowed = Cow::borrowed("Hello");
let owned = Cow::from(String::from("World"));

assert_eq!(
    format!("{} {}!", borrowed, owned),
    "Hello World!",
);

// beef::Cow is 3 word sized, while std::borrow::Cow is 4 word sized
assert!(std::mem::size_of::<Cow<str>>() < std::mem::size_of::<std::borrow::Cow<str>>());

```

[Github](https://github.com/maciejhirsz/beef/)

### Confy 0.4

Rust CLI 工作组宣布发布Confy 0.4。

```
#[derive(Default, Debug, Serialize, Deserialize)]
struct MyConfig {
    version: u8,
    api_key: String,
}

fn main() -> Result<(), ::std::io::Error> {
    let cfg: MyConfig = confy::load("my-app-name")?;
    dbg!(cfg);
    Ok(())
}

```

[crates.io链接](https://crates.io/crates/confy)

[Github](https://github.com/rust-cli/confy)

### navi

`navi`  是用 Rust 编写的命令行的交互式备忘单工具，它可以浏览备忘单并执行命令，并且可以提示你输入参数值。

![](https://user-images.githubusercontent.com/3226564/76437136-ddc35900-6397-11ea-823c-d2da7615fe60.gif)

GitHub 仓库地址：https://github.com/denisidoro/navi

Reddit 上参与讨论：https://www.reddit.com/r/rust/comments/fgzifj/an_interactive_cheatsheet_tool_for_the/

### rust-doc.vim

#rust #tool

vim党请收下，一个在Vim中查找Rust文档，然后在浏览器打开的插件。

[Read More](https://github.com/rhysd/rust-doc.vim)

### Crabler

Crabler，Rust语言开发的基于异步的Web爬虫。

[Docs](https://docs.rs/crabler/)，[Github](https://github.com/Gonzih/crabler)

---
++++++
---

## ffi

#### `unsafe Qt`  Rust语言绑定新版本发布。

[New version of unsafe Qt bindings for Rust is released](https://rust-qt.github.io/blog/qt_crates_release_0_5/)

#### 我用Rust语言重写`Python VM`，欢迎大家提意见反馈。

[I've written a Python VM in Rust and open for any feedback](https://github.com/FKLC/PyVM)

### Electron+Rust模版

一个Electron+Rust的模板项目。

[Github](https://github.com/usagi/template-rust-backend-with-electron-frontend)

### A C# programmer 尝试 Rust - Part 1

推荐阅读。

附带赠送一个小小的性能评测。

```
Test 	Elapsed Milliseconds 	Peak Memory Usage 	Memory Usage After Processing 	Memory Usage After Gen2 GC
C# - Imperative 	5444 	3.4GB 	3.4GB 	2.05GB
C# - Declarative 	6785 	3.2GB 	3.2GB 	1.9GB
Rust - Declarative 	2851 	859MB 	464MB 	N/A

```

https://treit.github.io/programming,/rust,/c%23/2020/03/06/StartingRust.html

### Rust语言开发JVM

正在开发中的用Rust语言开发的Java虚拟机

[Github](https://github.com/douchuan/jvm)

### 在 Flutter 插件上运行原生 Rust！

该项目是一个 flutter 的插件模板，它对所有可用的 iOS 和 Android 架构提供了交叉编译原生 Rust 代码的开箱即用支持，Dart 语言可以通过 FFI(Foreign Function Interface) 调用它。

该项目提供了一流的FFI支持，表现如下：

-   No Swift or Kotlin wrappers
-   No message channels
-   No async calls
-   No need to export aar bundles or .framework's

更多了解更看[项目地址](https://github.com/brickpop/flutter-rust-ffi):https://github.com/brickpop/flutter-rust-ffi

reddit上[参与讨论](https://www.reddit.com/r/rust/comments/fdzgc8/found_this_to_be_extremely_interesting/)：https://www.reddit.com/r/rust/comments/fdzgc8/found_this_to_be_extremely_interesting/

---
++++++
---

## Embedded

### audio 的 mp4 元数据解释器

`mp4ameta`  是受  [`id3`](https://crates.io/crates/id3)(https://crates.io/crates/id3) 和  [`metaflac`](https://crates.io/crates/metaflac)(https://crates.io/crates/metaflac) 项目启发，用于解析 MPEG-4 音频元数据（m4a和m4b）的库。

仓库地址：https://bitbucket.org/Saecki/rust-mp4ameta

### Agnostik: Executor Agnostic Runtime

Agnostik 可以作为应用和执行器在处理异步事物时的中间层. 它可以让你在切换执行器时更轻松并且不用改动太多代码.

详情：[https://github.com/bastion-rs/agnostik](https://github.com/bastion-rs/agnostik)

### 在Arduino Due上使用 Rust 编写的小示例应用程序, 适用于嵌入式开发的同学

Arduino是一个基于易用硬件和软件的原型平台（开源）。它由可编程的电路板（称为微控制器）和称为Arduino IDE（集成开发环境）的现成软件组成，用于将计算机代码写入并上传到物理板。

Arduino Due是基于Atmel SAM3X8E ARM Cortex-M3 CPU的微控制器板。它是第一款基于32位ARM内核微控制器的Arduino板。

几天前，作者在Arduino Due上进行了嵌入式开发的实验。相当不错的开发体验并且易于设置，但是Internet上的许多信息已经过时了。

作者总结了 Hello World 入门例子, 推荐给大家.  [https://github.com/sdroege/arduino-due-rust](https://github.com/sdroege/arduino-due-rust)

### Oxidize 1K：嵌入式 Rust 开发的远程会议

3月20日，星期五，欧洲中部时间17：00，有个嵌入式 Rust 开发的远程会议，大约 3-4 小时。活动将通过 Zoom 举办，欢迎来自世界各地的演讲者和参会者。

[网站](https://oxidizeconf.com/oxidize-1k/)

# 在嵌入式GDB除錯Rust

[說明](https://github.com/berkowski/rust-target-cmake)  [範例stm32l0xx-hal](https://github.com/berkowski/stm32l0xx-hal/)  [CLion embedded debugger](https://www.jetbrains.com/help/clion/embedded-gdb-server.html)

### chip8.rs

![chip8](http://q691wklq3.bkt.clouddn.com/chip8-invaders.jpg)

chip8.rs 博文主要讲述如何使用 Rust 实现 PineTime 智能手表的 CHIP-8 游戏模拟器。

原文地址：https://lupyuen.github.io/pinetime-rust-mynewt/articles/chip8

### 嵌入式开发中的 async/await

这篇[博客](https://ferrous-systems.com/blog/async-on-embedded/)中讨论了为什么"async/await"对于嵌入式开发来说是比较重要的一个功能. 文章从一下几个角度来分析：

-   从阻塞到非阻塞
-   多任务处理
-   线程
-   数据共享
-   ...

详情：[https://ferrous-systems.com/blog/async-on-embedded/](https://ferrous-systems.com/blog/async-on-embedded/)

---
++++++
---

## async

### parallel_stream：数据并行库

为 async std 开发的数据并行库，使用方式如下：

```
use parallel_stream::prelude::*;

#[async_std::main]
async fn main() {
    // Create a vec of numbers to square.
    let v = vec![1, 2, 3, 4];

    // Convert the vec into a parallel stream and collect each item into a vector.
    let mut res: Vec<usize> = v
        .into_par_stream()
        .map(|n| async move { n * n })
        .collect()
        .await;

    // Items are stored as soon as they're ready so we need to sort them.
    res.sort();
    assert_eq!(res, vec![1, 4, 9, 16]);
}

```

详情：[https://blog.yoshuawuyts.com/parallel-stream/](https://blog.yoshuawuyts.com/parallel-stream/)

# Async Interview: Withoutboats

Withoutboats是Rust lang小組的成員。 從2018年初開始，他們開始研究Rust的異步等待。

本文講解了異步語法應該要解決的太多問題

要保持異步和同步代碼為盡可能"類似"且好用。

[Read more](https://bit.ly/2wPQWb8)

# Rust:改善 spotify-tui 透過使用 async

作者通過實作 async/await 與使用 tokio

改善了UI效能

[Read more](https://bit.ly/2IFqCDc)

### 嵌入式开发中的 async/await

这篇[博客](https://ferrous-systems.com/blog/async-on-embedded/)中讨论了为什么"async/await"对于嵌入式开发来说是比较重要的一个功能. 文章从一下几个角度来分析：

-   从阻塞到非阻塞
-   多任务处理
-   线程
-   数据共享
-   ...

详情：[https://ferrous-systems.com/blog/async-on-embedded/](https://ferrous-systems.com/blog/async-on-embedded/)


---
++++++
---

## job

### Rust-IPFS 正在寻找 Rust 开发者

Parity 在 rust-libp2p 中所做的出色工作的基础上，已经开始进行全职的 Rust-IPFS 实现工作。 Equilbrium 在协议实验室的支持下带头推动了新的社区和实现，并且正在寻找更多的 Rust 开发人员来帮助构建 InterPlanetary File System 的 Rust 实现。查看原文：https://blog.ipfs.io/2020-03-18-announcing-rust-ipfs/

![](http://q691wklq3.bkt.clouddn.com/QmU7sssvo52Rrwj7MWZNpeHnFjjdG271Dx5zfGkZSbgVnN.png)

### 苹果招募 Rust 程序员

-   网络工程师：[https://jobs.apple.com/en-us/details/200144575/software-engineer](https://jobs.apple.com/en-us/details/200144575/software-engineer)
    
-   存储工程师：[https://jobs.apple.com/en-us/details/200117537/software-engineer](https://jobs.apple.com/en-us/details/200117537/software-engineer)