## 将目录压缩为tarball

[![flate2-badge]][flate2] [![tar-badge]][tar] [![cat-compression-badge]][cat-compression]

压缩`/var/log`目录进入`archive.tar.gz`。

创建一个[`File`]包装成[`GzEncoder`]和[`tar::Builder`]。</br>添加内容`/var/log`目录递归进入归档下`backup/logs`路径[`Builder::append_dir_all`]。[`GzEncoder`]负责在写入数据之前透明地压缩数据`archive.tar.gz`。

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
