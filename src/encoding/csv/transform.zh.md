## 转换 csv 列

[![csv-badge]][csv] [![serde-badge]][serde] [![cat-encoding-badge]][cat-encoding]

将包含颜色名称和十六进制颜色的 csv 文件转换为具有颜色名称和 RGB 颜色的文件。利用[猪瘟病毒]箱子读取和写入 csv 文件，以及[塞尔德]对字节之间的行进行反序列化和序列化。

见[`csv::Reader::deserialize`]，[`serde::Deserialize`]和[`std::str::FromStr`]

```rust
extern crate csv;
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate serde_derive;
extern crate serde;

use csv::{Reader, Writer};
use serde::{de, Deserialize, Deserializer};
use std::str::FromStr;
#
# error_chain! {
#    foreign_links {
#        CsvError(csv::Error);
#        ParseInt(std::num::ParseIntError);
#        CsvInnerError(csv::IntoInnerError<Writer<Vec<u8>>>);
#        IO(std::fmt::Error);
#        UTF8(std::string::FromUtf8Error);
#    }
# }

#[derive(Debug)]
struct HexColor {
    red: u8,
    green: u8,
    blue: u8,
}

#[derive(Debug, Deserialize)]
struct Row {
    color_name: String,
    color: HexColor,
}

impl FromStr for HexColor {
    type Err = Error;

    fn from_str(hex_color: &str) -> std::result::Result<Self, Self::Err> {
        let trimmed = hex_color.trim_matches('#');
        if trimmed.len() != 6 {
            Err("Invalid length of hex string".into())
        } else {
            Ok(HexColor {
                red: u8::from_str_radix(&trimmed[..2], 16)?,
                green: u8::from_str_radix(&trimmed[2..4], 16)?,
                blue: u8::from_str_radix(&trimmed[4..6], 16)?,
            })
        }
    }
}

impl<'de> Deserialize<'de> for HexColor {
    fn deserialize<D>(deserializer: D) -> std::result::Result<Self, D::Error>
    where
        D: Deserializer<'de>,
    {
        let s = String::deserialize(deserializer)?;
        FromStr::from_str(&s).map_err(de::Error::custom)
    }
}

fn run() -> Result<()> {
    let data = "color_name,color
red,#ff0000
green,#00ff00
blue,#0000FF
periwinkle,#ccccff
magenta,#ff00ff"
        .to_owned();
    let mut out = Writer::from_writer(vec![]);
    let mut reader = Reader::from_reader(data.as_bytes());
    for result in reader.deserialize::<Row>() {
        let res = result?;
        out.serialize((
            res.color_name,
            res.color.red,
            res.color.green,
            res.color.blue,
        ))?;
    }
    let written = String::from_utf8(out.into_inner()?)?;
    assert_eq!(Some("magenta,255,0,255"), written.lines().last());
    println!("{}", written);
    Ok(())
}
#
# quick_main!(run);
```

[`csv::reader::deserialize`]: https://docs.rs/csv/*/csv/struct.Reader.html#method.deserialize
[`csv::invalid_option`]: https://docs.rs/csv/*/csv/fn.invalid_option.html
[`serde::deserialize`]: https://docs.rs/serde/*/serde/trait.Deserialize.html
[`std::str::fromstr`]: https://doc.rust-lang.org/std/str/trait.FromStr.html
