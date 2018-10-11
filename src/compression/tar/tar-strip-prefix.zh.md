
## 从路径中删除前缀时解压缩tarball

[![flate2-badge]][flate2] [![tar-badge]][tar] [![cat-compression-badge]][cat-compression]

迭代了[`Archive::entries`].使用[`Path::strip_prefix`]删除指定的路径前缀(`bundle/logs`).最后,提取出来[`tar::Entry`]通过[`Entry::unpack`].

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate flate2;
extern crate tar;

use std::fs::File;
use std::path::PathBuf;
use flate2::read::GzDecoder;
use tar::Archive;
# 
# error_chain! {
#   foreign_links {
#     Io(std::io::Error);
#     StripPrefixError(::std::path::StripPrefixError);
#   }
# }

fn main() -> Result<()> {
    let file = File::open("archive.tar.gz")?;
    let mut archive = Archive::new(GzDecoder::new(file));
    let prefix = "bundle/logs";

    println!("Extracted the following files:");
    archive
        .entries()?
        .filter_map(|e| e.ok())
        .map(|mut entry| -> Result<PathBuf> {
            let path = entry.path()?.strip_prefix(prefix)?.to_owned();
            entry.unpack(&path)?;
            Ok(path)
        })
        .filter_map(|e| e.ok())
        .for_each(|x| println!("> {}", x.display()));

    Ok(())
}
```

[`archive::entries`]: https://docs.rs/tar/*/tar/struct.Archive.html#method.entries

[`entry::unpack`]: https://docs.rs/tar/*/tar/struct.Entry.html#method.unpack

[`path::strip_prefix`]: https://doc.rust-lang.org/std/path/struct.Path.html#method.strip_prefix

[`tar::entry`]: https://docs.rs/tar/*/tar/struct.Entry.html
