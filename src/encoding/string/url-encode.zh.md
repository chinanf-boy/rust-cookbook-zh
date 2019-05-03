## 将字符串编码为application/x-www-form-urlencoded

[![url-badge]][url] [![cat-encoding-badge]][cat-encoding]

将字符串编码为[应用程序/X-WWW-FORM-URLENCODED]语法使用[`form_urlencoded::byte_serialize`]然后用[`form_urlencoded::parse`]. 两个函数都返回迭代器，这些迭代器收集到`String`.

```rust
extern crate url;
use url::form_urlencoded::{byte_serialize, parse};

fn main() {
    let urlencoded: String = byte_serialize("What is ❤?".as_bytes()).collect();
    assert_eq!(urlencoded, "What+is+%E2%9D%A4%3F");
    println!("urlencoded:'{}'", urlencoded);

    let decoded: String = parse(urlencoded.as_bytes())
        .map(|(key, val)| [key, val].concat())
        .collect();
    assert_eq!(decoded, "What is ❤?");
    println!("decoded:'{}'", decoded);
}
```

[`form_urlencoded::byte_serialize`]: https://docs.rs/url/*/url/form_urlencoded/fn.byte_serialize.html

[`form_urlencoded::parse`]: https://docs.rs/url/*/url/form_urlencoded/fn.parse.html

[application/x-www-form-urlencoded]: https://url.spec.whatwg.org/#application/x-www-form-urlencoded
