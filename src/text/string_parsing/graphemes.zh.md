## 收集Unicode字形

[![unicode-segmentation-badge]][`unicode-segmentation`] [![cat-text-processing-badge]][cat-text-processing]

使用。从UTF-8字符串中收集单个Unicode字形[`UnicodeSegmentation::graphemes`]功能来自[`unicode-segmentation`]箱。

```rust
#[macro_use]
extern crate unicode_segmentation;
use unicode_segmentation::UnicodeSegmentation;

fn main() {
    let name = "José Guimarães\r\n";
    let graphemes = UnicodeSegmentation::graphemes(name, true)
    	.collect::<Vec<&str>>();
	assert_eq!(graphemes[3], "é");
}
```

[`unicodesegmentation::graphemes`]: https://docs.rs/unicode-segmentation/*/unicode_segmentation/trait.UnicodeSegmentation.html#tymethod.graphemes

[`unicode-segmentation`]: https://docs.rs/unicode-segmentation/1.2.1/unicode_segmentation/
