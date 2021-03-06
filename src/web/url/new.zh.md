## 从一个 base URL ，创建新的 URL

[![url-badge]][url] [![cat-net-badge]][cat-net]

这个[`join`]方法，用 base 路径和相对路径，创建新的 URL。

```rust
extern crate url;

use url::{Url, ParseError};

fn main() -> Result<(), ParseError> {
    let path = "/rust-lang/cargo";

    let gh = build_github_url(path)?;

    assert_eq!(gh.as_str(), "https://github.com/rust-lang/cargo");
    println!("The joined URL is: {}", gh);

    Ok(())
}

fn build_github_url(path: &str) -> Result<Url, ParseError> {
    const GITHUB: &'static str = "https://github.com";

    let base = Url::parse(GITHUB).expect("hardcoded URL is known to be valid");
    let joined = base.join(path)?;

    Ok(joined)
}
```

[`join`]: https://docs.rs/url/*/url/struct.Url.html#method.join
