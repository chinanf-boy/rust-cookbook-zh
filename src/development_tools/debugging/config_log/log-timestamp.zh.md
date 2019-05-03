## 在日志消息中包含时间戳

[![log-badge]][log] [![env_logger-badge]][env_logger] [![chrono-badge]][chrono] [![cat-debugging-badge]][cat-debugging]

使用创建自定义记录器配置[`Builder`]. 每个日志条目调用[`Local::now`]获取电流[`DateTime`]在本地时区和使用[`DateTime::format`]具有[`strftime::specifiers`]格式化在最终日志中使用的时间戳。

示例调用[`Builder::format`]要设置一个闭包，用时间戳格式化每个消息文本，[`Record::level`]和身体[`Record::args`]）

```rust
#[macro_use]
extern crate log;
extern crate chrono;
extern crate env_logger;

use std::io::Write;
use chrono::Local;
use env_logger::Builder;
use log::LevelFilter;

fn main() {
    Builder::new()
        .format(|buf, record| {
            writeln!(buf,
                "{} [{}] - {}",
                Local::now().format("%Y-%m-%dT%H:%M:%S"),
                record.level(),
                record.args()
            )
        })
        .filter(None, LevelFilter::Info)
        .init();

    warn!("warn");
    info!("info");
    debug!("debug");
}
```

stderr输出将包含

```
2017-05-22T21:57:06 [WARN] - warn
2017-05-22T21:57:06 [INFO] - info
```

[`datetime::format`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.format

[`datetime`]: https://docs.rs/chrono/*/chrono/datetime/struct.DateTime.html

[`local::now`]: https://docs.rs/chrono/*/chrono/offset/struct.Local.html#method.now

[`builder`]: https://docs.rs/env_logger/*/env_logger/struct.Builder.html

[`builder::format`]: https://docs.rs/env_logger/*/env_logger/struct.Builder.html#method.format

[`record::args`]: https://docs.rs/log/*/log/struct.Record.html#method.args

[`record::level`]: https://docs.rs/log/*/log/struct.Record.html#method.level

[`strftime::specifiers`]: https://docs.rs/chrono/*/chrono/format/strftime/index.html#specifiers
