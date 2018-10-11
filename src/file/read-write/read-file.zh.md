
## 从文件读取字符串行

[![std-badge]][std] [![cat-filesystem-badge]][cat-filesystem]

将三行消息写入文件,然后一次读取一行[`Lines`]创建的迭代器[`BufRead::lines`]. [`File`]器具[`Read`]提供[`BufReader`]特质.[`File::create`]打开一个[`File`]为了写作,[`File::open`]阅读.

```rust
# #[macro_use]
# extern crate error_chain;
#
use std::fs::File;
use std::io::{Write, BufReader, BufRead};
#
# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#     }
# }

fn run() -> Result<()> {
    let path = "lines.txt";

    let mut output = File::create(path)?;
    write!(output, "Rust\n💖\nFun")?;

    let input = File::open(path)?;
    let buffered = BufReader::new(input);

    for line in buffered.lines() {
        println!("{}", line?);
    }

    Ok(())
}
#
# quick_main!(run);
```

[`bufread::lines`]: https://doc.rust-lang.org/std/io/trait.BufRead.html#method.lines

[`bufread`]: https://doc.rust-lang.org/std/io/trait.BufRead.html

[`bufreader`]: https://doc.rust-lang.org/std/io/struct.BufReader.html

[`file::create`]: https://doc.rust-lang.org/std/fs/struct.File.html#method.create

[`file::open`]: https://doc.rust-lang.org/std/fs/struct.File.html#method.open

[`file`]: https://doc.rust-lang.org/std/fs/struct.File.html

[`lines`]: https://doc.rust-lang.org/std/io/struct.Lines.html

[`read`]: https://doc.rust-lang.org/std/io/trait.Read.html
