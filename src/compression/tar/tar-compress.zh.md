## 将目录压缩为一个 tarball

[![flate2-badge]][flate2] [![tar-badge]][tar] [![cat-compression-badge]][cat-compression]

把`/var/log`目录压缩，为`archive.tar.gz`。

创建一个[`File`]，包进[`GzEncoder`]，在包入[`tar::Builder`]。

- 用[`Builder::append_dir_all`]递归添加`/var/log`目录中的内容，归档到`backup/logs`路径下。
- [`GzEncoder`]负责在数据写入`archive.tar.gz`之前，透明地压缩数据。

```rust,no_run
extern crate tar;
extern crate flate2;

use std::fs::File;
use flate2::Compression;
use flate2::write::GzEncoder;

fn main() -> Result<(), std::io::Error> {
    let tar_gz = File::create("archive.tar.gz")?;
    let enc = GzEncoder::new(tar_gz, Compression::default());
    let mut tar = tar::Builder::new(enc);
    tar.append_dir_all("backup/logs", "/var/log")?;
    Ok(())
}
```

[`builder::append_dir_all`]: https://docs.rs/tar/*/tar/struct.Builder.html#method.append_dir_all
[`file`]: https://doc.rust-lang.org/std/fs/struct.File.html
[`gzencoder`]: https://docs.rs/flate2/*/flate2/write/struct.GzEncoder.html
[`tar::builder`]: https://docs.rs/tar/*/tar/struct.Builder.html
