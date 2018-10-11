
## 正确处理错误

[![error-chain-badge]][error-chain] [![cat-rust-patterns-badge]][cat-rust-patterns]

处理尝试打开不存在的文件时发生的错误.它是通过使用实现的[错误链-],一个库,它需要处理大量的样板代码[处理Rust中的错误].

`Io(std::io::Error)`内[`foreign_links`]允许自动转换[`std::io::Error`]成[`error_chain!`]实现的定义类型[`Error`]特征.

下面的配方将通过打开Unix文件来告诉系统运行了多长时间`/proc/uptime`并解析内容以获取第一个数字.除非出现错误,否则返回正常运行时间.

本书中的其他食谱将隐藏[错误链-]样板,可以通过使用⤢按钮扩展代码来查看.

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
