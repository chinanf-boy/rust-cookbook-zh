## 使用自定义记录器，记录消息

[![log-badge]][log] [![cat-debugging-badge]][cat-debugging]

实现一个自定义记录器`ConsoleLogger`，它打印到 stdout。为了使用记录的宏，`ConsoleLogger`实现[`log::Log`] trait，那么[`log::set_logger`]就能安装它了。

```rust
#[macro_use]
extern crate log;

use log::{Record, Level, Metadata, LevelFilter, SetLoggerError};

static CONSOLE_LOGGER: ConsoleLogger = ConsoleLogger;

struct ConsoleLogger;

impl log::Log for ConsoleLogger {
  fn enabled(&self, metadata: &Metadata) -> bool {
     metadata.level() <= Level::Info
    }

    fn log(&self, record: &Record) {
        if self.enabled(record.metadata()) {
            println!("Rust says: {} - {}", record.level(), record.args());
        }
    }

    fn flush(&self) {}
}

fn main() -> Result<(), SetLoggerError> {
    log::set_logger(&CONSOLE_LOGGER)?;
    log::set_max_level(LevelFilter::Info);

    info!("hello log");
    warn!("warning");
    error!("oops");
    Ok(())
}
```

[`log::log`]: https://docs.rs/log/*/log/trait.Log.html
[`log::set_logger`]: https://docs.rs/log/*/log/fn.set_logger.html
