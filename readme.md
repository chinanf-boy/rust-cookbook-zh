# rust-lang-nursery/rust-cookbook [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 这个*Rust Cookbook*是一个简单的[rust]生态系统的crate包集合, 展示完成常见编程任务的良好实践的示例.」

[中文](./readme.md) | [english](https://github.com/rust-lang-nursery/rust-cookbook)

---

## 校对 🀄️

<!-- doc-templite START generated -->
<!-- repo = 'rust-lang-nursery/rust-cookbook' -->
<!-- commit = '5d3f4a1e76c589c6d9c20b1cf55b104461cd09b5' -->
<!-- time = '2018-10-10' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018-10-10 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/rust-lang-nursery/rust-cookbook.svg
[commit]: https://github.com/rust-lang-nursery/rust-cookbook/tree/5d3f4a1e76c589c6d9c20b1cf55b104461cd09b5

<!-- doc-templite END generated -->

- [ ] [readme]

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc -->
<!-- END doctoc -->

# Rust Cookbook  [![Build Status travis]][travis] [![Build Status appveyor]][appveyor]

[build status travis]: https://api.travis-ci.org/rust-lang-nursery/rust-cookbook.svg?branch=master
[travis]: https://travis-ci.org/rust-lang-nursery/rust-cookbook
[build status appveyor]: https://ci.appveyor.com/api/projects/status/k56hklb7puv7c4he?svg=true
[appveyor]: https://ci.appveyor.com/project/rust-lang-libs/rust-cookbook

**[在这里阅读]**.

这个*Rust Cookbook*是一个简单的[rust]生态系统的crate包集合, 展示完成常见编程任务的良好实践的示例.

这些例子是完整的,适合直接复制到新的货物项目中.它们经过测试并保证可以正常工作.

## 离线阅读

如果您想在本地阅读:

```bash
$ git clone https://github.com/rust-lang-nursery/rust-cookbook
$ cd rust-cookbook
$ cargo install mdbook --vers "0.1.8"
$ mdbook serve --open
```

输出也可以从打开`book`Web 浏览器中的子目录.

```bash
$ xdg-open ./book/index.html # linux
$ start .\book\index.html    # windows
$ open ./book/index.html     # mac
```

[read it here]: https://rust-lang-nursery.github.io/rust-cookbook
[rust]: https://www.rust-lang.org/

## 贡献

该项目旨在轻松实现新目标[rust]程序员为 Rust 社区做出贡献,并且很容易参与其中.它需要并欢迎帮助.

详情见[CONTRIBUTING.zh.md]在 GitHub 上.

[contributing.md]: https://github.com/rust-lang-nursery/rust-cookbook/blob/master/CONTRIBUTING.md

## 执照[![cc0-badge]][cc0-deed]

Rust Cookbook 根据 Creative Commons Zero v1.0 Universal License 获得([许可证 CC0](LICENSE-CC0)要么<https://creativecommons.org/publicdomain/zero/1.0/legalcode>)

除非您另有明确说明,否则您按照 CC0-1.0 许可证的规定有意提交包含在 Rust Cookbook 中的任何贡献应为[致力于公共领域][cc0-deed]如上所述,没有任何附加条款或条件.

[cc0-deed]: https://creativecommons.org/publicdomain/zero/1.0/deed.en
[cc0-badge]: https://mirrors.creativecommons.org/presskit/buttons/80x15/svg/cc-zero.svg
