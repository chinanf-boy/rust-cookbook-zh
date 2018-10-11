
## 从URL中删除片段标识符和查询对

[![url-badge]][url] [![cat-net-badge]][cat-net]

解析[`Url`]把它切成薄片[`url::Position`]删除不必要的URL部分.

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
    let parsed = Url::parse("https://github.com/rust-lang/rust/issues?labels=E-easy&state=open")?;
    let cleaned: &str = &parsed[..Position::AfterPath];
    println!("cleaned: {}", cleaned);
    Ok(())
}
#
# quick_main!(run);
```

[`url::position`]: https://docs.rs/url/*/url/enum.Position.html

[`url`]: https://docs.rs/url/*/url/struct.Url.html
