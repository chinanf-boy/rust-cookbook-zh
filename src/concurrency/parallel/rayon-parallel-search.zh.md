## 使用给定断言，并行搜索项目

[![rayon-badge]][rayon] [![cat-concurrency-badge]][cat-concurrency]

这个例子使用[`rayon::find_any`]和[`par_iter`]获得一个，通过并行搜索，满足给定闭包中断言的元素向量。

如果，有多个元素满足[`rayon::find_any`]闭包参数中，定义的断言，`rayon`返回找到的第一个，但不一定是(顺序上的)第一个。

另请注意，闭包的参数是对一个引用的一个引用（`&&x`）。请查阅[`std::find`]的讨论，了解更多细节。

```rust
extern crate rayon;

use rayon::prelude::*;

fn main() {
    let v = vec![6, 2, 1, 9, 3, 8, 11];

    let f1 = v.par_iter().find_any(|&&x| x == 9);
    let f2 = v.par_iter().find_any(|&&x| x % 2 == 0 && x > 6);
    let f3 = v.par_iter().find_any(|&&x| x > 8);

    assert_eq!(f1, Some(&9));
    assert_eq!(f2, Some(&8));
    assert!(f3 > Some(&8));
}
```

[`par_iter`]: https://docs.rs/rayon/*/rayon/iter/trait.IntoParallelRefIterator.html#tymethod.par_iter
[`rayon::find_any`]: https://docs.rs/rayon/*/rayon/iter/trait.ParallelIterator.html#method.find_any
[`std::find`]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.find
