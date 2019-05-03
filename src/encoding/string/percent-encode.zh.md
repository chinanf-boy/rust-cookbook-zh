## 百分比编码字符串

[![url-badge]][url] [![cat-encoding-badge]][cat-encoding]

输入字符串的编码方式[百分比编码-]使用[`utf8_percent_encode`]函数来自`url`机箱。然后使用[`percent_decode`]功能。

```rust
extern crate url;

use url::percent_encoding::{utf8_percent_encode, percent_decode, DEFAULT_ENCODE_SET};
use std::str::Utf8Error;

fn main() -> Result<(), Utf8Error> {
    let input = "confident, productive systems programming";

    let iter = utf8_percent_encode(input, DEFAULT_ENCODE_SET);
    let encoded: String = iter.collect();
    assert_eq!(encoded, "confident,%20productive%20systems%20programming");

    let iter = percent_decode(encoded.as_bytes());
    let decoded = iter.decode_utf8()?;
    assert_eq!(decoded, "confident, productive systems programming");

    Ok(())
}
```

编码集定义哪些字节（除了非ASCII和控件之外）需要百分比编码。此集合的选择取决于上下文。例如，`url`编码`?`在URL路径中，但不在查询字符串中。

编码的返回值是的迭代器`&str`切片收集成`String`.

[`percent_decode`]: https://docs.rs/percent-encoding/*/percent_encoding/fn.percent_decode.html

[`utf8_percent_encode`]: https://docs.rs/percent-encoding/*/percent_encoding/fn.utf8_percent_encode.html

[percent-encoding]: https://en.wikipedia.org/wiki/Percent-encoding
