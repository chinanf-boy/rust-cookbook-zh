
## 将调试消息记录到控制台

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

该`log`crate提供日志工具.该`env_logger`crate通过环境变量配置日志记录.该[`debug!`]宏像其他工作[`std::fmt`]格式化字符串

```rust
#[macro_use]
extern crate log;
extern crate env_logger;

fn execute_query(query: &str) {
    debug!("Executing query: {}", query);
}

fn main() {
    env_logger::init();

    execute_query("DROP TABLE students");
}
```

运行此代码时不输出任何输出.默认情况下,日志级别为`error`,任何较低的级别都会被删除.

设置`RUST_LOG`环境变量来打印消息:

```
$ RUST_LOG=debug cargo run
```

Cargo打印调试信息,然后在输出的最后输出以下行:

```
DEBUG:main: Executing query: DROP TABLE students
```

[`debug!`]: https://docs.rs/log/*/log/macro.debug.html

[`std::fmt`]: https://doc.rust-lang.org/std/fmt/
