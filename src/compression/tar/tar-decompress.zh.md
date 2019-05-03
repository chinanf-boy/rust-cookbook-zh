## 解压缩tarball

[![flate2-badge]][flate2] [![tar-badge]][tar] [![cat-compression-badge]][cat-compression]

解压缩（[`GzDecoder`]）和提取物（[`Archive::unpack`]）来自压缩tarball命名的所有文件`archive.tar.gz`位于当前工作目录中的同一位置。

```rust,no_run
extern crate flate2;
extern crate tar;

use std::fs::File;
use flate2::read::GzDecoder;
use tar::Archive;

fn main() -> Result<(), std::io::Error> {
    let path = "archive.tar.gz";

    let tar_gz = File::open(path)?;
    let tar = GzDecoder::new(tar_gz);
    let mut archive = Archive::new(tar);
    archive.unpack(".")?;

    Ok(())
}
```

[`archive::unpack`]: https://docs.rs/tar/*/tar/struct.Archive.html#method.unpack

[`gzdecoder`]: https://docs.rs/flate2/*/flate2/read/struct.GzDecoder.html
