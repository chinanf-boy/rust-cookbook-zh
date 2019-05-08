## 将日期转换为 Unix 时间戳，反之亦然

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

[`NaiveDate::from_ymd`]和[`NaiveTime::from_hms`]给出一个日期，用[`NaiveDateTime::timestamp`]转换到[UNIX 时间戳][unix timestamp]。然后使用[`NaiveDateTime::from_timestamp`]，它计算从 1970 1，01 0:00:00 UTC 开始，10 亿秒后的日期。

```rust
extern crate chrono;

use chrono::{NaiveDate, NaiveDateTime};

fn main() {
    let date_time: NaiveDateTime = NaiveDate::from_ymd(2017, 11, 12).and_hms(17, 33, 44);
    println!(
        "Number of seconds between 1970-01-01 00:00:00 and {} is {}.",
        date_time, date_time.timestamp());

    let date_time_after_a_billion_seconds = NaiveDateTime::from_timestamp(1_000_000_000, 0);
    println!(
        "Date after a billion seconds since 1970-01-01 00:00:00 was {}.",
        date_time_after_a_billion_seconds);
}
```

[`naivedate::from_ymd`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveDate.html#method.from_ymd
[`naivedatetime::from_timestamp`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveDateTime.html#method.from_timestamp
[`naivedatetime::timestamp`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveDateTime.html#method.timestamp
[`naivetime::from_hms`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveTime.html#method.from_hms
[unix timestamp]: https://en.wikipedia.org/wiki/Unix_time
