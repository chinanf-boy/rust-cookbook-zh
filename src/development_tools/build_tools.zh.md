
# 构建时间工具

本节介绍"构建时"工具,或者在编译包的源代码之前运行的代码.通常,构建时代码存在于**build.rs**文件,通常称为"构建脚本".常见用例包括生锈代码生成和捆绑的C/C ++/asm代码的编译.见crates.io's[有关此事的文件][build-script-docs]了解更多信息.

{{#include build_tools/cc-bundled-static.zh.md}}

{{#include build_tools/cc-bundled-cpp.zh.md}}

{{#include build_tools/cc-defines.zh.md}}

{{#include ../links.zh.md}}

[build-script-docs]: http://doc.crates.io/build-script.html
