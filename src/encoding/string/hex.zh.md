## 编码和解码十六进制

[![data-encoding-badge]][data-encoding] [![cat-encoding-badge]][cat-encoding]

这个[`data_encoding`]箱子提供一个`HEXUPPER::encode`方法，它会获取一个`&[u8]`，并返回一个`String`，其中包含数据的十六进制表示形式。

类似地，一个`HEXUPPER::decode`提供的方法，也获取一个`&[u8]`，并如果输入数据解码成功的话，就返回一个`Vec<u8>`。

下面的例子，将`&[u8]`数据转换为等效十六进制。将此值与预期值，进行比较。

```rust
extern crate data_encoding;

use data_encoding::{HEXUPPER, DecodeError};

fn main() -> Result<(), DecodeError> {
    let original = b"The quick brown fox jumps over the lazy dog.";
    let expected = "54686520717569636B2062726F776E20666F78206A756D7073206F76\
        657220746865206C617A7920646F672E";

    let encoded = HEXUPPER.encode(original);
    assert_eq!(encoded, expected);

    let decoded = HEXUPPER.decode(&encoded.into_bytes())?;
    assert_eq!(&decoded[..], &original[..]);

    Ok(())
}
```

[`data_encoding`]: https://docs.rs/data-encoding/*/data_encoding/
