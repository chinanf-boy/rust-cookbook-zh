## 将错误消息记录到控制台

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

正确的错误处理将异常视为异常。此处，错误日志记录到stderr`log`的便利宏[`error!`].

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
