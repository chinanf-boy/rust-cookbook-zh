## 检查API资源是否存在

[![reqwest-badge]][reqwest] [![cat-net-badge]][cat-net]

使用头请求查询GitHub用户终结点（[`Client::head`]）然后检查响应代码以确定是否成功。这是一种无需接收主体即可快速查询REST资源的方法。[`reqwest::Client`]与…合作[`ClientBuilder::timeout`]确保请求的持续时间不会超过超时。

```rust,no_run
extern crate reqwest;

use reqwest::Error;
use std::time::Duration;
use reqwest::ClientBuilder;


fn main() -> Result<(), Error> {
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
```

[`client::head`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html#method.head

[`clientbuilder::timeout`]: https://docs.rs/reqwest/*/reqwest/struct.ClientBuilder.html#method.timeout

[`reqwest::client`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html
