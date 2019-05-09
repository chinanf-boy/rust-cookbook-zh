## 使用自定义环境变量，设置日志记录

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

[`Builder`]配置日志记录。

[`Builder::parse`]解析`MY_APP_LOG`环境变量内容，变为[`RUST_LOG`]语法形式。然后，[`Builder::init`]初始化记录器。所有这些步骤，通常都是由[`env_logger::init`]内部完成。

```rust
#[macro_use]
extern crate log;
extern crate env_logger;

use std::env;
use env_logger::Builder;

fn main() {
    Builder::new()
        .parse(&env::var("MY_APP_LOG").unwrap_or_default())
        .init();

    info!("informational message");
    warn!("warning message");
    error!("this is an error {}", "message");
}
```

[`env_logger::init`]: https://docs.rs/env_logger/*/env_logger/fn.init.html
[`builder`]: https://docs.rs/env_logger/*/env_logger/struct.Builder.html
[`builder::init`]: https://docs.rs/env_logger/*/env_logger/struct.Builder.html#method.init
[`builder::parse`]: https://docs.rs/env_logger/*/env_logger/struct.Builder.html#method.parse
[`rust_log`]: https://docs.rs/env_logger/*/env_logger/#enabling-logging
