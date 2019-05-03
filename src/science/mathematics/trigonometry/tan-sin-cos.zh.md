## 验证tan等于sin除以cos

[![std-badge]][std] [![cat-science-badge]][cat-science]

验证tan（x）是否等于sin（x）/cos（x），对于x=6。

```rust
fn main() {
    let x: f64 = 6.0;

    let a = x.tan();
    let b = x.sin() / x.cos();

    assert_eq!(a, b);
}
```
