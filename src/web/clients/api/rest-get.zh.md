## 查询GitHub API

[![reqwest-badge]][reqwest] [![serde-badge]][serde] [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding]

GITHUB查询[stargazers API v3](https://developer.github.com/v3/activity/starring/#list-stargazers)具有[`reqwest::get`]获取用星号标记GitHub项目的所有用户的列表。[`reqwest::Response`]反序列化为[`Response::json`]进入之内`User`实现的对象[`serde::Deserialize`].

```rust,no_run
#[macro_use]
extern crate serde_derive;
extern crate reqwest;
use reqwest::Error;

#[derive(Deserialize, Debug)]
struct User {
    login: String,
    id: u32,
}

fn main() -> Result<(), Error> {
    let request_url = format!("https://api.github.com/repos/{owner}/{repo}/stargazers",
                              owner = "rust-lang-nursery",
                              repo = "rust-cookbook");
    println!("{}", request_url);
    let mut response = reqwest::get(&request_url)?;

    let users: Vec<User> = response.json()?;
    println!("{:?}", users);
    Ok(())
}
```

[`reqwest::get`]: https://docs.rs/reqwest/*/reqwest/fn.get.html

[`reqwest::response`]: https://docs.rs/reqwest/*/reqwest/struct.Response.html

[`response::json`]: https://docs.rs/reqwest/*/reqwest/struct.Response.html#method.json

[`serde::deserialize`]: https://docs.rs/serde/*/serde/trait.Deserialize.html
