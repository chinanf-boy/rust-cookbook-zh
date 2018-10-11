
## 用另一个模式替换一个文本模式的所有出现.

[![regex-badge]][regex] [![lazy_static-badge]][lazy_static] [![cat-text-processing-badge]][cat-text-processing]

取代标准ISO 8601的所有发生*YYY-MM-DD*日期模式与等效美国英语日期与斜线.例如`2013-01-15`变成`01/15/2013`.

方法[`Regex::replace_all`]替换全部正则表达式的所有发生.`&str`实现`Replacer`允许变量的特性`$abcde`引用相应的命名捕获组`(?P<abcde>REGEX)`从搜索正则表达式.见[替换字符串语法]举例说明和逃避细节.

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
