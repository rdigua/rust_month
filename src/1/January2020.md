# January 2020 


## [【Rust日报】 2020-01-31](https://rust.cc/article?id=927b3dee-3245-48b4-b19c-21855b2eacd3)

[damody](https://rust.cc/blog_with_author?author_id=55ad9d89-6929-4a73-baa5-cf0a99a9abad)  发表于  2020-01-31 10:22

Tags：rust

# rust 1.41了！

除了一些功能更新

重要的是不再支援32-bit Apple產品了

[read more](https://bit.ly/2S1iam9)

# open-source security key

google 使用rust實作了 OpenSK

支援 FIDO U2F, FIDO2 兩種標準

[read more](https://bit.ly/2vBMiwS)

# Rust編譯模型災難

文章作者Brian Anderson是Rust編程語言 及其姊妹項目Servo Web瀏覽器的共同創始人之一。

他現在在PingCAP擔任高級數據庫工程師。

他希望解決TiKV編譯緩慢的問題

在開發模式下進行完全重建可能需要15分鐘，在發布模式下可能需要30分鐘。

對於大型系統項目的開發人員來說，這聽起來可能並不那麼糟糕，

但是它比許多開發人員對現代編程環境所期望的要慢得多。

TiKV是一個相對較大的Rust代碼庫，

有200萬行程式碼。相比之下，Rust本身包含300萬行，而Servo則包含270萬行。

編程語言設計充滿了權衡利弊。這些基本選擇之一是runtime性能與編譯性能，

Rust團隊幾乎總是選擇runtime性能而不是編譯更快速。

如果快速編譯時間不是Rust設計的核心原則，那麼Rust的核心設計原則是什麼？這裡有一些：

實用性-它應該是一種可以在現實世界中使用的語言。

實用主義-它應該要讓人覺得可用，並且將其整合到之前的系統中。

內存安全性-它必須強制執行內存安全性，並且不能接受記憶體存取錯誤。

性能-它必須與C++在一樣快。

並發-它必須提供現代的解決方案來編寫並發代碼。

但這並不是說Rust設計師沒有在快速編譯時間中考慮任何因素。

但因為利弊的權衡，編譯器的性能還是愈來愈慢。

當作者每天使用Rust編譯器工作時，

電腦上至少擁有三份程式碼是很常見的，在其他所有版本都在構建和測試的同時。

我將開始在工作區1編寫程式，開始編譯，然後跳到工作區2，

開始在工作區2工作，編譯後再切換回工作區1。不斷進行在不同的工作區中切換。

雖然在2019年Rust的編譯速度有了提升，但目前Rust還是編譯的不夠快。

下一集會是作者如何優化Rust的編譯速度以達到產品經理的期待

[read more](https://bit.ly/2vD5I4v)

# Bastion 0.34

什麼是Bastion？

Bastion是一個高度可用的容錯runtime系統，具有面向動態調度的輕量級流程模型。

它為輕量級過程實現提供了諸如並發之類的參與者模型，

並有效地利用了所有系統資源，並保證了每次傳送最多的消息。

基於消息的通信與actor model的Mesh網路。

runtime容錯能力使其成為分佈式系統的理想選擇。

具有NUMA感知和仿射緩存SMP執行程序的完全異步runtime。

監督系統使管理生命週期變得容易。

目前哪邊有用到Bastion？

SkyNet (Discord 機器人，用來重新發送已刪除的訊息)

在AWS Lambda中，我們使用Bastion啟用重試機制，並嘗試不同的解析策略來處理數據。

[read more](https://bit.ly/2Ua9mgr)

# Tide 0.6 了

Tide是一個還不成熟的 web framework

這一版增加了對CORS的支持與新的cookies API

也增加了一些新語法讓人用起來更簡單

[read more](https://bit.ly/3aTpglc)

# oreboot

oreboot是coreboot的分支

https://zh.wikipedia.org/wiki/Coreboot

來自維基百科的說明

coreboot，原名LinuxBIOS，是一個旨在取代大多數電腦中專有韌體（BIOS或UEFI）的軟體專案，它採用輕量級韌體設計，只執行載入和執行現代32位元或64位元作業系統所需的最少量任務。

Oreboot當前僅支援LinuxBoot。

Oreboot想利用Rust的安全性製作一個安全穩定快速的BIOS程式。

[read more](https://bit.ly/2S4RuAP)

----------

From 日报小组 @Damody

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-1-30 r/rust 频道的数据统计](https://rust.cc/article?id=935d4727-1dfa-404b-8792-f55c679595a3)

[Jancd](https://rust.cc/blog_with_author?author_id=d32af902-7816-4c8c-838d-60351791516d)  发表于  2020-01-30 22:19

Tags：rust,news

### r/rust 频道的数据统计

在过去的一年左右的时间里，[reddit.com](https://www.reddit.com/)  的 r/rust 频道的订阅人数约为过去六年的总和。

![rust_reddit](https://cdn.nlark.com/yuque/0/2020/png/439468/1580394282792-d129dccd-09fe-42ca-8209-abd5393cfeb7.png?x-oss-process=image/resize,w_1492)

数据源：https://subredditstats.com/r/rust

Reddit 上参与讨论：https://www.reddit.com/r/rust/comments/ew1i8w/in_the_last_year_or_so_rrust_gained_about_as_many/

### Tide 考虑支持 WebSocket

[Tide](https://github.com/http-rs/tide)  对 WebSocket（WS）的支持一直是人们期待已久的功能。最近，我们还收集了 Server Sent Events（SSE）这样的需求。我们将研究 Tide 中  `WS`  和  `SSE`  支持的动机，要求和设计。以下是个参考：

```
let mut app = tide::new();
app.at("/sse").get(tide::sse()); // Endpoint to connect new SSE channels on.
app.at("/").get(async |req| {
    req.sse().send(b"hello chashu").await?; // Send a message over the SSE channel.
    Response::new(200)
});
app.listen("127.0.0.1:8080").await?;

```

更多请看原文：https://blog.yoshuawuyts.com/tide-channels/

twttier 上参与讨论：https://twitter.com/yoshuawuyts/status/1222556805521399810

### google/evcxr 项目

`google/evcxr`  : A Jupyter Kernel for the Rust programming language.

The following example shows how you might provide a custom display function for a type Matrix.

```
use std::fmt::Debug;
pub struct Matrix<T> {pub values: Vec<T>, pub row_size: usize}
impl<T: Debug> Matrix<T> {
    pub fn evcxr_display(&self) {
        let mut html = String::new();
        html.push_str("<table>");
        for r in 0..(self.values.len() / self.row_size) {
            html.push_str("<tr>");
            for c in 0..self.row_size {
                html.push_str("<td>");
                html.push_str(&format!("{:?}", self.values[r * self.row_size + c]));
                html.push_str("</td>");
            }
            html.push_str("</tr>");
        }
        html.push_str("</table>");
        println!("EVCXR_BEGIN_CONTENT text/html\n{}\nEVCXR_END_CONTENT", html);
    }
}
let m = Matrix {values: vec![1,2,3,4,5,6,7,8,9], row_size: 3};
m

```

Reddit 上参与讨论：https://www.reddit.com/r/rust/comments/evrexn/evcxrevcxr_jupyter_jupyter_kernel_for_rust/

### ferrugo

Ferrugo(https://github.com/maekawatoshiki/ferrugo) is a JVM implementation written in Rust

Reddit 上参与讨论：https://www.reddit.com/r/rust/comments/evnv8z/ferrugo_a_jvm_implementation_written_in_rust/

### self_update

`self_update`  提供更新程序，用于从各种发行版本的后端可以就地更新 rust 可执行文件。

项目地址：https://github.com/jaemk/self_update

----------

From 日报小组 @Jancd

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust 日报】2020-01-29 Nushell 0.9.0](https://rust.cc/article?id=fffadea3-28df-4dd3-9145-8236323e7a21)

[挺肥](https://rust.cc/blog_with_author?author_id=24518f05-19a2-4748-b5ce-f936f5adc0d0)  发表于  2020-01-30 00:51

Tags：rust日报;

### Ferrugo : JVM 的 Rust 实现

目前还只是玩具项目，[详情](https://github.com/maekawatoshiki/ferrugo)

### Thirtyfour : Rust 版 selenium 库

用于自动化 web 测试，[详情](https://github.com/stevepryde/thirtyfour)

### 【博客】Rust 嵌入式项目——钢琴测量

此项目为了研究钢琴键与弹奏着的关系，给实验用的琴键安装了一组感应器，当机器手指用不用的力度按压琴键时，这些传感器会将琴键的行为进行视觉信息进行编码。最终的目的是把这些编码信息可以让人类识别并在电脑上演奏.  [项目详情](https://jitter.company/blog/2020/01/28/measuring-space-time-behaviours-of-piano-keys-with-rust/)

![image.png](https://i.loli.net/2020/01/30/L48oi9ZQqAYmE5M.png)

### Nushell 0.9.0

许多改进以及新的命令，[详情](https://www.nushell.sh/blog/2020/01/28/nushell-0_9_0.html)

----------

From 日报小组 @挺肥

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】2020-01-28 Security By Design, A Brief Introduction To Rust](https://rust.cc/article?id=12daf4f4-3689-45dc-851e-9271749a78d9)

[Mike Tang](https://rust.cc/blog_with_author?author_id=09e42b7c-c2bc-410a-9079-8ad0370d2603)  发表于  2020-01-28 22:53

Tags：rust

### Bitfields Forever: Why we need a C-compatible Rust Crate

Rust中关于位运算编程的一篇综合性的文章，推荐阅读。

[https://immunant.com/blog/2020/01/bitfields/](https://immunant.com/blog/2020/01/bitfields/)

### Security By Design, A Brief Introduction To Rust

从原理性的层面，讲Rust这个语言出身的环境，要解决的问题，以及从安全性出发进行的设计。推荐阅读。

[https://medium.com/tadaweb/security-by-design-a-brief-introduction-to-rust-378060e45038](https://medium.com/tadaweb/security-by-design-a-brief-introduction-to-rust-378060e45038)

### diffeq - 基础常微分方程解法器

Basic Ordinary Differential Equation solvers。

[https://github.com/mattsse/diffeq](https://github.com/mattsse/diffeq)

### Units of Measure in Rust with Refinement Types

Rust在测量单位上的Refinement Types模式的开发尝试。

To this day, F# is the only mainstream programming language which provides first class support to make sure that you will not accidentally confuse meters and feet, euros and dollars, but that you can still convert between watts·hours and joules.

作者用Rust尝试了一下，发现还挺好使。不但好使，还挺快乐！

[https://yoric.github.io/post/uom.rs/](https://yoric.github.io/post/uom.rs/)

--

From 日报小组 Mike

## [【Rust日报】2020-01-27](https://rust.cc/article?id=655e6f49-0566-4b12-a740-02a52273d04b)

[LacneQin](https://rust.cc/blog_with_author?author_id=f9ed70f9-be28-4b68-9b3b-2812c23a1ccc)  发表于  2020-01-27 22:32

Tags：rust

## QIP：Rust中的量子计算模拟

量子计算库利用图形构建来构建有效的量子电路仿真。对于借口模型的量子计算，Rust是一种很棒的语言，因为借位检查器与无克隆定理非常相似。

请参阅Github仓库的[examples目录](https://github.com/Renmusxd/RustQIP/tree/master/examples "examples目录")中的所有示例。

### 范例（CSWAP）

这是一个小电路的示例，其中两组寄存器在第三个寄存器之间交换。该电路非常小，只有三个操作加上一个测量值，因此，与之相比，样板看起来会很大，但是这种设置能够在电路变大时轻松、安全地构造电路。

```
use qip::*;

// Make a new circuit builder.
let mut b = OpBuilder::new();

// Make three registers of sizes 1, 3, 3 (7 qubits total).
let q = b.qubit();  // Same as b.register(1)?;
let ra = b.register(3)?;
let rb = b.register(3)?;

// We will want to feed in some inputs later, hang on to the handles
// so we don't need to actually remember any indices.
let a_handle = ra.handle();
let b_handle = rb.handle();

// Define circuit
// First apply an H to r
let q = b.hadamard(q);
// Then swap ra and rb, conditioned on q.
let (q, _, _) = b.cswap(q, ra, rb)?;
// Finally apply H to q again.
let q = b.hadamard(q);

// Add a measurement to the first qubit, save a reference so we can get the result later.
let (q, m_handle) = b.measure(q);

// Now q is the end result of the above circuit, and we can run the circuit by referencing it.

// Make an initial state: |0,000,001> (default value for registers not mentioned is 0).
let initial_state = [a_handle.make_init_from_index(0b000)?,
                     b_handle.make_init_from_index(0b001)?];
// Run circuit with a given precision.
let (_, measured) = run_local_with_init::<f64>(&q, &initial_state)?;

// Lookup the result of the measurement we performed using the handle, and the probability
// of getting that measurement.
let (result, p) = measured.get_measurement(&m_handle).unwrap();

// Print the measured result
println!("Measured: {:?} (with chance {:?})", result, p);

```

[Github仓库](https://github.com/Renmusxd/RustQIP "Github仓库")

[博客文章](https://docs.rs/qip/0.10.4/qip/ "博客文章")

## 用Rust编写的Trello CLI客户端

首先，在path上创建一个配置文件`~/.config/tro/config.toml`。设置`host`，`key`与`token`的值：

```
host = "https://api.trello.com"
key = "<MYKEY>"
token = "<MYTOKEN>"

```

该工具中的大多数子命令通过指定以下形式的一种或多种模式来工作：

```
<board> <list> <card>

```

模式是简单的正则表达式模式匹配。您也可以指定简单的模式，例如子字符串。

然后，Trello-rs尝试使用此过程查找您请求的对象：

-   如果该工具无法找到一个或多个指定项的匹配项，则它将： 显示适当的错误。
    
-   如果该工具设法为指定的每个项目找到唯一的匹配项，则它将成功： 显示您请求的对象。
    
-   如果一个或多个模式与多个可能的项目匹配，则该工具将失败： 检索您请求的对象，并尽力解释原因。
    

项目详情请访问[GitHub仓库](https://github.com/MichaelAquilina/trello-rs "GitHub仓库")。

## ureq HTTP客户端库的未来

该库提供一个方便的具有最小的依赖关系树和明显的API的请求库。

ureq来自以用户需求为中心（或者也许是“人体工程学”？）库的想法。[SuperAgent](https://visionmedia.github.io/superagent/ "SuperAgent")是简单易用的API的一大灵感。这并不是说reqwest不容易使用，reqwest还是可以的。但是，面对简易API和高性能API之间的折衷，它又向“简易”迈进了多远呢？

Hyper是reqwest的主要支撑，其主要目标是“ 为Rust提供快速、正确的 HTTP 实现”。这有时会将重要信息“泄漏”给用户。

具有明确的“用户至上”理念的库可能仍然是一个好的出发点。将用户输入视为“让它起作用”的作用，而不是强制正确性。

前往[GitHub](https://github.com/algesten/ureq/blob/future/THOUGHTS.md "GitHub")阅读文章原文。

## 部署容器运行时的Shim：交互式容器

容器只是孤立的Linux进程的幻想。每个进程都有一个`stdin`流从`stdout`  /  `stderr`流中读取输入数据，并将产生的输出打印到该输出中。容器也是如此。

从前面的文章中我们了解到，当我们创建一个容器时，其`stdout`和`stderr`会受到相应的运行时填充程序进程的控制。通常，这些流的内容将转发到容器日志文件。读者还可以注意到，容器的标准输入流只是默默地设置为`/dev/null`。

但是，如果我们想将一些数据发送到容器的`stdin`并在运行时将其`stdout`和/或`stderr`流返回该怎么办？至少在调试会话期间，这个工具就可能非常有用。

![](https://iximiuz.com/implementing-container-runtime-shim-3/interactive-containers-top-level-overview.png)

上面的图只是一个简化。由于Docker（或Kubernetes）分层设计，在流数据的方式上可能会有更多的中间组件，因此图上的容器管理器应被视为容器管理软件的相当高级的抽象。最接近图真实世界的设置将会是[crictl](https://github.com/kubernetes-sigs/cri-tools "crictl")（作为一个命令行客户端）与交互[CRI-O](https://github.com/cri-o/cri-o "CRI-O")  （作为CRI兼容的容器管理器）。

至少在以下情况下，我们可以发现在第三方应用的相同的交互式容器技术：

```
# Docker
docker run -i   # or --interactive
docker attach   # interactive by default
docker exec -i  # or --interactive

# Kubernetes
kubectl run --stdin     # or -i
kubectl run --attach
kubectl attach --stdin  # or -i
kubectl exec --stdin    # or -i

# ctr (containerd CLI)
ctr run  # interactive by default

# CLI for kubelet CRI
crictl attach --stdin

```

前往[作者个人博客](https://iximiuz.com/en/posts/implementing-container-runtime-shim-3/?utm_medium=reddit&utm_source=r_rust "博客")浏览更多信息。

----------

From 日报小组 @Lance

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】2020-01-25 Rust 2020 路线图，typed-builder，format!](https://rust.cc/article?id=7fc4d8b4-31ab-4d28-93cc-70f4ee8a7306)

[洋芋](https://rust.cc/blog_with_author?author_id=207704d2-4f5e-4219-a631-6ab4ab4d8929)  发表于  2020-01-25 21:51

Tags：rust, 日报

### Rust 2020 路线图

[Rust 2020 路线图](https://mp.weixin.qq.com/s/upqwhYyTlYPCXBEXjnGo7g)

### typed-builder v0.5.0

typed-builder，创建经过编译时验证的构建器，发布了v0.5.0版本。示例：

```
#[macro_use]
extern crate typed_builder;

#[derive(TypedBuilder)]
struct Foo {
    // Mandatory Field:
    x: i32,

    // #[builder(default)] without parameter - use the type's default
    // #[builder(setter(strip_option))] - wrap the setter argument with `Some(...)`
    #[builder(default, setter(strip_option))]
    y: Option<i32>,

    // Or you can set the default
    #[builder(default=20)]
    z: i32,
}

Foo::builder().x(1).y(2).z(3).build();
Foo::builder().z(1).x(2).y(3).build();

Foo::builder().x(1).build();

Foo::builder().build(); // missing x
Foo::builder().x(1).y(2).y(3); // y is specified twice

```

[crate地址](https://crates.io/crates/typed-builder)

### RtcSms

RtcSms，用来发送短信报告下一辆公交车到达前所剩余的时间。

[Github](https://github.com/gelendir/rtcsms)

### 宏format!

`format!`宏旨在使那些使用C语言的`printf/fprintf`函数或Python语言的`str.format`函数的用户提供熟悉格式化方法。

```
format!("Hello");                 // => "Hello"
format!("Hello, {}!", "world");   // => "Hello, world!"
format!("The number is {}", 1);   // => "The number is 1"
format!("{:?}", (3, 4));          // => "(3, 4)"
format!("{value}", value=4);      // => "4"
format!("{} {}", 1, 2);           // => "1 2"
format!("{:04}", 42);             // => "0042" with leading zeros

```

[使用文档](https://doc.rust-lang.org/std/fmt/#usage)

--

From 日报小组  [洋芋](https://rust.cc/blog_with_author?author_id=207704d2-4f5e-4219-a631-6ab4ab4d8929)

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust 日报】2020-01-22 Fourier: 最快的快速傅里叶变换](https://rust.cc/article?id=fd078819-9512-43e6-ae4e-252ae1e2af64)

[挺肥](https://rust.cc/blog_with_author?author_id=24518f05-19a2-4748-b5ce-f936f5adc0d0)  发表于  2020-01-23 00:34

Tags：rust日报;

### std.rs 直接访问 Rust 文档

有人买了 std.rs 这个域名，然后配置成直接跳转到 Rust 文档 https://doc.rust-lang.org/stable/std/ , 他说虽然 docs.rs/std 也可以做到，但是可以少打4个字母

### ptable : 完整的元素周期表 crate

一个 Rust 版的完整元素周期表，包括原子数、符号、名称、电子数等等，[详情](https://crates.io/crates/ptable)

### Fourier: 最快的快速傅里叶变换

作者觉得  [FFTW](http://www.fftw.org/)  的协议“传染性”太高了，所以给出一个Rust版的竞争产品  [Fourier](https://github.com/calebzulawski/fourier)

----------

From 日报小组 @挺肥

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-21 rweb: 又一个Rust的 web 服务器框架](https://rust.cc/article?id=eb56896a-0bdf-4165-9475-7fee6a67accb)

[joshsulin](https://rust.cc/blog_with_author?author_id=bbc523d4-9fd5-47a7-9d04-c61eda0d97e7)  发表于  2020-01-21 23:51

Tags：rust, 日报

### rweb: 又一个Rust的 web 服务器框架

注意: 这不是一个稳定的版本.

Rweb 是一个基于 warp 的小型 http 框架。 它快速、安全(由于变形和超级)、易于使用和可扩展。

与现有的框架相比，这样做有什么好处，或者说目标是什么？

与warp相比，它更容易使用，也更容易扩展。

与 activex-web 相比，它使用更简单，编译时间更短。

与 rocket 相比，它工作稳定，并支持异步 / 等待。

前往[GitHub](https://github.com/kdy1/rweb)仓库详细了解项目。

### 为什么开发者会时不时的想到使用Rust

我的日常工作是使用Java，具有GC和一个大型运行时的便利设施。 如果你能负担得起GC带来的停顿，就使用 GC。 如果性能不是问题，我有时甚至编写 python。 为什么开发者会时不时的想到使用Rust？

详情请阅读这篇文章:  [https://llogiq.github.io/2020/01/10/rustvsgc.html](https://llogiq.github.io/2020/01/10/rustvsgc.html)

### Rust准备参与Unreal Engine开发

作者最近完成了将 Rust 代码集成到 Unreal 引擎的概念验证。

细节:  [https://ejmahler.github.io/rust_in_unreal/](https://ejmahler.github.io/rust_in_unreal/)

----------

From 日报小组 @joshsulin

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)

## [【Rust日报】 2020-01-20 通过全局分配器对不安全的Rust代码进行杀毒](https://rust.cc/article?id=c4bd43bb-36ad-4374-ace1-2f3085f341fb)

[LacneQin](https://rust.cc/blog_with_author?author_id=f9ed70f9-be28-4b68-9b3b-2812c23a1ccc)  发表于  2020-01-20 23:18

Tags：rust

## 通过全局分配器对不安全的Rust代码进行杀毒

Checkers是Rust的简单分配清理工具。它通过全局分配器插入，可以在集成测试过程中检查不安全的Rust。由于它是通过全局分配器插入的，因此它不需要任何其他依赖关系，并且可以在所有平台上使用，但它可以验证的内容受到更多限制。

它可以检查以下内容：

-   双重释放。
-   内存泄漏。
-   释放未分配的区域。
-   仅释放分配的部分区域。
-   释放布局不匹配的区域。
-   基础分配器产生的区域遵守所请求的布局。即大小和对齐方式。
-   有关内存使用的详细信息。
-   其他用户定义的条件（请参阅[test](https://github.com/udoprog/checkers/blob/master/tests/leaky_tests.rs "test")）。

目前尚未完成的功能：

-   测试多线程代码。（由于分配器是全局的，因此很难为每个测试用例确定状态范围。）
-   检测越界访问。

前往[GitHub仓库](https://github.com/udoprog/checkers "GitHub仓库")详细了解项目。

## ttyplot-rs：绘制从stdin到tty终端的流数据

ttyplot-rs能够绘制从stdin到tty终端的流数据。对于显示从串行端口或长期运行的管道传输的数据很有用。

![](https://github.com/mogenson/ttyplot-rs/raw/master/demo.svg?sanitize=true)

将流程中的数据传输到中`ttyplot-rs`。按ctrl+c退出。

项目详细开源代码前往[GitHub仓库](https://github.com/mogenson/ttyplot-rs "GitHub仓库")查看。

## 在Rust中编写操作系统：分配器设计

[此篇文章](https://os.phil-opp.com/allocator-designs/ "此篇文章")解释了如何从头开始实现堆分配器。它提出并讨论了不同的分配器设计，包括凹凸分配，链表分配和固定大小的块分配。对于这三种设计中的每一种，我们将创建一个可用于内核的基本实现。

分配器的职责是管理可用的堆内存。它需要在`alloc`调用时返回未使用的内存，并跟踪释放的内存，`dealloc`以便再次使用它。最重要的是，它绝不能分发已经在其他地方使用的内存，因为这会导致不确定的行为。

除了正确性之外，还有许多次要设计目标。例如，分配器应有效地利用可用内存并使碎片减少。此外，它对于并发应用程序应能很好地工作，并可以扩展到任意数量的处理器。为了获得最佳性能，它甚至可以针对CPU缓存优化内存布局，以提高缓存位置并避免错误共享。

这些要求会使好的分配器非常复杂。例如，jemalloc具有超过30.000行代码。这种复杂性在内核代码中通常是不希望的，因为单个错误会导致严重的安全漏洞。幸运的是，与用户空间代码相比，内核代码的分配模式通常要简单得多，因此相对简单的分配器设计通常就足够了。

前往[博客文档](https://os.phil-opp.com/allocator-designs/ "博客文档")了解更多。

----------

From 日报小组 @Lance

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-18 Actix Web，Lemmy v0.6.0，panda-api](https://rust.cc/article?id=31febfbf-11b3-4c19-ad93-d429b8e5322d)

[洋芋](https://rust.cc/blog_with_author?author_id=207704d2-4f5e-4219-a631-6ab4ab4d8929)  发表于  2020-01-18 22:28

Tags：rust, 日报

### 如何看待Actix Web事件？

小编整理了Actix作者的原文，及Rust社区对此事件的一些评论文章，供大家借鉴。

-   [Actix project postmortem](https://github.com/actix/actix-web)，Actix作者的原文
-   [A sad day for Rust](https://words.steveklabnik.com/a-sad-day-for-rust)
-   [The Soundness Pledge](https://raphlinus.github.io/rust/2020/01/18/soundness-pledge.html)
-   [世界的本质就是Unsafe，美好需要我们共同创造](https://zhuanlan.zhihu.com/p/103353305)
-   [暴走的程序员](https://mp.weixin.qq.com/s/gjWDWO2XqRZ8mhpHqc0U5g)

### Lemmy v0.6.0

Lemmy，是一个基于actix-web 2.0开发的开源reddit项目。

[Github](https://github.com/dessalines/lemmy)

[Lemmy](https://dev.lemmy.ml/)

### panda-api

panda-api，是一个基于actix-web 2.0开发的接口文档管理工具，可以在接口文档定义好的时候，直接为前端提供开发接口服务，不需要等待后端开发。

[Github](https://github.com/arlicle/panda-api)

### verona

verona，微软的研究性编程语言，以实现并发所有权。

[Github](https://github.com/microsoft/verona)

--

From 日报小组  [洋芋](https://rust.cc/blog_with_author?author_id=207704d2-4f5e-4219-a631-6ab4ab4d8929)

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-17 Actix 作者受不了了 直接刪庫庫](https://rust.cc/article?id=c144ca7f-d003-4cad-b301-accf150dd641)

[damody](https://rust.cc/blog_with_author?author_id=55ad9d89-6929-4a73-baa5-cf0a99a9abad)  发表于  2020-01-17 20:38

Tags：rust

### Actix 作者受不了了 直接刪庫庫

https://gitter.im/actix/actix

大家快去給作者關心跟鼓勵，讓大家知道還是有很多人支持他的

拜託拜託

[Read more](https://github.com/actix/actix-web)

### 測試了一些 HTTP client 就是這篇文他Actix作者不爽了

目前爆文 600 多

[Read more](https://medium.com/@shnatsel/smoke-testing-rust-http-clients-b8f2ee5db4e6)

### warp v0.2

新的web server framework

目前還很新 有興趣可以關注一下

[Read more](https://seanmonstar.com/post/190293882502/warp-v02)

### 一個更好地支持模糊測試的方式

cargo fuzzy

之前有介紹過一個可以更好的測試怎樣的輸入會讓你的程式當掉的小工具

現在有更新了

[Read more](https://fitzgeraldnick.com/2020/01/16/better-support-for-fuzzing-structured-inputs-in-rust.html)

### TerminusDB

只能用 HTTP API 溝通的DB

[Read more](https://terminusdb.com/)

[Read more](https://github.com/terminusdb/terminus-store)

### Rust裡怎麼使用建造者模式 builder pattern

[Read more](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/builder-pattern/landing.html)

### Deadpool 0.5

一個非同步的連接池 支援

postgres, lapin(AMQP), redis

[Read more](https://crates.io/crates/deadpool/0.5.0)

----------

From 日报小组 @Damody

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-1-16 用 Rust 来诠释 Epoll, Kqueue 和 IOCP](https://rust.cc/article?id=e066c8d9-6da8-4590-9797-252833408272)

[Jancd](https://rust.cc/blog_with_author?author_id=d32af902-7816-4c8c-838d-60351791516d)  发表于  2020-01-16 23:37

Tags：rust,news

### 用 Rust 来诠释 Epoll, Kqueue 和 IOCP

这其实是一本书，旨在说明 Epoll，Kqueue 和 IOCP 的工作原理，我们可以将其用于高效率、高性能的 I/O。其中一些实现将会使用 rust，原文地址：https://cfsamsonbooks.gitbook.io/epoll-kqueue-iocp-explained/

扩展阅读：[Green Threads Explained in 200 Lines of Rust](https://cfsamson.gitbook.io/green-threads-explained-in-200-lines-of-rust/)

reddit 上参与讨论：https://www.reddit.com/r/rust/comments/ephm4t/epoll_kqueue_and_iocp_explained_with_rust/

### Deadpool

`Deadpool`  是一个死的简单异步池，用于任何类型的连接和对象。

#### Example

```
use async_trait::async_trait;

#[derive(Debug)]
enum Error { Fail }

struct Computer {}
struct Manager {}
type Pool = deadpool::managed::Pool<Computer, Error>;

impl Computer {
    async fn get_answer(&self) -> i32 {
        42
    }
}

#[async_trait]
impl deadpool::managed::Manager<Computer, Error> for Manager {
    async fn create(&self) -> Result<Computer, Error> {
        Ok(Computer {})
    }
    async fn recycle(&self, conn: &mut Computer) -> deadpool::managed::RecycleResult<Error> {
        Ok(())
    }
}

#[tokio::main]
async fn main() {
    let mgr = Manager {};
    let pool = Pool::new(mgr, 16);
    let mut conn = pool.get().await.unwrap();
    let answer = conn.get_answer().await;
    assert_eq!(answer, 42);
}

```

这个库还提供：Database connection pools，GitHub 地址：https://github.com/bikeshedder/deadpool

### factori

`Factori`  is a testing factory library inspired by Ruby's FactoryBot.

Example

`Factori`  provides two macros: factori!, which defines a factory for a type, and  `create!`  which instantiates it:

```
#[macro_use]
extern crate factori;

pub struct Vehicle {
    number_wheels: u8,
    electric: bool,
}

factori!(Vehicle, {
    default {
        number_wheels = 4,
        electric = false,
    }

    mixin bike {
        number_wheels = 2,
    }
});

fn main() {
    let default = create!(Vehicle);
    assert_eq!(default.number_wheels, 4);
    assert_eq!(default.electric, false);

    // Its type is Vehicle, nothing fancy:
    let vehicle: Vehicle = default;

    let three_wheels = create!(Vehicle, number_wheels: 3);
    assert_eq!(three_wheels.number_wheels, 3);

    let electric_bike = create!(Vehicle, :bike, electric: true);
    assert_eq!(electric_bike.number_wheels, 2);
    assert_eq!(electric_bike.electric, true);
}

```

----------

From 日报小组 @Jancd

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [2020-01-15 Dashmap v3](https://rust.cc/article?id=c2710bdf-4132-4797-8af7-f678358b0e3c)

[挺肥](https://rust.cc/blog_with_author?author_id=24518f05-19a2-4748-b5ce-f936f5adc0d0)  发表于  2020-01-17 23:30

Tags：rust日报;

### 【Rustacean 播客】Rust 1.40 有新的内容？

["The Rustacean Station Podcast"](https://rustacean-station.org/)  是一个围绕 Rust 内容音频项目，这一期内容带来的是 Rust 1.40 的解读，[详情](https://rustacean-station.org/episode/010-rust-1.40.0/).

### Dashmap v3

[Dashmap](https://github.com/xacrimon/dashmap)  是 HashMap 的快速并发版，与第一版相比有以下改进:

-   Better iterator API
-   Entry API which tries to mimick std::collections::HashMap
-   Low level raw shard access support
-   Massively improved performance (see below)
-   Serde support
-   Common iterator traits implemented
-   Rustified and cleaner API
-   More relaxed trait bounds

### Rust 像素风 RPG 游戏 Veloren 第 50 周

Veloren 的系列博客  [“TWiV”](https://veloren.net/devblog-50/)，过去一周添加了 *scrolling combat * 文本效果，以及对框架的优化.  [详情](https://veloren.net/devblog-50/)

![image.png](https://i.loli.net/2020/01/17/NoTclFCGYmR67WL.png)

----------

From 日报小组 @挺肥

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-14](https://rust.cc/article?id=205fefe1-8bad-4139-951d-b89e4f9bc0ca)

[joshsulin](https://rust.cc/blog_with_author?author_id=bbc523d4-9fd5-47a7-9d04-c61eda0d97e7)  发表于  2020-01-14 23:42

Tags：rust, 日报

### ASM工作组已提交“关于提供稳定的内联汇编”的第一稿RFC

内联汇编（Inline assembly）：目前，对内联汇编方面来讲，Rust 非常接近于 LLVM，这是一种不同于 gcc 的格式，因此，我们必须解决这种不匹配的问题。我们期待将来有一天，Rust 能够为内联汇编提供稳定的支持。

了解更多, 请阅读。  [https://www.reddit.com/r/rust/comments/eo9pks/the_asm_working_group_has_submitted_their_first/](https://www.reddit.com/r/rust/comments/eo9pks/the_asm_working_group_has_submitted_their_first/)

### 如何你想深入探讨 ELF、x86指令、内存映射、gdb、动态加载程序等知识, 以下内容对你有用.

[Linux 可执行文件是什么？](https://fasterthanli.me/blog/2020/whats-in-a-linux-executable/)

[不使用 exec 运行可执行文件](https://fasterthanli.me/blog/2020/running-an-executable-without-exec/)

......

有兴趣的, 可以关注作者.

### 小工具包 parse_int 发布0.3.0 版本

将字符串中带有常用前缀的整数值 解析成 数字.

```
use parse_int::parse;
 
// decimal
let d = parse::<usize>("42")?;
assert_eq!(42, d);
 
// hex
let d = parse::<isize>("0x42")?;
assert_eq!(66, d);
 
// octal explicit
let d = parse::<u8>("0o42")?;
assert_eq!(34, d);
 
#[cfg(feature = "implicit-octal")]
{
    let d = parse::<i8>("042")?;
    assert_eq!(34, d);
}
 
// binary
let d = parse::<u16>("0b0110")?;
assert_eq!(6, d);

```

----------

From 日报小组 @joshsulin

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【rust日报】 2020-01-13 用rust编写的最小系统兼容服务管理器 : rustysd 更新](https://rust.cc/article?id=e3c57e85-5470-4728-ab54-2a1220fdb31e)

[LacneQin](https://rust.cc/blog_with_author?author_id=f9ed70f9-be28-4b68-9b3b-2812c23a1ccc)  发表于  2020-01-13 22:14

Tags：rust

## 用rust编写的最小系统兼容服务管理器 : rustysd 更新

Rustysd是一个服务管理器，复制系统行为一部分配置。它着重于服务管理器的核心功能。因此，rustysd提供的功能数量很少。如果使用musl和strip'ed构建二进制文件，则二进制文件可能会很小，但通常rust会生成相对较大的二进制文件。

这意味着只要服务知知悉rustysd可以读取systemd单元文件（的一部分）并像运行systemd一样运行它们。由于rustysd不需要是PID1，因此它可以为不使用systemd的Linux发行版以及FreeBSD提供此功能（现在还未经测试其他BSD）。另外，它可以在docker中用作PID1，因此您可以运行需要由systemd在容器中运行的服务。

rustysd的下一个目标是：

-   成为一个很好的工具
-   成为rustysd在VM中充当init系统
-   开发一个测试套件以能够捕获回归/错误的功能

项目仓库地址：[https://github.com/KillingSpark/rustysd/tree/v0.1.0](https://github.com/KillingSpark/rustysd/tree/v0.1.0 "https://github.com/KillingSpark/rustysd/tree/v0.1.0")

## 用于Rust的Cranelift后端

目前项目正在进行中的工作是为在Cranelift 上构建的Rust创建[后端](https://github.com/bjorn3/rustc_codegen_cranelift "后端")，这有望大大减少调试编译耗时。

除了Rustc测试套件中的57个测试之外，其他所有测试都已通过，并取得惊人的进步。

几乎所有这些工作都是由[bjorn3](https://github.com/bjorn3 "bjorn3")一手完成的。

详情前往项目[GitHub仓库](https://github.com/bjorn3/rustc_codegen_cranelift "GitHub仓库")查看。

## Rust数据库连接性（RDBC）更新

同时支持面向行和面向列的数据实际上非常简单。RDBC API应该支持将成批数据提取到实现`RowSet`特征的行集中，从而提供面向行和面向列的访问。

因为列中的所有值都具有相同的数据类型，所以我们可以使用类型安全的特征来访问这些值。

```
pub trait ColumnAccessor<T> {
    fn get(&self, i: u64) -> Result<Option<T>>;
}

```

行通常包含混合类型，因此这里我们将在方法而不是特征上指定泛型。

```
pub trait RowAccessor {
    fn get<T>(&self, i: u64) -> Result<Option<T>> where Self: Sized;
}

```

`RowSet`特征示例

```
pub trait RowSet {
    /// get meta data about this row set
    fn meta_data(&self) -> Result<Box<dyn RowSetMetaData>>;
    /// Get an accessor for a row containing mixed types
    fn get_row(&self, i: u64) -> Result<Box<dyn RowAccessor>>;
    /// Get a column as a type-safe accessor
    fn get_column<T>(&self, i: u64) -> Result<Box<dyn ColumnAccessor<T>>>;
}

```

支持的数据`RowSet`将是面向行的或面向列的,始终可以同时以行和列的形式访问数据，但是其中一种方法肯定比另一种方法更有效。对于大多数用例来说这可能并不太重要，但是在某些用例中却很重要，因此元数据应公开有关本机格式的信息。

```
pub trait RowSetMetaData {
    fn row_oriented(&self) -> bool;
    fn num_rows(&self) -> u64;
    fn num_columns(&self) -> u64;
    fn column_name(&self, i: u64) -> String;
    fn column_type(&self, i: u64) -> DataType;
}

```

RDBC只是底层数据访问和查询执行API。它不打算取代像Diesel这样的ORM，尽管很快将有可能使用RDBC代替Diesel构建应用程序。

前往[博客](https://andygrove.io/2020/01/rust-database-connectivity-rdbc/ "博客")了解有关RDBC连接与RDBC迁移至东京的消息。

## git-poly：用rust编写的极简multi repo工具

帮助越跨50多个git仓库进行开发更加轻松的工具。这是一个简单、轻巧的工具，可并行处理许多git repos。

以下项目与本项目处于同一位置：

-   git repo
    
-   git subtree
    
-   git slave
    
-   git submodule
    

前往[Gitlab](https://luke_titley.gitlab.io/git-poly/ "Gitlab")了解项目详情。

----------

From 日报小组 @Lance

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-12 Rust编译出的可执行文件体积优化方法](https://rust.cc/article?id=5ee8c5f8-3502-42c7-a93e-980b669fd924)

[makeco](https://rust.cc/blog_with_author?author_id=17589eca-5f9f-4542-9938-585c74ef6b39)  发表于  2020-01-12 22:16

Tags：rust

### 为什么Rust编译出的可执行文件那么大？

#rust #exe

为什么相同应用用Rust编译出的可执行文件比C编译出的要大？下面这篇文章详细阐述了原因，并提出了多重可行的方案，帮你减小可执行文件的体积，这几种方法是：

-   使用`--release`模式进行编译
-   在发布之前，开启LTO压缩二进制文件体积
-   如果你的应用不是内存密集型，使用系统分配器（需要nightly)
-   你可以开启编译优化等级s/z
-   还有一点建议对小的可执行文件效果不明显，但是你可以尝试UPX和其他可执行文件压缩，如果你的应用很大的话

[Read More](https://lifthrasiir.github.io/rustlog/why-is-a-rust-executable-large.html?nsukey=0pCaOk1Jqd5C4VixWGd5tgKPJdT%2BZ0JBecpENw8OxAfDUNwoEn9uLbfSVdGlOi5PIs2B9IhRzfMsCx8zvneeOgjek%2Bkx4%2FR7f9RckVFUSUyrPgIo7Hwke%2BrRae6LN897PVrUF1IRCIHCN1m9cwhpVMxMhGERUJ8oN1f4W4%2BcI3AJ9yQ8zuVvWcftwoMCvVQJV9m%2FglpOiosgLKu0UBEfBg%3D%3D)

### 不在微信也能运行小程序？小程序硬件框架正式上线！

#rust #mini

小程序从诞生到现在，我们经常收到这样的询问：小程序能脱离微信在其他终端上运行么？

例如，在跑步机上玩跳一跳；查看冰箱库存时顺手在显示屏使用生鲜网购小程序；酒店智能固话使用周边服务小程序，叫个送餐，定个电影票；甚至照个镜子都能用小程序。

答案是，可以！1月9日，微信小程序硬件框架正式开放，小程序可以脱离微信在不同终端上运行，各种硬件上都能跑小程序啦。

运行小程序硬件框架的设备要求

■ 最低配置

四核1.5GHz CPU

内存1GB RAM+4GB ROM

安卓5.0及以上

■ 建议配置

四核2GHz CPU

内存2GB RAM+8GB ROM

安卓7.1及以上

[Read More](https://mp.weixin.qq.com/s/HZ5ixmfKc_o5oyvXc0JQKw)

----------

From 日报小组 格朗

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc 论坛: 支持 rss](https://rust.cc/)
-   [Rust Force: 支持 rss](https://rustforce.net/)
-   [微信公众号：Rust 语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-11 postgres-query, 新的分词器库tokenizers](https://rust.cc/article?id=ea1759ae-b1e5-411b-affa-9676a7bc07be)

[洋芋](https://rust.cc/blog_with_author?author_id=207704d2-4f5e-4219-a631-6ab4ab4d8929)  发表于  2020-01-11 22:54

Tags：rust, 日报

### postgres-query

这个crate提供了方便的宏和trait，可帮助编写SQL查询并将其结果收集到静态类型的结构中。

示例代码：

```
// Connect to the database
let client: Client = connect(/* ... */);

// Construct the query
let query = query!(
    "SELECT name, age FROM people WHERE age >= $min_age",
    min_age = 18
);

// Define the structure of the data returned from the query
#[derive(FromSqlRow)]
struct Person {
    age: i32,
    name: String,
}

// Execute the query
let people: Vec<Person> = query.fetch(&client).await?;

// Use the results
for person in people {
    println!("{} is {} years young", person.name, person.age);
}

```

[Github](https://github.com/nolanderc/rust-postgres-query)

### 新的分词器库tokenizers

分词器的核心是用Rust编写的。提供当今最常用的分词器的实现，重点是性能和多功能性。

示例代码

```
use tokenizers::tokenizer::{Result, Tokenizer, EncodeInput};
use tokenizers::models::bpe::BPE;

fn main() -> Result<()> {
	let bpe_builder = BPE::from_files("./path/to/vocab.json", "./path/to/merges.txt")?;
	let bpe = bpe_builder
		.dropout(0.1)
		.unk_token("[UNK]".into())
		.build()?;

	let mut tokenizer = Tokenizer::new(Box::new(bpe));

	let encoding = tokenizer.encode(EncodeInput::Single("Hey there!".into()))?;
	println!("{:?}", encoding.get_tokens());

	Ok(())
}

```

[Github](https://github.com/huggingface/tokenizers/tree/master/tokenizers)

### 一个PR，在Rust 1.40中删除对proc-macro-hack的依赖

使用Rust 1.40时，类似函数的宏可以生成macro_rules!，因此，删除对`proc-macro-hack`的依赖非常容易。

[PR信息](https://github.com/RustPython/RustPython/pull/1669)

--

From 日报小组  [洋芋](https://rust.cc/blog_with_author?author_id=207704d2-4f5e-4219-a631-6ab4ab4d8929)

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-10 track_caller 錯誤處理大突破](https://rust.cc/article?id=dcee075c-0da9-499f-a93a-e07679f633ca)

[damody](https://rust.cc/blog_with_author?author_id=55ad9d89-6929-4a73-baa5-cf0a99a9abad)  发表于  2020-01-11 14:43

Tags：rust

### 更新我們的Rust Boilerplate server 使用 GraphQL (Async and Actix-web 2)

做了以下的更新

use async/await

use actix-web version 2

use anyhow + thiserror in place of failure

structopt

[Read more](https://github.com/clifinger/canduma)

### sntpc Rust SNTP 客戶端可以從 NTP servers 拿 timestamp

[Read more](https://github.com/vpetrigo/sntpc)

### 有人成功的驗證了rust可以跟unreal遊戲引擎整合

[Read more](https://ejmahler.github.io/rust_in_unreal/)

### Rust基礎建設

目標1：明確Rust作為獨立項目的地位

有些公司想要商業投資Rust但因為 Mozilla 持有這個項目而卻步。

Rust應該要有自己的獨立基金會。

目標2：減輕一些實際困難

儘管Rust項目擁有自己的治理系統，但它從未擁有自己獨特的法人實體。該角色一直由Mozilla扮演。例如，Mozilla擁有Rust商標，而Mozilla是crates.io等服務的合法運營商。

作者希望Rust獨立出來，Mozilla成為其中一個投資者而不是持有者。

但作者又不希望Rust基金會不應僱用全職開發人員

造成這種情況的原因有很多，但最大的原因就是價格太貴了。

為該工作量提供資金將需要大量預算，這將需要大量籌款。

[Read more](http://smallcultfollowing.com/babysteps/blog/2020/01/09/towards-a-rust-foundation/)

### 有人使用了Rust實作了BLAKE3

BLAKE3 是一種 cryptographic hash

類似 MD5 SHA1 等  [Read more](https://github.com/BLAKE3-team/BLAKE3-specs)

### Library team 從 IRC 移動到 Zulip

https://zulipchat.com/ 是一個類似slack的軟件。

[Read more](https://internals.rust-lang.org/t/the-library-team-is-moving-from-irc-to-zulip/11598)

### Way Cooler驗屍報告

作者做了一個開源專案但是死的很慘

他用這篇文章做一個記錄

我最初的計劃是用C語言編寫它，因為這似乎是複合語言的流行語言（當時只有Gnome，KDE，Weston，E，Orbment和Sway的早期版本）。 Snirk 說服我研究Rust。 他對它的強大可靠性保證很感興趣（他的研究領域是編譯器和語言設計）。 它獨特的內存管理方法吸引了我，在嘗試了該語言之後，我們開始研究Way Cooler。

當時他們在 libweston, swc, wlc 中做選擇

最後他們選了 wlc

更清楚的是如何包裝Rust所使用的API。它具有非常簡單的內存模型和非常小的API界面。

我們試了範圍，並開始包裝wlc庫，以便能在Rust中使用它。我們設定了一個短期目標，用約400行程式碼從C轉換為慣用的Rust。

但是，在此階段犯了兩個錯誤，乍看之下似乎是矛盾的：我們跳入包裝wlc的速度太快了，但與此同時卻花了太多時間。

封裝給Rust使用的C庫並不是一件容易的事，如果我們知道這個問題，可能就不會這樣做了。

後面想支援Lua又想支援Nodejs然後庫的API又大改在3.X=>4.X 做了不相容更新。

然後我們都是自學很少跟人合作，在閱讀他人的代碼上異常困難。

後面又因為 Rust 實作樹資料結構不好作，搞了很久。

太長了，大家有興趣可以看原文

[Read more](http://way-cooler.org/blog/2020/01/09/way-cooler-post-mortem.html)

### Arc 怎麼在Rust運作的呢？

就是原子計數器加指標

[Read more](https://medium.com/@CookieReviews/how-arc-works-in-rust-b06192acd0a6)

### Terminal 0.2.0

類似 termion, crossterm, ncurses, pancurses 的

命令列 UI library

[Read more](https://github.com/crossterm-rs/terminal)

### track_caller 錯誤處理大突破

`Option::{expect,unwrap}`  跟  `Result::{expect, expect_err, unwrap, unwrap_err}`  有  `#[track_caller]`  了

從

```
thread 'main' panicked at 'called `Option::unwrap()` on a `None` value', /rustc/da3629b05f8f1b425a738bfe9fe9aedd47c5417a/src/libcore/macros/mod.rs:16:40
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace.

```

變成

```
thread 'main' panicked at 'called `Option::unwrap()` on a `None` value', src/main.rs:3:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace.

```

[Read more](https://github.com/rust-lang/rust/pull/67887)

### duckscript

用rust實作的腳本語言

[Read more](https://github.com/sagiegurari/duckscript)

### 為什麼要用Rust？我們有GC啊

Rust有速度上的優勢，並發上的自動檢查。

但跟Java一樣都開發的不快，Python是開發速度的首選。

不過Java有更好的IDE支援，生態系統與社群更強大，

對老闆來說更安心。

[Read more](https://llogiq.github.io/2020/01/10/rustvsgc.html)


## [【Rust日报】2020-01-09 在 Rust 实现的内核中实现协作调度器](https://rust.cc/article?id=c4e6078b-ac47-410a-bdfc-a448a1fc8563)

[Jancd](https://rust.cc/blog_with_author?author_id=d32af902-7816-4c8c-838d-60351791516d)  发表于  2020-01-09 22:19

Tags：rust,news

### 在 Rust 实现的内核中实现协作调度器

背景：OxidizedOS 是用 Rust 编写的多核 x86-64 内核。有关更多信息，请参见简介：https://ryan-jacobs1.github.io/2019/12/30/an-introduction.html。

在本文中，我们将实现协作式多任务处理。为简单起见，我们将使用循环调度器，其中每个线程将以 FIFO 顺序运行。更多请看原文：https://ryan-jacobs1.github.io/2020/01/06/scheduler.html

reddit 参与讨论：https://www.reddit.com/r/rust/comments/elzh3x/blog_post_implementing_a_cooperative_scheduler_in/

### canduma

该仓库包含样板 Rust 代码，用于通过 JWT 启动并快速运行 GraphQL 原型。

它使用  [actix-web](https://actix.rs/)，[Juniper](https://graphql-rust.github.io/juniper/current/)，[Diesel](https://diesel.rs/)  和  [jsonwebtoken](https://docs.rs/jsonwebtoken)。

Benchmarks with insert into PostgreSQL:

```
▶ ./bombardier -c 125 -n 10000000 http://localhost:3000/graphql -k -f body --method=POST -H "Content-Type: application/json" -s
Bombarding http://localhost:3000/graphql with 10000000 request(s) using 125 connection(s)

10000000 / 10000000 [===========================================================================] 100.00% 28777/s 5m47s
Done!
Statistics        Avg      Stdev        Max
  Reqs/sec     28788.66    2183.47   34605.95
  Latency        4.32ms   543.07us   110.95ms
  HTTP codes:
    1xx - 0, 2xx - 10000000, 3xx - 0, 4xx - 0, 5xx - 0
    others - 0
  Throughput:    20.75MB/s

```

项目地址：https://github.com/clifinger/canduma

reddit 参与讨论：https://www.reddit.com/r/rust/comments/em8bx9/update_of_our_rust_boilerplate_server_with/

### RustZone: Writing Trusted Applications in Rust (Black Hat Asia 2018)

演讲中将探索使用 Rust 语言编写受信任的应用程序。 Rust 允许开发人员编写系统级代码，但提供安全性功能，包括内存安全性，类型安全性和错误处理。这些是开发受信任的应用程序的理想功能。油管地址：https://www.youtube.com/watch?v=5fxPuOrlE2I&feature=youtu.be

### Rust Belt Rust 2019 的视频已发布

Rust Belt Rust（http://www.rust-belt-rust.com/）是在美国 Rust Belt 地区举行的关于 Rust 编程语言的会议。 Rust Belt Rust 2019 于 10 月 18 日星期五和 10 月 19 日星期六在俄亥俄州代顿举行。再次感谢我们所有的与会者，演讲者和赞助商！油管地址：https://t.co/DTFoG1dDyr?amp=1

### 编写 Web server 及其以外的技巧

油管地址：https://youtu.be/ZDy71QtAQgs?list=PLgC1L0fKd7UkVwjVlOySfMnn80Qs5TOLb

----------

From 日报小组 @Jancd

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [2020-01-08 Nushell 0.8 发布](https://rust.cc/article?id=01c3324a-8f15-4ae3-8dc1-8f9a10f5c5a7)

[挺肥](https://rust.cc/blog_with_author?author_id=24518f05-19a2-4748-b5ce-f936f5adc0d0)  发表于  2020-01-08 20:30

Tags：rust日报;

### Elastic 官方发布 Elasticsearch Rust 客户端

ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。是目前十分流行的企业级搜索引擎.

[详情](https://github.com/elastic/elasticsearch-rs)

### Nushell 0.8 发布

(简称Nu)是一种新型的shell，它采用现代的结构化方法来处理命令行。它与来自文件系统、操作系统和越来越多的文件格式的数据无缝地工作，使构建强大的命令行管道变得容易.

此次更新，优化以及添加了一些命令.  [详情](https://www.nushell.sh/blog/2020/01/07/nushell-0_8_0.html)

### 把 Quake 3 翻译成 Rust 版

有人把游戏 Quake 3 编译为了 Rust 版，[详情](https://immunant.com/blog/2020/01/quake3/)

![image.png](https://i.loli.net/2020/01/08/UjkOi1IygVApMFG.png)

----------

From 日报小组 @挺肥

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-07](https://rust.cc/article?id=ea6bfd06-c374-4cb8-8408-3a9e542c4a02)

[joshsulin](https://rust.cc/blog_with_author?author_id=bbc523d4-9fd5-47a7-9d04-c61eda0d97e7)  发表于  2020-01-08 00:54

Tags：rust, 日报

### Yew发布 v0.11

前往[GitHub](https://github.com/yewstack/yew)了解更多。

### MuOxi MUD/MU* Rustic 游戏引擎 v0.1.0

前往[GitHub](https://github.com/duysqubix/MuOxi)了解更多。

### 欢迎讨论, 哪些应用更适合用Rust来开发?

国外一名开发者, 提出了这个问题? 其实我与这名开发者有一样的疑问和迷茫, 在哪些应用程序中用Rust编写更有意义？我确实想学习该语言，但是很难找到一个比其他选择更有意义的项目.

[欢迎大家加入讨论](https://rust.cc/reddit.com/r/rust/comments/el9p2x/what_applications_are_better_written_in_rust_than/)

----------

From 日报小组 @joshsulin

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-06 tomaka / redshirt：在0环中运行的WASM二进制的操作系统原型](https://rust.cc/article?id=2159ca11-c190-47d9-9660-c5562fb733f6)

[LacneQin](https://rust.cc/blog_with_author?author_id=f9ed70f9-be28-4b68-9b3b-2812c23a1ccc)  发表于  2020-01-07 11:38

Tags：Rust

## tomaka / redshirt：在0环中运行的WASM二进制的操作系统原型

redshirt操作系统是建立某种形式与操作系统类似环境的实验，其中的可执行文件都在WASM并从类似IPFS的去中心化网络被加载。

此存储库中有两种二进制文件：

-   “托管内核”是执行WASM程序并使用主机操作系统的常规二进制文件。
-   独立式内核是兼容multiboot2的内核，可以与GRUB2或任何兼容的引导程序一起加载。

对于托管内核：

```
# You need the WASI target installed:
rustup target add wasm32-wasi

# Then:
cargo run

```

对于独立内核：

```
rustup target add wasm32-wasi

# From the root directory of this repository (where the `arm-freestanding.json` file is located):
RUST_TARGET_PATH=`pwd` cargo +nightly build -Z build-std=core,alloc --target arm-freestanding --package redshirt-standalone-kernel

# You now have a `target/arm-freestanding/debug/redshirt-standalone-kernel`.
# It can be loaded directly by QEMU:
qemu-system-arm -M raspi2 -m 2048 -serial stdio -kernel ./target/arm-freestanding/debug/redshirt-standalone-kernel

```

支持x86_64的独立内核：

```
RUST_TARGET_PATH=`pwd` cargo +nightly build -Z build-std=core,alloc --target x86_64-multiboot2 --package redshirt-standalone-kernel

```

前往[GitHub](https://github.com/tomaka/redshirt)了解更多。

## Rust官方发布：任务监视器扩展task_scope

task_scope crates是一个运行时用于向现有运行时添加对结构化并发的支持的扩展。

### 什么是结构化并发？

[结构化并发](https://en.wikipedia.org/wiki/Structured_concurrency)是一种编程范例，它允许异步操作仅在特定范围内运行，以便它们像常规函数调用堆栈一样形成操作堆栈。当父操作等待所有子代完成时，结构化并发有助于并发程序的本地引导。

### 可撤回点

`task_scope`要求任务定期通过一个可撤回点才能有效地工作。

```
use tokio::io::*;

let mut read = repeat(42); // very fast input
let mut write = sink(); // very fast output

copy(&mut read, &mut write).await.unwrap();

```

实际上，该程序回进入无限循环，因为`read`并且`write`永远不会终止。更糟糕的是，程序无法从外部关闭，因为I / O操作始终会成功，并且`copy`功能会尝试尽可能继续。因此，产生的任务必须协同检查取消或定期循环执行以保持结构良好。

`task_scope`提供便利功能`cancelable`以自动处理取消。它封装给特定的`Future`/ `AsyncRead`/ `AsyncWrite`并在进行内部计算之前检查取消。

```
use futures::pin_mut;
use tokio::io::*;

use task_scope::cancelable;

let read = cancelable(repeat(42)); // very fast, but cancelable input
pin_mut!(read); // needed for Unpin bound of copy
let mut write = sink(); // very fast output

// this will terminate with an error on cancellation
copy(&mut read, &mut write).await.unwrap();

```

如果这个取消逻辑比较复杂，则可以使用`Cancellation`手动轮询以检查取消信号。

详细信息前往[Rust官方博客](https://docs.rs/task_scope/0.1.0/task_scope/)浏览

## 新版本sysinfo（OSX性能改进）

[sysinfo](https://github.com/GuillaumeGomez/sysinfo)用于创建系统信息（支持Linux，Windows，OSX，Android和raspberry pi）。

此版本是性能改进系列的最后一个版本，专注于OSX。

关于sysinfo前往[GitHub](https://github.com/GuillaumeGomez/sysinfo)了解更多。

前往[https://blog.guillaume-gomez.fr/articles/2020-01-06+New+sysinfo+release+(OSX+performance+improvements)](https://blog.guillaume-gomez.fr/articles/2020-01-06+New+sysinfo+release+%28OSX+performance+improvements%29%0D) 查看更新日志。

## restq-一种适用于rest api的紧凑型查询语言

```
/person?age=lt.42&(student=eq.true|gender=eq.'M')&group_by=sum(age),grade,gender&having=min(age)=gt.42&order_by=age.desc,height.asc&page=20&page_size=100

```

大致转换成sql即为：

```
SELECT * FROM person
WHERE age < 42
    AND (student = true OR gender = 'M')
GROUP BY sum(age), grade, gender
HAVING min(age) > 42
ORDER BY age DESC, height ASC
LIMIT 100 OFFSET 1900 ROWS

```

RestQ的语句/语法

```
create  = table, column_def_list, "\n", csv

select = table, [join_table], column_list, [ "?", condition]

delete = table, [ "?", condition ]

update = table, set_expr_list, [ "?", condition]

drop = "-", table

alter = table, { drop_column | add_column | alter_column }

drop_column = "-", column

add_column = "+", column_def

alter_column = column, "=", column_def


column_def_list =  "{", { column_def }, "}"
        | "(", { column_def }, ")"

column_def = [ { column_attributes } ], column, [ "(" foreign ")" ], ":", data_type, [ "(" default_value ")" ]

column_attributes = primary | index | unique

primary = "*"

index = "@"

unique = "&"

data_type = "bool" | "s8" | "s16" | "s32" | "s64" | "u8" | "u16", etc

default_value  = value

value = number | string | bool ,..etc

column = string, ".", string
        | string

table = string

foreign = table

insert = table, column_list ,"\n", csv

column_list = "{", { column }, "}"
        | "(", { column }, ")"


join_table = table, join_type, table

join_type = right_join | left_join | inner_join | full_join

right_join = "->" | "-^"

left_join = "<-"  | "^-"

inner_join = "-><-" | "-^^-"

full_join = "<-->"  | "^--^"

condition = expr

expr =  column | value | binary_operation

binary_operation = expr, operator, expr

operator = "and" | "or" | "eq" | "gte" | "lte" ,..etc

```

更多详细功能与用法前往[GitHub](https://github.com/ivanceras/restq)查看。

----------

From 日报小组 @Lance

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】2020-01-05](https://rust.cc/article?id=1385da68-b786-467e-ba68-b10d6c61779c)

[makeco](https://rust.cc/blog_with_author?author_id=17589eca-5f9f-4542-9938-585c74ef6b39)  发表于  2020-01-05 20:59

### sourmesh 3.0发布，从C++迁移到了Rust

#rust #c++

sourmesh 是一款超快、轻量级核酸搜索和比对软件，此版本与sourmash 2.0兼容，包括sourmash Python API、命令行、签名和数据库文件格式都相同。

[Read More](https://sourmash.readthedocs.io/en/v3.0.1/release-notes/sourmash-3.0.html)

### rio 一个纯Rust的io_uring库

#rust

rio只依赖于libc、工作线程和异步，主要是想面向有高性能存储需求的用户。虽然它只是一个pre-alpha版本，但是已经让作者的笔记本电脑达到了6Gbps的读写速度，这还是在debug模式编译后的情况。

[Repo](https://github.com/spacejam/rio)

### 推荐阅读——面向大众的Rust和WebAssembly教程

-   [Introduction](https://dev.to/sendilkumarn/rust-and-webassembly-for-masses-introduction-1034)
-   [wasm-bindgen](https://dev.to/sendilkumarn/rust-and-webassembly-for-the-masses-wasm-bindgen-57fl)
-   [Sharing Classes](https://dev.to/sendilkumarn/rust-and-webassembly-for-the-masses-sharing-classes-jjo)

----------

From 日报小组 格朗

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc 论坛: 支持 rss](https://rust.cc/)
-   [Rust Force: 支持 rss](https://rustforce.net/)
-   [微信公众号：Rust 语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】2020-01-04 Rust将减少对苹果32位系统的支持](https://rust.cc/article?id=62599e61-4eb6-4cca-89a0-d00d60dba437)

[LacneQin](https://rust.cc/blog_with_author?author_id=f9ed70f9-be28-4b68-9b3b-2812c23a1ccc)  发表于  2020-01-04 19:25

Tags：rust

## Rust将减少对苹果32位系统的支持

Rust团队遗憾地宣布，Rust 1.41.0 将于2020年1月30日发布，这是对32位Apple目标当前支持水平的最后一个版本。从Rust 1.42.0开始，这些目标的支持将降级为Tier 3。

该决定是在[RFC 2837](https://github.com/rust-lang/rfcs/pull/2837 "RFC 2837")上发布的，并被编译器团队和发行团队接受。上述文章解释了做出这个更改的意义，以及对现有项目会产生什么样的影响。

受到此更改影响的主要是32位macOS（`i686-apple-darwin`），支持级别将从级别1降级为3级。这将影响在32位Mac硬件上使用编译器以及从以下版本任何其他平台的交叉编译32位macOS二进制文件。

此外，以下32位iOS系统将从2级降级为3级：

-   `armv7-apple-ios`
-   `armv7s-apple-ios`
-   `i386-apple-ios`

更多详情请阅读[Rust博客原文](https://blog.rust-lang.org/2020/01/03/reducing-support-for-32-bit-apple-targets.html "Rust博客原文")

## Razor发布，一阶理论的模型发现者

razor-fol：一个用于解析和语法处理一阶（逻辑）公式的库。 razor-chase：一个用于构造一阶理论模型的库。剃刀：一阶理论的模型发现工具。

这是GitHub仓库的链接：[https://github.com/salmans/rusty-razor](https://github.com/salmans/rusty-razor "https://github.com/salmans/rusty-razor")

该项目仍处于起步阶段，但是作者进行了部分试验。证明定理的正确性和程序运行速度，因此在不久的将来或许能在Rust中看到类似的项目。

### 运行

#### solve

使用`solve`命令查找`<input>`文件中编写的理论模型：

```
razor solve -i <input>

```

`--count`参数限制了要构建的模型的数量：

```
razor solve -i <input> --count <number>

```

#### 有界模型查找

与传统的模型查找器（例如[Alloy](http://alloytools.org/ "Alloy")）不同，Razor不需要用户为其构造的模型的大小提供界限。但是，当在带有无限的模型的理论上运行时，Razor进程可能永远不会终止。可以证明，在不满足要求的理论（即，没有模型的理论）上运行非常长的时间之后，Razor可以保证能够终止（尽管这可能需要很长时间才能完成）这是一阶逻辑的半判定性的直接结果。

为了保证有穷性，请使用`--bound` 带有`domain`参数值的命令，通过结果模型的元素数量限制结果模型的大小：

```
razor solve -i <input> --bound domain=<number>

```

前往[GitHub仓库](https://github.com/salmans/rusty-razor "GitHub仓库")获取更多信息。

## Nvim-rs：针对Neovim客户的Rust库

[`nvim-rs`](https://crates.io/crates/nvim-rs/0.1.0 "`nvim-rs`")的第一个版本刚刚发布，该库用于在Rust中编写neovim客户程序。

它的主要功能是使用异步来正确嵌套请求，但我也将工作放在错误处理、常规处理、文档示例中。这个项目将会有更多的东西出现，目前很少有功能是固定的，所以尝试一下。

前往[GitHub](https://github.com/KillTheMule/nvim-rs/issues "GitHub")参与讨论/了解更多。

----------

From 日报小组 @Lance

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】 2020-01-03](https://rust.cc/article?id=bcd24f0d-2bbb-4635-b9d7-b0cab4cb379e)

[damody](https://rust.cc/blog_with_author?author_id=55ad9d89-6929-4a73-baa5-cf0a99a9abad)  发表于  2020-01-04 01:14

Tags：rust

### 改非同步沒什麼壓力啊

作者想講的是背壓的問題

Back Pressure

以作者的說法就是生產者消費者問題

生產者速度太快，消費者跟不上的壓力叫背壓

非同步就是把這個等待的時間壓力分散掉的一種方式

當消費者是OS或是其它程式時，用async await寫非同步

就跟寫同步程式一樣簡單

[Read more](https://lucumr.pocoo.org/2020/1/1/async-pressure/)

### const generics 進度更新

這個RFC被接受以來已經有2年多了

自上次更新以來的過去幾個月中，已經取得了良好的進展。

[Read more](https://github.com/rust-lang/rust/issues/44580#issuecomment-570191702)

### Happy Nu Year 2020

NuShell的開發者很感謝2019年有60多位朋友一起開發與協助。

希望2020跟大家一起前進 做的更好

文內有感謝名單

[Read more](https://www.nushell.sh/blog/2019/12/31/happy-nu-year-2020.html)

### postgres-query

一個使用 async 的 psql orm

[Read more](https://github.com/nolanderc/rust-postgres-query)

### This Week in Rust 319

在Rust中重寫m4vgalib。

一個思想實驗：在遊戲引擎之外使用ECS模式。

自旋鎖被認為是有害的。

內部可變性模式。

應該從哪裡來照顧Clippy？

在Rust中編寫AWS Lambda函數。

Rust生命週期和迭代器。

Rocket 與 Multipart forms

Lion 0.15.0-新的面三角化庫。

嵌入式的Raspberry Pi OS開發教程：教程13-使用QEMU的內核單元，集成和控制台測試

使用Rust和Mynewt優化PineTime的顯示驅動程序

嵌入式新聞 22

rust分析變更日誌5

Rust在區塊鏈 7

[Read more](https://this-week-in-rust.org/blog/2019/12/31/this-week-in-rust-319/)

### Podcast 在Etsy中使用Rust在搜索中使用機器學習

[Read more](https://changelog.com/practicalai/70)

### AeroRust 航空航天業的非官方工作組

我們很高興宣布組建AeroRust非官方工作組。 最近，航空航天業正在加快商業化的速度，甚至在該地區的發展越來越快。

該工作組旨在通過向愛好者和行業提供信息，材料，工具等，幫助將開源社區更多地推向不斷發展的航空航天行業。

[Read more](https://github.com/AeroRust/Welcome)

----------

From 日报小组 @Damody

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [【Rust日报】2020-01-02 The Embedded Working Group Newsletter - 22](https://rust.cc/article?id=5576ef88-da16-4291-a297-71d327c0c903)

[Jancd](https://rust.cc/blog_with_author?author_id=d32af902-7816-4c8c-838d-60351791516d)  发表于  2020-01-02 20:16

Tags：rust,news

### The Embedded Working Group Newsletter - 22

这是 Rust Embedded WG 的第 22 期通讯，我们重点介绍新的进展，为出色的项目加油，感谢社区并宣传需要帮助的项目！（如果您想在下一期通讯中提及，请联系我们。）例如：用 Rust 在树莓派上进行操作系统开发教程：https://github.com/rust-embedded/rust-raspi3-OS-tutorials。

查看原文：https://rust-embedded.github.io/blog/newsletter-22/

reddit 参与讨论：https://www.reddit.com/r/rust/comments/eiisk9/the_22nd_embedded_working_group_newsletter/

### Spinlocks Considered Harmful

In this post, I will be expressing strong opinions about a topic I have relatively little practical experience with, so feel free to roast and educate me in comments (link at the end of the post) :-)

Specifically, I’ll talk about:

-   spinlocks,
-   spinlocks in Rust with #[no_std],
-   priority inversion,
-   CPU interrupts,
-   and a couple of neat/horrible systemsy Rust hacks.

Read more ：https://matklad.github.io//2020/01/02/spinlocks-considered-harmful.html

reddit参与讨论：https://www.reddit.com/r/rust/comments/eis1tr/blog_post_spinlocks_considered_harmful/

### 理解  `Tokio`, pt. 1

“我想了解 Tokio 的工作方式。我的兴趣涉及事物的实时性和并行性，但是我对 Tokio 本身并不了解。在引入异步和稳定的期货之前，我或多或少有意地避免学习它，这并不是毫无道理的认为 Tokio 是错的，但是只有有限的时间来学习东西，学习一些新东西是一项艰巨的任务。”

“因此我写下了这些学习 Tokio 的笔记。我没有计划如何学习它的内部原理，但是总的来说，当我有某种项目可以帮助我阅读时，我会学得最好。上下文确实有帮助。我不知道我要长期构建什么，但是一个 HTTP 负载生成器可以很好地工作，它可以扩展自身以找到服务器每秒可以处理的最大请求，同时仍然满足一些延迟约束。这确实意味着我需要将我的学习与另一个库 -  `hyper`  相结合，但是我以前使用过它，并且认为我可以将其保留为黑匣子。”

阅读原文：https://blog.troutwine.us/2019/12/31/understanding-tokio-pt1/

### 面向大众的 Rust 和 WebAssembly 教程

如果您认为 WebAssembly 最适合游戏应用程序，Online IDE 以及其他资源密集型和占用内存的应用程序，那么您在技术上是正确的。但是我们也可以在一个简单的应用程序中获得 WebAssembly 的好处。

对于我们开发的普通应用程序（即始终不需要超快速响应的应用程序），有些部分需要进行性能调整。有时，我们必须删除仅在某些浏览器上而不在其他浏览器上运行的很丑陋的代码。那么 WebAssembly 是一个很好的选择。

使用 Rust 和 WebAssembly，可以使用更快，一致的 WebAssembly 代码轻松弥补这些领域的不足。

详情请看：https://dev.to/sendilkumarn/rust-and-webassembly-for-masses-introduction-1034

### 关于 Rust 代码测试的讨论

详情请看：https://www.reddit.com/r/rust/comments/eiji29/rust_webapps_and_testing/

----------

From 日报小组 @Jancd

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)

## [2020-01-01 2019年 Rust 库增长率以 58% 排名第一](https://rust.cc/article?id=4611cbeb-2381-464f-9ac0-04ed0d71523e)

[挺肥](https://rust.cc/blog_with_author?author_id=24518f05-19a2-4748-b5ce-f936f5adc0d0)  发表于  2020-01-01 23:21

Tags：rust日报;

### 用 Rust 重写 m4vgalib

作者用 Rust 重写了自己多年前用 C++ 写的视频生成库  [m4vgalib](https://github.com/cbiffle/m4vgalib). 介绍了 Rust 的一些优点，如包管理、API 设计、内存安全等.  
[详情](http://cliffle.com/blog/m4vga-in-rust/#rust-has-a-package-manager)

### 2019年 Rust 库增长率以 58% 排名第一

有人根据 modulecounts.com 网站的数据统计了2019年各种语言的库增长率，Rust 以 58% 排名第一，NPM 以 55%排名第二，另外还有 Julia 40%, Python 29%, Nim 28%, Hex 25%……

![image.png](https://i.loli.net/2020/01/01/R9ITq2QXJDs3pVB.png)

### aspotify：异步 Spotify Web API 客户端

作者觉得现有的几个库有一些问题：

-   spotify : 没有包含所有的 API
-   rspotify : API 比较难用
-   spotrust : 没有文档

所以作者就用 Rust 写了[这个库](https://github.com/KaiJewson/aspotify)

### Druid 状态更新以及 0.5 路线图

[Druid](https://github.com/xi-editor/druid)  是一个实验阶段的 Rust-native UI 工具库，主要目标是表现 Rust 开发应用的潜力. 05 版的主要任务有：

-   addressable widgets
-   lifecycle refactor
-   z-order painting
-   paint bounds
-   modal widgets

[详情](https://github.com/xi-editor/druid/issues/434#issue-544082945)

----------

From 日报小组 @挺肥

日报订阅地址：

独立日报订阅地址：

-   [Telgram Channel](https://t.me/rust_daily_news)
-   [阿里云语雀订阅](https://www.yuque.com/chaosbot/rustnews)
-   [Steemit](https://steemit.com/@blackanger)
-   [GitHub](https://github.com/RustStudy/rust_daily_news)

社区学习交流平台订阅：

-   [Rust.cc论坛: 支持rss](https://rust.cc/)
-   [Rust Force: 支持rss](https://rustforce.net/)
-   [微信公众号：Rust语言学习交流](https://rust.cc/article?id=ed7c9379-d681-47cb-9532-0db97d883f62)