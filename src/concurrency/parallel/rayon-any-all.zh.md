## 如果集合的任何或所有元素与给定谓词匹配，则并行测试

[![rayon-badge]][rayon] [![cat-concurrency-badge]][cat-concurrency]

这个例子演示了如何使用[`rayon::any`]和[`rayon::all`]方法，是与...相对应的并行方法[`std::any`]和[`std::all`]。[`rayon::any`]并行检查迭代器的任何元素是否与谓词匹配，并在找到一个元素后立即返回。[`rayon::all`]并行检查迭代器的所有元素是否与谓词匹配，并在找到非匹配元素后立即返回。

```rust
extern crate rayon;

use rayon::prelude::*;

fn main() {
    let mut vec = vec![2, 4, 6, 8];

    assert!(!vec.par_iter().any(|n| (*n % 2) != 0));
    assert!(vec.par_iter().all(|n| (*n % 2) == 0));
    assert!(!vec.par_iter().any(|n| *n > 8 ));
    assert!(vec.par_iter().all(|n| *n <= 8 ));

    vec.push(9);

    assert!(vec.par_iter().any(|n| (*n % 2) != 0));
    assert!(!vec.par_iter().all(|n| (*n % 2) == 0));
    assert!(vec.par_iter().any(|n| *n > 8 ));
    assert!(!vec.par_iter().all(|n| *n <= 8 )); 
}
```

[`rayon::all`]: https://docs.rs/rayon/*/rayon/iter/trait.ParallelIterator.html#method.all

[`rayon::any`]: https://docs.rs/rayon/*/rayon/iter/trait.ParallelIterator.html#method.any

[`std::all`]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.all

[`std::any`]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.any
