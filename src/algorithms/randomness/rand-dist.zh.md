
## 生成具有给定分布的随机数

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

默认情况下,随机数有[均匀分布].要使用其他分布生成数字,您需要实例化分布,然后使用该分布进行采样[`IndependentSample::ind_sample`]借助随机数生成器[`rand::Rng`].

该[可用的分发在此记录][rand-distributions].一个使用的例子[`Normal`]分布如下所示.

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
