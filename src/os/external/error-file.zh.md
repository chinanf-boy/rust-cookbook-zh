
## 将子进程的STDUT和STDRR重定向到同一个文件

[![std-badge]][std] [![cat-os-badge]][cat-os]

生成子进程并重定向`stdout`和`stderr`到同一个文件.它遵循同样的想法[run piped external
commands](#run-piped-external-commands)然而[`process::Stdio`]写入指定文件.[`File::try_clone`]引用相同的文件句柄`stdout`和`stderr`. 它将确保两个句柄用相同的光标位置写入.

下面的配方相当于运行UNIX shell命令`ls
. oops >out.txt 2>&1`.

```rust,no_run
# #[macro_use]
# extern crate error_chain;
#
use std::fs::File;
use std::process::{Command, Stdio};

# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#     }
# }
#
fn run() -> Result<()> {
    let outputs = File::create("out.txt")?;
    let errors = outputs.try_clone()?;

    Command::new("ls")
        .args(&[".", "oops"])
        .stdout(Stdio::from(outputs))
        .stderr(Stdio::from(errors))
        .spawn()?
        .wait_with_output()?;

    Ok(())
}
#
# quick_main!(run);
```

[`file::try_clone`]: https://doc.rust-lang.org/std/fs/struct.File.html#method.try_clone

[`process::stdio`]: https://doc.rust-lang.org/std/process/struct.Stdio.html
