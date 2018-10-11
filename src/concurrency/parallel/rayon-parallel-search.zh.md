
## 使用给定谓词并行搜索项目

[![rayon-badge]][rayon] [![cat-concurrency-badge]][cat-concurrency]

这个例子使用[`rayon::find_any`]和[`par_iter`]并行地搜索满足给定闭包中谓词的元素.

如果有多个元素满足闭包参数中定义的谓词[`rayon::find_any`],`rayon`返回找到的第一个,不一定是第一个.

另请注意,闭包的参数是对引用的引用(`&&x`).请参阅讨论[`std::find`]了解更多细节.

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
