## 并行，排序 vector

[![rayon-badge]][rayon] [![rand-badge]][rand] [![cat-concurrency-badge]][cat-concurrency]

此示例：并行排序字符串 vector。

分配一个空字符串的 vector。`par_iter_mut().for_each`会并发填充随机值。虽然存在[多种选择][multiple options]，可以对可枚举数据类型进行排序，[`par_sort_unstable`]通常比[稳定排序][stable sorting]算法快。

```rust
extern crate rand;
extern crate rayon;

use rand::{Rng, thread_rng};
use rand::distributions::Alphanumeric;
use rayon::prelude::*;

fn main() {
  let mut vec = vec![String::new(); 100_000];
  vec.par_iter_mut().for_each(|p| {
    let mut rng = thread_rng();
    *p = (0..5).map(|_| rng.sample(&Alphanumeric)).collect()
  });
  vec.par_sort_unstable();
}
```

[`par_sort_unstable`]: https://docs.rs/rayon/*/rayon/slice/trait.ParallelSliceMut.html#method.par_sort_unstable
[multiple options]: https://docs.rs/rayon/*/rayon/slice/trait.ParallelSliceMut.html
[stable sorting]: https://docs.rs/rayon/*/rayon/slice/trait.ParallelSliceMut.html#method.par_sort
