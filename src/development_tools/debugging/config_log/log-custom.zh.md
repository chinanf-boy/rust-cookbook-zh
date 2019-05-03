## 将消息记录到自定义位置

[![log-badge]][log] [![log4rs-badge]][log4rs] [![cat-debugging-badge]][cat-debugging]

[log4rs]将日志输出配置到自定义位置。[log4rs]可以使用外部yaml文件或生成器配置。

使用创建日志配置[`log4rs::append::file::FileAppender`]. 附加器定义日志记录目标。配置继续使用来自的自定义模式进行编码[`log4rs::encode::pattern`]. 将配置分配给[`log4rs::config::Config`]并设置默认值[`log::LevelFilter`].

```rust,no_run
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate log;
extern crate log4rs;

use log::LevelFilter;
use log4rs::append::file::FileAppender;
use log4rs::encode::pattern::PatternEncoder;
use log4rs::config::{Appender, Config, Root};
#
# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#         LogConfig(log4rs::config::Errors);
#         SetLogger(log::SetLoggerError);
#     }
# }

fn run() -> Result<()> {
    let logfile = FileAppender::builder()
        .encoder(Box::new(PatternEncoder::new("{l} - {m}\n")))
        .build("log/output.log")?;

    let config = Config::builder()
        .appender(Appender::builder().build("logfile", Box::new(logfile)))
        .build(Root::builder()
                   .appender("logfile")
                   .build(LevelFilter::Info))?;

    log4rs::init_config(config)?;

    info!("Hello, world!");

    Ok(())
}
#
# quick_main!(run);
```

[`log4rs::append::file::fileappender`]: https://docs.rs/log4rs/*/log4rs/append/file/struct.FileAppender.html

[`log4rs::config::config`]: https://docs.rs/log4rs/*/log4rs/config/struct.Config.html

[`log4rs::encode::pattern`]: https://docs.rs/log4rs/*/log4rs/encode/pattern/index.html

[`log::levelfilter`]: https://docs.rs/log/*/log/enum.LevelFilter.html
