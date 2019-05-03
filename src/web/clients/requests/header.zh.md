## 为REST请求设置自定义头和URL参数

[![reqwest-badge]][reqwest] [![hyper-badge]][hyper] [![url-badge]][url] [![cat-net-badge]][cat-net]

为HTTP GET请求设置标准和自定义HTTP头以及URL参数。创建类型为的自定义页眉`XPoweredBy`具有[`hyper::header!`]宏。

使用生成复杂的URL[`Url::parse_with_params`].  设置标准标题[`header::UserAgent`]，[`header::Authorization`]和习俗`XPoweredBy`具有[`RequestBuilder::header`]然后用[`RequestBuilder::send`].

请求目标<http://httpbin.org/headers>服务，它用包含所有请求头的JSON dict响应，以便于验证。

```rust,no_run,ignore
# #[macro_use]
# extern crate error_chain;
extern crate url;
extern crate reqwest;
#[macro_use]
extern crate hyper;
#[macro_use]
extern crate serde_derive;

use std::collections::HashMap;
use url::Url;
use reqwest::Client;
use reqwest::header::{UserAgent, Authorization, Bearer};

header! { (XPoweredBy, "X-Powered-By") => [String] }

#[derive(Deserialize, Debug)]
pub struct HeadersEcho {
    pub headers: HashMap<String, String>,
}
#
# error_chain! {
#     foreign_links {
#         Reqwest(reqwest::Error);
#         UrlParse(url::ParseError);
#     }
# }

fn run() -> Result<()> {
    let url = Url::parse_with_params("http://httpbin.org/headers",
                                     &[("lang", "rust"), ("browser", "servo")])?;

    let mut response = Client::new()
        .get(url)
        .header(UserAgent::new("Rust-test"))
        .header(Authorization(Bearer { token: "DEadBEEfc001cAFeEDEcafBAd".to_owned() }))
        .header(XPoweredBy("Guybrush Threepwood".to_owned()))
        .send()?;

    let out: HeadersEcho = response.json()?;
    assert_eq!(out.headers["Authorization"],
               "Bearer DEadBEEfc001cAFeEDEcafBAd");
    assert_eq!(out.headers["User-Agent"], "Rust-test");
    assert_eq!(out.headers["X-Powered-By"], "Guybrush Threepwood");
    assert_eq!(response.url().as_str(),
               "http://httpbin.org/headers?lang=rust&browser=servo");

    println!("{:?}", out);
    Ok(())
}
#
# quick_main!(run);
```

[`header::authorization`]: https://doc.servo.org/hyper/header/struct.Authorization.html

[`header::useragent`]: https://doc.servo.org/hyper/header/struct.UserAgent.html

[`hyper::header!`]: https://doc.servo.org/hyper/macro.header.html

[`requestbuilder::header`]: https://docs.rs/reqwest/*/reqwest/struct.RequestBuilder.html#method.header

[`requestbuilder::send`]: https://docs.rs/reqwest/*/reqwest/struct.RequestBuilder.html#method.send

[`url::parse_with_params`]: https://docs.rs/url/*/url/struct.Url.html#method.parse_with_params
