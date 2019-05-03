## 将本地时间转换为其他时区

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

获取本地时间并使用[`offset::Local::now`]然后使用[`DateTime::from_utc`]结构方法。然后使用[`offset::FixedOffset`]然后结构和UTC时间转换为UTC+8和UTC-2。

```rust
extern crate chrono;

use chrono::{DateTime, FixedOffset, Local, Utc};

fn main() {
    let local_time = Local::now();
    let utc_time = DateTime::<Utc>::from_utc(local_time.naive_utc(), Utc);
    let china_timezone = FixedOffset::east(8 * 3600);
    let rio_timezone = FixedOffset::west(2 * 3600);
    println!("Local time now is {}", local_time);
    println!("UTC time now is {}", utc_time);
    println!(
        "Time in Hong Kong now is {}",
        utc_time.with_timezone(&china_timezone)
    );
    println!("Time in Rio de Janeiro now is {}", utc_time.with_timezone(&rio_timezone));
}
```

[`datetime::from_utc`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.from_utc

[`offset::fixedoffset`]: https://docs.rs/chrono/*/chrono/offset/struct.FixedOffset.html

[`offset::local::now`]: https://docs.rs/chrono/*/chrono/offset/struct.Local.html#method.now
