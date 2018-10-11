
# 网页编程

## 刮削网页

| 食谱 | 板条箱 | 类别 |
| --- | --- | --- |
| [从网页HTML中提取所有链接][ex-extract-links-webpage] | [![reqwest-badge]][reqwest] [![select-badge]][select] | [![cat-net-badge]][cat-net] |
| [检查网页断链][ex-check-broken-links] | [![reqwest-badge]][reqwest] [![select-badge]][select] [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [从MyaWiKi标记提取所有唯一链接][ex-extract-mediawiki-links] | [![reqwest-badge]][reqwest] [![regex-badge]][regex] | [![cat-net-badge]][cat-net] |

## 统一资源位置(URL)

| 食谱 | 板条箱 | 类别 |
| --- | --- | --- |
| [解析从字符串到URL的URL`Url`类型][ex-url-parse] | [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [通过删除路径段创建基本URL][ex-url-base] | [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [从基本URL创建新URL][ex-url-new-from-base] | [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [提取URL原点(方案/主机/端口)][ex-url-origin] | [![url-badge]][url] | [![cat-net-badge]][cat-net] |
| [从URL中删除片段标识符和查询对][ex-url-rm-frag] | [![url-badge]][url] | [![cat-net-badge]][cat-net] |

## 媒体类型(MIME)

| 食谱 | 板条箱 | 类别 |
| --- | --- | --- |
| [从字符串中获取MIME类型][ex-mime-from-string] | [![mime-badge]][mime] | [![cat-encoding-badge]][cat-encoding] |
| [从文件名中获得MIME类型][ex-mime-from-filename] | [![mime-badge]][mime] | [![cat-encoding-badge]][cat-encoding] |
| [解析HTTP响应的MIME类型][ex-http-response-mime-type] | [![mime-badge]][mime] [![reqwest-badge]][reqwest] | [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding] |

{{包括Web/Copys.Md}}

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

{{包括链接.Md}}
