## 计算一个三角形的边长

[![std-badge]][std] [![cat-science-badge]][cat-science]

计算直角三角形斜边的长度，斜边的角度为 2 弧度，对边的长度为 80。

```rust
fn main() {
    let angle: f64 = 2.0;
    let side_length = 80.0;

    let hypotenuse = side_length/angle.sin();

    println!("Hypotenuse: {}", hypotenuse);
}
```
