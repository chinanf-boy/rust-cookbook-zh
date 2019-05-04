# rust-lang-nursery/rust-cookbook [![translate-svg]][translate-list]

[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list

「 这个*Rust Cookbook*是一个简单的[rust]生态系统的 crate 包集合, 展示完成常见编程任务的良好实践的示例.」

[中文](./readme.zh.md) | [english](https://github.com/rust-lang-nursery/rust-cookbook)

---

## 校对 🀄️

<!-- doc-templite START generated -->
<!-- repo = 'rust-lang-nursery/rust-cookbook' -->
<!-- commit = 'cb949b04c036c8cc0f864697590d33ca2aaf349f' -->
<!-- time = '2019-04-16' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018-10-10 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/rust-lang-nursery/rust-cookbook.svg
[commit]: https://github.com/rust-lang-nursery/rust-cookbook/tree/5d3f4a1e76c589c6d9c20b1cf55b104461cd09b5

<!-- doc-templite END generated -->

- [x] [readme]
- [x] [src/SUMMARY.md](src/SUMMARY.md)# 概要

- [x] [目录表](/src/intro.zh.md)
- [x] [关于](/src/about.zh.md)

- [x] [算法](/src/algorithms.zh.md)
  - [x] [生成随机值](/src/algorithms/randomness.zh.md)
    - [x] [randomness/rand.zh.md](/src/algorithms/randomness/rand.zh.md)
    - [x] [randomness/rand-range.zh.md](/src/algorithms/randomness/rand-range.zh.md)
    - [x] [randomness/rand-dist.zh.md](/src/algorithms/randomness/rand-dist.zh.md)
    - [x] [randomness/rand-custom.zh.md](/src/algorithms/randomness/rand-custom.zh.md)
    - [x] [randomness/rand-passwd.zh.md](/src/algorithms/randomness/rand-passwd.zh.md)
    - [x] [randomness/rand-choose.zh.md](/src/algorithms/randomness/rand-choose.zh.md)
  - [x] [排序向量](/src/algorithms/sorting.zh.md)
    - [ ] [sorting/sort.zh.md](./src/algorithms/sorting/sort.zh.md)
    - [ ] [sorting/sort_float.zh.md](./src/algorithms/sorting/sort_float.zh.md)
    - [ ] [sorting/sort_struct.zh.md](./src/algorithms/sorting/sort_struct.zh.md)
- [ ] [命令行](/src/cli.zh.md)
  - [ ] [参数解析](/src/cli/arguments.zh.md)
  - [ ] [ANSI 终端](/src/cli/ansi_terminal.zh.md)
- [ ] [压缩](/src/compression.zh.md)
  - [ ] [与 Tarballs 合作](/src/compression/tar.zh.md)
- [ ] [并发性](/src/concurrency.zh.md)
  - [ ] [显式线程](/src/concurrency/threads.zh.md)
  - [ ] [数据并行性](/src/concurrency/parallel.zh.md)
- [ ] [密码学](/src/cryptography.zh.md)
  - [ ] [哈希](/src/cryptography/hashing.zh.md)
  - [ ] [加密](/src/cryptography/encryption.zh.md)
- [ ] [数据结构](/src/data_structures.zh.md)
  - [ ] [位字段](/src/data_structures/bitfield.zh.md)
- [ ] [数据库](/src/database.zh.md)
  - [ ] [SQLite](/src/database/sqlite.zh.md)
  - [ ] [Postgres](/src/database/postgres.zh.md)
- [ ] [日期和时间](/src/datetime.zh.md)
  - [ ] [持续时间和计算](/src/datetime/duration.zh.md)
  - [ ] [解析与显示](/src/datetime/parse.zh.md)
- [ ] [开发工具](/src/development_tools.zh.md)
  - [ ] [调试](/src/development_tools/debugging.zh.md)
    - [ ] [日志消息](/src/development_tools/debugging/log.zh.md)
    - [ ] [配置日志记录](/src/development_tools/debugging/config_log.zh.md)
  - [ ] [版本控制](/src/development_tools/versioning.zh.md)
  - [ ] [建立时间工具](/src/development_tools/build_tools.zh.md)
- [ ] [编码](/src/encoding.zh.md)
  - [ ] [字符集](/src/encoding/strings.zh.md)
  - [ ] [CSV 处理](/src/encoding/csv.zh.md)
  - [ ] [结构化数据](/src/encoding/complex.zh.md)
- [ ] [错误处理](/src/errors.zh.md)
  - [ ] [处理错误变量](/src/errors/handle.zh.md)
- [ ] [文件系统](/src/file.zh.md)
  - [ ] [读写](/src/file/read-write.zh.md)
  - [ ] [目录穿越漏洞](/src/file/dir.zh.md)
- [ ] [硬件支持](/src/hardware.zh.md)
  - [ ] [处理器](/src/hardware/processor.zh.md)
- [ ] [内存管理](/src/mem.zh.md)
  - [ ] [全局静态](/src/mem/global_static.zh.md)
- [ ] [网络](/src/net.zh.md)
  - [ ] [服务器](/src/net/server.zh.md)
- [ ] [操作系统](/src/os.zh.md)
  - [ ] [外部命令](/src/os/external.zh.md)
- [ ] [科学类](/src/science.zh.md)
  - [ ] [数学](/src/science/mathematics.zh.md)
    - [ ] [线性代数](/src/science/mathematics/linear_algebra.zh.md)
    - [ ] [三角法](/src/science/mathematics/trigonometry.zh.md)
    - [ ] [复数](/src/science/mathematics/complex_numbers.zh.md)
    - [ ] [统计](/src/science/mathematics/statistics.zh.md)
    - [ ] [混杂](/src/science/mathematics/miscellaneous.zh.md)
- [ ] [文本处理](/src/text.zh.md)
  - [ ] [正则表达式](/src/text/regex.zh.md)
  - [ ] [字符串解析](/src/text/string_parsing.zh.md)
- [ ] [网页编程](/src/web.zh.md)
  - [ ] [提取链接](/src/web/scraping.zh.md)
  - [ ] [统一资源定位地址:URL](/src/web/url.zh.md)
  - [ ] [媒体类型](/src/web/mime.zh.md)
  - [ ] [客户端](/src/web/clients.zh.md)
    - [ ] [提出请求](/src/web/clients/requests.zh.md)
    - [ ] [调用 Web API](/src/web/clients/apis.zh.md)
    - [ ] [下载](/src/web/clients/download.zh.md)

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[If help, **buy** me coffee —— 营养跟不上了，给我来瓶营养快线吧! 💰](https://github.com/chinanf-boy/live-need-money)

---

# Rust Cookbook  [![Build Status travis]][travis] [![Build Status appveyor]][appveyor]

[build status travis]: https://api.travis-ci.org/rust-lang-nursery/rust-cookbook.svg?branch=master
[travis]: https://travis-ci.org/rust-lang-nursery/rust-cookbook
[build status appveyor]: https://ci.appveyor.com/api/projects/status/k56hklb7puv7c4he?svg=true
[appveyor]: https://ci.appveyor.com/project/rust-lang-libs/rust-cookbook

**[read it here]**.

这个*Rust Cookbook*是一个简单的[rust]生态系统的 crate 包集合, 展示完成常见编程任务的良好实践的示例.

这些例子是完整的,适合直接复制到新的 Cargo 项目中.它们经过测试并保证可以正常工作.

## 离线阅读

如果您想在本地阅读:

```bash
$ git clone https://github.com/rust-lang-nursery/rust-cookbook
$ cd rust-cookbook
$ cargo install mdbook --vers "0.1.8"
$ mdbook serve --open
```

这会输出在`book`子目录.可以从打开 Web 浏览器

```bash
$ xdg-open ./book/index.html # linux
$ start .\book\index.html    # windows
$ open ./book/index.html     # mac
```

[read it here]: https://rust-lang-nursery.github.io/rust-cookbook
[rust]: https://www.rust-lang.org/

## 贡献

这个项目旨在让新的 [rust] 程序员更容易做出贡献,并且是参与 Rust 社区的简单方法.它需要并欢迎帮助.详情见[贡献.](contributing.zh.md).

- [ ] [ ] 详情在 GitHub 上的[CONTRIBUTING.zh.md](./CONTRIBUTING.zh.md).

## 执照[![cc0-badge]][cc0-deed]

Rust Cookbook 根据 Creative Commons Zero v1.0 Universal License 获得([许可证 CC0](LICENSE-CC0)要么<https://creativecommons.org/publicdomain/zero/1.0/legalcode>)

除非您另有明确说明,否则您按照 CC0-1.0 许可证的规定有意提交包含在 Rust Cookbook 中的任何贡献, 应为[致力于公共领域][cc0-deed]上所述的,并没有任何附加条款或条件.

[cc0-deed]: https://creativecommons.org/publicdomain/zero/1.0/deed.en
[cc0-badge]: https://mirrors.creativecommons.org/presskit/buttons/80x15/svg/cc-zero.svg
