## 复数相加

[![num-badge]][num] [![cat-science-badge]][cat-science]

对复数执行数学运算与内置类型相同：涉及的数字必须是同一类型（即浮点数或整数）。

```rust
extern crate num;

fn main() {
    let complex_num1 = num::complex::Complex::new(10.0, 20.0); // Must use floats
    let complex_num2 = num::complex::Complex::new(3.1, -4.2);

    let sum = complex_num1 + complex_num2;

    println!("Sum: {}", sum);
}
```
