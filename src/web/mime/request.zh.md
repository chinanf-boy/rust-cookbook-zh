## 分析HTTP响应的mime类型

[![reqwest-badge]][reqwest] [![mime-badge]][mime] [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding]

接收来自的HTTP响应时`reqwest`这个[哑剧类型]或媒体类型可以在[内容类型-]标题。[`reqwest::header::HeaderMap::get`]将头检索为[`reqwest::header::HeaderValue`]，可以转换为字符串。这个`mime`然后板条箱就可以分析它，产生一个[`mime::Mime`]价值。

这个`mime`板条箱还定义了一些常用的mime类型。

请注意[`reqwest::header`]模块从导出[`http`]机箱。

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
