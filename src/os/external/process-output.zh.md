
## 运行外部命令并处理STDUT

[![regex-badge]][regex] [![cat-os-badge]][cat-os] [![cat-text-processing-badge]][cat-text-processing]

跑`git log --oneline`作为一个外部[`Command`]并检查其[`Output`]使用[`Regex`]获取最后5个提交的哈希和消息.

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate regex;

use std::process::Command;
use regex::Regex;
#
# error_chain!{
#     foreign_links {
#         Io(std::io::Error);
#         Regex(regex::Error);
#         Utf8(std::string::FromUtf8Error);
#     }
# }

#[derive(PartialEq, Default, Clone, Debug)]
struct Commit {
    hash: String,
    message: String,
}

fn run() -> Result<()> {
    let output = Command::new("git").arg("log").arg("--oneline").output()?;

    if !output.status.success() {
        bail!("Command executed with failing error code");
    }

    let pattern = Regex::new(r"(?x)
                               ([0-9a-fA-F]+) # commit hash
                               (.*)           # The commit message")?;

    String::from_utf8(output.stdout)?
        .lines()
        .filter_map(|line| pattern.captures(line))
        .map(|cap| {
                 Commit {
                     hash: cap[1].to_string(),
                     message: cap[2].trim().to_string(),
                 }
             })
        .take(5)
        .for_each(|x| println!("{:?}", x));

    Ok(())
}
#
# quick_main!(run);
```

[`command`]: https://doc.rust-lang.org/std/process/struct.Command.html

[`output`]: https://doc.rust-lang.org/std/process/struct.Output.html

[`regex`]: https://docs.rs/regex/*/regex/struct.Regex.html
