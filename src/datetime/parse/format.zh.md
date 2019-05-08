## 显示格式化的日期和时间

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

使用[`Utc::now`]，获取并显示当前时间（以 UTC 为单位）。以众所周知的格式[RFC 2822]，格式化当前时间，通过[`DateTime::to_rfc2822`]。还有[RFC 3339]格式，可以使用[`DateTime::to_rfc3339`]，除此之外，用[`DateTime::format`]可以自定义格式。

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
