## 解压缩 一个 tarball

[![flate2-badge]][flate2] [![tar-badge]][tar] [![cat-compression-badge]][cat-compression]

解压缩（[`GzDecoder`]）和提取（[`Archive::unpack`]）当前工作目录中的压缩包`archive.tar.gz`的所有文件，并放在同一位置。

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
