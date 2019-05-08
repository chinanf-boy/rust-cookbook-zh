## 将字符串解析为 datetime 结构

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

解析已知的字符串表达格式[RFC 2822]，[RFC 3339]和自定义格式，将其变为一个[`DateTime`]结构，可以分别使用[`DateTime::parse_from_rfc2822`]，[`DateTime::parse_from_rfc3339`]和[`DateTime::parse_from_str`]。

可以在[`chrono::format::strftime`]找到，转义序列，让其可用于[`DateTime::format`]。 请注意[`DateTime::parse_from_str`]要求一个 DateTime 结构，必须是创建的，唯一标识的日期和时间。请使用[`NaiveDate`]，[`NaiveTime`]和[`NaiveDateTime`]，分析没有时区的日期和时间。

```rust
extern crate chrono;
use chrono::{DateTime, NaiveDate, NaiveDateTime, NaiveTime};
use chrono::format::ParseError;


fn main() -> Result<(), ParseError> {
    let rfc2822 = DateTime::parse_from_rfc2822("Tue, 1 Jul 2003 10:52:37 +0200")?;
    println!("{}", rfc2822);

    let rfc3339 = DateTime::parse_from_rfc3339("1996-12-19T16:39:57-08:00")?;
    println!("{}", rfc3339);

    let custom = DateTime::parse_from_str("5.8.1994 8:00 am +0000", "%d.%m.%Y %H:%M %P %z")?;
    println!("{}", custom);

    let time_only = NaiveTime::parse_from_str("23:56:04", "%H:%M:%S")?;
    println!("{}", time_only);

    let date_only = NaiveDate::parse_from_str("2015-09-05", "%Y-%m-%d")?;
    println!("{}", date_only);

    let no_timezone = NaiveDateTime::parse_from_str("2015-09-05 23:56:04", "%Y-%m-%d %H:%M:%S")?;
    println!("{}", no_timezone);

    Ok(())
}
```

[`chrono::format::strftime`]: https://docs.rs/chrono/*/chrono/format/strftime/index.html
[`datetime::format`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.format
[`datetime::parse_from_rfc2822`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.parse_from_rfc2822
[`datetime::parse_from_rfc3339`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.parse_from_rfc3339
[`datetime::parse_from_str`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.parse_from_str
[`datetime::to_rfc2822`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.to_rfc2822
[`datetime::to_rfc3339`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.to_rfc3339
[`datetime`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html
[`naivedate`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveDate.html
[`naivedatetime`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveDateTime.html
[`naivetime`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveTime.html
[rfc 2822]: https://www.ietf.org/rfc/rfc2822.txt
[rfc 3339]: https://www.ietf.org/rfc/rfc3339.txt
