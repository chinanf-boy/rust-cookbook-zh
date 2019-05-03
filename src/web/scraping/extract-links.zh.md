## 从网页HTML中提取所有链接

[![reqwest-badge]][reqwest] [![select-badge]][select] [![cat-net-badge]][cat-net]

使用[`reqwest::get`]执行HTTP GET请求，然后使用[`Document::from_read`]将响应解析为HTML文档。[`find`]以…为标准[`Name`]是“A”检索所有链接。呼叫[`filter_map`]上[`Selection`]从包含“href”的链接中检索URL[`attr`](attribute).

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
