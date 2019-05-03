## 处理限速API

[![reqwest-badge]][reqwest] [![hyper-badge]][hyper] [![cat-net-badge]][cat-net]

此示例使用[Github API-速率限制]作为如何处理远程服务器错误的示例。此示例使用[`hyper::header!`]要分析响应头并检查的宏[`reqwest::StatusCode::Forbidden`]. 如果响应超过速率限制，则示例将等待并重试。

```rust,no_run,ignore
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate hyper;
extern crate reqwest;

use std::time::{Duration, UNIX_EPOCH};
use std::thread;
use reqwest::StatusCode;
#
# error_chain! {
#    foreign_links {
#        Io(std::io::Error);
#        Time(std::time::SystemTimeError);
#        Reqwest(reqwest::Error);
#    }
# }

header! { (XRateLimitLimit, "X-RateLimit-Limit") => [usize] }
header! { (XRateLimitRemaining, "X-RateLimit-Remaining") => [usize] }
header! { (XRateLimitReset, "X-RateLimit-Reset") => [u64] }

fn run() -> Result<()> {
    let url = "https://api.github.com/users/rust-lang-nursery ";
    let client = reqwest::Client::new();
    let response = client.get(url).send()?;

    let rate_limit = response.headers().get::<XRateLimitLimit>().ok_or(
        "response doesn't include the expected X-RateLimit-Limit header",
    )?;

    let rate_remaining = response.headers().get::<XRateLimitRemaining>().ok_or(
        "response doesn't include the expected X-RateLimit-Remaining header",
    )?;

    let rate_reset_at = response.headers().get::<XRateLimitReset>().ok_or(
        "response doesn't include the expected X-RateLimit-Reset header",
    )?;

    let rate_reset_within = Duration::from_secs(**rate_reset_at) - UNIX_EPOCH.elapsed()?;

    if response.status() == StatusCode::Forbidden && **rate_remaining == 0 {
        println!("Sleeping for {} seconds.", rate_reset_within.as_secs());
        thread::sleep(rate_reset_within);
        return run();
    }
    else {
        println!(
            "Rate limit is currently {}/{}, the reset of this limit will be within {} seconds.",
            **rate_remaining,
            **rate_limit,
            rate_reset_within.as_secs(),
        );
    }

    Ok(())
}
#
# quick_main!(run);
```

[`hyper::header!`]: https://doc.servo.org/hyper/header/index.html#defining-custom-headers

[`reqwest::statuscode::forbidden`]: https://docs.rs/reqwest/*/reqwest/struct.StatusCode.html#associatedconstant.FORBIDDEN
