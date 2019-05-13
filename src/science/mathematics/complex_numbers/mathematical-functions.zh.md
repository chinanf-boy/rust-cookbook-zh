## 数学函数

[![num-badge]][num] [![cat-science-badge]][cat-science]

当涉及如何与其他数学函数交互时，复数有一系列有趣的性质，尤其是类似数字的正弦家族函数。要将这些函数与复数一起使用，复数类型有一些内置函数，所有这些函数都可以找：[`num::complex::Complex`]。

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
