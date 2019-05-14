## 从 URL 中，删除片段标识符和查询对

[![url-badge]][url] [![cat-net-badge]][cat-net]

解析[`Url`]，并[`url::Position`]把它切成片，删除不需要的 URL 部分。

```rust
extern crate url;

use url::{Url, Position, ParseError};

fn main() -> Result<(), ParseError> {
    let parsed = Url::parse("https://github.com/rust-lang/rust/issues?labels=E-easy&state=open")?;
    let cleaned: &str = &parsed[..Position::AfterPath];
    println!("cleaned: {}", cleaned);
    Ok(())
}
```

[`url::position`]: https://docs.rs/url/*/url/enum.Position.html
[`url`]: https://docs.rs/url/*/url/struct.Url.html
