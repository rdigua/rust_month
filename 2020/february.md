# February 2020

## rust

### pallet，基于sled和tantivy的可搜索数据存储

基于[sled](https://docs.rs/sled)和[tantivy](https://docs.rs/tantivy/0.12.0/tantivy/)的可搜索文档数据存储。

为sled数据库提供类型树（typed-tree）接口，并带有标准的数据存储操作（查找，创建，更新，删除），还提供Lucene/Elasticsearch方式的搜索。

[docs.rs](https://docs.rs/pallet/0.4.1/pallet/)和[Github](https://github.com/kardeiz/pallet)

### arcs v0.3.0

arcs，Rust语言开发的CAD系统，用于构建2D计算机辅助设计应用程序的库。v0.3.0，具有更多的算法和更良好的文档。

[docs.rs](https://docs.rs/arcs/0.3.0/arcs/)

# Rust 1.41.1

Rust 1.41.1解決了Rust 1.41.0中引入的兩個關鍵問題：

一個與靜態生命週期相關的健全漏洞

一個導致分段錯誤的錯誤編譯

[Read more](https://bit.ly/2T7XAC4)

# Tokio v0.2.12

StreamMap 把多個channel 組合起來聽事件

Notify 提供async / await下一步的通知用

[Read more](https://bit.ly/32AKl0c)

# RustCrypto: AEADs

Authenticated Encryption with Associated Data

提供多個加密選項

但不相容openssl不建議使用

[Read more](https://bit.ly/2weJBS0)

### Rust: Veriform 安全面向的序列化庫

看起來像內建blockchain的Protocol Buffers

[https://github.com/iqlusioninc/veriform](https://github.com/iqlusioninc/veriform)

### nix-query-tree-viewer —— nix store可视化工具

[nix](https://nixos.org/nix/manual/#ch-about-nix)是一个纯粹的功能包管理器，Nix将Package保存在Nix-Store，通常保存路径是/nix/store，每个Package都有自己独一无二的子文件夹，比如

```
/nix/store/b6gvzjyb2pg0kjfwrjmg1vfhh54ad73z-firefox-33.1/

```

`b6gvzjyb2pg0…`是该包的唯一标识，可以捕获其所有依赖项目。

[nix-query-tree-viewer](https://github.com/cdepillabout/nix-query-tree-viewer)是一个对`nix store --query --tree`命令结果可视化展示的工具。它提供了树形视图模式，可以展开折叠某一项，并提供多种排序方式和搜索功能。

[Read More](https://linuxwit.ch/blog/2020/02/the-future-of-rusoto/)

### DHAT 一个动态堆内存分析工具

DHAT（A dynamic heap analysis tool）是用于检查程序如何使用其堆分配的工具，它跟踪已分配的块，并检查每个内存访问以查找要访问的块（如果有）。 它在分配点的基础上提供有关这些块的信息，例如大小，生存期，读写次数以及读写模式。它可以帮你找到能够尽量避免掉的short-lived内存分配，如果要使用这个工具，需要在valgrind命令后加上`--tool=dhat`。

[Read More](https://valgrind.org/docs/manual/dh-manual.html)

### dua，Macbook 磁盘使用情况分析器

dua crate  [链接](https://crates.io/crates/dua-cli)

### dtool v0.8.0

dtool是有助于开发的命令行工具集合。新的功能：

-   添加EdDSA（ed25519签名）模块
-   添加sr25519签名模块

[Github](https://github.com/guoxbin/dtool)

### rust nightly版本多种架构的docker image

Docker  [tags](https://hub.docker.com/r/jdrouet/rust-nightly/tags)

### Pangolin

Pangolin 是用于 K8s 的增强型水平 Pod 自动缩放器，用 Rust 实现，它可以使用多种高度可配置的控制策略，根据 Prometheus 指标扩展部署。而且它使用起来还是挺便捷的，

仓库地址：https://github.com/dpeckett/pangolin

reddit 上参与讨论：https://www.reddit.com/r/rust/comments/f7ewtn/pangolin_a_kubernetes_autoscaler_written_in_rust/

### CrabQuery - like JQuery, but for Crabs

CrabQuery 是一个小型、简单的库，可查询 HTML 标记来满足您 Web 抓取需求。

使用示例:

```
use crabquery::Document;

let doc = Document::from(
    "<div class='container'>
       <a class='link button' id='linkmain'>
         <span>text hi there</span>
       </a>
     </div>",
);

let sel = doc.select("div.container > a.button.link[id=\"linkmain\"]");
let el = sel.first().unwrap();

assert_eq!(el.attr("id"), Some("linkmain".to_string()));

let sel = doc.select("div > a > span");
let el = sel.first().unwrap();

assert_eq!(el.text(), Some("text hi there".to_string()));

```

reddit 上参与讨论：https://www.reddit.com/r/rust/comments/f7dir1/crabquery_like_jquery_but_for_crabs/

### teloxide Telegram機器人Framework

一個功能齊全的框架，使您能夠使用Rust中的async / .await語法

輕鬆構建Telegram機器人。

[Read more](https://bit.ly/2T1HLeX)

### Tokenizers 快速的分詞器

Fast State-of-the-Art Tokenizers optimized for Research and Production

可以訓練新的詞語

每1GB的資料可以在他們的Server上以少於20秒的時間內分完

有需要的人應該會覺得好用

[Read more](https://bit.ly/2V5b2YV)

### oox-rs Office Open XML讀取庫

專門讀取 Microsoft's OfficeOpen XML 的庫

[Read more](https://bit.ly/3bNVRJP)

### cow-utils：用于Rust写入时复制字符串实用程序

一些`str`方法执行的转换具有破坏性，因此`String`即使不需要修改，它们也可以分配，复制并返回新的方法 中。

此软件包提供了一种具有辅助特性的`CowUtils`，其中包含此类方法的直接插入变体，它们的行为方式相同，但是在不需要修改时避免额外的副本和分配。

目前，它仅针对`&str`和返回 实现`std::borrow::Cow<str>`，但将来可能会扩展到可能进行更有效处理的其他类型（例如，对可变字符串进行就地修改）。

#### 性能

这个箱子的主要动机是在没有找到匹配的情况下执行零分配替换的功能，因此现在仅显示`.replacevs`的结果`.cow_replace`。

实际结果将根据输入而有所不同，但这是一个品尝者，基于`"a".repeat(40)`输入和各种模式（不匹配，匹配和替换的所有内容，从开始到删除的所有匹配项）：

参数

.replace（ns）

.cow_replace（ns）

区别 （％）

（"a", " "）

408.59

290.27

-29

（“ b”，“ c”）

98.78

54.00

-45

（“ a”，“ b”）

985.99

1,000.70

+1

关于项目详情访问[GitHub](https://github.com/RReverser/cow-utils-rs)。

# 這禮拜的Rust

Alex Crichton：減少對Rust的參與。

將異步/等待帶入嵌入式Rust。

Rust宣布成立ICE-breaker組。

Rust遊戲開發生態系統調查的結果。

std::future::Rusoto的未來。

在VSCode中調試Rust。

從React的角度來看Rust和GTK。

Rust Async入門。

解決Rust中的稀疏矩陣系統。

Markedit。

創建交互應用程式。

Async採訪6：Eliza Weisman。

[read more](https://bit.ly/38qmvX5)

### Boa

它是用 Rust 编写的实验性 Javascript 词法分析器，解析器和编译器。

示例：

![](https://github.com/jasonwilliams/boa/raw/master/docs/img/latestDemo.gif)

项目地址：https://github.com/jasonwilliams/boa

### `git-trim`

![](https://github.com/foriequal0/git-trim/raw/master/images/logo.png)

`git-trim`  是 Rust 编写的项目，他可以自动修剪合并或消失的 git 远程跟踪分支。

仓库地址：https://github.com/foriequal0/git-trim

### rust-bert

NLP 模型 BERT 的 Rust 版，使用了 tch-rs crate并用 rust-tokenizers 进行了预处理，支持多线程分词以及 GPU 接口.  [详情](https://github.com/guillaume-be/rust-bert)

### Rusoto

Rusoto 是一个 Rust 实现的 AWS SDK，目前在 beta 版本 v0.43.0-beta.1 中兼容了std::future::Future.

[Read More](https://linuxwit.ch/blog/2020/02/the-future-of-rusoto/)

### image.rs 发布了0.23版本

#rust #crate

image.rs 是一个用来处理图片的包，新版本ChangeLog:

-   改进了异常捕获机制
-   新的解码器接口
-   更新了依赖
-   寻求更好的色彩空间处理

### krabs —— 一个x86引导程序

#rust #crate

Krabs可以引导用bzip2压缩的ELF格式的内核。Krabs解压缩bz2镜像并重新定位ELF镜像，然后引导内核。一些源代码使用libbzip2 C库进行解压缩，但其余的完全仅是Rust。Krabs 目前还不能运行vmlinux。尚未测试。

[Repo](https://github.com/ellbrid/krabs)

### unbound-telemetry

Prometheus的Unbound DNS解析器已基本完成。

[Github](https://github.com/svartalf/unbound-telemetry)

# 成立LLVM ICE-breaker小組| Inside Rust博客

什麼是Cleaning Crew ICE-breaker組？ “ Cleanup Crew”專注於改進錯誤報告。具體而言，目標是嘗試確保每個錯誤報告都包含修復它所需的所有信息：

一個錯誤的最小程式範例。

連接錯誤報告到重複錯誤報告或相關錯誤報告

如果錯誤是重新出現（曾經有用，但不再有效），把修正的PR的分為stable, nightly

誰應該加入？ 熟悉Rust的任何人都可以完成此工作，而無需特別了解編譯器。

您可以在rustc-guide部分找到有關該組的更多信息。

[read more](https://bit.ly/2UvNood)

### Rust 实现低功耗数字信号处理

[详情](https://interrupt.memfault.com/blog/rust-for-digital-signal-processing)

# Rust Analyzer更新了

rust-analyzer是補助支援Rust IDE分析程式碼的庫

像是Emacs, Visual studio code等

增加了自動 import 的功能

[read more](https://bit.ly/2GNPLL9)

###markedit : 一個編輯Markdown文檔的庫

[read more](https://bit.ly/31ouNMi)

Rust 1.41.0 发布更新要点
Mike Tang 发表于 2020-02-02 21:35

Tags：rust

2020年1月30日 The Rust Release Team

Rust 1.41.0 于美国时间 2020年1月30日 发布。来看看主要有哪些改进。

孤儿规则适当放宽
孤儿规则（orphan rule）指的是

A trait impl is only allowed if either the trait or the type being implemented is local to (defined in) the current crate as opposed to a foreign crate.

在 1.41.0 之前，下面这种写法是不行的：

impl<T> From<BetterVec<T>> for Vec<T> {
    // ...
}
或者更一般的表达：

impl<T> ForeignTrait<LocalType> for ForeignType<T> {
    // ...
}
这是不行的，因为 From 和 Vec 都定义在标准库中，相对于当前 crate 是外部 crate. 虽然有的时候可以通过 newtype 这种设计模式来绕过，但始终还是有很多不方便，甚至不可能。

Rust 1.41.0 中，适当放宽了孤儿规则限制：只要 trait 带一个本地类型作为泛型参数，就可以通过编译。所以 Rust 1.41.0 支持上述写法。不再需要绕弯子了。

cargo install 加强
以往，我们要用 cargo install 安装一个工具的时候，如果之前已经安装过同一个工具的老版本，它会在编译完后，再说，已经有一个老版本存在了，安装失败。浪费时间和能量。

也可以加 --force 参数，强制安装。但是这个意义还是有些区别的。

现在，如果之前装过工具，直接执行 cargo install，会自动升级这个工具的版本到最新。

与 git 配合更加友好的 Cargo.lock 内容格式
之前我们开发，特别是多人协作开发的时候，Cargo.lock 往往会成为一个捣蛋鬼，可能代码其它地方并没有改变，只是重新编译了一次，结果生成了不同的 Cargo.lock 文件，结果被提交到 git 仓库中了。给 git 历史带来了无效的提交，对别人也是一种干扰。

甚至还会造成一些合并冲突。

现在，优化了 Cargo.lock 的格式。解决了上述那些问题。详情请看原文。

FFI 的时候可以直接用 Box 了
Box<T>, 其中，T: Sized，现在与 C 语言的 指针类型（T*）ABI 兼容了。所以，现在可以直接这样写了：

C 这边

// C header */

// Returns ownership to the caller.
struct Foo* foo_new(void);

// Takes ownership from the caller; no-op when invoked with NULL.
void foo_delete(struct Foo*);
Rust 这边

#[repr(C)]
pub struct Foo;

#[no_mangle]
pub extern "C" fn foo_new() -> Box<Foo> {
    Box::new(Foo)
}

// The possibility of NULL is represented with the `Option<_>`.
#[no_mangle]
pub extern "C" fn foo_delete(_: Option<Box<Foo>>) {}
方便好多啊，而且更自然，更形象了。更细致的说明，请阅读下面英文原文。

其它
对 32-bit Apple 编译目标即将停止支持，1.41.0 是最后一版支持了。
标准库中的一些函数，稳定了；
其它一些细节，请参考原文。

Ext Link: https://blog.rust-lang.org/2020/01/30/Rust-1.41.0.html

### Pueue

Pueue，是一个命令行任务管理工具，用于顺序和并行执行长时间运行的任务。

![Pueue](https://raw.githubusercontent.com/Nukesor/images/master/pueue.gif)

**为什么要使用它？**

想象一下必须将大量数据从不同目录解压缩或传输到其他目录。

Pueue是专门为这些情况而设计的。它在各自的目录中执行长时间运行的任务，而不受任何终端的约束。一些可能的应用程序：

-   复制大量的东西
-   压缩任务
-   电影编码
-   rsync任务
-   任何花费超过5分钟的任务

[Github](https://github.com/nukesor/pueue)

### Nestur

Nestur，Rust中的NES模拟器。

[Github](https://github.com/spieglt/nestur)

### Veloren v0.5

Veloren，是一个开放世界，开放源代码的多人体素（voxel）RPG。该游戏尚处于开发初期，但可以玩。

[Veloren](https://veloren.net/)

[Gitlab](https://gitlab.com/veloren)

---
++++++
---

## learning

### 使用 WebAssembly 和 Rust 保护 Firefox

这是个很有意思的博文。保护个人的安全和隐私是 Mozilla 使命的核心原则，因此 Mozilla 不断努力使用户在线更加安全。 对于像 Firefox 这样的复杂且高度优化的系统，内存安全是最大的安全挑战之一。

Firefox 主要是用 C 和 C++ 编写的，而尽管 Firefox 中广泛使用沙箱（sandboxing）和 Rust，但它们都有其局限性。流程级沙箱可很好地用于大型的现有组件，但会消耗大量系统资源，因此必须谨慎使用。Rust 是轻量级的，但是重写数百万行的现有 C++ 代码是一个极其劳动密集型的过程。

所以 Mozilla 是如何使用 WebAssembly 和 Rust 保护 Firefox 的呢？  [请看原文](https://hacks.mozilla.org/2020/02/securing-firefox-with-webassembly/)：https://hacks.mozilla.org/2020/02/securing-firefox-with-webassembly/

[Reddit 上参与讨论](https://www.reddit.com/r/rust/comments/f9qk28/securing_firefox_with_webassembly_and_rust/):https://www.reddit.com/r/rust/comments/f9qk28/securing_firefox_with_webassembly_and_rust/

### Rust: 教你如何比sort|uniq快30倍

簡單好用的小技巧

[https://medium.com/adobetech/filtering-duplicates-on-the-command-line-30x-faster-than-sort-uniq-96ca5f7b4277](https://medium.com/adobetech/filtering-duplicates-on-the-command-line-30x-faster-than-sort-uniq-96ca5f7b4277)

### Rust: rustc profiler

profiler教學搭配官方維護的profiler

分別是 crox flamegraph summarize

有時間比較、火焰圖、函數時間圖

![image.png](https://i.loli.net/2020/02/27/OsZhHY2LSpfrVQi.png)  ![image.png](https://i.loli.net/2020/02/27/tvACRj5pBikOwUu.png)  ![image.png](https://i.loli.net/2020/02/27/mWDajrPKhMlZnGS.png)

[https://blog.rust-lang.org/inside-rust/2020/02/25/intro-rustc-self-profile.html](https://blog.rust-lang.org/inside-rust/2020/02/25/intro-rustc-self-profile.html)

### Rust的 Type-Driven 开发简介

这篇博客的目的是研究Rust的Type-Driven开发。Type-Driven开发是一种使用类型系统开发强大且经过验证的软件的方法。

博客原文：[https://medium.com/@11Takanori/introduction-to-type-driven-development-with-rust-6f8a767cc3df](https://medium.com/@11Takanori/introduction-to-type-driven-development-with-rust-6f8a767cc3df)

## Rust/WinRT即将到来

在过去五个月左右的时间里，团队一直在疯狂地研究Rust / WinRT，因此我团队在rust方面的努力仍在继续。我期待着尽快向社区开放。即使那样，这仍将是早期的日子，但仍有很多工作要做，我们基本上同意建立语言投影大约需要三年。自然地，这其中蕴含着十分大的价值。

仍然可以使用Rust / WinRT进行API调用，并且看到它们结合在一起非常令人满意。因此，我将带给您一些先睹为快的信息，以使您了解Rust中调用Windows API的外观。这是古老的`Windows.Foundation.Uri`类：

```
use windows::foundation::*;

let uri = Uri::create_uri("https://kennykerr.ca")?;
assert!(uri.domain()? == "kennykerr.ca");
assert!(uri.port()? == 443);
assert!(uri.to_string()? == "https://kennykerr.ca/");

```

这是使用`Windows.ApplicationModel.DataTransfer`命名空间将一些值复制到剪贴板的另一个示例：

```
use windows::application_model::data_transfer::*;

let content = DataPackage::new()?;
content.set_text("Rust/WinRT")?;

Clipboard::set_content(content)?;
Clipboard::flush()?;

```

这里我们调用了DataPackage的默认构造函数，但是Rust当然没有构造函数。因此，默认构造函数被常规的new方法替换。

最后，这是使用`Windows.UI.Composition API`的示例：

```
use windows::foundation::numerics::*;
use windows::ui::composition::*;
use windows::ui::*;

let compositor = Compositor::new()?;
let visual = compositor.create_sprite_visual()?;
let red = Colors::red()?;
assert!(red == Color { a: 255, r: 255, g: 0, b: 0 });

let brush = compositor.create_color_brush_with_color(red)?;
visual.set_brush(brush)?;

visual.set_offset(Vector3 { x: 1.0, y: 2.0, z: 3.0, })?;
assert!(visual.offset()? == Vector3 { x: 1.0, y: 2.0, z: 3.0 });

```

在这里您可以看到我们正在创建一个合成器。我们使用合成器使用红色笔刷创建一个精灵视觉效果，然后设置视觉效果的偏移量。这看起来很简单，但这证明了Rust / WinRT的开发已经进行了大量工作，以使其看起来像Rust一样自然和原生。Composition API是Windows API中仅有的两种类型层次结构之一，需要特别注意才能正确使用任何语言，更不用说缺乏传统继承的语言了。

Rust / WinRT允许您使用直接从描述API的规范元数据中即时生成的代码调用，现在和将来的任何 Windows API，然后直接进入您的Rust包，在其中您可以像调用另一个一样调用它们的rust模块。

博客原文：[https://kennykerr.ca/2020/02/22/rust-winrt-coming-soon/](https://kennykerr.ca/2020/02/22/rust-winrt-coming-soon/)

## Plotly for Rust

由Plotly JS支持的Rust绘图库。

#### Plotly的功能

绘制折现与散点图

```
extern crate plotly;
use plotly::charts::{Mode, Scatter};
use plotly::Plot;

fn line_and_scatter_plot() {
    let trace1 = Scatter::new(vec![1, 2, 3, 4], vec![10, 15, 13, 17])
        .name("trace1")
        .mode(Mode::Markers);
    let trace2 = Scatter::new(vec![2, 3, 4, 5], vec![16, 5, 11, 9])
        .name("trace2")
        .mode(Mode::Lines);
    let trace3 = Scatter::new(vec![1, 2, 3, 4], vec![12, 9, 15, 12]).name("trace3");

    let mut plot = Plot::new();
    plot.add_trace(trace1);
    plot.add_trace(trace2);
    plot.add_trace(trace3);
    plot.show();
}

fn main() -> std::io::Result<()> {
    line_and_scatter_plot();
    Ok(())
}

```

![](https://github.com/igiagkiozis/plotly/raw/master/docs/images/line_and_scatter_plot.png)

```
extern crate plotly;
use plotly::charts::{Line, LineShape, Legend, Font};
use plotly::charts::Layout;
use plotly::charts::{Mode, Scatter};
use plotly::Plot;

fn line_shape_options_for_interpolation() {
    let trace1 = Scatter::new(vec![1, 2, 3, 4, 5], vec![1, 3, 2, 3, 1])
        .mode(Mode::LinesMarkers)
        .name("linear")
        .line(Line::new().shape(LineShape::Linear));
    let trace2 = Scatter::new(vec![1, 2, 3, 4, 5], vec![6, 8, 7, 8, 6])
        .mode(Mode::LinesMarkers)
        .name("spline")
        .line(Line::new().shape(LineShape::Spline));
    let trace3 = Scatter::new(vec![1, 2, 3, 4, 5], vec![11, 13, 12, 13, 11])
        .mode(Mode::LinesMarkers)
        .name("vhv")
        .line(Line::new().shape(LineShape::Vhv));
    let trace4 = Scatter::new(vec![1, 2, 3, 4, 5], vec![16, 18, 17, 18, 16])
        .mode(Mode::LinesMarkers)
        .name("hvh")
        .line(Line::new().shape(LineShape::Hvh));
    let trace5 = Scatter::new(vec![1, 2, 3, 4, 5], vec![21, 23, 22, 23, 21])
        .mode(Mode::LinesMarkers)
        .name("vh")
        .line(Line::new().shape(LineShape::Vh));
    let trace6 = Scatter::new(vec![1, 2, 3, 4, 5], vec![26, 28, 27, 28, 26])
        .mode(Mode::LinesMarkers)
        .name("hv")
        .line(Line::new().shape(LineShape::Hv));

    let mut plot = Plot::new();
    let layout = Layout::new()
        .legend(Legend::new().y(0.5).trace_order("reversed")
            .font(Font::new().size(16)));
    plot.add_layout(layout);
    plot.add_trace(trace1);
    plot.add_trace(trace2);
    plot.add_trace(trace3);
    plot.add_trace(trace4);
    plot.add_trace(trace5);
    plot.add_trace(trace6);
    plot.show();
}

fn main() -> std::io::Result<()> {
    line_shape_options_for_interpolation();
    Ok(())
}

```

![](https://github.com/igiagkiozis/plotly/raw/master/docs/images/line_shape_options_for_interpolation.png)

了解其更多用法与工程源码请访问[GitHub仓库](https://github.com/igiagkiozis/plotly/tree/master)。

### 为什么Rust同时有String和&str?

[Read More](https://fasterthanli.me/blog/2020/working-with-strings-in-rust/)

### kibi 文本编辑器

用不超过 1024行 Rust 代码写的文本编辑器， 支持 UTF-8、增量搜索、语法高亮、行号等，欢迎贡献.  [详情](https://github.com/ilai-deutel/kibi)

### 给 Java 程序员的 Rust 教程

[全文](https://leshow.github.io/post/rust_for_java_devs/)

# 看nnethercote怎麼優化程式的

他利用Callgrind來看程式碼的執行時間

```
265,344,872 ( 2.97%)  :rustc::ty::query::on_disk_cache::__ty_decoder_impl
236,097,015 ( 2.64%)  :<rustc::ty::query::on_disk_cache::CacheEncoder<E>
213,551,888 ( 2.39%)  :rustc::ty::codec::encode_with_shorthand
165,042,682 ( 1.85%)  :<rustc_target::abi::VariantIdx
 40,540,500 ( 0.45%)  :<u32 as serialize::serialize::Encodable>::encode
 24,026,292 ( 0.27%)  :serialize::serialize::Encoder::emit_seq
 20,160,540 ( 0.23%)  :<rustc::dep_graph::serialized::SerializedDepNodeIndex
  9,661,323 ( 0.11%)  :serialize::serialize::Decoder::read_tuple
  4,898,927 ( 0.05%)  :<rustc::ty::query::on_disk_cache::CacheEncoder<E>
  3,384,018 ( 0.04%)  :<rustc_metadata::rmeta::encoder::EncodeContext
  2,296,440 ( 0.03%)  :<rustc::ty::UniverseIndex

```

一步一步的迭代 最後優化了11~13%

[read more](https://bit.ly/2OTrffR)

### 在 VSCode 中调试 Rust 程序

作者的这个博文基于上文提到的  [Boa](https://github.com/jasonwilliams/boa)  项目。我们可以有多种方法调试  [Boa](https://github.com/jasonwilliams/boa)  的操作，以此去了解它是如何工作的，甚至测试一些 javaScript 的代码。

了解具体的配置方法以及具体实现请看  [博文地址](https://jason-williams.co.uk/debugging-rust-in-vscode)：https://jason-williams.co.uk/debugging-rust-in-vscode

### Rust 零成本的抽象

零成本抽象的概念对于某些编程语言非常重要，比如 Rust 和 C++，这些语言的目的是使用户能够用相对较少的努力编写具有出色性能的程序。

作者认为他写的[这篇文章](https://carette.xyz/posts/zero_cost_abstraction/)正确地反映什么是零成本抽象. 实际上，零成本抽象(即“零开销”)是很难理解的, 也很难与其他编译器优化分离开来，并且很容易被误解.  [这篇博客文章中](https://carette.xyz/posts/zero_cost_abstraction/)，讨论了这个特性，并给出了 Rust 如何使用它来交付您的抽象项目的优化代码的示例.

[https://carette.xyz/posts/zero_cost_abstraction/](https://carette.xyz/posts/zero_cost_abstraction/)

### Pointer-utils: 指针工具集

a collection of crates, providing simple custom DSTs, pointer unions, borrowed reference counts, and more!

[https://github.com/CAD97/pointer-utils/blob/master/blog/Announcement.md](https://github.com/CAD97/pointer-utils/blob/master/blog/Announcement.md)

### Async Diesel

这个仓库简洁、有效地将  `Diesel`  集成到  `async-std`  中,如果你用 Rust 构建后端程序的时候想使用数据库连接池，可以考虑这种方式。

使用示例：

```

#[macro_use]
extern crate diesel;

use async_diesel::*;
use diesel::{
    prelude::*,
    r2d2::{ConnectionManager, Pool},
};
use std::error::Error;
use uuid::Uuid;

// Schema
table! {
    users (id) {
        id -> Uuid,
    }
}

#[async_std::main]
async fn main() -> Result<(), Box<dyn Error>> {
    // Connect
    let manager =
        ConnectionManager::<PgConnection>::new("postgres://postgres@localhost/async_diesel__test");
    let pool = Pool::builder().build(manager)?;

    // Add
    println!("add a user");
    diesel::insert_into(users::table)
        .values(users::id.eq(Uuid::new_v4()))
        .execute_async(&pool)
        .await?;

    // Count
    let num_users: i64 = users::table.count().get_result_async(&pool).await?;
    println!("now there are {:?} users", num_users);

    Ok(())
}

```

项目地址：https://github.com/mehcode/async-diesel

### Cross Compiling Rust for the Raspberry Pi

This guide covers how to set up your linux computer to  `compile`,  `upload`, and  `run`  a Rust binary on your Raspberry Pi.

read more:https://chacin.dev/blog/cross-compiling-rust-for-the-raspberry-pi/

### 用rust实现操作系统教程

#rust #os

用rust实现操作系统的教程，rust官方还有一个用树莓派3实现操作系统的教程。

[Read More](https://os.phil-opp.com/)  [Repo](https://github.com/phil-opp/blog_os)

### 关于executor的博客文章

推荐一篇博客文章，介绍如何从头开始编写更现代，更干净的[juliex](https://github.com/withoutboats/juliex)（最小化executor，是Rust中最早支持async/await的其中之一）。

博客文章：[Build your own executor](https://stjepang.github.io/2020/01/31/build-your-own-executor.html)

---
++++++
---

## strory

### 《深入设计模式》

#code

推荐一个学习设计模式的网站，春节在家自我隔离时系统的学习了设计模式，[这个网站](https://refactoringguru.cn/design-patterns/book)插图丰富，讲解比较细致，还可以购买电子版，支持PDF、 EPUB、 MOBI、 KF。示例语言包括： Java、 C#、 C++、 PHP、 Python、 Ruby、 Swift 和 TypeScript。

[Read More](https://refactoringguru.cn/design-patterns)

### rust编译模型的灾难

#rust

Brian Anderson是rust前核心团队成员，目前已经加入PingCap。

> Rust语言被设计为编译时间久的，但这并不是它的目标。任何语言的设计都面临着很多权衡，而在rust的设计过程中，**运行时性能**和**编译时性能**就是其中之一，Rust永远只考虑运行时的性能，这就导致了它编译时慢得糟糕，很糟糕。

[Read More](https://pingcap.com/blog/rust-compilation-model-calamity/)

----------

---
++++++
---

## wasm

### CasperLabs进入Rust生态

cargo-casperlabs，用于创建和测试Wasm智能合约，在CasperLabs网络上使用的命令行工具，为Rust开发人员提供开发区块链合约的无缝体验。

crate  [链接](https://crates.io/crates/cargo-casperlabs)

### github pages 上托管 Rust + Wasm 项目教程

地址直达：https://github.com/sn99/wasm-template-rust

### WASM向量图形 --wasm_svg_graphics 0.3.0

一个用于通过WASM渲染SVG图形的Rust库

它提供了快速有效的方法，可以使用WebAssembly与SVG进行交互。它能够：

-   声明形状和样式以用于这些形状
-   使用SVG 标签将这些形状渲染到DOM
-   自动检测两个形状是否相同，因此只有一个SVG 将添加到DOM中
-   声明已命名的项目/容器，以便以后进行例如隐藏，重新显示和重新放置之类的调整。

#### 声明

开发团队已测试版本0.3.0的稳定性，并且可以在开发中使用。

此软件包仍在开发中，但大多数对1.0.0的API调用已完成。如果发现任何错误，请在[GitHub](https://github.com/coastalwhite/WasmSVGGraphics)上提交问题或诉求。

原文请查阅[crates.io网站](https://crates.io/crates/wasm_svg_graphics)

### 使用wasm-bindgen-test测试Rust + WebGL渲染器

一周前，作者对改进客户端代码体系结构的所有细节感到有些不知所措，但是从那时起，作者就为所有主要部分布置了数据结构和测试，并对所有组件的安装方式有了很好的认识一起。

因此，现在正在努力的只是编写和实施更多测试，直到所有内容都准备就绪。

在进行这种重构方面，似乎需要多花1~2周的时间，然后我们才能重新投入实际游戏的开发工作中。

-   地形加载和渲染
-   输入事件处理器系统
-   用户界面元素
-   WebGL渲染器

详情前往[作者博客](https://devjournal.akigi.com/february-2020/2020-02-16.html#input-event-processor-system)查看。

### bazel_rust_wasm_azure_functions

这个小项目介绍如何用 Bazel 将 Rust 编译成 wasm 并部署成为 Azure 云函数.  [详情](https://github.com/manekinekko/bazel_rust_wasm_azure_functions)

### Seed 0.6 发布

Seed是使用Rust+Wasm进行前端Web开发的框架。小编个人非常喜欢。

这次主要是内部的大量重构。

[https://seed-rs.org/guide/changelog](https://seed-rs.org/guide/changelog)

### 一个 Yew 个人博客样例

看了一下，效果挺不错的。

[http://shafiqahmad.com/#blog](http://shafiqahmad.com/#blog)

### 嵌入式Rust与`async/await`

sheevink的博客文章，如何将`async/await`引入嵌入式Rust。

[博客文章](https://ferrous-systems.com/blog/embedded-async-await/)

### wasm-pack 0.9.1发布了！

wasm-pack，该工具旨在成为一站式平台，用于构建Rust生成的WebAssembly，希望使用它与JavaScript，浏览器或Node.js进行互操作。同时该项目是rust-wasm工作组的一部分。

[Github](https://github.com/rustwasm/wasm-pack/releases/tag/v0.9.1)  wasm-pack release 0.9.1

### `Strings`  in Rust and WebAssembly

如标题所说，我们将讨论 WebAssembly（Wasm）中的  `String`，说明 Rust 的  `String`  是如何运作的。并且使用  `Wasm-pack`  来构建 HelloWorld 程序。原文地址：https://medium.com/wasm/strings-in-webassembly-wasm-57a05c1ea333

reddit 上参与讨论：https://www.reddit.com/r/rust/comments/ezbebl/strings_in_rust_and_webassembly/

# 有人用WASM寫了GameBoy模擬器

https://i.imgur.com/msv73e8.png

[read more](https://bit.ly/2UnmKOf)

---
++++++
---

## game

### Rust 游戏开发聚合网站

[are we game yet](https://arewegameyet.com/)  此网站聚合了有关Rust游戏开发的资讯、开发工具包索引、Rust 游戏索引、学习资源索引等内容

# Rust遊戲開發-生態系統調查

去年八月，我們對Rust gamedev生態系統進行了一項調查。

現在終於可以展示結果了。

1.  是業餘愛好者，還是專業遊戲開發想用Rust做遊戲呢？

75%是業餘愛好者 20%是商業遊戲開發人員

2.  你有用過Rust在遊戲開發嗎？

45% 考慮使用 50%正在用

3.  作為一種語言和生態系統，Rust會給您作為遊戲開發人員帶來最大的負面影響嗎？

專業人士和業餘愛好者的工作重點基本相同。最大的區別是：

愛好者希望將生態系統成熟度提高兩倍。

愛好者更關心手機、網路的支援程度

專業人士更關心console(Xbox, PS4)支援

專業人士更關心C++互相溝通

4.  Rust的其它問題

無法正確除錯，例如hashmap絕對無法查看內容。不知道它在Rust是如何運作的。

缺少像Visual Studio這類強大的IDE支援

會Rust的人太少，不好找

Sony或Microsoft尚未正式在console(Xbox, PS4)上支援Rust

沒有專業的遊戲引擎（UE4，Unity）與Rust集成。

程式碼以及引擎都是C++。一起使用Rust和C++會很痛苦，

而將現有技術完全重寫為Rust將成本太高。

[read more](https://bit.ly/31wmqyg)

### Rust 游戏开发系列博客

此系列博客的目的是描述怎样用 Rust 来完成一个开源的多人在线RPG游戏，

[详情](https://medium.com/@ryan.cjw/adventures-with-rust-game-development-1d998c45381c)

# Riven: Riot API Library for Rust

查LOL戰績可以用？

[read more](https://bit.ly/2Scobwj)

---
++++++
---

## async

### Roa，异步web框架

```
# Cargo.toml

[dependencies]
roa = "0.4"
async-std = { version = "1.4", features = ["attributes"] }

```

```
// main.rs
use roa::core::App;
use roa::preload::*;
use std::error::Error as StdError;

#[async_std::main]
async fn main() -> Result<(), Box<dyn StdError>> {
    let mut app = App::new(());
    app.end(|mut ctx| async move {
        ctx.write_text("Hello, World").await
    });
    app.listen("127.0.0.1:8000", |addr| {
        println!("Server is listening on {}", addr)
    })?
    .await?;
    Ok(())
}

```

[Github](https://github.com/Hexilee/roa)

### Rust异步入门

本文并不全面介绍Rust异步主题，但如果您不了解Rust中的异步编程或一般的异步编程，则可能是一个简单的概述.

推荐大家阅读这篇文章:  [https://omarabid.com/async-rust](https://omarabid.com/async-rust)

### WUFEI - Async Kuberenetes Namespace Log Recorder / Streamer

灵感来自：[https://github.com/johanhaleby/kubetail](https://github.com/johanhaleby/kubetail)

作者通过这个异步工具解决了他们CPU使用率过高的问题。

[https://github.com/ericmcbride/wufei](https://github.com/ericmcbride/wufei)

### actix-ratelimit

actix-ratelimit，Actix-Web的速率限制中间件框架。

[Github](https://github.com/TerminalWitchcraft/actix-ratelimit)

### 嵌入式Rust与`async/await`

sheevink的博客文章，如何将`async/await`引入嵌入式Rust。

[博客文章](https://ferrous-systems.com/blog/embedded-async-await/)

# rust的 async-std 1.5.0 了

更新了async-std之前的BUG

改進效能、穩定性以及各種附加功能

並且在許多情況下，在內部實作中使用Clone取代Arc。

[read more](https://bit.ly/3b6PZLa)

---
++++++
---

## story

# Rust week 327

```
教學：在Rust中使用字串
Rust / WinRT即將推出
rustc的self profiler簡介
crates.io 2020-02-20事件報告
如何比sort | uniq快30倍。
製作可執行的打包程式
使用Ramer–Douglas–Peucker簡化不規則線段
異步HTTP
關於異步/等待的進一步思考
Rust團隊按比例分流
Dali 圖像處理服務
async_executors 可以構建非同步執行流程
使用vgtk構建TodoMVC
在github頁面或其他頁面上使用 Rust + Wasm項目。
Servo：實作BroadcastChannel。
Fuchsia 程式語言規則
rust-analyzer changelog 113。

```

[Read more](https://bit.ly/2VsjCB9)


### crates.io 2020-02-20 事件报告

UTC 时间 2020 年 2 月 20 日 21:28，我们收到了来自 crates.io 用户的报告，即使自上传 10 分钟后，索引中的仓库仍不可用。这是由于 GitHub 中断导致 crates.io 网站 web 程序中的 bug 被触发。

[在 Rust 官方博客查看报告原文](https://blog.rust-lang.org/inside-rust/2020/02/26/crates-io-incident-report.html):https://blog.rust-lang.org/inside-rust/2020/02/26/crates-io-incident-report.html

此外  [Reddit 上关于此事讨论](https://www.reddit.com/r/rust/comments/f8ney8/hey_rustaceans_got_an_easy_question_ask_here_92020/)：https://www.reddit.com/r/rust/comments/f8ney8/hey_rustaceans_got_an_easy_question_ask_here_92020/

### 高薪招聘 Rust 工程师

4万/月招资深 Rust 后端开发工程师！！！详情请看：https://rust-china.org/article?id=0cac0b1f-b721-4b6a-85b6-48c7481836ba

### Rust: bottom 跨平台工作管理員

![image.png](https://i.loli.net/2020/02/27/zQjPOkoC7xGnFVR.png)

[https://github.com/ClementTsang/bottom](https://github.com/ClementTsang/bottom)

### docs.rs团队负责人离开

[@QuietMisdreavus](https://twitter.com/QuietMisdreavus)在3年半前加入rust，在这段时间他参与领导docs.rs，并且是Rustdoc和Document小组的成员，如今他退出了小组，这篇文章说明了他这段时间的心路历程以及团队的变动。又是一个在开源中筋疲力尽的人。

[Read More](https://quietmisdreavus.net/self/2020/02/17/rust-ghost-signing-off/)

### 福利！Rust 高清壁纸来啦！

![](https://cdn.nlark.com/yuque/0/2020/png/439468/1582346556542-4a9ceeb3-4a2c-455f-aeb6-eb4b72d6e64e.png?x-oss-process=image/resize,w_746)

大图或者原图请戳这里：https://www.reddit.com/r/rust/comments/f796ds/made_a_rusty_rust_wallpaper_the_other_image_was/

### Docs.rs 团队 leader 卸任

[详情](https://quietmisdreavus.net/self/2020/02/17/rust-ghost-signing-off/)

### IntelliJ Rust 更新日志 #116

[详情](https://intellij-rust.github.io/2020/02/18/changelog-116.html)

### Krabs：可以引导vmlinux的x86引导程序

Krabs是用Rust编写的实验性x86 / x86_64引导程序。

Krabs可以引导用bzip2压缩的ELF格式的内核、解压缩bz2映像并重新定位ELF映像，然后引导内核。

一些源代码使用libbzip2 C库进行解压缩，但其余的完全使用Rust。

Krabs正在致力于在32位/ 64位PC上引导以ELF格式格式化的vmlinux和其他内核，并且正在开发中。

Krabs还旨在仅支持最小的Linux启动协议。这使您可以指定内核命令行并在启动时操纵内核的行为。另一个功能是，为了节省空间，ELF格式内核在使用前先使用bzip2进行了压缩，并使用libbzip2库进行解压缩。

下面是一个例子：

```
$ ./tools/build.sh -k vmlinux -i initramfs.cpio.gz -c "clocksource=tsc" disk.img

```

![](https://github.com/ellbrid/krabs/raw/master/docs/images/cmdline.gif)

工程详情与构建方法前往[GitHub](https://github.com/ellbrid/krabs)查看。

### 为什么Rust是最受欢迎的编程语言？

Aleksey Kladov，是一位喜欢简单代码和编程语言的程序员。他写的一篇博客文章，小编这里简单列几个文章中提到的理由：

-   跨平台二进制文件
-   `Ord`，`Debug & Display`
-   详细的数据类型

```
#[derive(
    Debug,
    Clone, Copy,
    PartialEq, Eq,
    PartialOrd, Ord,
    Hash,
    Serialize, Deserialize,
)]
struct Point {
    x: i64,
    y: i64,
}

```

详细参见Aleksey Kladov的[博客文章](https://matklad.github.io/2020/02/14/why-rust-is-loved.html)

# 为什么你写的代码糟透了？

發現昨天看的英文新聞有人翻譯成簡中了

分享一下

[read more](https://bit.ly/2SLA7Fo)

# Sealed Rust

Sealed Rust是Ferrous Systems 的努力的目標

希望從理論上驗證軟體的安全性，並以實作即規範的方式來開發。

目標是通過將Rust編程語言用於安全關鍵軟件開發，

從而改善安全關鍵領域中質量和正確性的現狀。

他們目前制定了一些計劃

1.  制定Rust語言以及最小環境所需的所有關鍵庫與工具
2.  制定Rust編譯器前端產生並由Rust編譯器後端或靜態/動態分析工具使用的Rust語言的IR
3.  驗證Rust編譯器前端能否根據與Rust語言規範相一致的並給程式碼輸入生成正確的IR
4.  驗證Rust編譯器後端從給定的IR生成正確的機器碼的能力
5.  制定特定領域資格認證，例如：適用於汽車，醫療或航空電子相關的工具鑑定標準

[read more](https://bit.ly/2UOPpvZ)

### 关于 Rust 并行编程的讨论

水友请看：https://www.reddit.com/r/rust/comments/f2uqa7/parallel_programming_in_rust/

### ergo 键盘

一个使用 Rust 固件的 ergo 键盘

![image.png](https://i.loli.net/2020/02/13/nY7oWtzxOGsl3ew.png)

### 减少我对 Rust 的参与

Alex Crichton 是 Mozilla Rust 的开发人员，他对 Rust 做出了很多贡献。几天前他宣布将减少对 Rust 的参与，原因是觉得有点累，想歇一歇

[详情](https://internals.rust-lang.org/t/scaling-back-my-involvement-in-rust/11754)

### Rust代码生成器几乎完成了

详情请阅读这篇文章:  [https://github.com/lupyuen/blockly-mynewt-rust](https://github.com/lupyuen/blockly-mynewt-rust)

### reddit /r/rust 订阅已过9w

Reddit /r/rust 应该是全世界最活跃的Rust主题公告和讨论板了。现在订阅数已超9w了。

[https://subredditstats.com/r/rust](https://subredditstats.com/r/rust)

### 一个 Rustacean 的心路历程

作者做了4年scala开发，然后学了半年haskell，然后看了两周Rust，就 fall in love 了。准备今年开始用Rust做一个 MVP 项目。

[https://www.reddit.com/r/rust/comments/f1c3v6/a_rustacean_change_of_heart/](https://www.reddit.com/r/rust/comments/f1c3v6/a_rustacean_change_of_heart/)

### Redox 已经可以在 T520 笔记本上启动了

[https://www.reddit.com/r/rust/comments/f12plt/got_redox_booted_on_a_t520/](https://www.reddit.com/r/rust/comments/f12plt/got_redox_booted_on_a_t520/)

# 為什麼 Discord 要從go轉換到rust

今天來講的更詳細一點

他們發現go程式每兩分鐘就會有一個延遲高峰

這個延遲高峰是因為go每兩分鐘就要清一次記憶體垃圾

這個問題出現在 go 1.9.2 也許最新版修掉了

不過已經對Discord沒有意義了

這次的測試是在 2019年5月進行的

結論：

有GC的語言不代表你可以不用處理記憶體問題

他會在未來轉化成另一種成本更高的問題，如果你有做起來的話

但有GC的開發速度的確快，可以先用有GC的語言先開發個雛形驗證商業模式

在你的商業模式短時間不會改變的情況下，再用其它高效安全沒GC的語言去重寫

[read more](https://bit.ly/38dIGQd)

### 那些在生产中使用 Rust 的公司

按行业组织的，在生产中使用 Rust 的公司的精选列表。可供大家参考，GitHub 地址：https://github.com/omarabid/rust-companies

reddit 上参与讨论：https://www.reddit.com/r/rust/comments/ez7m4u/rust_companies_in_production_list_feel_free_to/

### 为什么 DIscord 正在从 Go 切换到 Rust？

DIscord 是一款实时互动的在线社交应用，主要使用场景是玩游戏的时候可以找队友聊天。官方博客中讲了为什么DIscord 正在从 Go 切换到 Rust，[详情](https://blog.discordapp.com/why-discord-is-switching-from-go-to-rust-a190bbca2b1f)

---
++++++
---

## gui

### KAS GUI 0.3 发布

KAS 0.3 版本发布, 此版本已经在主题，图形和绘图API上进行了大量工作，包括用于Mandlebrot分形的交互式查看器（通过WebGPU着色器），模拟钟面（通过某种程度上可用的绘图API），可切换的主题和不起眼的单选按钮小部件。

该项目的目标是：

1、功能齐全的直观GUI

2、可嵌入游戏或任何窗口管理器中

3、花式/高度灵活的硬件加速渲染（但理论上也可以支持软件渲染）

4、代码内的简单，表达规范（目前受Rust语言限制的束缚，希望将来能解决）

6、用户代码中的自定义小部件不受限制

7、无错误，带有API，可简化编译器正确性

8、高性能/低资源使用率（可选的精美图形除外）

该项目的状态为Alpha：在实现所有目标方面均取得了进展，但功能和愚蠢的图形存在明显的局限性。 可移植性是有限的，需要每晚的Rust和wgpu支持。

了解其更多 请访问  [GitHub仓库](https://github.com/dhardy/kas)

### dali是一项执行图像转换的服务, 该应用程序支持:

1、从HTTP URL检索源图像

2、将图像编码为PNG，JPEG，WEBP或HEIC

3、调整图像大小

4、旋转影像

5、将水印图像应用于图像

这篇文章介绍了 Dali 诞生的背景.  [https://tech.olx.com/presenting-dali-an-image-processor-service-514e6be00de8](https://tech.olx.com/presenting-dali-an-image-processor-service-514e6be00de8), 强烈推荐阅读这段文章.

了解其更多 请访问  [GitHub仓库](https://github.com/olxgroup-oss/dali)

### Pushrod 0.2.27: SDL2-based GUI for Rust - Call for Help!

Pushrod GUI 框架的作者一个人开发了一年多，想邀请更多的开发者参与进来开发。有兴趣的可以了解一下哦。

[https://www.github.com/KenSuenobu/rust-pushrod/issues/](https://www.github.com/KenSuenobu/rust-pushrod/issues/)

# 從React的角度來看Rust和GTK

作者試了幾種能讓React跨平台的方案都失敗後決定來用native的UI

最後他選擇了 Rust + GTK

這種轉換對過去都寫前端的他並不容易

所以他整理了一些方向

方便之後有寫過React的Web前端

快速上手Rust + GTK來做Native前端

[read more](https://bit.ly/31DBp9F)

---
++++++
---

## db

### redisgraph-rs

Redis 图形化数据库，[详情](https://github.com/malte-v/redisgraph-rs)

### `麻辣火锅-DB`？？？

![](https://cdn.nlark.com/yuque/0/2020/png/439468/1581608456941-96e3cfcf-7a1d-456a-a723-b3e101c75666.png)

当然，标题是开玩笑的orz，实际上这个项目是  `hotpot-db`，它是围绕 SQLite 的 JSON 扩展的 API，它使您能够以 NoSQL 的方式（像DynamoDB这样）存储数据。

使用示例：

```
use hotpot_db::*;
use serde::{Deserialize, Serialize};

#[derive(Debug, Serialize, Deserialize)]
struct Person {
    name: String,
    age: u8,
}

fn main() -> Result<(), hotpot_db::Error> {
    let mut pot = HotPot::new();

    // lets make a new collection
    pot.create_collection("address_book")?;

    // well make a new item we want to store
    let person = Person {
        name: String::from("david holtz"),
        age: 26,
    };

    // we insert the object into the collection!
    pot.insert::<Person>("address_book", &person)?;

    // before we query we can add an index to speed things up
    pot.add_index_to_collection("address_book", "name", "naming_index")?;

    // finally we can query
    let query = QueryBuilder::new()
        .collection("address_book")
        .kind(QueryKind::Object)
        .key("name")
        .comparison("=")
        .string("david holtz")
        .finish();

    let results = pot.execute(query);
    println!("{:#?}", results);

    Ok(())
}

```

项目地址：https://github.com/drbh/hotpot-db

reddit 上参与讨论：https://www.reddit.com/r/rust/comments/f2vbji/github_drbhhotpotdb_hottest_way_to_store_data_on/

## full-text

### Tantivy是一個受Apache Lucene啟發的全文搜尋引擎

現在0.12版了

[Read more](https://bit.ly/2P8d5ru)

---
++++++
---

## web

### xworks，静态站点生成器

xworks，简单，没有框架，没有额外的样式表。它生成一个HTML文件，其中包含60行漂亮的内联CSS。

[Github](https://github.com/t1ra/xworks)

## 高度灵活的可用于管理和协调JWT工作流的库

#### 特点

-   管理和协调JWT以进行用户登录、注销和续订
-   异步就绪
-   轻松启动
-   没有不安全的代码
-   在稳定的rust下运行
-   库方法（不需要运行时调用）
-   支持可插拔组件
-   更新新的刷新令牌后使旧的刷新无效
-   更新新的身份验证令牌后使旧的身份验证无效
-   在身份验证令牌到期时处理Thundering herd问题

目前工程需要添加更多示，并提高覆盖率。

前往[GitHub仓库](https://github.com/sgrust01/jwtvault)了解更多。

---
++++++
---

## Embedded

### 搭建我的嵌入式 Rust 开发环境

这是博主关于 Rust 嵌入式开发系列博文的开题文章，博客地址：https://josh.robsonchase.com/。

目前相关的系列博文有：

-   [Bootstrapping My Embedded Rust Development Environment](https://josh.robsonchase.com/embedded-bootstrapping/)
-   [Embedded Rust Frustrations](https://josh.robsonchase.com/embedded-frustrations/)
-   [Building an Embedded Futures Executor](https://josh.robsonchase.com/embedded-executor/)
-   [Building an Embedded Futures Executor II](https://josh.robsonchase.com/embedded-executor-2/)

[Reddit 上相关近期讨论](https://www.reddit.com/r/rust/comments/f9tjeu/embedded_rust_frustrations/):https://www.reddit.com/r/rust/comments/f9tjeu/embedded_rust_frustrations/

---
++++++
---

## tools

# superluminal: 強大的profiler

支援 rust, C++, windows, Xbox

可在windows上運行

![](https://superluminal.eu/wp-content/uploads/2020/02/Rust_Hero.png)

[Read more](https://bit.ly/3a9DTzC)

---
++++++
---

## ffi

### FFI模式

FFI模式一，将复杂的Rust数据结构无缝地暴露给C++。

[博客文章](https://crisal.io/words/2020/02/28/C++-rust-ffi-patterns-1-complex-data-structures.html)
