
## 验证谭等于罪除以

[![std-badge]][std] [![cat-science-badge]][cat-science]

验证TaN(x)等于x(x)/COS(x),x=6.

```rust
fn main() {
    let x: f64 = 6.0;

    let a = x.tan();
    let b = x.sin() / x.cos();

    assert_eq!(a, b);
}
```
