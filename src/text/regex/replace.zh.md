## 将一个文本模式的所有出现项，替换为另一个模式。

[![regex-badge]][regex] [![lazy_static-badge]][lazy_static] [![cat-text-processing-badge]][cat-text-processing]

将所有出现的标准 ISO 8601 _YYY-MM－DD_ 的日期模式，替换等效的带斜线美式英文日期。例如`2013-01-15`变成`01/15/2013`.

方法[`Regex::replace_all`]会替换整个正则式的所有出现项。`&str`实现了`Replacer`trait，这允许类似`$abcde`这样的变量，去引用在搜索的正则式中，相应的命名捕获组`(?P<abcde>REGEX)`。见[替换字符串语法][replacement string syntax]示例，和转义的细节。

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
