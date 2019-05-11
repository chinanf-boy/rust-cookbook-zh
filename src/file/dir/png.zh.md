## 递归查找所有 PNG 文件

[![glob-badge]][glob] [![cat-filesystem-badge]][cat-filesystem]

递归查找，当前目录中的所有 PNG 文件。在这种情况下，`**`模式匹配当前目录和所有子目录。

可在任何路径部分，使用`**`模式。例如，`/media/**/*.png`，会匹配`media`下的所有 PNG，且是子目录。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate glob;

use glob::glob;
#
# error_chain! {
#     foreign_links {
#         Glob(glob::GlobError);
#         Pattern(glob::PatternError);
#     }
# }

fn run() -> Result<()> {
    for entry in glob("**/*.png")? {
        println!("{}", entry?.display());
    }

    Ok(())
}
#
# quick_main!(run);
```
