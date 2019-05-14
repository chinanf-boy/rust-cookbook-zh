## 通过移除路径段，创建一个 base URL

[![url-badge]][url] [![cat-net-badge]][cat-net]

base URL 包括一个协议和一个域。base URL 没有文件夹、文件或查询字符串。这每一项都将从给定的 URL 中，剥离出来。[`PathSegmentsMut::clear`]会删除路径，和[`Url::set_query`]会删除查询字符串。

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
#     errors {
#         CannotBeABase
#     }
# }

fn run() -> Result<()> {
    let full = "https://github.com/rust-lang/cargo?asdf";

    let url = Url::parse(full)?;
    let base = base_url(url)?;

    assert_eq!(base.as_str(), "https://github.com/");
    println!("The base of the URL is: {}", base);

    Ok(())
}

fn base_url(mut url: Url) -> Result<Url> {
    match url.path_segments_mut() {
        Ok(mut path) => {
            path.clear();
        }
        Err(_) => {
            return Err(Error::from_kind(ErrorKind::CannotBeABase));
        }
    }

    url.set_query(None);

    Ok(url)
}
#
# quick_main!(run);
```

[`pathsegmentsmut::clear`]: https://docs.rs/url/*/url/struct.PathSegmentsMut.html#method.clear
[`url::set_query`]: https://docs.rs/url/*/url/struct.Url.html#method.set_query
