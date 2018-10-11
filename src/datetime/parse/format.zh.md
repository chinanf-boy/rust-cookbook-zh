
## 显示格式化的日期和时间

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

以UTC为单位获取并显示当前时间[`Utc::now`].以众所周知的格式格式化当前时间[RFC 2822]运用[`DateTime::to_rfc2822`]和[RFC 3339]运用[`DateTime::to_rfc3339`],并以自定义格式使用[`DateTime::format`].

```rust
extern crate chrono;
use chrono::{DateTime, Utc};

fn main() {
    let now: DateTime<Utc> = Utc::now();

    println!("UTC now is: {}", now);
    println!("UTC now in RFC 2822 is: {}", now.to_rfc2822());
    println!("UTC now in RFC 3339 is: {}", now.to_rfc3339());
    println!("UTC now in a custom format is: {}", now.format("%a %b %e %T %Y"));
}
```

[`datetime::format`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.format

[`datetime::to_rfc2822`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.to_rfc2822

[`datetime::to_rfc3339`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.to_rfc3339

[`utc::now`]: https://docs.rs/chrono/*/chrono/offset/struct.Utc.html#method.now

[rfc 2822]: https://www.ietf.org/rfc/rfc2822.txt

[rfc 3339]: https://www.ietf.org/rfc/rfc3339.txt
