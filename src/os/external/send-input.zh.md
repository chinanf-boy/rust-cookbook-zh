## 运行传递 stdin 的外部命令，并检查错误代码

[![std-badge]][std] [![cat-os-badge]][cat-os]

使用外部[`Command`]，打开`python`解释程序，并将 python (语言)语句传递给它，以供执行。之后的输出[`Output`]会被解析。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
#
use std::collections::HashSet;
use std::io::Write;
use std::process::{Command, Stdio};
#
# error_chain!{
#     errors { CmdError }
#     foreign_links {
#         Io(std::io::Error);
#         Utf8(std::string::FromUtf8Error);
#     }
# }

fn run() -> Result<()> {
    let mut child = Command::new("python").stdin(Stdio::piped())
        .stderr(Stdio::piped())
        .stdout(Stdio::piped())
        .spawn()?;

    child.stdin
        .as_mut()
        .ok_or("Child process stdin has not been captured!")?
        .write_all(b"import this; copyright(); credits(); exit()")?;

    let output = child.wait_with_output()?;

    if output.status.success() {
        let raw_output = String::from_utf8(output.stdout)?;
        let words = raw_output.split_whitespace()
            .map(|s| s.to_lowercase())
            .collect::<HashSet<_>>();
        println!("Found {} unique words:", words.len());
        println!("{:#?}", words);
        Ok(())
    } else {
        let err = String::from_utf8(output.stderr)?;
        bail!("External command failed:\n {}", err)
    }
}
#
# quick_main!(run);
```

[`command`]: https://doc.rust-lang.org/std/process/struct.Command.html
[`output`]: https://doc.rust-lang.org/std/process/struct.Output.html
