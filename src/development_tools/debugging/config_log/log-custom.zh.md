## 将消息记录，到自定义位置

[![log-badge]][log] [![log4rs-badge]][log4rs] [![cat-debugging-badge]][cat-debugging]

[log4rs]能配置日志记录，输出到自定义的位置。[log4rs]可以使用外部 yaml 文件，或一个生成器配置。

使用[`log4rs::append::file::FileAppender`]创建一个日志配置。该配置继续使用来自[`log4rs::encode::pattern`]的自定义模式，进行编码，要知道，这个配置其实是定义日录记录目标的附加项。待会，还要将附加项配置，分配给[`log4rs::config::Config`]，并设置默认值[`log::LevelFilter`]。

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
