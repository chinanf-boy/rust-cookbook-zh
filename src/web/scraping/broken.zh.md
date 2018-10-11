
## 检查网页断链

[![reqwest-badge]][reqwest] [![select-badge]][select] [![url-badge]][url] [![cat-net-badge]][cat-net]

呼叫`get_base_url`检索基本URL.如果文档具有基本标记,则获取HERF.[`attr`]从基础标签.[`Position::BeforePath`]原始URL充当默认值.

迭代文档中的链接并解析[`url::ParseOptions`]和[`Url::parse`])向ReqWestern链接请求并验证[`StatusCode`].

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate reqwest;
extern crate select;
extern crate url;

use std::collections::HashSet;

use url::{Url, Position};
use reqwest::StatusCode;
use select::document::Document;
use select::predicate::Name;
#
# error_chain! {
#   foreign_links {
#       ReqError(reqwest::Error);
#       IoError(std::io::Error);
#       UrlParseError(url::ParseError);
#   }
# }

fn get_base_url(url: &Url, doc: &Document) -> Result<Url> {
    let base_tag_href = doc.find(Name("base")).filter_map(|n| n.attr("href")).nth(0);

    let base_url = base_tag_href.map_or_else(
        || Url::parse(&url[..Position::BeforePath]),
        Url::parse,
    )?;

    Ok(base_url)
}

fn check_link(url: &Url) -> Result<bool> {
    let res = reqwest::get(url.as_ref())?;

    Ok(res.status() != StatusCode::NOT_FOUND)
}

fn run() -> Result<()> {
    let url = Url::parse("https://www.rust-lang.org/en-US/")?;

    let res = reqwest::get(url.as_ref())?;
    let document = Document::from_read(res)?;

    let base_url = get_base_url(&url, &document)?;

    let base_parser = Url::options().base_url(Some(&base_url));

    let links: HashSet<Url> = document
        .find(Name("a"))
        .filter_map(|n| n.attr("href"))
        .filter_map(|link| base_parser.parse(link).ok())
        .collect();

    links
        .iter()
        .filter(|link| check_link(link).ok() == Some(false))
        .for_each(|x| println!("{} is broken.", x));

    Ok(())
}
#
# quick_main!(run);
```

[`attr`]: https://docs.rs/select/*/select/node/struct.Node.html#method.attr

[`position::beforepath`]: https://docs.rs/url/*/url/enum.Position.html#variant.BeforePath

[`statuscode`]: https://docs.rs/reqwest/*/reqwest/struct.StatusCode.html

[`url::parse`]: https://docs.rs/url/*/url/struct.Url.html#method.parse

[`url::parseoptions`]: https://docs.rs/url/*/url/struct.ParseOptions.html
