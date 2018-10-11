
## 解析从字符串到URL的URL`Url`类型

[![url-badge]][url] [![cat-net-badge]][cat-net]

这个[`parse`]方法从`url`机箱验证和解析`&str`变成一个[`Url`]结构.输入字符串可能变形,因此此方法返回`Result<Url, ParseError>`.

一旦解析了URL,它就可以与`Url`类型.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate url;

use url::Url;
#
# error_chain! {
#     foreign_links {
#         UrlParse(url::ParseError);
#     }
# }

fn run() -> Result<()> {
    let s = "https://github.com/rust-lang/rust/issues?labels=E-easy&state=open";

    let parsed = Url::parse(s)?;
    println!("The path part of the URL is: {}", parsed.path());

    Ok(())
}
#
# quick_main!(run);
```

[`parse`]: https://docs.rs/url/*/url/struct.Url.html#method.parse

[`url`]: https://docs.rs/url/*/url/struct.Url.html
