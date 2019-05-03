## 跳过点文件时遍历目录

[![walkdir-badge]][walkdir] [![cat-filesystem-badge]][cat-filesystem]

使用[`filter_entry`]递归下降到通过`is_not_hidden`谓词因此跳过隐藏的文件和目录。[`Iterator::filter`]适用于每个[`WalkDir::DirEntry`]即使父目录是隐藏目录。

根目录`"."`通过收益[`WalkDir::depth`]在使用中`is_not_hidden`谓语。

```rust,no_run
extern crate walkdir;

use walkdir::{DirEntry, WalkDir};

fn is_not_hidden(entry: &DirEntry) -> bool {
    entry
         .file_name()
         .to_str()
         .map(|s| entry.depth() == 0 || !s.starts_with("."))
         .unwrap_or(false)
}

fn main() {
    WalkDir::new(".")
        .into_iter()
        .filter_entry(|e| is_not_hidden(e))
        .filter_map(|v| v.ok())
        .for_each(|x| println!("{}", x.path().display()));
}
```

[`filter_entry`]: https://docs.rs/walkdir/*/walkdir/struct.IntoIter.html#method.filter_entry

[`iterator::filter`]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.filter

[`walkdir::depth`]: https://docs.rs/walkdir/*/walkdir/struct.DirEntry.html#method.depth

[`walkdir::direntry`]: https://docs.rs/walkdir/*/walkdir/struct.DirEntry.html
