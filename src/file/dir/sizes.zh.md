## 在给定深度(目录)，递归计算文件大小

[![walkdir-badge]][walkdir] [![cat-filesystem-badge]][cat-filesystem]

递归一定深度的目录，可以通过以下方式灵活设置：[`WalkDir::min_depth`] & [`WalkDir::max_depth`]方法。 3 个子文件夹深度的所有文件，其总和大小的计算，忽略根文件夹中的文件。

```rust
extern crate walkdir;

use walkdir::WalkDir;

fn main() {
    let total_size = WalkDir::new(".")
        .min_depth(1)
        .max_depth(3)
        .into_iter()
        .filter_map(|entry| entry.ok())
        .filter_map(|entry| entry.metadata().ok())
        .filter(|metadata| metadata.is_file())
        .fold(0, |acc, m| acc + m.len());

    println!("Total size: {} bytes.", total_size);
}
```

[`walkdir::max_depth`]: https://docs.rs/walkdir/*/walkdir/struct.WalkDir.html#method.max_depth
[`walkdir::min_depth`]: https://docs.rs/walkdir/*/walkdir/struct.WalkDir.html#method.min_depth
