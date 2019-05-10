## URL 编码字符串

[![url-badge]][url] [![cat-encoding-badge]][cat-encoding]

编码一个输入字符串，编码方式为[URL 编码][percent-encoding]，可通过使用来自`url`箱子的[`utf8_percent_encode`]函数完成。然后再使用[`percent_decode`]函数。

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

该编码集定义哪些字节（除了非 ASCII 和控制键位之外）需要 URL 编码。此集合的选择取决于上下文。例如，`url`会编码 URL 路径中的`?`，但不会在查询字符串。

编码的返回值是，`&str`切片的迭代器，这能收集（collect）成一个`String`。

[`percent_decode`]: https://docs.rs/percent-encoding/*/percent_encoding/fn.percent_decode.html
[`utf8_percent_encode`]: https://docs.rs/percent-encoding/*/percent_encoding/fn.utf8_percent_encode.html
[percent-encoding]: https://en.wikipedia.org/wiki/Percent-encoding
