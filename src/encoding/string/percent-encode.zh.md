
## 百分比编码字符串

[![url-badge]][url] [![cat-encoding-badge]][cat-encoding]

使用编码输入字符串[百分号编码-]使用[`utf8_percent_encode`]功能来自`percent-encoding`箱.然后使用.解码[`percent_decode`]功能.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate url;

use url::percent_encoding::{utf8_percent_encode, percent_decode, DEFAULT_ENCODE_SET};
#
# error_chain! {
#     foreign_links {
#         Utf8(std::str::Utf8Error);
#     }
# }

fn run() -> Result<()> {
    let input = "confident, productive systems programming";

    let iter = utf8_percent_encode(input, DEFAULT_ENCODE_SET);
    let encoded: String = iter.collect();
    assert_eq!(encoded, "confident,%20productive%20systems%20programming");

    let iter = percent_decode(encoded.as_bytes());
    let decoded = iter.decode_utf8()?;
    assert_eq!(decoded, "confident, productive systems programming");

    Ok(())
}
#
# quick_main!(run);
```

编码集定义了哪些字节(除了非ASCII和控件之外)需要进行百分比编码.该集的选择取决于上下文.例如,`url`编码`?`在URL路径中但不在查询字符串中.

encoding的返回值是迭代器`&str`收集成的切片`String`.

[`percent_decode`]: https://docs.rs/percent-encoding/*/percent_encoding/fn.percent_decode.html

[`utf8_percent_encode`]: https://docs.rs/percent-encoding/*/percent_encoding/fn.utf8_percent_encode.html

[percent-encoding]: https://en.wikipedia.org/wiki/Percent-encoding
