
## 三角形的边长计算

[![std-badge]][std] [![cat-science-badge]][cat-science]

计算直角三角形斜边的长度,其角度为2弧度,相对边长为80.

```rust
fn main() {
    let angle: f64 = 2.0;
    let side_length = 80.0;

    let hypotenuse = side_length/angle.sin();

    println!("Hypotenuse: {}", hypotenuse);
}
```
