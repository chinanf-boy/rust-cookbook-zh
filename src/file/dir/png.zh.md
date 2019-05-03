## 递归查找所有PNG文件

[![glob-badge]][glob] [![cat-filesystem-badge]][cat-filesystem]

递归查找当前目录中的所有PNG文件。在这种情况下，`**`模式匹配当前目录和所有子目录。

使用`**`任何路径部分的模式。例如，`/media/**/*.png`匹配中的所有PNG`media`它是子目录。

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
