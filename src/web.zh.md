# 网页编程

## 刮擦网页

| 烹饪书                                                            | 箱子                                                                      | 类别                        |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------- | --------------------------- |
| [从网页 HTML 中提取所有链接][ex-extract-links-webpage]            | [![reqwest-badge]][reqwest] [![select-badge]][select]                     | [![cat-net-badge]][cat-net] |
| [检查网页是否有断开的链接][ex-check-broken-links]                 | [![reqwest-badge]][reqwest] [![select-badge]][select] [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [从 Mediawiki 标记中提取所有唯一链接][ex-extract-mediawiki-links] | [![reqwest-badge]][reqwest] [![regex-badge]][regex]                       | [![cat-net-badge]][cat-net] |

## 统一资源位置（URL）

| 烹饪书                                            | 箱子                | 类别                        |
| ------------------------------------------------- | ------------------- | --------------------------- |
| [将 URL 从字符串解析为`Url`类型][ex-url-parse]    | [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [通过删除路径段创建基 URL][ex-url-base]           | [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [从基 URL 创建新的 URL][ex-url-new-from-base]     | [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [提取 URL 源（方案/主机/端口）][ex-url-origin]    | [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [从 URL 中删除片段标识符和查询对][ex-url-rm-frag] | [![url-badge]][url] | [![cat-net-badge]][cat-net] |

## 媒体类型（MIME）

| 烹饪书                                                   | 箱子                                              | 类别                                                              |
| -------------------------------------------------------- | ------------------------------------------------- | ----------------------------------------------------------------- |
| [从字符串获取 mime 类型][ex-mime-from-string]            | [![mime-badge]][mime]                             | [![cat-encoding-badge]][cat-encoding]                             |
| [从文件名获取 mime 类型][ex-mime-from-filename]          | [![mime-badge]][mime]                             | [![cat-encoding-badge]][cat-encoding]                             |
| [分析 HTTP 响应的 mime 类型][ex-http-response-mime-type] | [![mime-badge]][mime] [![reqwest-badge]][reqwest] | [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding] |

包括 web/clients.md

[ex-extract-links-webpage]: web/scraping.html#extract-all-links-from-a-webpage-html
[ex-check-broken-links]: web/scraping.html#check-a-webpage-for-broken-links
[ex-extract-mediawiki-links]: web/scraping.html#extract-all-unique-links-from-a-mediawiki-markup
[ex-url-parse]: web/url.html#parse-a-url-from-a-string-to-a-url-type
[ex-url-base]: web/url.html#create-a-base-url-by-removing-path-segments
[ex-url-new-from-base]: web/url.html#create-new-urls-from-a-base-url
[ex-url-origin]: web/url.html#extract-the-url-origin-scheme--host--port
[ex-url-rm-frag]: web/url.html#remove-fragment-identifiers-and-query-pairs-from-a-url
[ex-mime-from-string]: web/mime.html#get-mime-type-from-string
[ex-mime-from-filename]: web/mime.html#get-mime-type-from-filename
[ex-http-response-mime-type]: web/mime.html#parse-the-mime-type-of-a-http-response

{{#include links.zh.md}}
