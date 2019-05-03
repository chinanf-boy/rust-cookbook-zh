## 反转矩阵

[![nalgebra-badge]][nalgebra] [![cat-science-badge]][cat-science]

使用创建3x3矩阵[`nalgebra::Matrix3`]如果可能的话，将其反转。

```rust
extern crate nalgebra;

use nalgebra::Matrix3;

fn main() {
    let m1 = Matrix3::new(2.0, 1.0, 1.0, 3.0, 2.0, 1.0, 2.0, 1.0, 2.0);
    println!("m1 = {}", m1);
    match m1.try_inverse() {
        Some(inv) => {
            println!("The inverse of m1 is: {}", inv);
        }
        None => {
            println!("m1 is not invertible!");
        }
    }
}
```

[`nalgebra::matrix3`]: https://docs.rs/nalgebra/*/nalgebra/base/type.Matrix3.html
