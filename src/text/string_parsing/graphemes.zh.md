## 收集 Unicode 字形

[![unicode-segmentation-badge]][`unicode-segmentation`] [![cat-text-processing-badge]][cat-text-processing]

[`unicode-segmentation`]箱子的[`UnicodeSegmentation::graphemes`]函数，可用来，从 UTF-8 字符串中，收集单个 Unicode 字形。

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
