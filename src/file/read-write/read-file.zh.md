## 从文件中，读取字符串行

[![std-badge]][std] [![cat-filesystem-badge]][cat-filesystem]

将一份三行的消息写入文件，然后由[`BufRead::lines`]，返回[`Lines`]迭代器，用来一次读取一行。 [`File`]实现了[`Read`]，也就是提供[`BufReader`] trait。[`File::create`]会打开一个[`File`]，用于写入(文件)，而[`File::open`]用来读取。

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
