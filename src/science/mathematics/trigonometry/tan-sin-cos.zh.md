## 验证 tan 等于，sin 除以 cos

[![std-badge]][std] [![cat-science-badge]][cat-science]

验证 `tan(x)`是否等于 `sin(x)/cos(x)`，给出 `x=6`。

```rust
fn main() {
    let x: f64 = 6.0;

    let a = x.tan();
    let b = x.sin()/x.cos();

    assert_eq!(a, b);
}
```
