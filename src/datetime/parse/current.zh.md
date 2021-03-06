## 检查日期和时间

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

[`DateTime`]获取当前的 UTC，还有[`Timelike`]，能得到它的小时/分钟/秒（hour/minute/second），通过[`Datelike`]，则能获得它的年/月/日/周末（year/month/day/weekday）。

```rust
extern crate chrono;
use chrono::{Datelike, Timelike, Utc};

fn main() {
    let now = Utc::now();

    let (is_pm, hour) = now.hour12();
    println!(
        "The current UTC time is {:02}:{:02}:{:02} {}",
        hour,
        now.minute(),
        now.second(),
        if is_pm { "PM" } else { "AM" }
    );
    println!(
        "And there have been {} seconds since midnight",
        now.num_seconds_from_midnight()
    );

    let (is_common_era, year) = now.year_ce();
    println!(
        "The current UTC date is {}-{:02}-{:02} {:?} ({})",
        year,
        now.month(),
        now.day(),
        now.weekday(),
        if is_common_era { "CE" } else { "BCE" }
    );
    println!(
        "And the Common Era began {} days ago",
        now.num_days_from_ce()
    );
}
```

[`datelike`]: https://docs.rs/chrono/*/chrono/trait.Datelike.html
[`datetime`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html
[`timelike`]: https://docs.rs/chrono/*/chrono/trait.Timelike.html
