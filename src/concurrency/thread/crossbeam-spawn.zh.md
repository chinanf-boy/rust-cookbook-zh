## 产生一个短命的线程

[![crossbeam-badge]][crossbeam] [![cat-concurrency-badge]][cat-concurrency]

该示例使用了[横梁]crate，为并发和并行编程提供数据结构和函数。[`Scope::spawn`]生成一个新的作用域线程，保证在从传入的闭包返回之前终止[`crossbeam::scope`]功能，意味着您可以从调用函数引用数据。

此示例将数组拆分为一半，并在单独的线程中执行工作。

```rust
extern crate crossbeam;

fn main() {
    let arr = &[1, 25, -4, 10];
    let max = find_max(arr);
    assert_eq!(max, Some(25));
}

fn find_max(arr: &[i32]) -> Option<i32> {
    const THRESHOLD: usize = 2;

    if arr.len() <= THRESHOLD {
        return arr.iter().cloned().max();
    }

    let mid = arr.len()/2;
    let (left, right) = arr.split_at(mid);

    crossbeam::scope(|s| {
        let thread_l = s.spawn(|_| find_max(left));
        let thread_r = s.spawn(|_| find_max(right));

        let min_l = thread_l.join().unwrap()?;
        let min_r = thread_r.join().unwrap()?;

        Some(min_l.max(min_r))
    }).unwrap()
}
```

[`crossbeam::scope`]: https://docs.rs/crossbeam/*/crossbeam/fn.scope.html
[`scope::spawn`]: https://docs.rs/crossbeam/*/crossbeam/thread/struct.Scope.html#method.spawn
