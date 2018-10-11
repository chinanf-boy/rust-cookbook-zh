
## 使用自定义记录器记录消息

[![log-badge]][log] [![cat-debugging-badge]][cat-debugging]

实现自定义记录器`ConsoleLogger`打印到stdout.为了使用日志记录宏,`ConsoleLogger`实现[`log::Log`]特质和[`log::set_logger`]安装它.

```rust
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate log;

use log::{Record, Level, Metadata, LevelFilter};

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
#
# error_chain! {
#     foreign_links {
#         SetLogger(log::SetLoggerError);
#     }
# }

fn run() -> Result<()> {
    log::set_logger(&CONSOLE_LOGGER)?;
    log::set_max_level(LevelFilter::Info);

    info!("hello log");
    warn!("warning");
    error!("oops");
    Ok(())
}
#
# quick_main!(run);
```

[`log::log`]: https://docs.rs/log/*/log/trait.Log.html

[`log::set_logger`]: https://docs.rs/log/*/log/fn.set_logger.html
