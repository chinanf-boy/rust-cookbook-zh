## 主要正确处理错误

[![error-chain-badge]][error-chain] [![cat-rust-patterns-badge]][cat-rust-patterns]

处理尝试打开不存在的文件时发生的错误。它是通过使用[误差链-]，一个处理大量样板代码的库[处理生锈的错误].

`Io(std::io::Error)`里面[`foreign_links`]允许自动转换自[`std::io::Error`]进入之内[`error_chain!`]定义的类型实现[`Error`]特质。

下面的方法将通过打开 unix 文件来告诉系统运行了多长时间。`/proc/uptime`然后分析内容得到第一个数字。返回正常运行时间，除非出现错误。

本书中的其他烹饪书将隐藏[误差链-]样板文件，可以通过按钮展开代码来查看。

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
