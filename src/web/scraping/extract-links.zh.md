## 从网页 HTML 中，提取所有链接

[![reqwest-badge]][reqwest] [![select-badge]][select] [![cat-net-badge]][cat-net]

使用[`reqwest::get`]，去执行一个 HTTP GET 请求，然后使用[`Document::from_read`]将响应解析为 HTML 文档。拿[`find`]，配上[`Name`]标准“a”，检索所有链接。在[`Selection`]上，调用[`filter_map`]留下链接中 URL，包含“href”[`attr`](attribute)的。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate reqwest;
extern crate select;

use select::document::Document;
use select::predicate::Name;
#
# error_chain! {
#    foreign_links {
#        ReqError(reqwest::Error);
#        IoError(std::io::Error);
#    }
# }

fn run() -> Result<()> {
    let res = reqwest::get("https://www.rust-lang.org/en-US/")?;

    Document::from_read(res)?
        .find(Name("a"))
        .filter_map(|n| n.attr("href"))
        .for_each(|x| println!("{}", x));

    Ok(())
}
#
# quick_main!(run);
```

[`attr`]: https://docs.rs/select/*/select/node/struct.Node.html#method.attr
[`document::from_read`]: https://docs.rs/select/*/select/document/struct.Document.html#method.from_read
[`filter_map`]: https://doc.rust-lang.org/core/iter/trait.Iterator.html#method.filter_map
[`find`]: https://docs.rs/select/*/select/document/struct.Document.html#method.find
[`name`]: https://docs.rs/select/*/select/predicate/struct.Name.html
[`reqwest::get`]: https://docs.rs/reqwest/*/reqwest/fn.get.html
[`selection`]: https://docs.rs/select/*/select/selection/struct.Selection.html
