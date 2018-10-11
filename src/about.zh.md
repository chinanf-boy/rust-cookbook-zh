
# 关于"生锈的东西"

## 目录

-   [Who this book is for](#who-this-book-is-for)
-   [How to read this book](#how-to-read-this-book)
-   [How to use the recipes](#how-to-use-the-recipes)
-   [A note about error handling](#a-note-about-error-handling)
-   [A note about crate representation](#a-note-about-crate-representation)

## 这本书的用途是谁

本手册适用于新的Rust程序员,因此他们可以快速了解Rust crate生态系统的功能.它也适用于经验丰富的Rust程序员,他们应该在食谱中找到如何完成常见任务的简单提醒.

## 如何阅读本书

烹饪书[指数]包含完整的食谱列表,分为多个部分:"基础知识","编码","并发"等.这些部分本身或多或少地按顺序排序,后面的部分更先进,偶尔建立在

前面部分的概念.在索引中,每个部分都包含一个配方列表.配方是要完成的任务的简单陈述,例如"生成范围内的随机数";*并且每个食谱都标有徽章,表明哪个*包装箱[![rand-badge]][rand]他们使用,像[.以及哪些类别]crates.io[![cat-science-badge]][cat-science]那些板条箱属于,像

.新的Rust程序员应该从第一部分到最后一部分阅读起来很舒服,这样做应该给出一个对箱子生态系统的强烈概述.

单击索引中的节标题,或单击侧栏以导航到该书的该部分的页面.如果您只是在寻找简单任务的解决方案,那么今天的食谱更难以导航.查找特定配方的最简单方法是扫描索引,查找感兴趣的包装箱和类别.从那里,单击配方名称进行查看.这将在未来得到改善.

## 如何使用食谱

食谱旨在让您即时访问工作代码,并全面解释其正在执行的操作,并指导您获取更多信息.

食谱中的所有食谱都是完整的,自包含的程序,因此可以将它们直接复制到您自己的项目中进行实验.为此,请按照以下说明操作.

考虑这个例子"生成一个范围内的随机数":

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

```rust
extern crate rand;
use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();
    println!("Random f64: {}", rng.gen::<f64>());
}
```

要在本地使用它,我们可以运行以下命令来创建一个新的货物项目,并切换到该目录:

```sh
cargo new my-example --bin
cd my-example
```

现在,我们还需要添加必要的板条箱[Cargo.toml]如箱子徽章所示,在这种情况下只是"兰德".为此,我们将使用`cargo add`命令,由...提供[`cargo-edit`]箱子,我们需要先安装:

```sh
cargo install cargo-edit
cargo add rand
```

现在你可以替换`src/main.rs`使用示例的完整内容并运行它:

```sh
cargo run
```

示例附带的板条徽章链接到板条箱的完整文档[docs.rs],并且通常是您在决定哪个crate套件后您应该阅读的下一个文档.

## 关于错误处理的说明

如果正确完成,Rust中的错误处理是健壮的,但在今天的Rust中它需要相当多的样板.因为这个经常看到Rust填充的例子`unwrap`调用而不是正确的错误处理.

由于这些配方旨在按原样重复使用并鼓励最佳实践,因此它们可以正确设置错误处理`Result`涉及的类型.

我们使用的基本模式是拥有一个`fn run() -> Result`这就像"真正的"主要功能.我们使用[错误链-]箱子做`?`在...内工作`run`.

结构通常如下:

```rust
#[macro_use]
extern crate error_chain;

use std::net::IpAddr;
use std::str;

error_chain! {
    foreign_links {
        Utf8(std::str::Utf8Error);
        AddrParse(std::net::AddrParseError);
    }
}

fn run() -> Result<()> {
    let bytes = b"2001:db8::1";

    // Bytes to string.
    let s = str::from_utf8(bytes)?;

    // String to IP address.
    let addr: IpAddr = s.parse()?;

    println!("{:?}", addr);
    Ok(())
}

quick_main!(run);
```

这是使用`error_chain!`宏来定义自定义`Error`和`Result`类型,以及来自两个标准库错误类型的自动转换.自动转换使得`?`操作员工作.该`quick_main!`宏生成实际`main`如果发生错误,则打印出错误.

为了便于阅读,错误处理样板默认隐藏,如下所示.要阅读完整内容,请单击"展开"(<i class="fa fa-expand"></i>)按钮位于代码段的右上角.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate url;

use url::{Url, Position};
#
# error_chain! {
#     foreign_links {
#         UrlParse(url::ParseError);
#     }
# }

fn run() -> Result<()> {
    let parsed = Url::parse("https://httpbin.org/cookies/set?k2=v2&k1=v1")?;
    let cleaned: &str = &parsed[..Position::AfterPath];
    println!("cleaned: {}", cleaned);
    Ok(())
}
#
# quick_main!(run);
```

有关Rust中错误处理的更多背景知识,请阅读[这本Rust书的页面][error-docs]和[这篇博文][error-blog].

## 关于板条箱表示的说明

这本食谱最终旨在提供对Rust crate生态系统的广泛报道,但今天我们得到它的自助范围,并在演示文稿上工作.希望从小范围开始并缓慢扩展将有助于烹饪书更快地成为高质量的资源,并使其在增长时保持一致的质量水平.

目前,该手册主要关注标准库,以及"核心"或"基础",板条箱 - 构成最常见编程任务的板条箱,以及生态系统的其余部分.

这本食谱与之密切相关[Rust Libz Blitz],一个识别和提高此类板条箱质量的项目,因此它在很大程度上将板条箱选择推迟到该项目.已经作为该过程的一部分进行评估的任何板条箱都在食谱的范围内,正在等待评估的板条箱也是如此.

{{#include links.zh.md}}

[index]: intro.html

[error-docs]: https://doc.rust-lang.org/book/error-handling.html

[error-blog]: https://brson.github.io/2016/11/30/starting-with-error-chain

[error-chain]: https://docs.rs/error-chain/

[rust libz blitz]: https://internals.rust-lang.org/t/rust-libz-blitz/5184

[crates.io]: https://crates.io

[docs.rs]: https://docs.rs

[cargo.toml]: http://doc.crates.io/manifest.html

[`cargo-edit`]: https://github.com/killercup/cargo-edit
