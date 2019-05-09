## 登录到 Unix 系统日志

[![log-badge]][log] [![syslog-badge]][syslog] [![cat-debugging-badge]][cat-debugging]

将消息记录到[UNIX 系统日志][unix syslog]。用[`syslog::init`]初始化记录器后端。 [`syslog::Facility`]表明该程序，添加的日志条目分类，[`log::LevelFilter`]表示允许的日志等级，和`Option<&str>`持有可选的应用程序名称。

```rust
#[macro_use]
extern crate log;
# #[cfg(target_os = "linux")]
extern crate syslog;

# #[cfg(target_os = "linux")]
use syslog::{Facility, Error};

# #[cfg(target_os = "linux")]
fn main() -> Result<(), Error> {
    syslog::init(Facility::LOG_USER,
                 log::LevelFilter::Debug,
                 Some("My app name"))?;
    debug!("this is a debug {}", "message");
    error!("this is an error!");
    Ok(())
}

# #[cfg(not(target_os = "linux"))]
# fn main() {
#     println!("So far, only Linux systems are supported.");
# }
```

[`log::levelfilter`]: https://docs.rs/log/*/log/enum.LevelFilter.html
[`syslog::facility`]: https://docs.rs/syslog/*/syslog/enum.Facility.html
[`syslog::init`]: https://docs.rs/syslog/*/syslog/fn.init.html
[unix syslog]: https://www.gnu.org/software/libc/manual/html_node/Overview-of-Syslog.html
