## 将记录序列化为csv

[![csv-badge]][csv] [![cat-encoding-badge]][cat-encoding]

这个例子演示了如何序列化一个rust元组。[`csv::writer`]支持从锈类型到csv记录的自动序列化。[`write_record`]只写入包含字符串数据的简单记录。具有更复杂值（如数字、浮点数和选项）的数据使用[`serialize`]. 因为csv编写器使用内部缓冲区，所以始终显式[`flush`]做完之后。

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
