## 登录到 stdout 而不是 stderr

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

使用[`Builder::target`]创建一个自定义记录器配置，将日志输出的目标设置为[`Target::Stdout`]。

```rust
#[macro_use]
extern crate log;
extern crate env_logger;

use env_logger::{Builder, Target};

fn main() {
    Builder::new()
        .target(Target::Stdout)
        .init();

    error!("This error has been printed to Stdout");
}
```

[`builder::target`]: https://docs.rs/env_logger/*/env_logger/struct.Builder.html#method.target
[`target::stdout`]: https://docs.rs/env_logger/*/env_logger/fmt/enum.Target.html
