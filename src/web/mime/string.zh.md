
## 从字符串中获取MIME类型

[![mime-badge]][mime] [![cat-encoding-badge]][cat-encoding]

下面的示例演示如何解析[`MIME`]使用字符串从[哑剧演员]机箱.[`FromStrError`]产生默认值[`MIME`]键入`unwrap_or`条款.

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
