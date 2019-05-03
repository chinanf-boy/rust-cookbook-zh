## 使用内存映射随机访问文件

[![memmap-badge]][memmap] [![cat-filesystem-badge]][cat-filesystem]

使用创建文件的内存映射[记忆地图]并模拟从文件中进行的一些非顺序读取。使用内存映射意味着您只需要索引到一个切片，而不是处理[`seek`]导航文件。

这个[`Mmap::map`]函数假定内存映射后面的文件不会同时被另一个进程修改，或者[竞争条件]发生。

```rust
extern crate memmap;

use memmap::Mmap;
use std::fs::File;
use std::io::{Write, Error};

fn main() -> Result<(), Error> {
#     write!(File::create("content.txt")?, "My hovercraft is full of eels!")?;
#
    let file = File::open("content.txt")?;
    let map = unsafe { Mmap::map(&file)? };

    let random_indexes = [0, 1, 2, 19, 22, 10, 11, 29];
    assert_eq!(&map[3..13], b"hovercraft");
    let random_bytes: Vec<u8> = random_indexes.iter()
        .map(|&idx| map[idx])
        .collect();
    assert_eq!(&random_bytes[..], b"My loaf!");
    Ok(())
}
```

[`mmap::map`]: https://docs.rs/memmap/*/memmap/struct.Mmap.html#method.map

[`seek`]: https://doc.rust-lang.org/std/fs/struct.File.html#method.seek

[race condition]: https://en.wikipedia.org/wiki/Race_condition#File_systems
