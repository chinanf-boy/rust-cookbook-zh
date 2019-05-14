## 通过匹配多个正则表达式，筛选日志文件

[![regex-badge]][regex] [![cat-text-processing-badge]][cat-text-processing]

读取名为`application.log`的文件，并且只输出包含“version x.x.x”、或一些 IP 地址跟着端口 443（例如“192.168.0.1:443”）或特殊 warning 的那些行。

一个[`regex::RegexSetBuilder`]组成一个[`regex::RegexSet`]。 因为反斜杠在正则表达式中，非常常见，所以使用[原始字符串文本][raw string literals]能让它们更具可读性。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate regex;

use std::fs::File;
use std::io::{BufReader, BufRead};
use regex::RegexSetBuilder;

# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#         Regex(regex::Error);
#     }
# }
#
fn run() -> Result<()> {
    let log_path = "application.log";
    let buffered = BufReader::new(File::open(log_path)?);

    let set = RegexSetBuilder::new(&[
        r#"version "\d\.\d\.\d""#,
        r#"\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}:443"#,
        r#"warning.*timeout expired"#,
    ]).case_insensitive(true)
        .build()?;

    buffered
        .lines()
        .filter_map(|line| line.ok())
        .filter(|line| set.is_match(line.as_str()))
        .for_each(|x| println!("{}", x));

    Ok(())
}
#
# quick_main!(run);
```

[`regex::regexset`]: https://docs.rs/regex/*/regex/struct.RegexSet.html
[`regex::regexsetbuilder`]: https://docs.rs/regex/*/regex/struct.RegexSetBuilder.html
[raw string literals]: https://doc.rust-lang.org/reference/tokens.html#raw-string-literals
