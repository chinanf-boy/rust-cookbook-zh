## 将URL从字符串解析为`Url`类型

[![url-badge]][url] [![cat-net-badge]][cat-net]

这个[`parse`]方法从`url`板条箱验证并分析`&str`变成一个[`Url`]结构。输入字符串可能格式不正确，因此此方法返回`Result<Url, ParseError>`.

一旦解析了URL，它就可以与`Url`类型。

```rust
extern crate url;

use url::{Url, ParseError};

fn main() -> Result<(), ParseError> {
    let s = "https://github.com/rust-lang/rust/issues?labels=E-easy&state=open";

    let parsed = Url::parse(s)?;
    println!("The path part of the URL is: {}", parsed.path());

    Ok(())
}
```

[`parse`]: https://docs.rs/url/*/url/struct.Url.html#method.parse

[`url`]: https://docs.rs/url/*/url/struct.Url.html
