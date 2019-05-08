## 执行，检查日期和时间的计算

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

使用[`DateTime::checked_add_signed`]，计算并显示两周后的日期和时间，以及用[`DateTime::checked_sub_signed`]，那天(两周后)，前一天的日期。 如果无法计算日期和时间，则方法返回“None”。

可以在[`chrono::format::strftime`]找到，转义序列，让其可用于[`DateTime::format`]。

```rust
extern crate chrono;
use chrono::{DateTime, Duration, Utc};

fn day_earlier(date_time: DateTime<Utc>) -> Option<DateTime<Utc>> {
    date_time.checked_sub_signed(Duration::days(1))
}

fn main() {
    let now = Utc::now();
    println!("{}", now);

    let almost_three_weeks_from_now = now.checked_add_signed(Duration::weeks(2))
            .and_then(|in_2weeks| in_2weeks.checked_add_signed(Duration::weeks(1)))
            .and_then(day_earlier);

    match almost_three_weeks_from_now {
        Some(x) => println!("{}", x),
        None => eprintln!("Almost three weeks from now overflows!"),
    }

    match now.checked_add_signed(Duration::max_value()) {
        Some(x) => println!("{}", x),
        None => eprintln!("We can't use chrono to tell the time for the Solar System to complete more than one full orbit around the galactic center."),
    }
}
```

[`chrono::format::strftime`]: https://docs.rs/chrono/*/chrono/format/strftime/index.html
[`datetime::checked_add_signed`]: https://docs.rs/chrono/*/chrono/struct.Date.html#method.checked_add_signed
[`datetime::checked_sub_signed`]: https://docs.rs/chrono/*/chrono/struct.Date.html#method.checked_sub_signed
[`datetime::format`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.format
