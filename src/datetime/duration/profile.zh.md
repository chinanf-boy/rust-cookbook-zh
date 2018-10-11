
## 测量两个代码段之间的经过时间

[![std-badge]][std] [![cat-time-badge]][cat-time]

措施[`time::Instant::elapsed`]以来[`time::Instant::now`].

调用[`time::Instant::elapsed`]返回一个[`time::Duration`]我们在示例的末尾打印.此方法不会改变或重置[`time::Instant`]目的.

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
