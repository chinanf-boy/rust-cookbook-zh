## 保持全球可变状态

[![lazy_static-badge]][lazy_static] [![cat-rust-patterns-badge]][cat-rust-patterns]

使用声明全局状态[lazy_static]。[lazy_static]创造全球可用`static ref`这需要一个[`Mutex`]允许变异（也参见[`RwLock`]）。该[`Mutex`]wrap确保多个线程不能同时访问状态，从而防止竞争条件。一个[`MutexGuard`]必须获取以读取或改变存储在a中的值[`Mutex`]。

```rust
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate lazy_static;

use std::sync::Mutex;
#
# error_chain!{ }

lazy_static! {
    static ref FRUIT: Mutex<Vec<String>> = Mutex::new(Vec::new());
}

fn insert(fruit: &str) -> Result<()> {
    let mut db = FRUIT.lock().map_err(|_| "Failed to acquire MutexGuard")?;
    db.push(fruit.to_string());
    Ok(())
}

fn run() -> Result<()> {
    insert("apple")?;
    insert("orange")?;
    insert("peach")?;
    {
        let db = FRUIT.lock().map_err(|_| "Failed to acquire MutexGuard")?;

        db.iter().enumerate().for_each(|(i, item)| println!("{}: {}", i, item));
    }
    insert("grape")?;
    Ok(())
}
#
# quick_main!(run);
```

[`mutex`]: https://doc.rust-lang.org/std/sync/struct.Mutex.html

[`mutexguard`]: https://doc.rust-lang.org/std/sync/struct.MutexGuard.html

[`rwlock`]: https://doc.rust-lang.org/std/sync/struct.RwLock.html
