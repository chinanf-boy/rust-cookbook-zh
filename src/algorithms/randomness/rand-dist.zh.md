## 生成给定分布的随机数

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

默认情况下，随机数有[均匀(Uniform) 分布][uniform distribution]。要使用其他（概率/类型的）分布生成数字，您需要实例化一个分布(distribution)，然后用分布下的[`Distribution::sample`]方法，在随机数生成器[`rand::Rng`]的帮助下，进行采样。

关于[可用分布的文档，在此][rand-distributions]。下面是，一个使用[`Normal`]分布的的例子。

```rust
extern crate rand;

use rand::distributions::{Normal, Distribution};

fn main() {
  let mut rng = rand::thread_rng();
  let normal = Normal::new(2.0, 3.0);
  let v = normal.sample(&mut rng);
  println!("{} is from a N(2, 9) distribution", v)
}
```

[`distribution::sample`]: https://docs.rs/rand/*/rand/distributions/trait.Distribution.html#tymethod.sample

[`normal`]: https://docs.rs/rand/*/rand/distributions/normal/struct.Normal.html

[`rand::rng`]: https://docs.rs/rand/*/rand/trait.Rng.html

[rand-distributions]: https://docs.rs/rand/*/rand/distributions/index.html

[uniform distribution]: https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)
