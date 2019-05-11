## main 中的正确处理错误

[![error-chain-badge]][error-chain] [![cat-rust-patterns-badge]][cat-rust-patterns]

要处理尝试打开不存在的文件时，发生的错误。我们会用到[error-chain]，这是一个大量样板代码的库，用来[处理 Rust 的错误]。

[`foreign_links`]里面的`Io(std::io::Error)`，允许从[`std::io::Error`]到[`error_chain!`]所定义类型的自动转换，这些类型会实现[`Error`] trait。

下面的食谱是，在打开 unix 文件`/proc/uptime`，然后分析内容得到第一个数字期间，告诉我们系统运行了多长时间。要返回 uptime，除非出现错误。

本书中的其他食谱，会隐藏[error-chain]样板文件，可以通过按钮（展开代码）来查看。

```rust
#[macro_use]
extern crate error_chain;

use std::fs::File;
use std::io::Read;

error_chain!{
    foreign_links {
        Io(std::io::Error);
        ParseInt(::std::num::ParseIntError);
    }
}

fn read_uptime() -> Result<u64> {
    let mut uptime = String::new();
    File::open("/proc/uptime")?.read_to_string(&mut uptime)?;

    Ok(uptime
        .split('.')
        .next()
        .ok_or("Cannot parse uptime data")?
        .parse()?)
}

fn main() {
    match read_uptime() {
        Ok(uptime) => println!("uptime: {} seconds", uptime),
        Err(err) => eprintln!("error: {}", err),
    };
}
```

[`error_chain!`]: https://docs.rs/error-chain/*/error_chain/macro.error_chain.html
[`error`]: https://doc.rust-lang.org/std/error/trait.Error.html
[`foreign_links`]: https://docs.rs/error-chain/*/error_chain/#foreign-links
[`std::io::error`]: https://doc.rust-lang.org/std/io/struct.Error.html
[handle errors in rust]: https://doc.rust-lang.org/book/second-edition/ch09-00-error-handling.html
