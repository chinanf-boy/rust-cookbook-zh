## 分析 HTTP 响应的 mime 类型

[![reqwest-badge]][reqwest] [![mime-badge]][mime] [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding]

从`reqwest`那里，接收到一个 HTTP 响应的时候，这个[MIME 类型][mime type]或是媒体类型，可以在[Content-Type]标头中找到。[`reqwest::header::HeaderMap::get`]将标头检索为[`reqwest::header::HeaderValue`]，这可以转换为一个字符串。这个`mime`箱子，之后就可以解析它了，并产生一个[`mime::Mime`]值。

这个`mime`箱子，还定义了一些常用的 MIME 类型。

请注意[`reqwest::header`]模块，是从[`http`]箱子导出的。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate mime;
extern crate reqwest;

use mime::Mime;
use std::str::FromStr;
use reqwest::header::CONTENT_TYPE;

#
# error_chain! {
#    foreign_links {
#        Reqwest(reqwest::Error);
#        Header(reqwest::header::ToStrError);
#        Mime(mime::FromStrError);
#    }
# }

fn run() -> Result<()> {
    let response = reqwest::get("https://www.rust-lang.org/logos/rust-logo-32x32.png")?;
    let headers = response.headers();

    match headers.get(CONTENT_TYPE) {
        None => {
            println!("The response does not contain a Content-Type header.");
        }
        Some(content_type) => {
            let content_type = Mime::from_str(content_type.to_str()?)?;
            let media_type = match (content_type.type_(), content_type.subtype()) {
                (mime::TEXT, mime::HTML) => "a HTML document",
                (mime::TEXT, _) => "a text document",
                (mime::IMAGE, mime::PNG) => "a PNG image",
                (mime::IMAGE, _) => "an image",
                _ => "neither text nor image",
            };

            println!("The reponse contains {}.", media_type);
        }
    };

    Ok(())
}
#
# quick_main!(run);
```

[`http`]: https://docs.rs/http/*/http/
[`mime::mime`]: https://docs.rs/mime/*/mime/struct.Mime.html
[`reqwest::header::headermap::get`]: https://docs.rs/reqwest/*/reqwest/header/struct.HeaderMap.html#method.get
[`reqwest::header::headervalue`]: https://docs.rs/reqwest/*/reqwest/header/struct.HeaderValue.html
[`reqwest::header`]: https://docs.rs/reqwest/*/reqwest/header/index.html
[content-type]: https://developer.mozilla.org/docs/Web/HTTP/Headers/Content-Type
[mime type]: https://developer.mozilla.org/docs/Web/HTTP/Basics_of_HTTP/MIME_types
