## POST 一个文件，到 paste.rs

[![reqwest-badge]][reqwest] [![cat-net-badge]][cat-net]

[`reqwest::Client`]建立起到 <https://paste.rs> 的一个连接，遵循着[`reqwest::RequestBuilder`]模式。调用[`Client::post`]，加上 目标 URL 参数，[`RequestBuilder::body`]通过读取文件，设置要发送的内容，以及[`RequestBuilder::send`]会堵塞，直到文件上载并返回响应。[`read_to_string`]返回响应，并显示在控制台中。

```rust,no_run
extern crate reqwest;

# #[macro_use]
# extern crate error_chain;
#
use std::fs::File;
use std::io::Read;
use reqwest::Client;
#
# error_chain! {
#     foreign_links {
#         HttpRequest(reqwest::Error);
#         IoError(::std::io::Error);
#     }
# }

fn run() -> Result<()> {
    let paste_api = "https://paste.rs";
    let file = File::open("message")?;

    let mut response = Client::new().post(paste_api).body(file).send()?;
    let mut response_body = String::new();
    response.read_to_string(&mut response_body)?;
    println!("Your paste is located at: {}", response_body);
    Ok(())
}
#
# quick_main!(run);
```

[`client::post`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html#method.post
[`read_to_string`]: https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_string
[`requestbuilder::body`]: https://docs.rs/reqwest/*/reqwest/struct.RequestBuilder.html#method.body
[`requestbuilder::send`]: https://docs.rs/reqwest/*/reqwest/struct.RequestBuilder.html#method.send
[`reqwest::client`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html
[`reqwest::requestbuilder`]: https://docs.rs/reqwest/*/reqwest/struct.RequestBuilder.html
