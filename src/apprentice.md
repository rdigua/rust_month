
## Rust 语言新人入门指南

Mike Tang  Rust语言中文社区  _1周前_

首先，学习  Rust  不能急躁。如果你抱着之前  1  天上手  Python,  2  天入门  Go  的经验和优越感来学习  Rust  的话，你可能会遭遇严重的失败感。如果你来自  Haskell/Ocaml  等函数式语言社区，你会有相当的亲切感。对于有丰富  C++  开发经验的同学来说，上手可能相对比较容易。

  

**了解**

  

一般来说，要决定学习一门新语言之前，会先大体了解下这门语言的特点和目前的发展情况。这时，建议看

  

-   Rust  官网  https://rust-lang.org
    
-   Rust  语言中文社区论坛  https://rustcc.cn
    
-   《Rust语言中文社区》公众号，每日  Rust  新闻和知识推送
    
-   知乎  有很多关于  Rust  相关的知识、专栏、博客等
    

  

**看书**

  

了解大体情况后，可能就想看看书，系统的学习一下。目前，网络上  Rust  电子书籍有：

  

-   The  Book -  https://doc.rust-lang.org/book/  官方的  Rust  书（最新第二版，必看）
    
-   The  Book  中文翻译 -  https://github.com/KaiserY/rust-book-chinese
    
-   Rust  Primer -  https://rustcc.gitbooks.io/rustprimer/content/  Rust  中文社区推出的教程
    
-   本地的Rust文档 
    
    ```shell
    rustup doc
    ```
    
    

电子书看着没感觉，想买实体书来看看，目前国内有如下两本已出版  Rust  学习教程。

  

实体书

  

-   《Rust  编程之道》  张汉东  电子工业出版社  2019-1
    
-   《深入浅出Rust》范长春  机械工业出版社  2018-8
    

  

**练习**

  

想做下练习

  

-   Rust  By  Example  https://doc.rust-lang.org/stable/rust-by-example/
-   Rustlings     https://github.com/rust-lang/rustlings

  

看着看着书，想加入社区，与大家交流一下？下面罗列了国内目前QQ群和微信群

  

**QQ  群**

  

综合群：

  

-   Rust编程语言社区1群，群号：303838735  （已满，只能内部邀请）
    
-   Rust编程语言社区2群，群号：813448660
    
-   Rust水群(编程社区子群)，群号：253849562
    

  

专题群：

  

-   Rust  Redox发行版开发群，群号：437268658
    
-   Rust  Data  Science  研究小组，群号：681142501
    
-   Rust  webassembly/wasm社区，群号：347929175
    
-   Rust社群-区块链研究，群号：617238820
    
-   Rust  嵌入式开发，群号：825820683
    
-   φ  Rust图形学，群号：812748521
    
-   哲学与计算，群号：446590168
    

  

地方线下聚会群：

  

-   北京：305842562
    
-   上海：966129249
    
-   深圳：673715651
    
-   广州：738772514
    
-   成都：131080784
    
-   重庆：962149536
    

  

**微信群**

  

主题群

  

-   Rust  China  Community  （已满）
    
-   Rust  语言中文社区  2  群 （已满）
    
-   Rust  语言中文社区  3  群
    
-   RustCon  Asia  2019
    
-   Rust  移动端音视频开发
    
-   Rust  编程
    
-   CSDN  Rust  语言群
    
-   魅力  Rust（《Rust编程之道》读者交流群）
    

  

同城群

  

-   Rust  Meetup  -  BJ  北京
    
-   Rust  Meetup  -  SH  上海
    
-   Rust  Meetup  -  HZ  杭州
    
-   Rust  Meetup  -  SuZhou  苏州
    
-   Rust  Meetup  -  NJ  南京
    
-   Rust  Meetup  -  CD  成都
    
-   Rust  Meetup  -  CQ  重庆
    
-   Rust  Meetup  -  XA  西安
    
-   Rust  Meetup  -  WH  武汉
    
-   Rust  Meetup  -  CS  长沙
    
-   Rust  Meetup  -  大湾区  深圳、大湾区
    
-   Rust  Meetup  -  GZ  广州
    
-   Rust  Meetup  -  SG  新加坡
    
-   Rust  Meetup  -  Canada  加拿大
    

  

（以上微信群，请加  daogangtang  微信号后申请进入）

  

**开发**

  

开始开发具体的工程了，cargo  和  crates.io  必须好好了解一下。

  

国内  crates.io  源太慢，有解决办法：

  

Rustcc  联合  LongHash  提供了国内  Rust  开发者专属  crates.io  镜像。把下面内容填充到你的  ~/.cargo/config  文件中（没有就创建一个）。

  

```toml
[source.crates-io]
replace-with = "rustcc"

[source.rustcc]
registry = "git://crates.rustcc.cn/crates.io-index"
```

  

然后，就尽情地享受飞一般的感觉吧。

  

**招聘情况**  

  

想了解一下目前国内的  Rust  招聘情况，可以看这里

  

招聘：https://rustcc.cn/section?id=fed6b7de-0a74-48eb-8988-1978858c9b35

  

**更多话题**

  

更多话题  ，比如  编辑器如何配置，哪个IDE最好，如何配置，Rust  目前在哪些领域有应用，Rust  有什么杀手锏应用，区块链为什么越来越多选择用  Rust  来实现，WebAssembly  与  Rust  的关系等等，就不展开介绍了，上面提到的各种资源，以及网络上，有丰富的信息，大家可以自行查阅。

  

最后

  

In  Rust,  We  Trust.