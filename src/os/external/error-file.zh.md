## 将子进程的 stdout 和 stderr 重定向到同一文件

[![std-badge]][std] [![cat-os-badge]][cat-os]

生成子进程并重定向`stdout`和`stderr`到同一个文件。它遵循与[run piped external
commands](#run-piped-external-commands)然而[`process::Stdio`]写入指定的文件。[`File::try_clone`]引用相同的文件句柄`stdout`和`stderr`. 它将确保两个句柄使用相同的光标位置写入。

下面的食谱相当于运行 unix shell 命令`ls . oops >out.txt 2>&1`.

```rust,no_run
use std::fs::File;
use std::io::Error;
use std::process::{Command, Stdio};

fn main() -> Result<(), Error> {
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
```

[`file::try_clone`]: https://doc.rust-lang.org/std/fs/struct.File.html#method.try_clone
[`process::stdio`]: https://doc.rust-lang.org/std/process/struct.Stdio.html
