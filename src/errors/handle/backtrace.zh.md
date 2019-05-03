## 获取复杂错误场景的回溯

[![error-chain-badge]][error-chain] [![cat-rust-patterns-badge]][cat-rust-patterns]

这个方法演示了如何处理复杂的错误场景，然后打印回溯。它依赖于[`chain_err`]通过附加新错误来扩展错误。可以解开错误堆栈，从而提供更好的上下文来理解引发错误的原因。

以下配方尝试反序列化值`256`变成一个`u8`. 错误将从serde冒泡，然后是csv，最后是用户代码。

```rust
# extern crate csv;
#[macro_use]
extern crate error_chain;
# #[macro_use]
# extern crate serde_derive;
#
# use std::fmt;
#
# error_chain! {
#     foreign_links {
#         Reader(csv::Error);
#     }
# }

#[derive(Debug, Deserialize)]
struct Rgb {
    red: u8,
    blue: u8,
    green: u8,
}

impl Rgb {
    fn from_reader(csv_data: &[u8]) -> Result<Rgb> {
        let color: Rgb = csv::Reader::from_reader(csv_data)
            .deserialize()
            .nth(0)
            .ok_or("Cannot deserialize the first CSV record")?
            .chain_err(|| "Cannot deserialize RGB color")?;

        Ok(color)
    }
}

# impl fmt::UpperHex for Rgb {
#     fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
#         let hexa = u32::from(self.red) << 16 | u32::from(self.blue) << 8 | u32::from(self.green);
#         write!(f, "{:X}", hexa)
#     }
# }
#
fn run() -> Result<()> {
    let csv = "red,blue,green
102,256,204";

    let rgb = Rgb::from_reader(csv.as_bytes()).chain_err(|| "Cannot read CSV data")?;
    println!("{:?} to hexadecimal #{:X}", rgb, rgb);

    Ok(())
}

fn main() {
    if let Err(ref errors) = run() {
        eprintln!("Error level - description");
        errors
            .iter()
            .enumerate()
            .for_each(|(index, error)| eprintln!("└> {} - {}", index, error));

        if let Some(backtrace) = errors.backtrace() {
            eprintln!("{:?}", backtrace);
        }
#
#         // In a real use case, errors should handled. For example:
#         // ::std::process::exit(1);
    }
}
```

已呈现回溯错误：

```text
Error level - description
└> 0 - Cannot read CSV data
└> 1 - Cannot deserialize RGB color
└> 2 - CSV deserialize error: record 1 (line: 2, byte: 15): field 1: number too large to fit in target type
└> 3 - field 1: number too large to fit in target type
```

使用`RUST_BACKTRACE=1`显示详细信息[`backtrace`]与此错误关联。

[`backtrace`]: https://docs.rs/error-chain/*/error_chain/trait.ChainedError.html#tymethod.backtrace

[`chain_err`]: https://docs.rs/error-chain/*/error_chain/index.html#chaining-errors
