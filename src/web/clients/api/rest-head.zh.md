
## 检查是否存在API资源

[![reqwest-badge]][reqwest] [![cat-net-badge]][cat-net]

使用头部请求查询GITHUB用户端点([`Client::head`]然后检查响应代码以确定成功.这是一种快速查询REST资源而不需要接收体的方法.[`reqwest::Client`]与…合作[`ClientBuilder::timeout`]确保请求不会持续超过超时时间.

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate reqwest;

use std::time::Duration;
use reqwest::ClientBuilder;
#
# error_chain! {
#     foreign_links {
#         Reqwest(reqwest::Error);
#     }
# }

fn run() -> Result<()> {
    let user = "ferris-the-crab";
    let request_url = format!("https://api.github.com/users/{}", user);
    println!("{}", request_url);

    let timeout = Duration::new(5, 0);
    let client = ClientBuilder::new().timeout(timeout).build()?;
    let response = client.head(&request_url).send()?;

    if response.status().is_success() {
        println!("{} is a user!", user);
    } else {
        println!("{} is not a user!", user);
    }

    Ok(())
}
#
# quick_main!(run);
```

[`client::head`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html#method.head

[`clientbuilder::timeout`]: https://docs.rs/reqwest/*/reqwest/struct.ClientBuilder.html#method.timeout

[`reqwest::client`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html
