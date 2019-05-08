## 连续处理子进程的输出

[![std-badge]][std] [![cat-os-badge]][cat-os]

在[Run an external command and process stdout](#run-an-external-command-and-process-stdout)，直到外部[`Command`]完成了。下面的方法调用[`Stdio::piped`]创建管道并读取`stdout`一旦[`BufReader`]更新。

下面的食谱相当于 unix shell 命令`journalctl | grep usb`.

```rust,no_run
use std::process::{Command, Stdio};
use std::io::{BufRead, BufReader, Error, ErrorKind};

fn main() -> Result<(), Error> {
    let stdout = Command::new("journalctl")
        .stdout(Stdio::piped())
        .spawn()?
        .stdout
        .ok_or_else(|| Error::new(ErrorKind::Other,"Could not capture standard output."))?;

    let reader = BufReader::new(stdout);

    reader
        .lines()
        .filter_map(|line| line.ok())
        .filter(|line| line.find("usb").is_some())
        .for_each(|line| println!("{}", line));

     Ok(())
}
```

[`bufreader`]: https://doc.rust-lang.org/std/io/struct.BufReader.html
[`command`]: https://doc.rust-lang.org/std/process/struct.Command.html
[`stdio::piped`]: https://doc.rust-lang.org/std/process/struct.Stdio.html
