## 将错误消息，记录到控制台

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

正确的错误处理，会异常情况，视为错误。此处，`log`的方便宏[`error!`]，把错误日志记录到 stderr。

```rust
#[macro_use]
extern crate log;
extern crate env_logger;

fn execute_query(_query: &str) -> Result<(), &'static str> {
    Err("I'm afraid I can't do that")
}

fn main() {
    env_logger::init();

    let response = execute_query("DROP TABLE students");
    if let Err(err) = response {
        error!("Failed to execute query: {}", err);
    }
}
```

[`error!`]: https://docs.rs/log/*/log/macro.error.html
