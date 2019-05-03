## 通过删除路径段创建基URL

[![url-badge]][url] [![cat-net-badge]][cat-net]

基本URL包括协议和域。基本URL没有文件夹、文件或查询字符串。这些项中的每一项都将从给定的URL中剥离出来。[`PathSegmentsMut::clear`]删除路径和[`Url::set_query`]删除查询字符串。

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
