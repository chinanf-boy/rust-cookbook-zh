
## 避免从同一文件中读写

[![same_file-badge]][same_file] [![cat-filesystem-badge]][cat-filesystem]

使用[`same_file::Handle`]到可以与其他句柄进行相等测试的文件.在这个例子中,要读取的文件和要写入的文件的句柄被测试为相等.

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate same_file;

use same_file::Handle;
use std::path::Path;
use std::fs::File;
use std::io::{BufRead, BufReader};
#
# error_chain! {
#     foreign_links {
#          IOError(::std::io::Error);
#     }
# }

fn run() -> Result<()> {
    let path_to_read = Path::new("new.txt");

    let stdout_handle = Handle::stdout()?;
    let handle = Handle::from_path(path_to_read)?;

    if stdout_handle == handle {
        bail!("You are reading and writing to the same file");
    } else {
        let file = File::open(&path_to_read)?;
        let file = BufReader::new(file);
        for (num, line) in file.lines().enumerate() {
            println!("{} : {}", num, line?.to_uppercase());
        }
    }

    Ok(())
}
#
# quick_main!(run);
```

```bash
cargo run
```

显示文件Ne.txt的内容.

```bash
cargo run >> ./new.txt
```

因为两个文件相同,所以出现错误.

[`same_file::handle`]: https://docs.rs/same-file/*/same_file/struct.Handle.html
