## 避免在错误转换期间，丢掉了错误

[![error-chain-badge]][error-chain] [![cat-rust-patterns-badge]][cat-rust-patterns]

这个[error-chain]箱子，能[匹配][matching]函数返回的不同错误类型，可能是相对紧凑的。[`ErrorKind`]能确定错误类型。

使用[reqwest]查询一个随机整数生成器的 Web 服务。将响应的字符串，转换为整数。我们有 Rust 标准库，[reqwest]，并且 Web 服务的全部错误都会(可能)发生。要明确定义的 Rust 错误，请使用[`foreign_links`]。 对于额外的 Web 服务错误[`ErrorKind`]变种，使用`error_chain!`宏的`errors`代码块。

```rust
#[macro_use]
extern crate error_chain;
extern crate reqwest;

use std::io::Read;

error_chain! {
    foreign_links {
        Io(std::io::Error);
        Reqwest(reqwest::Error);
        ParseIntError(std::num::ParseIntError);
    }

    errors { RandomResponseError(t: String) }
}

fn parse_response(mut response: reqwest::Response) -> Result<u32> {
    let mut body = String::new();
    response.read_to_string(&mut body)?;
    body.pop();
    body.parse::<u32>()
        .chain_err(|| ErrorKind::RandomResponseError(body))
}

fn run() -> Result<()> {
    let url =
        format!("https://www.random.org/integers/?num=1&min=0&max=10&col=1&base=10&format=plain");
    let response = reqwest::get(&url)?;
    let random_value: u32 = parse_response(response)?;

    println!("a random number between 0 and 10: {}", random_value);

    Ok(())
}

fn main() {
    if let Err(error) = run() {
        match *error.kind() {
            ErrorKind::Io(_) => println!("Standard IO error: {:?}", error),
            ErrorKind::Reqwest(_) => println!("Reqwest error: {:?}", error),
            ErrorKind::ParseIntError(_) => println!("Standard parse int error: {:?}", error),
            ErrorKind::RandomResponseError(_) => println!("User defined error: {:?}", error),
            _ => println!("Other error: {:?}", error),
        }
    }
}
```

[`errorkind`]: https://docs.rs/error-chain/*/error_chain/example_generated/enum.ErrorKind.html
[`foreign_links`]: https://docs.rs/error-chain/*/error_chain/#foreign-links
[matching]: https://docs.rs/error-chain/*/error_chain/#matching-errors
