## 使用 GitHub API 创建和删除 Gist

[![reqwest-badge]][reqwest] [![serde-badge]][serde] [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding]

创建一个向 Github 发出 POST 请求的 Gist[gists API v3](https://developer.github.com/v3/gists/)使用[`Client::post`]并使用删除请求将其删除[`Client::delete`].

这个[`reqwest::Client`]负责两个请求的详细信息，包括 URL、主体和身份验证。柱体来自[`serde_json::json!`]宏提供任意 JSON 主体。调用给[`RequestBuilder::json`]设置请求正文。[`RequestBuilder::basic_auth`]处理身份验证。呼唤[`RequestBuilder::send`]同步执行请求。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate reqwest;
#[macro_use]
extern crate serde_derive;
#[macro_use]
extern crate serde_json;

use std::env;
use reqwest::Client;
#
# error_chain! {
#     foreign_links {
#         EnvVar(env::VarError);
#         HttpRequest(reqwest::Error);
#     }
# }

#[derive(Deserialize, Debug)]
struct Gist {
    id: String,
    html_url: String,
}

fn run() -> Result<()> {
    let gh_user = env::var("GH_USER")?;
    let gh_pass = env::var("GH_PASS")?;

    let gist_body = json!({
        "description": "the description for this gist",
        "public": true,
        "files": {
             "main.rs": {
             "content": r#"fn main() { println!("hello world!");}"#
            }
        }});

    let request_url = "https://api.github.com/gists";
    let mut response = Client::new()
        .post(request_url)
        .basic_auth(gh_user.clone(), Some(gh_pass.clone()))
        .json(&gist_body)
        .send()?;

    let gist: Gist = response.json()?;
    println!("Created {:?}", gist);

    let request_url = format!("{}/{}",request_url, gist.id);
    let response = Client::new()
        .delete(&request_url)
        .basic_auth(gh_user, Some(gh_pass))
        .send()?;

    println!("Gist {} deleted! Status code: {}",gist.id, response.status());
    Ok(())
}
#
# quick_main!(run);
```

示例使用[HTTP 基本 AUTH]为了授权访问[GitHub API]. 典型的用例将使用更复杂的[奥瑙]授权流程。

[`client::delete`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html#method.delete
[`client::post`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html#method.post
[`requestbuilder::basic_auth`]: https://docs.rs/reqwest/*/reqwest/struct.RequestBuilder.html#method.basic_auth
[`requestbuilder::json`]: https://docs.rs/reqwest/*/reqwest/struct.RequestBuilder.html#method.json
[`requestbuilder::send`]: https://docs.rs/reqwest/*/reqwest/struct.RequestBuilder.html#method.send
[`reqwest::client`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html
[`serde_json::json!`]: https://docs.rs/serde_json/*/serde_json/macro.json.html
[github api]: https://developer.github.com/v3/auth/
[http basic auth]: https://tools.ietf.org/html/rfc2617
[oauth]: https://oauth.net/getting-started/
