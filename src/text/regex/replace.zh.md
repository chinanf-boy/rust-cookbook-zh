## 将一个文本模式的所有出现项替换为另一个模式。

[![regex-badge]][regex] [![lazy_static-badge]][lazy_static] [![cat-text-processing-badge]][cat-text-processing]

替换所有出现的标准ISO 8601*YYY-MM－DD*带斜线的等效美英日期的日期模式。例如`2013-01-15`变成`01/15/2013`.

方法[`Regex::replace_all`]替换整个regex的所有出现项。`&str`实现`Replacer`允许变量的特征`$abcde`引用相应的命名捕获组`(?P<abcde>REGEX)`从搜索regex。见[替换字符串语法]例如和转义细节。

```rust
extern crate regex;
#[macro_use]
extern crate lazy_static;

use std::borrow::Cow;
use regex::Regex;

fn reformat_dates(before: &str) -> Cow<str> {
    lazy_static! {
        static ref ISO8601_DATE_REGEX : Regex = Regex::new(
            r"(?P<y>\d{4})-(?P<m>\d{2})-(?P<d>\d{2})"
            ).unwrap();
    }
    ISO8601_DATE_REGEX.replace_all(before, "$m/$d/$y")
}

fn main() {
    let before = "2012-03-14, 2013-01-15 and 2014-07-05";
    let after = reformat_dates(before);
    assert_eq!(after, "03/14/2012, 01/15/2013 and 07/05/2014");
}
```

[`regex::replace_all`]: https://docs.rs/regex/*/regex/struct.Regex.html#method.replace_all

[replacement string syntax]: https://docs.rs/regex/*/regex/struct.Regex.html#replacement-string-syntax
