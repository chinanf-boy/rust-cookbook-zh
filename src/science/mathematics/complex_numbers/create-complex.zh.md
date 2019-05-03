## 创建复数

[![num-badge]][num] [![cat-science-badge]][cat-science]

创建类型的复数[`num::complex::Complex`]. 复数的实部和虚部必须是同一类型。

```rust
extern crate num;

fn main() {
    let complex_integer = num::complex::Complex::new(10, 20);
    let complex_float = num::complex::Complex::new(10.1, 20.1);

    println!("Complex integer: {}", complex_integer);
    println!("Complex float: {}", complex_float);
}
```

[`num::complex::complex`]: https://autumnai.github.io/cuticula/num/complex/struct.Complex.html
