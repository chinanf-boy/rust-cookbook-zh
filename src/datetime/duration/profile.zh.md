## 测量两个代码段之间经过的时间

[![std-badge]][std] [![cat-time-badge]][cat-time]

措施[`time::Instant::elapsed`]自从[`time::Instant::now`].

打电话[`time::Instant::elapsed`]返回A[`time::Duration`]我们在示例末尾打印的。此方法不会改变或重置[`time::Instant`]对象。

```rust
use std::time::{Duration, Instant};
# use std::thread;
#
# fn expensive_function() {
#     thread::sleep(Duration::from_secs(1));
# }

fn main() {
    let start = Instant::now();
    expensive_function();
    let duration = start.elapsed();

    println!("Time elapsed in expensive_function() is: {:?}", duration);
}
```

[`time::duration`]: https://doc.rust-lang.org/std/time/struct.Duration.html

[`time::instant::elapsed`]: https://doc.rust-lang.org/std/time/struct.Instant.html#method.elapsed

[`time::instant::now`]: https://doc.rust-lang.org/std/time/struct.Instant.html#method.now

[`time::instant`]: https://doc.rust-lang.org/std/time/struct.Instant.html
