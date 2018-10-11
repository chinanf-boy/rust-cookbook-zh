
## 启用每个模块的日志级别

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

创建两个模块`foo`和嵌套`foo::bar`与日志指令分别控制[`RUST_LOG`]环境变量.

```rust
#[macro_use]
extern crate log;
extern crate env_logger;

mod foo {
    mod bar {
        pub fn run() {
            warn!("[bar] warn");
            info!("[bar] info");
            debug!("[bar] debug");
        }
    }

    pub fn run() {
        warn!("[foo] warn");
        info!("[foo] info");
        debug!("[foo] debug");
        bar::run();
    }
}

fn main() {
    env_logger::init();
    warn!("[root] warn");
    info!("[root] info");
    debug!("[root] debug");
    foo::run();
}
```

[`RUST_LOG`]环境变量控制[`env_logger`][env_logger]输出.模块声明采用逗号分隔的条目格式化为`path::to::module=log_level`.跑过`test`申请如下:

```bash
RUST_LOG="warn,test::foo=info,test::foo::bar=debug" ./test
```

设置默认值[`log::Level`]至`warn`,模块`foo`和模块`foo::bar`至`info`和`debug`.

```bash
WARN:test: [root] warn
WARN:test::foo: [foo] warn
INFO:test::foo: [foo] info
WARN:test::foo::bar: [bar] warn
INFO:test::foo::bar: [bar] info
DEBUG:test::foo::bar: [bar] debug
```

[`log::level`]: https://docs.rs/log/*/log/enum.Level.html

[`rust_log`]: https://docs.rs/env_logger/*/env_logger/#enabling-logging
