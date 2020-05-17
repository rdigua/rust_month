
# Epoll, Kqueue and IOCP Explained with Rust

Cross Platform Event Queues Explained With Rust

This book aims to explain how `Epoll`, `Kqueue`and `IOCP`works, and how we can use this for efficient, high performance I/O. The book is divided into three parts:

**Part 1 - An express explanation:** is probably what you want to read if you're interested in a short introduction.

**The Appendix** contains some additional references and small articles explaining some concepts that I found interesting and which is related to the kind of code we write here.

**Part 2 is special.** 99% of readers should not even go there. You'll find page up and down with code and explanations just to implement the simplest example of a cross-platform-eventloop that actually works. Turns out that there is no "express" way of doing this.

The reason I added Part 2 was all the work I've put into exploring things from the ground and up. It sets up a pretty bare bones cross platform event loop we can use to toy around with. It's just an example meant to explore how a proper cross platform event loop works since such code bases can be pretty daunting to dive into themselves.

Later in another book we might use this exact code to explore how higher level concepts like`Reactors`, `Executors`and `Futures`in Rust work.

**Part 2** could also serve as an introduction to make it easier to read and understand the source code of libraries like [mio](https://github.com/tokio-rs/mio) or [BOOST ASIO](https://www.boost.org/doc/libs/1_42_0/boost/asio/). Even though these libraries have extensive documentation already it can be difficult to know where to start.

**This book is developed in the open and there are some resources I'll point you at right away:**

**​**[**The repository for this Gitbook:**](https://github.com/cfsamson/book-exploring-epoll-kqueue-iocp) The repository contains the text of this book. Use the [Issue Tracker](https://github.com/cfsamson/book-exploring-epoll-kqueue-iocp/issues) if you have questions or feedback of any kind. If you spot any mistaks, want to suggest changes or otherwise contribute to this book please make a [Pull Request](https://github.com/cfsamson/book-exploring-epoll-kqueue-iocp/pulls).

​[**The example code for Part 2 of this book - the minimio library:**](https://github.com/cfsamson/examples-minimio) I suggest that you clone or fork the repository and explore, change and improve the example yourslf.

## 

Who is this book for?[](https://cfsamsonbooks.gitbook.io/epoll-kqueue-iocp-explained/#who-is-this-book-for)

This book should be interesting if you want to learn more about:

-   How FFI works in Rust and what the crates `libc` and `mio`provides for you
    
-   How to create a cross platform event loop using the same methods as `Node` and `Tokio`uses
    
-   How the `Reactor`in the async library your're most likely using works
    
-   How to create a library in Rust that conditionally compiles code for the three major platforms
    
-   How to make syscalls on Linux, OSX and Windows
    

_I'll avoid any external dependencies, so we make sure we remove as much "magic" as possible to make sure we really understand this from the ground up._

_Throughout this book I'll use Rusts own types when interfacing with the_ `_ffi_`_interface on all platforms. I do this to make the code as straight forward as possible, but it's not recommended if you care about maximising compatability._

## 

Prerequisites[](https://cfsamsonbooks.gitbook.io/epoll-kqueue-iocp-explained/#prerequisites)

This subject is admittedly pretty difficult. If both Rust and concurrent programming is something that's new to you, I do suggest that you check out my previous books first. After that you should be more than prepared for this book:

​[Green Threads Explained in 200 Lines of Rust](https://cfsamson.gitbook.io/green-threads-explained-in-200-lines-of-rust/)​

​[The Node Experiment - Exploring Async Basics with Rust](https://cfsamson.github.io/book-exploring-async-basics/)​

## 

Motivation[](https://cfsamsonbooks.gitbook.io/epoll-kqueue-iocp-explained/#motivation)

When researching information about Kqueue, Epoll and IOCP myself it turned out that getting a deeper understanding of this subject was pretty hard with information scattered around and mostly covering one aspect of either Epoll, Kqueue or IOCP. Therefore, I chose to spend some extra time and effort to collect this information and present it here to make it easier for the next person that ventures on the same quest as I did.

[](https://cfsamsonbooks.gitbook.io/epoll-kqueue-iocp-explained/part-1-an-express-explanation)
