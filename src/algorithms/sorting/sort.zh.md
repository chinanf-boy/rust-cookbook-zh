## 排序整数向量

[![std-badge]][std] [![cat-science-badge]][cat-science]

此示例使用[`vec::sort`]对整数向量进行排序。替代方案是使用[`vec::sort_unstable`]，它可以更快，但不保留相等元素的顺序。

```rust
fn main() {
    let mut vec = vec![1, 5, 10, 2, 15];

    vec.sort();

    assert_eq!(vec, vec![1, 2, 5, 10, 15]);
}
```

[`vec::sort`]: https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort
[`vec::sort_unstable`]: https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_unstable
