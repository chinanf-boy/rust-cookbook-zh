
## 编码和解码十六进制

[![data-encoding-badge]][data-encoding] [![cat-encoding-badge]][cat-encoding]

该[`data_encoding`]箱子提供了一个`HEXUPPER::encode`需要的方法`&[u8]`并返回一个`String`包含数据的十六进制表示.

同样,a`HEXUPPER::decode`提供了一种方法`&[u8]`并返回一个`Vec<u8>`如果输入数据被成功解码.

下面的例子是隐蔽的`&[u8]`数据到十六进制等效.将此值与预期值进行比较.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate data_encoding;

use data_encoding::{HEXUPPER, DecodeError};
#
# error_chain! {
#     foreign_links {
#         Decode(DecodeError);
#     }
# }

fn run() -> Result<()> {
    let original = b"The quick brown fox jumps over the lazy dog.";
    let expected = "54686520717569636B2062726F776E20666F78206A756D7073206F76\
        657220746865206C617A7920646F672E";

    let encoded = HEXUPPER.encode(original);
    assert_eq!(encoded, expected);

    let decoded = HEXUPPER.decode(&encoded.into_bytes())?;
    assert_eq!(&decoded[..], &original[..]);

    Ok(())
}
#
# quick_main!(run);
```

[`data_encoding`]: https://docs.rs/data-encoding/*/data_encoding/
