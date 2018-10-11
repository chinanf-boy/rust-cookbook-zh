
## 产生一个短命的线程

[![crossbeam-badge]][crossbeam] [![cat-concurrency-badge]][cat-concurrency]

该示例使用了[横梁]crate,为并发和并行编程提供数据结构和函数.[`Scope::spawn`]生成一个新的作用域线程,保证在从传入的闭包返回之前终止[`crossbeam::scope`]功能,意味着您可以从调用函数引用数据.

此示例将数组拆分为一半,并在单独的线程中执行工作.

```rust
extern crate crossbeam;

use std::cmp;

fn main() {
    let arr = &[-4, 1, 10, 25];
    let max = find_max(arr, 0, arr.len());
    assert_eq!(25, max);
}

fn find_max(arr: &[i32], start: usize, end: usize) -> i32 {
    const THRESHOLD: usize = 2;
    if end - start <= THRESHOLD {
        return *arr.iter().max().unwrap();
    }

    let mid = start + (end - start) / 2;
    crossbeam::thread::scope(|scope| {
        let left = scope.spawn(|| find_max(arr, start, mid));
        let right = scope.spawn(|| find_max(arr, mid, end));

        // NOTE(unwrap): `join` will return an error if the thread panicked.
        // This way, panics will be propagated up to the `scope` call
        cmp::max(left.join().unwrap(), right.join().unwrap())
    })
}
```

[`crossbeam::scope`]: https://docs.rs/crossbeam/*/crossbeam/fn.scope.html

[`scope::spawn`]: https://docs.rs/crossbeam/*/crossbeam/thread/struct.Scope.html#method.spawn
