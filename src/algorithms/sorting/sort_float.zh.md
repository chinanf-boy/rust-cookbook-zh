## 排序浮点数 vector

[![std-badge]][std] [![cat-science-badge]][cat-science]

可以使用[`vec::sort_by`]和[`PartialOrd::partial_cmp`]，对 `f32` 或 `f64` 的 vector 进行排序。

```rust
fn main() {
    let mut vec = vec![1.1, 1.15, 5.5, 1.123, 2.0];

    vec.sort_by(|a, b| a.partial_cmp(b).unwrap());

    assert_eq!(vec, vec![1.1, 1.123, 1.15, 2.0, 5.5]);
}
```

[`vec::sort_by`]: https://doc.rust-lang.org/std/primitive.slice.html#method.sort_by
[`partialord::partial_cmp`]: https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp
