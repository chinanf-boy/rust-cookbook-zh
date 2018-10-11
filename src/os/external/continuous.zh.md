
## 连续处理子进程的输出

[![std-badge]][std] [![cat-os-badge]][cat-os]

在[Run an external command and process stdout](#run-an-external-command-and-process-stdout)直到外部才开始处理.[`Command`]完成了.下面的食谱[`Stdio::piped`]创建管道,并读取`stdout`连续不断[`BufReader`]更新.

下面的配方相当于UNIX外壳命令`journalctl | grep usb`.

```rust,no_run
# #[macro_use]
# extern crate error_chain;
#
use std::process::{Command, Stdio};
use std::io::{BufRead, BufReader};

# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#     }
# }
#
fn run() -> Result<()> {
    let stdout = Command::new("journalctl")
        .stdout(Stdio::piped())
        .spawn()?
        .stdout
        .ok_or_else(|| "Could not capture standard output.")?;

    let reader = BufReader::new(stdout);

    reader
        .lines()
        .filter_map(|line| line.ok())
        .filter(|line| line.find("usb").is_some())
        .for_each(|line| println!("{}", line));

     Ok(())
}
#
# quick_main!(run);
```

[`bufreader`]: https://doc.rust-lang.org/std/io/struct.BufReader.html

[`command`]: https://doc.rust-lang.org/std/process/struct.Command.html

[`stdio::piped`]: https://doc.rust-lang.org/std/process/struct.Stdio.html
