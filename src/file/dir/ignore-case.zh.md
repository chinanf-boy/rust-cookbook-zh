## 查找具有给定模式的所有文件，忽略文件名大小写。

[![glob-badge]][glob] [![cat-filesystem-badge]][cat-filesystem]

在中查找所有图像文件`/media/`目录匹配`img_[0-9]*.png`模式。

风俗习惯[`MatchOptions`]结构传递给[`glob_with`]函数使全局模式不区分大小写，同时保留其他选项[`Default`].

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate glob;

use glob::{glob_with, MatchOptions};
#
# error_chain! {
#     foreign_links {
#         Glob(glob::GlobError);
#         Pattern(glob::PatternError);
#     }
# }

fn run() -> Result<()> {
    let options = MatchOptions {
        case_sensitive: false,
        ..Default::default()
    };

    for entry in glob_with("/media/img_[0-9]*.png", &options)? {
        println!("{}", entry?.display());
    }

    Ok(())
}
#
# quick_main!(run);
```

[`default`]: https://doc.rust-lang.org/std/default/trait.Default.html

[`glob_with`]: https://docs.rs/glob/*/glob/fn.glob_with.html

[`matchoptions`]: https://docs.rs/glob/*/glob/struct.MatchOptions.html
