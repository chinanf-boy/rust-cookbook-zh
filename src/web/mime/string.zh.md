## 从字符串获取 MIME 类型

[![mime-badge]][mime] [![cat-encoding-badge]][cat-encoding]

下面的示例演示，如何用[mime]箱子，从字符串中解析出一个[`MIME`]类型。[`FromStrError`]会在`unwrap_or`作用域，生成一个默认[`MIME`]类型。

```rust
extern crate mime;
use mime::{Mime, APPLICATION_OCTET_STREAM};

fn main() {
    let invalid_mime_type = "i n v a l i d";
    let default_mime = invalid_mime_type
        .parse::<Mime>()
        .unwrap_or(APPLICATION_OCTET_STREAM);

    println!(
        "MIME for {:?} used default value {:?}",
        invalid_mime_type, default_mime
    );

    let valid_mime_type = "TEXT/PLAIN";
    let parsed_mime = valid_mime_type
        .parse::<Mime>()
        .unwrap_or(APPLICATION_OCTET_STREAM);

    println!(
        "MIME for {:?} was parsed as {:?}",
        valid_mime_type, parsed_mime
    );
}
```

[`fromstrerror`]: https://docs.rs/mime/*/mime/struct.FromStrError.html
[`mime`]: https://docs.rs/mime/*/mime/struct.Mime.html
