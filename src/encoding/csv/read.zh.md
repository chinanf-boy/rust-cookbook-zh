## 读取 csv 记录

[![csv-badge]][csv] [![cat-encoding-badge]][cat-encoding]

将标准 csv 记录，读取到[`csv::StringRecord`]：一种弱类型数据表示形式，这需要有效的 UTF-8 行。或者，[`csv::ByteRecord`]，它不会对 UTF-8 有任何假设。

```rust
extern crate csv;
use csv::Error;

fn main() -> Result<(), Error> {
    let csv = "year,make,model,description
		1948,Porsche,356,Luxury sports car
		1967,Ford,Mustang fastback 1967,American car";

    let mut reader = csv::Reader::from_reader(csv.as_bytes());
    for record in reader.records() {
        let record = record?;
        println!(
            "In {}, {} built the {} model. It is a {}.",
            &record[0],
            &record[1],
            &record[2],
            &record[3]
        );
    }

    Ok(())
}
```

`serde` 将数据反序列化，为强类型结构。见[`csv::Reader::deserialize`]方法。

```rust
extern crate csv;
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate serde_derive;

# error_chain! {
#     foreign_links {
#         Reader(csv::Error);
#     }
# }
#
#[derive(Deserialize)]
struct Record {
    year: u16,
    make: String,
    model: String,
    description: String,
}

fn run() -> Result<()> {
    let csv = "year,make,model,description
1948,Porsche,356,Luxury sports car
1967,Ford,Mustang fastback 1967,American car";

    let mut reader = csv::Reader::from_reader(csv.as_bytes());

    for record in reader.deserialize() {
        let record: Record = record?;
        println!(
            "In {}, {} built the {} model. It is a {}.",
            record.year,
            record.make,
            record.model,
            record.description
        );
    }

    Ok(())
}
#
# quick_main!(run);
```

[`csv::byterecord`]: https://docs.rs/csv/*/csv/struct.ByteRecord.html
[`csv::reader::deserialize`]: https://docs.rs/csv/*/csv/struct.Reader.html#method.deserialize
[`csv::stringrecord`]: https://docs.rs/csv/*/csv/struct.StringRecord.html
