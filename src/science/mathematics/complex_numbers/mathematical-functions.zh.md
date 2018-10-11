
## 数学函数

[![num-badge]][num] [![cat-science-badge]][cat-science]

当涉及到复数如何与其他数学函数,尤其是正弦函数族和数字e相互作用时,复数具有一系列有趣的性质.N在这里找到:[`num::complex::Complex`].

```rust
extern crate num;

use std::f64::consts::PI;
use num::complex::Complex;

fn main() {
    let x = Complex::new(0.0, 2.0*PI);

    println!("e^(2i * pi) = {}", x.exp()); // =~1
}
```

[`num::complex::complex`]: https://autumnai.github.io/cuticula/num/complex/struct.Complex.html
