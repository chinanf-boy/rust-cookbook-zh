
## 序列化和反序列化非结构化JSON

[![serde-json-badge]][serde-json] [![cat-encoding-badge]][cat-encoding]

该[`serde_json`]箱子提供了一个[`from_str`]解析一个函数`&str`JSON.

非结构化JSON可以解析为通用[`serde_json::Value`]能够表示任何有效JSON数据的类型.

下面的例子显示了一个`&str`正在解析的JSON.使用the声明预期值[`json!`]宏.

```rust
# #[macro_use]
# extern crate error_chain;
#[macro_use]
extern crate serde_json;

use serde_json::Value;
#
# error_chain! {
#     foreign_links {
#         Json(serde_json::Error);
#     }
# }

fn run() -> Result<()> {
    let j = r#"{
                 "userid": 103609,
                 "verified": true,
                 "access_privileges": [
                   "user",
                   "admin"
                 ]
               }"#;

    let parsed: Value = serde_json::from_str(j)?;

    let expected = json!({
        "userid": 103609,
        "verified": true,
        "access_privileges": [
            "user",
            "admin"
        ]
    });

    assert_eq!(parsed, expected);

    Ok(())
}
#
# quick_main!(run);
```

[`from_str`]: https://docs.serde.rs/serde_json/fn.from_str.html

[`json!`]: https://docs.serde.rs/serde_json/macro.json.html

[`serde_json`]: https://docs.serde.rs/serde_json/

[`serde_json::value`]: https://docs.serde.rs/serde_json/enum.Value.html
