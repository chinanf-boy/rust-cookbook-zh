## 将字符串的一个 URL，解析为`Url`类型

[![url-badge]][url] [![cat-net-badge]][cat-net]

这个[`parse`]方法，它来自`url`箱子，用来验证并解析一个`&str`，变为一个[`Url`]结构。输入的字符串，可能格式不正确，因此，该方法返回`Result<Url, ParseError>`.

一旦解析了 URL，它就可以使用`Url`类型的所有方法。

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
