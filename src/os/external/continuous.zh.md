## 连续处理，子进程的输出

[![std-badge]][std] [![cat-os-badge]][cat-os]

在[运行外部命令，并处理 stdout](#run-an-external-command-and-process-stdout)食谱中，`stdout`的处理会在外部[`Command`]完成之后执行。而本食谱接下来的方法是，调用[`Stdio::piped`]创建一个管道，并在[`BufReader`]每次更新，都读取`stdout`(连续)。

下面的食谱，相当于 unix shell 命令：`journalctl | grep usb`.

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
