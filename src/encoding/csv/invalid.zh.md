## 使用 `serde` 处理无效的 csv 数据

[![csv-badge]][csv] [![serde-badge]][serde] [![cat-encoding-badge]][cat-encoding]

csv 文件通常包含无效数据。对于这些情况，`csv`箱子提供一个自定义反序列化程序，[`csv::invalid_option`]，自动将无效数据转换为 `None`值。

```rust
extern crate csv;
use csv::Error;
#[macro_use]
extern crate serde_derive;

#[derive(Debug, Deserialize)]
struct Record {
    name: String,
    place: String,
    #[serde(deserialize_with = "csv::invalid_option")]
    id: Option<u64>,
}

fn main() -> Result<(), Error> {
    let data = "name,place,id
mark,sydney,46.5
ashley,zurich,92
akshat,delhi,37
alisha,colombo,xyz";

    let mut rdr = csv::Reader::from_reader(data.as_bytes());
    for result in rdr.deserialize() {
        let record: Record = result?;
        println!("{:?}", record);
    }

    Ok(())
}
```

[`csv::invalid_option`]: https://docs.rs/csv/*/csv/fn.invalid_option.html
