
## 并行地变换数组的元素

[![rayon-badge]][rayon] [![cat-concurrency-badge]][cat-concurrency]

该示例使用了`rayon`crate,这是Rust的数据并行库.`rayon`提供[`par_iter_mut`]任何并行可迭代数据类型的方法.这是一个类似迭代器的链,可能并行执行.

```rust
extern crate rayon;

use rayon::prelude::*;

fn main() {
    let mut arr = [0, 7, 9, 11];
    arr.par_iter_mut().for_each(|p| *p -= 1);
    println!("{:?}", arr);
}
```

[`par_iter_mut`]: https://docs.rs/rayon/*/rayon/iter/trait.IntoParallelRefMutIterator.html#tymethod.par_iter_mut
