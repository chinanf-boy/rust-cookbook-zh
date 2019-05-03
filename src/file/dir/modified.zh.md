## 过去24小时内修改过的文件名

[![std-badge]][std] [![cat-filesystem-badge]][cat-filesystem]

通过调用[`env::current_dir`]，然后针对中的每个条目[`fs::read_dir`]提取[`DirEntry::path`]并通过[`fs::Metadata`]. 这个[`Metadata::modified`]返回[`SystemTime::elapsed`]上次修改后的时间。[`Duration::as_secs`]将时间转换为秒，并与24小时（24*六十*60秒）。[`Metadata::is_file`]筛选出目录。

```rust
# #[macro_use]
# extern crate error_chain;
#
use std::{env, fs};

# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#         SystemTimeError(std::time::SystemTimeError);
#     }
# }
#
fn run() -> Result<()> {
    let current_dir = env::current_dir()?;
    println!(
        "Entries modified in the last 24 hours in {:?}:",
        current_dir
    );

    for entry in fs::read_dir(current_dir)? {
        let entry = entry?;
        let path = entry.path();

        let metadata = fs::metadata(&path)?;
        let last_modified = metadata.modified()?.elapsed()?.as_secs();

        if last_modified < 24 * 3600 && metadata.is_file() {
            println!(
                "Last modified: {:?} seconds, is read only: {:?}, size: {:?} bytes, filename: {:?}",
                last_modified,
                metadata.permissions().readonly(),
                metadata.len(),
                path.file_name().ok_or("No filename")?
            );
        }
    }

    Ok(())
}
#
# quick_main!(run);
```

[`direntry::path`]: https://doc.rust-lang.org/std/fs/struct.DirEntry.html#method.path

[`duration::as_secs`]: https://doc.rust-lang.org/std/time/struct.Duration.html#method.as_secs

[`env::current_dir`]: https://doc.rust-lang.org/std/env/fn.current_dir.html

[`fs::metadata`]: https://doc.rust-lang.org/std/fs/struct.Metadata.html

[`fs::read_dir`]: https://doc.rust-lang.org/std/fs/fn.read_dir.html

[`metadata::is_file`]: https://doc.rust-lang.org/std/fs/struct.Metadata.html#method.is_file

[`metadata::modified`]: https://doc.rust-lang.org/std/fs/struct.Metadata.html#method.modified

[`systemtime::elapsed`]: https://doc.rust-lang.org/std/time/struct.SystemTime.html#method.elapsed
