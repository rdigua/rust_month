# April 2020

## rust

### DataFusion

DataFusion 是 Rust 原生的内存查询引擎，它是 Apache Arrow 项目的一部分。

[Apache Arrow 发布 v0.17.0 的文章](https://arrow.apache.org/blog/2020/04/21/0.17.0-release/)，https://arrow.apache.org/blog/2020/04/21/0.17.0-release/

### Logos 发布 v0.11

Logos，旨在创建快速的 Lexers。此次 v0.11 版本有许多重大更改，具体参见下面链接。

[Github Release](https://github.com/maciejhirsz/logos/releases/tag/v0.11.0)，https://github.com/maciejhirsz/logos/releases/tag/v0.11.0

# grex 1.1.0

用於從用戶提供的測試用例生成regex的工具

[Read more](https://github.com/pemistahl/grex)

[Read more](https://github.com/aclueless/spair)


### MongoDB 官方 Rust Driver

来自 MongoDB 官方支持的 MongoDB Rust 驱动程序，该客户端库可用于与 Rust 应用程序中的 MongoDB 部署进行交互。同时 BSON 的支持取决于社区支持的  [bson](https://docs.rs/bson)  库。（目前为 alpha 版本）

仓库 GitHub 地址：https://github.com/mongodb/mongo-rust-driver

### mini-redis

mini-redis 是使用 Tokio 构建的 Redis 客户端和服务器的惯用实现。目前还没有实现完全，该仓库更加丰富了 Tokio 的生态。

仓库地址：https://github.com/tokio-rs/mini-redis

### μfmt 项目

`μfmt`  是替代  `core::fmt`  的更小，更快，更轻松的选择，项目地址：https://github.com/japaric/ufmt

![](https://github.com/japaric/ufmt/raw/master/cg.png)

#### 4 -  `Rust`语言里通过`OpenSSH`的`Wrapping`脚本化实现`SSH`调用

[https://github.com/jonhoo/openssh-rs/](https://github.com/jonhoo/openssh-rs/)

### Intermodal

Intermodal，BitTorrent元信息实用程序，其二进制文件称为imdl。目前，它可以创建，验证和显示种子的内容。

[Github](https://github.com/casey/intermodal)，https://github.com/casey/intermodal

### 微软和GitHub都要求我们尝试GitHub Actions

此更改对Rust的任何用户都不会产生可见的影响，但将大大改善贡献者的体验。

[https://blog.rust-lang.org/inside-rust/2020/04/07/update-on-the-github-actions-evaluation.html](https://blog.rust-lang.org/inside-rust/2020/04/07/update-on-the-github-actions-evaluation.html)

### arrav

东半球最强Rust大神[Jonhoo](https://github.com/jonhoo)开发的库，代码量不多，是Const Generic特性的一个应用。

```
 pub const fn new() -> Self {
  Arrav {
    ts: [T::SENTINEL; N],
  }
}


```

采用类似的结构，为基本的数字类型都实现了Sentinel trait，所以基本数字类型都有一个默认的T::SENTINEL。

arrav里数组长度是依赖于T::SENTINEL来判断的，所以也对它做了SIMD优化，代码值得一读。此结构适合小型紧凑的数据。

[Repo](https://github.com/jonhoo/arrav)

### Fondant

Fondant，基于宏的CLI实用程序配置管理库。

-   支持json，yaml和toml
-   支持自定义配置路径
-   支持自定义配置文件名

![image](https://raw.githubusercontent.com/lesterli/blockchain/master/images/rust/fondant.png)

[Github](https://github.com/nerdypepper/fondant)，https://github.com/nerdypepper/fondant

# prodash 3.5發佈

prodash 是一個tui庫

可以平行繪製控制項

[Read more](https://docs.rs/prodash/3.5.0/prodash/)

### TinyVec

SmallVec 和 ArrayVec 100% 安全的替代品

详情：[https://github.com/Lokathor/tinyvec](https://github.com/Lokathor/tinyvec)

### R2: Rust 实现的路由器数据包转发引擎

介绍：

-   [https://r2.rs/](https://r2.rs/)
-   [https://github.com/gopakumarce/R2](https://github.com/gopakumarce/R2)

---
++++++
---

## learning

### [视频] 关于所有权，闭包和线程

[YouTube 视频](https://www.youtube.com/watch?v=2mwwYbBRJSo)，https://www.youtube.com/watch?v=2mwwYbBRJSo

### 一个关于3D图形、Rust、Vulkan、ash的教程

[教程在这里](https://hoj-senna.github.io/ashen-aetna/)，https://hoj-senna.github.io/ashen-aetna/

# 嵌入式Rust模式-零空間參考

文章提出一種參考方式可以在嵌入式系統使用 讓你可以在嵌入式系統中節省記憶體的使用

[Read more](https://ferrous-systems.com/blog/zero-sized-references/)

### CS-3210 课程推荐

大家可能对 stanford 的 cs140e 课程还有印象，现在他的“高阶版”来了。佐治亚理工学院 OS lab 开设了 CS-3210 课程，主要内容是设计和实现操作系统的核心组件。地址：https://tc.gts3.org/cs3210/2020/spring/info.html

### - 佐治亚理工学院 CS-3210 课程实验：用 Rust 为树莓派写一个操作系统

[Read More](https://tc.gts3.org/cs3210/2020/spring/lab.html)

### - Multiversion 0.5.0, 多版本函数宏，现在已经"可以跑生产系统"了。

> Multiversion 0.5.0, now "production ready"

[`Multiversion`  - 是`Rust`语言支持多版本函数的属性宏.](https://crates.io/crates/multiversion)

什么是`function multiversioning`?

> 大部分的CPU架构都有自己独特的指令集支持一些额外的功能。最常见的例子包括`x86/x86-64`  上的`SSE & AVX`，`NEON`上的`ARM/AArch64`指令集扩展`Single Instruction, Multiple Data(SIMD)`。 这些指令集扩展可以给某些特殊的函数提升大量的运行速度。这些特殊的功能是不能胡乱的编译到一个 不支持这些特殊功能CPU的可执行文件里去的，那样往往会造成系统崩溃。

`Function multiversioning`是一种特殊的编译方法，通过编译包含特殊功能支持的不同版本的函数 能够在运行时`runtime`检测到这些特殊的功能并匹配不同的版本的可执行函数。

Function multiversioning功能：

-   动态调控，启用运行时CPU功能检测
-   静态调控，避免嵌套式的重复功能检测（但允许行内嵌套）
-   支持所有类型的函数，包括generic和async类型的函数

例子： 用`clone`属性宏来实现多版本函数，类似GCC的`target_clones`

```
use multiversion::multiversion;

#[multiversion]
#[clone(target = "[x86|x86_64]+avx")]
#[clone(target = "x86+sse")]
fn square(x: &mut [f32]) {
   for v in x {
       *v *= *v;
   }
}

```

用`multiversion`和`target`属性宏来实现多版本函数.

```
use multiversion::{multiversion, target};

#[target("[x86|x86_64]+avx")]
unsafe fn square_avx(x: &mut [f32]) {
   for v in x {
       *v *= *v;
   }
}

#[target("x86+sse")]
unsafe fn square_sse(x: &mut [f32]) {
   for v in x {
       *v *= *v;
   }
}

#[multiversion]
#[specialize(target = "[x86|x86_64]+avx", fn = "square_avx", unsafe = true)]
#[specialize(target = "x86+sse", fn = "square_sse", unsafe = true)]
fn square(x: &mut [f32]) {
   for v in x {
       *v *= *v;
   }
}

```

[更多信息请点击crates官网说明-Read More](https://crates.io/crates/multiversion)

### - 如何在Windows 10系统环境安装原生Rust编程环境

> [How to install rust on Windows 10 (native)](https://estada.ch/2020/4/19/installing-rust-on-windows-10-native/)

下面是快速安装`Windows 10 2004`的步骤：

1.  下载并运行[rustup.rs](https://rustup.rs/)
2.  下载[`Build Tools for Visual Studio 2019`](https://visualstudio.microsoft.com/downloads/)，一般这个下载隐藏在微软下载链接的`"Tools for Visual Studio 2019"`下面。
3.  运行`Build Tools for Visual Studio 2019 Installer`并选择:
    -   `C++ Tools`
4.  `C++ Tools`中还必须同时选择安装`"Windows 10 SDK"`，安装程序提供多个版本，选最新的版本安装就好。

测试看看是否安装成功：

1.  打开PowerShell或命令行窗口，输入下面的命令并保证没有错误。
2.  切换到临时文件夹：`cd %TEMP%`
3.  创建一个测试项目：`cargo new toolchain_test`
4.  进入项目所在目录：`cd toolchain_test`
5.  编译并运行"Hello, world!"程序：`cargo run`

然后你应该可以得到一个编译的过程并看到结果显示`"Hello, world!"`

如果遇到类似`cargo command not found`的错误，你需要检查一下你的`%PATH%`看看是否设置好。

### 基于gfx-hal的Rust图形学教程-第三部分

#graphics

[part 3](https://www.falseidolfactory.com/2020/04/16/intro-to-gfx-hal-part-3-vertex-buffers.html)  [part 2](https://www.falseidolfactory.com/2020/04/01/intro-to-gfx-hal-part-2-push-constants.html)  [part 1](https://www.falseidolfactory.com/2020/04/01/intro-to-gfx-hal-part-1-drawing-a-triangle.html)


### 系列轻教程：在 Rust 中写 Python 代码

作者实现了一个 python! 宏，结合pyo3（一个流行的python api的rust ffi 绑定），可以让你在 Rust中编写python代码。

教程是他如何编写该库。 学习宏、FFi 可以参考该库。

[文章](https://blog.m-ou.se/writing-python-inside-rust-1/)，https://blog.m-ou.se/writing-python-inside-rust-1/  [代码](https://github.com/fusion-engineering/inline-python)，https://github.com/fusion-engineering/inline-python

# Hash 查找不用分配記憶體的方法

```
struct OwnedKey {
    s: String,
    bytes: Vec<u8>,
}

struct BorrowedKey<'a> {
    s: &'a str,
    bytes: &'a [u8],
}

//教你用BorrowedKey在 HashSet<OwnedKey> or BTreeSet<OwnedKey>容器中做查找

```

[Read more](https://github.com/sunshowers/borrow-complex-key-example/blob/master/README.md)

### μfmt 项目

`μfmt`  是替代  `core::fmt`  的更小，更快，更轻松的选择，项目地址：https://github.com/japaric/ufmt

![](https://github.com/japaric/ufmt/raw/master/cg.png)

##### 使用 Actix 和 Juniper 构建简单的 GraphQL API

#graphql

油管视频教程，该up主还做了一系列actix相关的视频教程，虽然看视频学的比较慢，但是很适合初学者。

[Read More](https://www.youtube.com/watch?v=aEAz5DHhpLo&feature=youtu.be)

### 如何在正确性至关重要的Rust项目中进行错误处理

#rust #error_handing

[Read More](http://sled.rs/errors)

# 分析rust的三種回傳包裝

```
// Ok-Wrapping
fn foo() -> Result<PathBuf, io::Error> {
    let base = env::current_dir()?;
    Ok(base.join("foo"))
}
// use exception
fn foo() -> PathBuf throws io::Error {
    let base = env::current_dir()?;
    base.join("foo")
}
//Try Functions
#![feature(try_blocks)]
fn foo() -> Result<PathBuf, io::Error> {
    try {
        let base = env::current_dir()?;
        base.join("foo")
    }
}

```

[Read more](https://yaah.dev/try-blocks)

# Ok(match thing { ... }) 不好嗎？

有人在boats最近的blog發現他不建議大家用

他建議除了作為返回值以外不要使用Ok-Wrapping

可以讓程式碼更清楚更容易看懂

[Read more](https://boats.gitlab.io/blog/post/why-ok-wrapping/)

# Ok-Wrapping的心理模型

這幾天大家瘋狂的在討論Ok-Wrapping

本文只是希望以一些分析性的方式來說明

為什麼我個人不喜歡Ok-wrapping的一些原因。

[Read more](https://vorner.github.io/2020/04/09/wrapping-mental-models.html)

### 200行代码讲透 Rust Futures

这是一个比较长的博客，主要是用一个例子驱动的方法来解释Rust中的Futures，探索为什么他们被设计成这样，以及他们如何工作，此外还介绍在编程中处理并发性时的一些替代方案。

原文地址：https://cfsamson.github.io/books-futures-explained/introduction.html，同时国内的大佬 白振轩的个人博客已经做了翻译，请看：https://stevenbai.top/rust/futures_explained_in_200_lines_of_rust/

### Rust 是 k8s 的不错选择

前些天，我们日报小组介绍了 Krustlet，这是 Rust 中一个基于 WebAssembly 的 Kubelet 实现。 我们选择使用Rust的原因有两个：1、Rust对WebAssembly编译提供了一些最好的支持（稍后会详细介绍），1、我们想证明 Rust 的优势可以应用于 Kubernetes 生态系统。 这篇文章旨在表明我们学到了什么以及为什么我们认为 Rust 是编写 Kubernetes 重点应用程序的绝佳选择（有时更好）【来自（DeisLabs）的博客】。

原文请看：https://deislabs.io/posts/kubernetes-a-rusty-friendship/

### proc-macro-error

proc-macro-error 的目标是使过程宏中的错误报告变得轻松便捷。

使用实例速览：

```
use proc_macro_error::*;
use proc_macro::TokenStream;
use syn::{spanned::Spanned, DeriveInput, ItemStruct, Fields, Attribute , parse_macro_input};
use quote::quote;

fn process_attrs(attrs: &[Attribute]) -> Vec<Attribute> {
    attrs
        .iter()
        .filter_map(|attr| match process_attr(attr) {
            Ok(res) => Some(res),
            Err(msg) => {
                emit_error!(attr, "Invalid attribute: {}", msg);
                None
            }
        })
        .collect()
}

fn process_fields(_attrs: &Fields) -> Vec<TokenStream> {
    // processing fields in pretty much the same way as attributes
    unimplemented!()
}

#[proc_macro]
#[proc_macro_error]
pub fn make_answer(input: TokenStream) -> TokenStream {
    let input = parse_macro_input!(input as ItemStruct);
    let attrs = process_attrs(&input.attrs);

    // abort right now if some errors were encountered
    // at the attributes processing stage
    abort_if_dirty();

    let fields = process_fields(&input.fields);

    // no need to think about emitted errors
    // #[proc_macro_error] will handle them for you
    //
    // just return a TokenStream as you normally would
    quote!(/* stuff */).into()
}

```

### 【博客】Rust 项目中的错误处理

[http://sled.rs/errors](http://sled.rs/errors)

#### [Voik - 一个试验性的分布式流平台](https://github.com/marceloboeira/voik)

项目目的

-   学习
-   实现类似Kinesis一样的流服务
-   单一可执行文件
-   轻松托管，执行和运营

已经发布的博文：

-   [Building a Distributed Log from Scratch, Part 1: Storage Mechanics](https://bravenewgeek.com/building-a-distributed-log-from-scratch-part-1-storage-mechanics/)
-   [Building a Distributed Log from Scratch, Part 2: Data Replication](https://bravenewgeek.com/building-a-distributed-log-from-scratch-part-2-data-replication)
-   [Building a Distributed Log from Scratch, Part 3: Scaling Message Delivery](https://bravenewgeek.com/building-a-distributed-log-from-scratch-part-3-scaling-message-delivery/)
-   [Building a Distributed Log from Scratch, Part 4: Trade-Offs and Lessons Learned](https://bravenewgeek.com/building-a-distributed-log-from-scratch-part-4-trade-offs-and-lessons-learned/)
-   [Building a Distributed Log from Scratch, Part 5: Sketching a New System](https://bravenewgeek.com/building-a-distributed-log-from-scratch-part-5-sketching-a-new-system/)
-   [The Log: What every software engineer should know about real-time data's unifying abstraction](https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying)
-   [How Kafka's Storage Internals Work](https://thehoard.blog/how-kafkas-storage-internals-work-3a29b02e026)

#### Servo浏览器编程: Service服务的Worker脚本进程.

描述Service workers网页服务后台脚本进程在整个Servo浏览器大架构里的地位，这些后台脚本都是用Rust语言来实现的并行Web引擎。

https://medium.com/programming-servo/programming-servo-workers-at-your-service-db71e5943511

### gfx-hal介绍第一部分-画三角形

#rust #webgl

这篇文章是rust图形编程教程系列的第一篇，使用的是gfx-hal这个库，介绍了通过这个库使用Rust实现一个webgl三角形。

[Read More](https://www.falseidolfactory.com/2020/04/01/intro-to-gfx-hal-part-1-drawing-a-triangle.html)

### Stjepan：为什么我要建立一个新的异步运行时？

Stjepan Glavina是Rust流行库Crossbeam的作者，最近一年专注于async-std的开发。

[博客文章](https://stjepang.github.io/2020/04/03/why-im-building-a-new-async-runtime.html)，https://stjepang.github.io/2020/04/03/why-im-building-a-new-async-runtime.html

# 寫一個Lambda演算解析器

有點lex, yacc的感覺

[Read more](https://christianpoveda.github.io/blog/parsing/)

### 【译文】Rust中的`String`和`&str`

当你开始 Rust 的学习之旅后，很可能遇到需要使用字符串的场景，但是编译器却无法让你的代码通过编译，因为有一部分代码，看起来像字符串，事实上却又不是。看下这个文章或许能给你解惑：https://zhuanlan.zhihu.com/p/123278299，内容来源：知乎-Praying。

原文地址：https://link.zhihu.com/?target=https%3A//blog.thoughtram.io/string-vs-str-in-rust/

### 【演讲】新机器的灵魂:重新思考计算机

分享者： 布莱恩·坎特里（Bryan Cantrill） - 氧化物（Oxide）计算机公司 2020年2月26日 活动：斯坦福研讨会 (Stanford Seminar )

尽管我们的软件系统变得越来越有弹性，但可用于运行该软件的物理基础（即计算机！）仍然停留在PC架构的旧时代。 超大型基础设施提供商早就意识到了这一点，制造出适合用途的机器，但这些进步却被大众市场所拒绝。

在本次演讲中，讨论对新型机架式服务器端机器的愿景，以及开放固件、RISC-V和Rust等技术进步将如何在实现这一愿景中发挥核心作用。

详情：[https://youtu.be/vvZA9n3e5pc](https://youtu.be/vvZA9n3e5pc)

---
++++++
---

## story

# 如何在2020年加速Rust編譯器

Nicholas 記錄了他們過去增加編譯速度的一些方法

[Read more](https://blog.mozilla.org/nnethercote/2020/04/24/how-to-speed-up-the-rust-compiler-in-2020/)

### Rust 1.43.0 发布

Rust 团队非常高兴地宣布 Rust 的新版本 1.43.0 发布，这个版本是相当小的的一个版本,没有新的主要功能。该版本提供了一些新的稳定的 API，以及一些编译器的性能改进以及与宏相关的小功能，请看请看官博参阅详细的发行说明，以了解本文未涵盖的其他更改：https://blog.rust-lang.org/2020/04/23/Rust-1.43.0.html

### Rust  `Mimalloc`  v0.1.19 版本更新

`Mimalloc`  是 Microsoft 构建的通用的，面向性能的分配器【https://github.com/microsoft/mimalloc】。`mimalloc_rust`  是围绕 mimalloc 分配器的嵌入式全局分配器包装器，github 地址：https://github.com/purpleprotocol/mimalloc_rust

reddit 上参与讨论：https://www.reddit.com/r/rust/comments/g6m1hp/rust_mimalloc_v0119_has_just_been_released/

### Arch Linux 宣布使用 rebuilderd 对二进制软件包进行独立验证

这个标题不是重点，重点是  `rebuilderd`  是一个 rust 程序  _。相关讨论：https://www.reddit.com/r/linux/comments/g6fo99/arch_linux_announces_independent_verification_of/

### 关于 tokio 库的  `runtime not found`  问题的讨论

使用  `TcpStream`  时，资源类型必须引用运行时才能起作用。鉴于 Tokio 在当前进程中可以运行任何数量的运行时，资源类型必须具有某种策略，通过它可以选择正确的运行时。

当前，这是通过使用本地线程来跟踪当前运行时来完成的。 在许多情况下，一个进程仅包含一个运行时。 尝试从运行时之外使用资源时会出现问题。 在这种情况下，尚不清楚资源类型应使用哪个运行时，并且会引发 panic。

如果你遇到相关问题，请围观：https://github.com/tokio-rs/tokio/issues/2435

## 3 - 感谢 ron 的作者

reddit 上有人发帖为 ron 疯狂打 call. 在他业余的项目中他一直被 JSON 的一些限制所困扰：

-   map 中的 key 必须是字符串
-   不可以添加评论
-   最后一个 item 之后不能跟逗号

[ron](https://crates.io/crates/ron)  很好的解决了这些问题.

[Read More](https://www.reddit.com/r/rust/comments/g5rlt5/thank_you_for_ron_rusty_object_notation/)

### 3 - 软件开发者经济学：现在估计全球有60万活跃Rust程序员。

下面链接是长达40多页纸的调查报告（可能国内用户需要科学上网才能下载）

-   DEVELOPER ECONOMICS: STATE OF THE DEVELOPERNATION 18th EDITION, PUBLISHED APRIL 2020
-   根据2019年第四季度对超过17000名软件开发人员进行的抽样调查的趋势报告

> [Active Rust developers estimated at 0.6 million (pdf, page 10)](https://s3-eu-west-1.amazonaws.com/vm-blog/uploads/2020/04/DE18-SoN-Digital-.pdf)

### 我们在用Go开发区块链！

#rust #blockchain

这是使用Go语言follow 《Rust开发区块链》的后续文章，内容涵盖基本功能以及设计决策，并做了两种语言的快速比较。

[Read More](https://lalot.ai/simple-blockchain-written-in-go)

### 对常用于Rust游戏开发的数学库进行构建时间比较

#rust #graphics

[Read More](https://bitshifter.github.io/2020/04/12/mathbench-build-timings/)

### 消息：rust.cc 搬国内了，新域名是 rustcc.cn，国内访问速度大增

rust.cc 搬国内来了，现在域名是 rustcc.cn。访问以前的域名会重定向过来。但是原来的rss好像不会收到更新了。大家使用过程中有什么问题，请直接与Mike老师联系。

[详细通告在这里](https://rustcc.cn/article?id=b1ccded3-0d45-4005-837c-ad54cf55ef54)，https://rustcc.cn/article?id=b1ccded3-0d45-4005-837c-ad54cf55ef54

以及 rustcc 源回来了，欢迎大家内测。

[详细信息在这里](https://rustcc.cn/article?id=f5d0773e-9086-48de-aae6-f2a66a83ce35)，https://rustcc.cn/article?id=f5d0773e-9086-48de-aae6-f2a66a83ce35

### Rust 2019 调查问卷结果出炉

> The survey was available in 14 different languages and we received 3997 responses.
> 
> 该调查以14种不同的语言提供，我们收到了3997份回复。

> Overall our users indicated that productivity is still an important goal for their work (with or without using Rust). The results show the overriding problem hindering use of Rust is adoption. The learning curve continues to be a challenge - we appear to most need to improve our follow through for intermediate users - but so are libraries and tooling.
> 
> 总体而言，我们的用户表示，生产力仍然是他们工作的重要目标（无论是否使用Rust）。 结果表明，阻碍使用Rust的首要问题是采用率。学习曲线仍然是一个挑战 - 我们似乎最需要提高对中级用户的关注度 - 库和工具也是如此。

[详细结果文章链接](https://blog.rust-lang.org/2020/04/17/Rust-survey-2019.html)，https://blog.rust-lang.org/2020/04/17/Rust-survey-2019.html

### 可靠的基准测试

Reddit 上的网友发起的一则讨论，他在进行基准测试以优化某些代码的时候，发现基准测试结果难以理解。感兴趣的朋友可以去[参与讨论](https://www.reddit.com/r/rust/comments/g29kz8/reliable_benchmarks/)：https://www.reddit.com/r/rust/comments/g29kz8/reliable_benchmarks/

### aeron：高效可靠的UDP和IPC信息传输模块

详情：[https://github.com/real-logic/aeron](https://github.com/real-logic/aeron)

### 【博客】Better stack fixing for Firefox

详情：[https://blog.mozilla.org/nnethercote/2020/04/15/better-stack-fixing-for-firefox/](https://blog.mozilla.org/nnethercote/2020/04/15/better-stack-fixing-for-firefox/)

### - Ruma死掉了, Ruma万岁! 于2020年4月10日

[Ruma is dead, long live Ruma! April 10, 2020](https://www.ruma.io/news/ruma-is-dead-long-live-ruma-2020-04-10)  作者：Jonas Platte

Ruma是一组由[Matrix](https://matrix.org/)  homeserver服务器，客户端和支持库组成的由Rust语言开发的软件组。Matrix是一个开放的在线通讯协议。关于这个项目的基本情况可以访问 项目主页。今天有点伤感的宣布：

-   Ruma，也就是项目的homeserver服务器端，不再继续开发了。
-   Ruma项目未来将继续开发支持库包，确保这些库还能继续支持Ruma服务器及各种应用。
-   如果你还对现在的Ruma homeserver开发感兴趣，可以考虑看看[Conduit](https://conduit.rs/)  这是用了Ruma支持库写的不一样的Ruma Homeserver实现。

### Rust 改变的有多频繁？

#rust

作者一直在思考Rust的更改频率。有些人断言，Rust如今保持相当静态，还有一些人说Rust的变化仍然太大。 在这篇博客中，作者对这个问题进行数据驱动的分析，拿事实数据说话。

[Read More](https://words.steveklabnik.com/how-often-does-rust-change)

### Steve 在写新的一本 Rust Book

[https://www.notion.so/A-book-about-Rust-a51507cd17bb4c379d705a4f282425d6](https://www.notion.so/A-book-about-Rust-a51507cd17bb4c379d705a4f282425d6)

### 9个补丁

长期以来，对rust-lang/rust的贡献一直是作者的愿望。 通过努力终于提交了9个补丁, 有兴趣的可以看看这9个补丁, 讲的很详细.

[https://blog.yoshuawuyts.com/nine-patches/](https://blog.yoshuawuyts.com/nine-patches/)

### std::slice::fill

#rust

std::slice::file将会加入到下一个nightly版本中，这是从c++20借鉴过来的一个API，JavaScript也有这样的API Array.prototype.fill。

```
let mut buf = Vec![0; 10];
buf.fill(1);
assert_eq!(buf, vec![1; 10]);

```

### Steve 并没有宣布要解散文档团队

上周六，小编发日报时疏忽大意。感谢今天张汉东老师的指正！

中文社区有人传：steve宣布解散文档团队。

其实这个事，就好比：

「你心血来潮建个xxx主题的群，结果进来的都是凑热闹的， 作为群主的你，号召了好几次，大家都为xxx主题行动起来，结果响应的人寥寥无几， 那么作为群主的你，只能宣告，“我们这个群已经名存实亡”了。 作为群主的你，还是继续默默自己一个人去为xxx主题努力着。 steve 就很像这个群主。」

他在文章结尾说了：

> As such, this blog post isn't really announcing the end of the docs team as much as it is describing what is already true today. I will still be doing my work on core, and the book. And I plan on submitting some more docs PRs in the future.

[原博客文章](https://blog.rust-lang.org/inside-rust/2020/03/27/goodbye-docs-team.html)，https://blog.rust-lang.org/inside-rust/2020/03/27/goodbye-docs-team.html

### 新项目用 Rust 还是 Go ？

如果你用 Rust 语言或 Go 语言编写过代码，就会发现它们之间有些相似之处和不同之处。这两种语言的设计目标有重叠的部分，但也有很多差异。正如我们知道的，该如何选择语言取决于要解决的问题。

很幸运，我们找到了一位对这两种语言都有着丰富经验的工程师 — Damien Stanton，并与他进行了一次交流。更多请看原文，地址：https://dmv.myhatchpad.com/insight/choosing-between-rust-or-go/，消息来源：微信公号-高可用架构。

### 今年RustConf 根据covid-19的情况，有可能开线上Conf

详情：[https://cfp.rustconf.com/events/rustconf-2020](https://cfp.rustconf.com/events/rustconf-2020)

此外 OxidizeConf 也因为新冠病毒推迟活动了，OxidizeConf 是嵌入式和IoT 主题的 Rust Conf

### Add a  `trustme`  keyword to define unsafe code blocks #2893

详情：[https://github.com/rust-lang/rfcs/pull/2893](https://github.com/rust-lang/rfcs/pull/2893)

### 自由职业者平台 Upwork 通过一则广告宣布 支持 Rust

Upwork是全球最大的、最优秀的、最规范的综合类人力外包服务平台.

详情：[https://youtu.be/h3yFOf6hIjQ](https://youtu.be/h3yFOf6hIjQ)

---
++++++
---

## wasm

###  -【博客】在 web 中使用 wgpu-rs

[gfx-rs](https://github.com/gfx-rs/gfx)  是一个致力于低 GPU 编程的 Rust 项目.  [wgpu-rs](https://github.com/gfx-rs/wgpu-rs)是基于 gfx-rs 并且更安全、更可用并且可移植性更强.

[Read More](https://gfx-rs.github.io/2020/04/21/wgpu-web.html)

### - Wired Logic - 运行在浏览器上的基于像素的电子元件模拟器（用`Rust`语言编译成`WASM`)

> Wired Logic - a pixel-based digital circuit simulator running in a browser (Rust compiled into WASM).

受[`wired-logic`](https://github.com/martinkirsche/wired-logic)启发，[`wired-logic-rs`](https://github.com/iostapyshyn/wired-logic-rs)  是一个基于像素的数字电路模拟器，核心技术采用`Rust`和`WebAssembly`

wired-logic-rs 是怎么工作的呢？ 系统先对图像进行扫描，然后采集一个线路，电能源，和各种晶体管，收集成一个集合， 然后对这些集合元素运行模拟仿真程序，只要确保模拟的状态不会重复就算是模拟成功。 然后再把模拟仿真结果渲染在一个GIF格式的图像上。

手动编译步骤：

```
$ wasm-pack build
$ npm install

$ npm run serve     # to start the webpack dev server
$ npm run bundle    # to create the production bundle

```

[点击进入模拟例子-Goto the Online Simulator](https://iostapyshyn.github.io/wired-logic/)

[更多请阅读-Read More in Project Github](https://github.com/iostapyshyn/wired-logic-rs "Wired Logic - a pixel-based digital circuit simulator running in a browser")

### 用Rust + WASM编写的RISC-V处理器仿真器。

#rust

用Rust + WASM编写的RISC-V processor仿真器，在浏览器里运行Linux。

另外[d0iasm](https://twitter.com/d0iasm)  正在写一本[关于用Rust实现RISC-V processor仿真器的书](https://book.rvemu.app/)，

想学习计算机体系结构的同学可以来看看。

[Repo](https://github.com/takahirox/riscv-rust)  [Read More](https://book.rvemu.app/)

[RISC-V processor emulator written in Rust+WASM](https://github.com/takahirox/riscv-rust)

# spair: Single Page Application in Rust

是一個製作單頁網頁的rust framework

### Yew 中文文档

详情：[https://yew.rs/docs/v/zh_cn/](https://yew.rs/docs/v/zh_cn/)

### 【博客】一个可能的 Rust 新后端

详情：[https://jason-williams.co.uk/a-possible-new-backend-for-rust](https://jason-williams.co.uk/a-possible-new-backend-for-rust)

#### Krustlet: 在Kubernetes中运行WebAssembly的Workloads (Rust语言实现)

[Krustlet: Running WebAssembly Workloads in Kubernetes (written in Rust)](https://deislabs.io/posts/introducing-krustlet/)

取名Krustlet就是指Kubernetes-rust-kubelet的意思。 项目的目的：

-   在Kubernetes上部署WebAssembly变得简单轻松。
-   就是想向技术社区证明和展示如何在Kubernetes上用不同的编程语言实现架构层的想法和设计。 因为很多Kubernetes的应用都是用GO语言编写的，我们现在用Rust语言来实现Krustlet。

# watson: no_std + alloc的最小的wasm解析器

[Read more](https://github.com/richardanaya/watson)

---
++++++
---

## game

### - 游戏开发中常用`mathbench`测量编译时间

[https://bitshifter.github.io/2020/04/12/mathbench-build-timings/](https://bitshifter.github.io/2020/04/12/mathbench-build-timings/)

### -  [Valora: 一个能打印的命令行电脑生成艺术图形库。](https://paytonturnage.gitbook.io/valora/)

[https://paytonturnage.gitbook.io/valora/](https://paytonturnage.gitbook.io/valora/)  [https://github.com/turnage/valora](https://github.com/turnage/valora)

[Valora](https://github.com/turnage/valora)是一个能作画的画笔，写的可视化构建可以：

-   通过rng种子管理可以做到不断重复
-   不通过改变大小就可以任意产生任意精度的像素。
-   严格的类型安全的颜色语法，确保打印的时候不会有色差
-   适应各种不同的硬件
-   用Rust语言开发，几乎不会出错！

大家可以试试下面的教程：

```
cargo new art --bin && cd art
cargo install cargo-edit && cargo add valora

```

然后在`main.rs`里面加入下面的代码：

```
use valora::prelude::*;

fn main() -> Result<()> {
    run_fn(Options::from_args(), |_gpu, world, _rng| {
        Ok(move |ctx: Context, canvas: &mut Canvas| {
            canvas.set_color(LinSrgb::new(1., 1., 1.));
            canvas.paint(Filled(ctx.world));

            let max_radius = world.width / 3.;
            let radius = ctx.time.as_secs_f32().cos().abs() * max_radius;

            canvas.set_color(LinSrgb::new(1., 0., 0.));
            canvas.paint(Filled(Ellipse::circle(world.center(), radius)));
        })
    })
}

```

运行就可以看到计算机创作的精美图案了：

```
cargo run --release

```

大家试一试！第一次编译的时候需要的时间稍微长点，当valora开始运行的时候， 你就可以看到一个不断变化大小的红圈！

### 康威生命游戏GameBoy Advance实现

#rust #gamedev

[康威生命游戏](https://zh.wikipedia.org/zh-hans/%E5%BA%B7%E5%A8%81%E7%94%9F%E5%91%BD%E6%B8%B8%E6%88%8F)是英国数学家约翰·何顿·康威在1970年发明的细胞自动机，每个格子代表一个细胞的状态，一个细胞的当前状态由它相邻的8个细胞的上个状态决定，这个游戏也是Rust WebAssembly教程的例子，[@bokuweb](https://github.com/bokuweb)在Gameboy Advance设备上实现了这个游戏。

[Repo](https://github.com/bokuweb/lifegameboy)

### Kubie简介

Kubie，是kubectx和kubens的强劲替代方案，其中功能包括：Shell隔离模式等。

[介绍文章](https://blog.sbstp.ca/introducing-kubie/)，https://blog.sbstp.ca/introducing-kubie/

[Github](https://github.com/sbstp/kubie)，https://github.com/sbstp/kubie

### Oxygen ：Rust实现的HTML5 Core的游戏引擎

HTML5 + WASM游戏引擎，适用于用Web-sys 和 Rust编写游戏。高度基于 specs 这个库来实现。游戏开发爱好者可以关注下。

详情：[https://github.com/PsichiX/Oxygengine](https://github.com/PsichiX/Oxygengine)

---
++++++
---

## gui

### - OrbTk 0.3.1-alpha2

Rust UI 工具库 OrbTk 发布新版本. OrbTk的目标是快速、易用以及跨平台. 灵感来自于Flutter、React、Yew.

![image.png](https://i.loli.net/2020/04/23/n1CcUyLa8Q7JBNM.png)

[Read More](https://github.com/redox-os/orbtk)

### 基于gfx-hal的Rust图形学教程-第三部分

#graphics

[part 3](https://www.falseidolfactory.com/2020/04/16/intro-to-gfx-hal-part-3-vertex-buffers.html)  [part 2](https://www.falseidolfactory.com/2020/04/01/intro-to-gfx-hal-part-2-push-constants.html)  [part 1](https://www.falseidolfactory.com/2020/04/01/intro-to-gfx-hal-part-1-drawing-a-triangle.html)

### WGPU-rs 1.5 发布

#rust #graphics

WGPU是一个基于 gfx-hal 的 WebGPU 原生实现。

[Repo](https://github.com/gfx-rs/wgpu/blob/master/CHANGELOG.md#v05-06-04-2020)

# iced: 新的跨平台gui

是一個參考Elm製作的gui https://elm-lang.org/

[畫面預覽](https://gfycat.com/littlesanehalicore-rust-gui)

[Read more](https://github.com/hecrj/iced)

---
++++++
---

## db


---
++++++
---

## web

### 5 -  `Apache Spark`的`Rust`语言绑定

> [Rust bindings for Apache Spark](https://github.com/ballista-compute/ballista/tree/master/rust/examples/apache-spark-rust-bindings)

这里例子演示使用Ballista Rust DataFrame API运行一个Apache Spark的查询请求.

[Rust Client:](https://github.com/ballista-compute/ballista/tree/master/rust/examples/apache-spark-rust-bindings#rust-client)

例子程序使用`Ballista's的[Rust DataFrame](https://github.com/ballista-compute/ballista/blob/master/rust/src/dataframe.rs).`  创建一个逻辑查询计划，对一个CVS文件做聚合查询：

```
let spark_master = "local[*]";

let mut spark_settings = HashMap::new();
spark_settings.insert("spark.app.name", "rust-client-demo");
spark_settings.insert("spark.ballista.host", "localhost");
spark_settings.insert("spark.ballista.port", "50051");

let ctx = Context::spark(spark_master, spark_settings);

let path = "/mnt/nyctaxi/csv/yellow/2019/yellow_tripdata_2019-01.csv";

let df = ctx
.read_csv(path, Some(nyctaxi_schema()), None, true)?
.aggregate(
   vec![col("passenger_count")], // group by 
   vec![min(col("fare_amount")), max(col("fare_amount"))] // aggregates
)?;

// print the query plan
df.explain();

// collect the results from the Spark executor
let results = df.collect().await?;

// display the results
utils::print_batches(&results)?;

```

当代码执行的时候`collect()`函数会将逻辑计划编码成protobuf格式， 然后发送给在`spark_settings`设置中设置了服务端口并运行了`Ballista Spark Executor`执行器的远程服务器节点。

上面的例子程序将执行显示如下结果：

```
Aggregate: groupBy=[[#passenger_count]], aggr=[[MIN(#fare_amount), MAX(#fare_amount)]]
 TableScan: /mnt/nyctaxi/csv/yellow/2019/yellow_tripdata_2019-01.csv projection=None
+-----------------+-------+-----------+
| passenger_count | MIN   | MAX       |
+-----------------+-------+-----------+
| 1               | -362  | 623259.86 |
| 6               | -52   | 262.5     |
| 3               | -100  | 350       |
| 5               | -52   | 760       |
| 9               | 9     | 92        |
| 4               | -52   | 500       |
| 8               | 7     | 87        |
| 7               | -75   | 78        |
| 2               | -320  | 492.5     |
| 0               | -52.5 | 36090.3   |
+-----------------+-------+-----------+

```

[Spark Executor](https://github.com/ballista-compute/ballista/tree/master/rust/examples/apache-spark-rust-bindings#spark-executor)  Ballista的Spark执行器[Spark Executor](https://github.com/ballista-compute/ballista/tree/master/rust/examples/apache-spark-rust-bindings#spark-executor)  在收到客户端发送过来的使用protobuf格式编码的逻辑查询计划请求后[翻译](https://github.com/ballista-compute/ballista/blob/master/spark/src/main/scala/org/ballistacompute/spark/executor/BallistaSparkContext.scala)  成如下的Spark执行计划：

```
== Physical Plan ==
*(2) HashAggregate(keys=[passenger_count#3], functions=[min(fare_amount#10), max(fare_amount#10)])
+- Exchange hashpartitioning(passenger_count#3, 200), true, [id=#18]
   +- *(1) HashAggregate(keys=[passenger_count#3], functions=[partial_min(fare_amount#10), partial_max(fare_amount#10)])
      +- *(1) Project [passenger_count#3, fare_amount#10]
         +- BatchScan[passenger_count#3, fare_amount#10] CSVScan Location: InMemoryFileIndex[file:/mnt/nyctaxi/csv/yellow/2019/yellow_tripdata_2019-01.csv], ReadSchema: struct<passenger_count:int,fare_amount:double>

```

> 上面的例子是用到了[Apache Arrow Flight](https://arrow.apache.org/blog/2019/10/13/introducing-arrow-flight/)协议， 想了解更多请参阅[SparkFlightProducer](https://github.com/ballista-compute/ballista/blob/master/spark/src/main/scala/org/ballistacompute/spark/executor/SparkFlightProducer.scala)代码实现。


---
++++++
---

## tools

# 用Rust編寫的GPLv2安全氣囊控制軟件

[Read more](https://github.com/victoredwardocallaghan/techair)

### monolith：将完整的网页保存为一个独立html页面

和一般浏览器的「保存为网页」不一样，该工具可以把所以的css、js、image等元素都保存到独立的html页面里，即便是离线，它也可以按当前浏览器呈现的状态来保存网页。（类似于Chrome的mth格式文件）

[https://github.com/Y2Z/monolith](https://github.com/Y2Z/monolith)

---
++++++
---

## ffi

### 6 - Rust语言Android SDK升级到API level 16了！(直接从level 14升级)

> [Upgrade Rust's Android SDK to API level 16 #71123](https://github.com/rust-lang/rust/pull/71123)

### 系列轻教程：在 Rust 中写 Python 代码

作者实现了一个 python! 宏，结合pyo3（一个流行的python api的rust ffi 绑定），可以让你在 Rust中编写python代码。

教程是他如何编写该库。 学习宏、FFi 可以参考该库。

[文章](https://blog.m-ou.se/writing-python-inside-rust-1/)，https://blog.m-ou.se/writing-python-inside-rust-1/  [代码](https://github.com/fusion-engineering/inline-python)，https://github.com/fusion-engineering/inline-python

### Boa 发布 v0.7，快乐

Boa 是个 JS 引擎，新版本v0.7，大部分工作是重写解析器，新解析器速度快了67%，

[Github Changelog](https://github.com/jasonwilliams/boa/blob/master/CHANGELOG.md)，https://github.com/jasonwilliams/boa/blob/master/CHANGELOG.md

# Rust's Android SDK 更新到 API level 16

[Read more](https://github.com/rust-lang/rust/pull/71123)

#### 3 -  `Flutter RS`  - 开发桌面版`Flutter App`  (用`Rust`做后端) 已经发布在`stable branch`上了。

[https://github.com/flutter-rs/flutter-rs](https://github.com/flutter-rs/flutter-rs)

用rust和Flutter开发桌面版应用。

需要安装的软件：

-   [Rust](https://www.rust-lang.org/tools/install)
-   [Flutter sdk](https://flutter.io/)

开发步骤：

-   安装cargo flutter命令
    
    ```
    cargo install cargo-flutter
    
    ```
    
-   从模版创建新项目
    
    ```
    git clone https://github.com/flutter-rs/flutter-app-template
    
    ```
    
-   采用cli hot-reloading开发:
    
    ```
    cd flutter-app-template
    cargo flutter run
    
    ```
    

发布：

最后要发布应用程序，只需运行：`cargo flutter --format appimage build --release`

### Servo编程

Servo是一个用Rust语言开发，可以在Spidermonkey VM中运行JS或WASM代码。该篇文章是关于Servo编程的，介绍了如何与Servo集成。

[Medium文章](https://medium.com/programming-servo/programming-servo-my-own-private-runtime-8a5ba74c63c8)，https://medium.com/programming-servo/programming-servo-my-own-private-runtime-8a5ba74c63c8

### Anagrams

Anagrams，使用Kotlin + Rust实现Anagrams原生移动应用。

[Gitlab](https://gitlab.com/dpezely/native-android-kotlin-rust)，https://gitlab.com/dpezely/native-android-kotlin-rust

### Malluscript，Rust实现的脚本语言

Malluscript是一种脚本语言，不是严格类型安全的，仅使用两种数据类型：字符串和整数，当前处于开发阶段。

[Github](https://github.com/Sreyas-Sreelal/malluscript)，https://github.com/Sreyas-Sreelal/malluscript

### `mun-lang`一门基于 Rust 的新生编程语言

这门语言刚起步，代码采用 Rust 提倡的多crate结构，逻辑看上去很清晰，对编程语言感兴趣的可以看看。

特点：

-   提前编译-Mun提前编译（AOT），而不是即时解释或编译（JIT）。 通过在AOT编译期间检测代码中的错误，可以消除整个运行时错误类别。 这使开发人员可以在自己的IDE舒适的范围内，而不必在IDE和目标应用程序之间切换以调试运行时错误。
    
-   静态类型-Mun在编译时而不是在运行时解析类型，从而在编写代码和打开强大的重构工具之门时立即得到反馈。
    
-   一流的热重载（hot-reloading ）Mun的每个方面在设计时都考虑了热重载。
    
-   性能-AOT编译与静态类型结合可确保将Mun编译为可以在任何目标平台上本地执行的机器代码。
    
-   LLVM用于编译和优化，以确保最佳性能。 热重载确实会引入一点运行时开销，但是可以在生产版本中禁用它，以确保最佳的运行时性能。
    
-   交叉编译-Mun编译器能够从任何受支持的编译器平台编译到所有受支持的目标平台。
    
-   强大IDE集成 (目前尚未实现) -Mun语言和编译器框架旨在支持源代码查询，从而实现了强大的IDE集成，例如代码完成和重构工具。
    

示例：

```
fn main() {
    let sum = add(a, b);

    // Comments: Mun natively supports bool, float, and int
    let is_true = true;
    let var: float = 0.5;
    
}

// The order of function definitions doesn't matter
fn add(a: int, b: int): int {
    a + b
}


```

---
++++++
---
消息来源：@Chaos 张老师 ，Mun 源码仓库： https://github.com/mun-lang/mun ，书籍 ： https://github.com/mun-lang/book

## Embedded

# 嵌入式Rust模式-零空間參考

文章提出一種參考方式可以在嵌入式系統使用 讓你可以在嵌入式系統中節省記憶體的使用

[Read more](https://ferrous-systems.com/blog/zero-sized-references/)

### 系列文章：通过构建 Risc-V 机器人来学习嵌入式 Rust

作者使用的是 SiFive FE310 RISC-V微控制器的HiFive1开发板

[https://k155la3.blog/tags/riscv/](https://k155la3.blog/tags/riscv/)

### MATRIX Creator 开发板的 Rust 硬件抽象层

MATRIX Creator是一款专为人工智能而生的功能齐全的开发板，包括传感器、无线通信和FPGA。MATRIX Creator的使命是为世界各地的每一个学生、研究人员、创客、喜欢小发明和开发人员提供一个完整的、经济的、用户友好的工具，用于简单到复杂的物联网(IoT)应用程序的创建。

组成：

-   处理器：Atmel Cortex-M3 ATSAM3S2
-   FPGA（可编程逻辑门）：Xilinx Spartan 6 XC6SLX4
-   麦克风阵列：8 MEMS MP34DB02 音频传感器数字麦克风
-   IMU：ST LSM9DS1 3D 加速度, 3D 陀螺仪e, 3d 地磁计
-   温度 /湿度：ST HTS221 电容式温度和相对湿度传感器
-   海拔传感器：NXP MPL3115A2 高精度压力传感器
-   zigbee：芯科 EM358X - 2.4 GHz IEEE 802.15.4
-   Z-Wave：Sigma Designs ZM5202 - 868/908/921 MHz
-   红外接收器：Vishay TSOP573 - carrier 38.0 kHz
-   红外发射:2 Vishay LEDs (front and bottom), 930nm, 100mA, 120° viewing angle
-   紫外线传感器:Vishay VEML6070 UV light sensor
-   NFC:NXP PN512 NFC 读卡器
-   Everloop:35 RGBW LEDS

NFC 通过移动设备或物理嵌入标签的安全交互。

麦克风阵列 驱动基于声音的行为与波束形成和回声消除从8个麦克风

传感器 对温度、压力、紫外线、运动和方位等实时信息做出测量。

斯巴达克-6 现场可编程逻辑门 用于机器学习、密码学、独立内存或软cpu的可重构计算能力。性能可以通过您自己的FPGA定制或下载我们的更新来定制和改进。

无线个域网 在你的家庭和企业中，与各种无线设备进行通信。

z - wave 控制2100多个z波段智能家居设备。

详情：[https://github.com/matrix-io/matrix-rhal](https://github.com/matrix-io/matrix-rhal)

---
++++++
---

## async

# Tide 0.8.0 發佈了！

新特色 Fallible endpoints

```
use async_std::{fs, io};
use tide::{Response, StatusCode};

#[async_std::main]
async fn main() -> io::Result<()> {
    let mut app = tide::new();

    app.at("/").get(|_| async move {
        let mut res = Response::new(StatusCode::Ok);
        res.set_body(fs::read("my_file").await?);
        Ok(res)
    });

    app.listen("localhost:8080").await?;
    Ok(())
}

```

新特色 Server-Sent Events

```
use tide::sse;

#[async_std::main]
async fn main() -> Result<(), std::io::Error> {
    let mut app = tide::new();
    app.at("/sse").get(sse::endpoint(|_req, sender| async move {
        sender.send("fruit", "banana", None).await;
        sender.send("fruit", "apple", None).await;
        Ok(())
    }));
    app.listen("localhost:8080").await?;
    Ok(())
}

```

新特色 Static file serving

```
#[async_std::main]
async fn main() -> Result<(), std::io::Error> {
    let mut app = tide::new();
    app.at("/public/images").serve_dir("images/")?;
    app.listen("127.0.0.1:8080").await?;
    Ok(())
}

```

[Read more](https://github.com/http-rs/tide/releases/tag/v0.8.0)

### async-graphql 1.8.0发布了！

#rust

新增Apollo Federation网关协议的支持，用rust写基于graphql接口的微服务成为可能！ 改变用rust来写graphql只能做做玩具项目的现状。。。

[Read More](https://github.com/sunli829/async-graphql)

### async-postgres：运行时独立的异步 PostgreSQL 客户端

[https://github.com/Hexilee/async-postgres](https://github.com/Hexilee/async-postgres)

### 对Rust中的Futures感兴趣吗?

[https://cfsamson.github.io/books-futures-explained/introduction.html](https://cfsamson.github.io/books-futures-explained/introduction.html)

---
++++++
---

## job
