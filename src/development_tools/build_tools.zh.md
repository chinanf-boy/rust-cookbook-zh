# 构建时工具

本节介绍在编译箱子源代码之前，运行的“构建时”工具或代码。通常，构建时代码，位于**build.rs**文件，通常称为“构建脚本”。常见的用例，包括：Rust 代码生成，和捆绑的 C/C++/ASM 代码的编译。查看 crates.io 的 [主分支文档][build-script-docs]，了解更多信息。

{{#include build_tools/cc-bundled-static.zh.md}}

{{#include build_tools/cc-bundled-cpp.zh.md}}

{{#include build_tools/cc-defines.zh.md}}

{{#include ../links.zh.md}}

[build-script-docs]: http://doc.crates.io/build-script.html
