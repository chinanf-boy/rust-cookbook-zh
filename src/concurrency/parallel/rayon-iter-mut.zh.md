## 并行，变换数组的元素

[![rayon-badge]][rayon] [![cat-concurrency-badge]][cat-concurrency]

该示例使用了`rayon`箱子，这是 Rust 的数据并行库。`rayon`提供了[`par_iter_mut`]方法，给任何的并行可迭代数据类型使用。这是一个类似迭代器的链，(潜在地)并行执行。

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
