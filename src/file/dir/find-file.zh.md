
## 递归查找具有给定谓词的所有文件

[![walkdir-badge]][walkdir] [![cat-filesystem-badge]][cat-filesystem]

查找当前目录中最后一天内修改的JSON文件.运用[`follow_links`]确保遵循符号链接,就像它们是普通的目录和文件一样.

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate walkdir;

use walkdir::WalkDir;
#
# error_chain! {
#     foreign_links {
#         WalkDir(walkdir::Error);
#         Io(std::io::Error);
#         SystemTime(std::time::SystemTimeError);
#     }
# }

fn run() -> Result<()> {
    for entry in WalkDir::new(".")
            .follow_links(true)
            .into_iter()
            .filter_map(|e| e.ok()) {
        let f_name = entry.file_name().to_string_lossy();
        let sec = entry.metadata()?.modified()?;

        if f_name.ends_with(".json") && sec.elapsed()?.as_secs() < 86400 {
            println!("{}", f_name);
        }
    }

    Ok(())
}
#
# quick_main!(run);
```

[`follow_links`]: https://docs.rs/walkdir/*/walkdir/struct.WalkDir.html#method.follow_links
