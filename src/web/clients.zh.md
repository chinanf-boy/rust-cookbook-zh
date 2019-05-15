## 客户端

| 食谱                                                         | 箱子                                                    | 类别                                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------- | --------------------------------------------------------------------- |
| [发出 HTTP GET 请求][ex-url-basic]                           | [![reqwest-badge]][reqwest]                             | [![cat-net-badge]][cat-net]                                           |
| [查询 GitHub API][ex-rest-get]                               | [![reqwest-badge]][reqwest] [![serde-badge]][serde]     | [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding]     |
| [检查 API 资源，是否存在][ex-rest-head]                      | [![reqwest-badge]][reqwest]                             | [![cat-net-badge]][cat-net]                                           |
| [使用 GitHub API ，创建和删除 Gist][ex-rest-post]            | [![reqwest-badge]][reqwest] [![serde-badge]][serde]     | [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding]     |
| [使用一个（具备）分页的 RESTful API][ex-paginated-api]       | [![reqwest-badge]][reqwest] [![serde-badge]][serde]     | [![cat-net-badge]][cat-net] [![cat-encoding-badge]][cat-encoding]     |
| [将文件下载到临时目录][ex-url-download]                      | [![reqwest-badge]][reqwest] [![tempdir-badge]][tempdir] | [![cat-net-badge]][cat-net] [![cat-filesystem-badge]][cat-filesystem] |
| [使用 HTTP range 标头，进行部分下载][ex-progress-with-range] | [![reqwest-badge]][reqwest]                             | [![cat-net-badge]][cat-net]                                           |
| [POST 文件，到 paste.rs ][ex-file-post]                      | [![reqwest-badge]][reqwest]                             | [![cat-net-badge]][cat-net]                                           |

[ex-url-basic]: web/clients/requests.zh.html#make-a-http-get-request
[ex-rest-custom-params]: web/clients/requests.zh.html#set-custom-headers-and-url-parameters-for-a-rest-request
[ex-rest-get]: web/clients/apis.zh.html#query-the-github-api
[ex-rest-head]: web/clients/apis.zh.html#check-if-an-api-resource-exists
[ex-rest-post]: web/clients/apis.zh.html#create-and-delete-gist-with-github-api
[ex-paginated-api]: web/clients/apis.zh.html#consume-a-paginated-restful-api
[ex-handle-rate-limited-api]: web/clients/apis.zh.html#handle-a-rate-limited-api
[ex-url-download]: web/clients/download.zh.html#download-a-file-to-a-temporary-directory
[ex-progress-with-range]: web/clients/download.zh.html#make-a-partial-download-with-http-range-headers
[ex-file-post]: web/clients/download.zh.html#post-a-file-to-paste-rs

{{#include ../links.zh.md}}
