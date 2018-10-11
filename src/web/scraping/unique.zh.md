
## 从MyaWiKi标记提取所有唯一链接

[![reqwest-badge]][reqwest] [![regex-badge]][regex] [![cat-net-badge]][cat-net]

使用MyaWiKi页面的源代码[`reqwest::get`]然后查找内部和外部链接的所有条目[`Regex::captures_iter`]. 使用[`Cow`]避免过度[`String`]分配.

描述了MyaWiKi链接语法[在这里][mediawiki link syntax].

```rust,no_run
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate lazy_static;
extern crate reqwest;
extern crate regex;

use std::io::Read;
use std::collections::HashSet;
use std::borrow::Cow;
use regex::Regex;

# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#         Reqwest(reqwest::Error);
#         Regex(regex::Error);
#     }
# }
#
fn extract_links(content: &str) -> Result<HashSet<Cow<str>>> {
    lazy_static! {
        static ref WIKI_REGEX: Regex =
            Regex::new(r"(?x)
                \[\[(?P<internal>[^\[\]|]*)[^\[\]]*\]\]    # internal links
                |
                (url=|URL\||\[)(?P<external>http.*?)[ \|}] # external links
            ").unwrap();
    }

    let links: HashSet<_> = WIKI_REGEX
        .captures_iter(content)
        .map(|c| match (c.name("internal"), c.name("external")) {
            (Some(val), None) => Cow::from(val.as_str().to_lowercase()),
            (None, Some(val)) => Cow::from(val.as_str()),
            _ => unreachable!(),
        })
        .collect();

    Ok(links)
}

fn run() -> Result<()> {
    let mut content = String::new();
    reqwest::get(
        "https://en.wikipedia.org/w/index.php?title=Rust_(programming_language)&action=raw",
    )?
        .read_to_string(&mut content)?;

    println!("{:#?}", extract_links(&content)?);

    Ok(())
}
#
# quick_main!(run);
```

[`cow`]: https://doc.rust-lang.org/std/borrow/enum.Cow.html

[`reqwest::get`]: https://docs.rs/reqwest/*/reqwest/fn.get.html

[`regex::captures_iter`]: https://docs.rs/regex/*/regex/struct.Regex.html#method.captures_iter

[`string`]: https://doc.rust-lang.org/std/string/struct.String.html

[mediawiki link syntax]: https://www.mediawiki.org/wiki/Help:Links
