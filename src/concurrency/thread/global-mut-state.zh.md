## 保持全局可变状态

[![lazy_static-badge]][lazy_static] [![cat-rust-patterns-badge]][cat-rust-patterns]

使用[lazy_static]声明全局状态。[lazy_static]创建一个全局可用`static ref`，这需要一个[`Mutex`]，来决定可变许可（也参见[`RwLock`]）。受[`Mutex`]包裹，能确保多个线程，不能同时访问（`FRUIT`）状态，从而防止竞争条件。必须获取一个[`MutexGuard`]，才能读取或改变存储在[`Mutex`]中的值。

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
