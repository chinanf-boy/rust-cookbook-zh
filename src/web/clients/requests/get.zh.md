## 发出 HTTP GET 请求

[![reqwest-badge]][reqwest] [![cat-net-badge]][cat-net]

解析提供的 URL ，并使用[`reqwest::get`]制作一个同步 HTTP 请求。 打印获得的[`reqwest::Response`]的状态和标头。通过使用[`read_to_string`]，将 HTTP 响应主体，读取到分配的[`String`]。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate reqwest;

use std::io::Read;
#
# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#         HttpRequest(reqwest::Error);
#     }
# }

fn run() -> Result<()> {
    let mut res = reqwest::get("http://httpbin.org/get")?;
    let mut body = String::new();
    res.read_to_string(&mut body)?;

    println!("Status: {}", res.status());
    println!("Headers:\n{:#?}", res.headers());
    println!("Body:\n{}", body);

    Ok(())
}
#
# quick_main!(run);
```

[`read_to_string`]: https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_string
[`reqwest::get`]: https://docs.rs/reqwest/*/reqwest/fn.get.html
[`reqwest::response`]: https://docs.rs/reqwest/*/reqwest/struct.Response.html
[`string`]: https://doc.rust-lang.org/std/string/struct.String.html
