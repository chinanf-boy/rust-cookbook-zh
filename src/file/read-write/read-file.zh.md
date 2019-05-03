## 从文件中读取字符串行

[![std-badge]][std] [![cat-filesystem-badge]][cat-filesystem]

将三行消息写入文件，然后使用[`Lines`]迭代器创建者[`BufRead::lines`]. [`File`]器具[`Read`]提供[`BufReader`]特质。[`File::create`]打开一个[`File`]为了写作，[`File::open`]阅读。

```rust
use std::fs::File;
use std::io::{Write, BufReader, BufRead, Error};

fn main() -> Result<(), Error> {
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
```

[`bufread::lines`]: https://doc.rust-lang.org/std/io/trait.BufRead.html#method.lines

[`bufread`]: https://doc.rust-lang.org/std/io/trait.BufRead.html

[`bufreader`]: https://doc.rust-lang.org/std/io/struct.BufReader.html

[`file::create`]: https://doc.rust-lang.org/std/fs/struct.File.html#method.create

[`file::open`]: https://doc.rust-lang.org/std/fs/struct.File.html#method.open

[`file`]: https://doc.rust-lang.org/std/fs/struct.File.html

[`lines`]: https://doc.rust-lang.org/std/io/struct.Lines.html

[`read`]: https://doc.rust-lang.org/std/io/trait.Read.html
