# 文本处理

| 烹饪书                                                                   | 箱子                                                        | 类别                                                |
| ------------------------------------------------------------------------ | ----------------------------------------------------------- | --------------------------------------------------- |
| [收集 Unicode 字形][ex-unicode-graphemes]                                | [![unicode-segmentation-badge]][unicode-segmentation]       | [![cat-encoding-badge]][cat-text-processing]        |
| [从电子邮件地址，提取登录信息并验证][ex-verify-extract-email]            | [![regex-badge]][regex] [![lazy_static-badge]][lazy_static] | [![cat-text-processing-badge]][cat-text-processing] |
| [从文本中，提取独一的`#`标签列表][ex-extract-hashtags]                   | [![regex-badge]][regex] [![lazy_static-badge]][lazy_static] | [![cat-text-processing-badge]][cat-text-processing] |
| [从文本中，提取电话号码][ex-phone]                                       | [![regex-badge]][regex]                                     | [![cat-text-processing-badge]][cat-text-processing] |
| [通过匹配多个正则表达式，筛选日志文件][ex-regex-filter-log]              | [![regex-badge]][regex]                                     | [![cat-text-processing-badge]][cat-text-processing] |
| [将一个文本模式的所有出现项，替换为另一个模式。][ex-regex-replace-named] | [![regex-badge]][regex] [![lazy_static-badge]][lazy_static] | [![cat-text-processing-badge]][cat-text-processing] |
| [为一个自定义`struct`，实现`FromStr`trait][string_parsing-from_str]      | [![std-badge]][std]                                         | [![cat-text-processing-badge]][cat-text-processing] |

[ex-verify-extract-email]: text/regex.zh.html#verify-and-extract-login-from-an-email-address
[ex-extract-hashtags]: text/regex.zh.html#extract-a-list-of-unique-hashtags-from-a-text
[ex-phone]: text/regex.zh.html#extract-phone-numbers-from-text
[ex-regex-filter-log]: text/regex.zh.html#filter-a-log-file-by-matching-multiple-regular-expressions
[ex-regex-replace-named]: text/regex.zh.html#replace-all-occurrences-of-one-text-pattern-with-another-pattern
[ex-unicode-graphemes]: text/string_parsing.zh.html#collect-unicode-graphemes
[string_parsing-from_str]: text/string_parsing.zh.html#implement-the-fromstr-trait-for-a-custom-struct

{{#include links.zh.md}}
