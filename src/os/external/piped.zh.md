## 运行管道外部命令

[![std-badge]][std] [![cat-os-badge]][cat-os]

显示到10<sup>钍</sup>当前工作目录中最大的文件和子目录。它相当于运行：`du -ah . |
sort -hr | head -n 10`.

[`Command`]S代表一个过程。子进程的输出用[`Stdio::piped`]在父级和子级之间。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
#
use std::process::{Command, Stdio};
#
# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#         Utf8(std::string::FromUtf8Error);
#     }
# }

fn run() -> Result<()> {
    let directory = std::env::current_dir()?;
    let mut du_output_child = Command::new("du")
        .arg("-ah")
        .arg(&directory)
        .stdout(Stdio::piped())
        .spawn()?;

    if let Some(du_output) = du_output_child.stdout.take() {
        let mut sort_output_child = Command::new("sort")
            .arg("-hr")
            .stdin(du_output)
            .stdout(Stdio::piped())
            .spawn()?;

        du_output_child.wait()?;

        if let Some(sort_output) = sort_output_child.stdout.take() {
            let head_output_child = Command::new("head")
                .args(&["-n", "10"])
                .stdin(sort_output)
                .stdout(Stdio::piped())
                .spawn()?;

            let head_stdout = head_output_child.wait_with_output()?;

            sort_output_child.wait()?;

            println!(
                "Top 10 biggest files and directories in '{}':\n{}",
                directory.display(),
                String::from_utf8(head_stdout.stdout).unwrap()
            );
        }
    }

    Ok(())
}
#
# quick_main!(run);
```

[`command`]: https://doc.rust-lang.org/std/process/struct.Command.html

[`stdio::piped`]: https://doc.rust-lang.org/std/process/struct.Stdio.html
