## 生成随机数

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

通过[`rand::thread_rng`]，在随机数生成器[`rand::Rng`]的帮助下，生成随机数。每个线程都有一个初始化的生成器。整数在该类型的范围（最大值 ～ 最小值）内，均匀分布，还有，浮点数是从 0 到 1，但不包括 1 的 均匀分布。

```rust
extern crate rand;

use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();

    let n1: u8 = rng.gen();
    let n2: u16 = rng.gen();
    println!("Random u8: {}", n1);
    println!("Random u16: {}", n2);
    println!("Random u32: {}", rng.gen::<u32>());
    println!("Random i32: {}", rng.gen::<i32>());
    println!("Random float: {}", rng.gen::<f64>());
}
```

[`rand::rng`]: https://docs.rs/rand/*/rand/trait.Rng.html

[`rand::thread_rng`]: https://docs.rs/rand/*/rand/fn.thread_rng.html
