
## 使用Serde处理无效的CSV数据

[![csv-badge]][csv] [![serde-badge]][serde] [![cat-encoding-badge]][cat-encoding]

CSV文件通常包含无效数据.对于这些情况,`csv`crate提供自定义反序列化器,[`csv::invalid_option`],自动将无效数据转换为无值.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate csv;
#[macro_use]
extern crate serde_derive;

#[derive(Debug, Deserialize)]
struct Record {
    name: String,
    place: String,
    #[serde(deserialize_with = "csv::invalid_option")]
    id: Option<u64>,
}
#
# error_chain! {
#     foreign_links {
#         CsvError(csv::Error);
#     }
# }

fn run() -> Result<()> {
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
#
# quick_main!(run);
```

[`csv::invalid_option`]: https://docs.rs/csv/*/csv/fn.invalid_option.html
