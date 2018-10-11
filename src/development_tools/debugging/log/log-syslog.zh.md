
## 登录Unix syslog

[![log-badge]][log] [![syslog-badge]][syslog] [![cat-debugging-badge]][cat-debugging]

将消息记录到[UNIX syslog].使用初始化记录器后端[`syslog::init`].[`syslog::Facility`]记录提交日志条目分类的程序,[`log::LevelFilter`]表示允许的日志详细程度和`Option<&str>`拥有可选的应用程序名

```rust
# #![allow(unused_imports)]
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate log;
# #[cfg(target_os = "linux")]
extern crate syslog;

# #[cfg(target_os = "linux")]
use syslog::Facility;
#
# #[cfg(target_os = "linux")]
# error_chain! {
#     foreign_links {
#         SetLogger(syslog::Error);
#     }
# }

# #[cfg(target_os = "linux")]
fn run() -> Result<()> {
    syslog::init(Facility::LOG_USER,
                 log::LevelFilter::Debug,
                 Some("My app name"))?;
    debug!("this is a debug {}", "message");
    error!("this is an error!");
    Ok(())
}
#
# #[cfg(not(target_os = "linux"))]
# error_chain! {}
# #[cfg(not(target_os = "linux"))]
# fn run() -> Result<()> {
#     Ok(())
# }
#
# quick_main!(run);
```

[`log::levelfilter`]: https://docs.rs/log/*/log/enum.LevelFilter.html

[`syslog::facility`]: https://docs.rs/syslog/*/syslog/enum.Facility.html

[`syslog::init`]: https://docs.rs/syslog/*/syslog/fn.init.html

[unix syslog]: https://www.gnu.org/software/libc/manual/html_node/Overview-of-Syslog.html
