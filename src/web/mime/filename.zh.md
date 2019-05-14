## 从文件名，获取 MIME 类型

[![mime-badge]][mime] [![cat-encoding-badge]][cat-encoding]

下面的示例演示，如何使用[mime]箱子，从给出的文件名中，返回当前 MIME 类型。程序将检查文件扩展名，并与已知列表匹配。返回值为[`mime:Mime`]。

```rust
extern crate mime;
use mime::Mime;

fn find_mimetype (filename : &String) -> Mime{

    let parts : Vec<&str> = filename.split('.').collect();

    let res = match parts.last() {
            Some(v) =>
                match *v {
                    "png" => mime::IMAGE_PNG,
                    "jpg" => mime::IMAGE_JPEG,
                    "json" => mime::APPLICATION_JSON,
                    &_ => mime::TEXT_PLAIN,
                },
            None => mime::TEXT_PLAIN,
        };
    return res;
}

fn main() {
    let filenames = vec!("foobar.jpg", "foo.bar", "foobar.png");
    for file in filenames {
	    let mime = find_mimetype(&file.to_owned());
	 	println!("MIME for {}: {}", file, mime);
	 }

}
```

[`mime:mime`]: https://docs.rs/mime/*/mime/struct.Mime.html
