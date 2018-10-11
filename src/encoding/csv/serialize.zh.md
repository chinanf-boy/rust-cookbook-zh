
## 将记录序列化为CSV

[![csv-badge]][csv] [![cat-encoding-badge]][cat-encoding]

此示例显示如何序列化Rust元组.[`csv::writer`]支持从Rust类型到CSV记录的自动序列化.[`write_record`]写一个只包含字符串数据的简单记录.具有更复杂值的数据(如数字,浮点数和选项)使用[`serialize`].由于CSV编写器始终使用内部缓冲区[`flush`]完成后.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate csv;

use std::io;
#
# error_chain! {
#     foreign_links {
#         CSVError(csv::Error);
#         IOError(std::io::Error);
#    }
# }

fn run() -> Result<()> {
    let mut wtr = csv::Writer::from_writer(io::stdout());

    wtr.write_record(&["Name", "Place", "ID"])?;

    wtr.serialize(("Mark", "Sydney", 87))?;
    wtr.serialize(("Ashley", "Dublin", 32))?;
    wtr.serialize(("Akshat", "Delhi", 11))?;

    wtr.flush()?;
    Ok(())
}
#
# quick_main!(run);
```

[`csv::writer`]: https://docs.rs/csv/*/csv/struct.Writer.html

[`flush`]: https://docs.rs/csv/*/csv/struct.Writer.html#method.flush

[`serialize`]: https://docs.rs/csv/*/csv/struct.Writer.html#method.serialize

[`write_record`]: https://docs.rs/csv/*/csv/struct.Writer.html#method.write_record
