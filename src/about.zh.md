# 关于“Rust 烹饪”

## 目录

<!-- START doctoc -->
<!-- END doctoc -->

## 这本书的目标受众

本手册适用于新的 Rust 程序员，因此他们可以快速了解 Rust crate(箱子) 生态系统的能力。它也适用于经验丰富的 Rust 程序员，他们应该在食谱中，找到如何完成常见任务的简单提示。

## 如何阅读本书

烹饪书的[索引页][index]包含完整的食谱列表，分为几个部分：“基础”，“编码”，“并发”等。这些部分本身或多或少地按顺序排列，后面的部分，更先进，偶尔是在前面部分的概念之上构建。

在索引中，每个部分都包含一个食谱列表。食谱是要完成任务的简单陈述，例如“生成范围内的随机数”；并且每个食谱都标有徽章，表明哪个*箱子*是他们所使用的，像[![rand-badge]][rand]，以及那些箱子在[crates.io]上，属于哪些类别。像[![cat-science-badge]][cat-science]。

新的 Rust 程序员，应该从第一部分开始，按顺序到最后一部分，这样阅读起来会很舒服，这样做可以让人们对 crate 生态系统，有一个很好的大菊观。单击，索引中的章节标题，或单击，侧栏以导航到某章节页面。

如果，您只是在寻找简单任务的解决方案，那么今时今日的烹饪书，还较难导航。查找特定食谱的最简单方法是扫描索引，查找感兴趣的箱子和类别。从那里，单击食谱名称进行查看。这导航方面在未来会改善的。

## 如何使用食谱

食谱旨在让您即时访问到，能工作的代码，并全面解释其正在执行的操作，并指导您获取更多信息。

烹饪书中的所有食谱都是完整的，自包含(自给自足)的程序，因此可以将它们直接复制到，您自己的项目中进行实验。为此，请按照以下说明，进行操作。

考虑这个例子：“生成一个范围内的随机数”：

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

```rust
extern crate rand;
use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();
    println!("Random f64: {}", rng.gen::<f64>());
}
```

要在本地使用它，我们可以运行以下命令，来创建一个新的货物(cargo)项目，并切换到该目录：

```sh
cargo new my-example --bin
cd my-example
```

现在，我们还需要添加必要的箱子到[Cargo.toml]，如箱子徽章所示，在这种情况下只是“rand”。为此，我们将使用`cargo add`命令，这是由[`cargo-edit`]箱子提供的(自定义)命令，我们需要先安装：

```sh
cargo install cargo-edit
cargo add rand
```

现在，你可以把`src/main.rs`，替换成，用例中的完整内容并运行：

```sh
cargo run
```

示例附带的箱子徽章，链接到箱子的完整[docs.rs]文档(一个专放Rust项目文档的官方托管网站)，并且通常，在你决定哪个箱子套件后，您应该阅读相关文档。

## 关于错误处理的说明

如果做得正确，Rust 中的错误处理是健壮的，但对今时今日的 Rust 来说，就需要相当多的模版。正是这个原因，你经常看到 Rust 的例子，充满了`unwrap`调用，而不是正确的错误处理。

由于这些食谱，具有原样复用的目标，并鼓励最佳实践，因此当涉及`Result`类型，它们就会正确设置错误处理。

我们使用的基本模式是，具备一个`fn run() -> Result`，让它像“真正的”main 函数行动。我们用的是[error-chain]箱子，使`?`在`run`里面工作。

错误处理的结构，通常如下：

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

    // Bytes 到 string.
    let s = str::from_utf8(bytes)?;

    // String 到 IP address.
    let addr: IpAddr = s.parse()?;

    println!("{:?}", addr);
    Ok(())
}

quick_main!(run);
```

这是使用`error_chain!`宏，自定义一个`Error`和`Result`类型，以及来自**两个标准库的错误类型**的自动转换。自动转换使`?`操作符工作。该`quick_main!`宏生成，实际`main`，并在发生错误时，打印出错误。

为了便于阅读，错误处理模版，默认隐藏，如下所示。要阅读完整内容，请单击“展开”（<i class="fa fa-expand"></i>）按钮，它位于代码段的右上角。

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

有关 Rust 中错误处理的更多背景知识，请阅读[这本 Rust 书][error-docs]和[这篇博文][error-blog]。

## 关于箱子表示的说明

这本烹饪书，最终的目标，是提供对 Rust crate 生态系统的广泛认知，但是，今天我们在它的引导下，进行演示时，范围还很有限。希望从小范围开始，缓慢扩展(认知)，将有助于烹饪书，更快地成为高质量的资源，常话说：不要急，最重要快！并在增长时，保持一致的质量水平。

目前，烹饪书专注于标准库，以及“核心”或“基础”，箱子 - 都是构成最常见的编程任务的那些箱子，其余的，就是生态系统的部分构建。

这本烹饪书与[Rust Libz Blitz]密切相关，一个识别和提高此类箱子质量的项目，因此该项目在很大程度上，延迟箱子入选的问题。该过程的一部分，作为已经评估的任何箱子，都在烹饪书的(书写)范围内，而正在等待评估的箱子也是如此。

{{#include links.zh.md}}

[index]: intro.zh.html
[error-docs]: https://doc.rust-lang.org/book/error-handling.html
[error-blog]: https://brson.github.io/2016/11/30/starting-with-error-chain
[error-chain]: https://docs.rs/error-chain/
[rust libz blitz]: https://internals.rust-lang.org/t/rust-libz-blitz/5184
[crates.io]: https://crates.io
[docs.rs]: https://docs.rs
[cargo.toml]: http://doc.crates.io/manifest.html
[`cargo-edit`]: https://github.com/killercup/cargo-edit
