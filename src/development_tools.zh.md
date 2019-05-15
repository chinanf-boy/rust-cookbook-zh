# 开发工具

{{#include development_tools/debugging.zh.md}}

## 版本控制

| 食谱                                                   | 箱子                      | 类别                                                                          |
| ------------------------------------------------------ | ------------------------- | ----------------------------------------------------------------------------- |
| [解析，并增加版本字符串][ex-semver-increment]          | [![semver-badge]][semver] | [![cat-config-badge]][cat-config]                                             |
| [分析，复杂版本字符串][ex-semver-complex]              | [![semver-badge]][semver] | [![cat-config-badge]][cat-config]                                             |
| [检查给定版本，是否为预发布版本][ex-semver-prerelease] | [![semver-badge]][semver] | [![cat-config-badge]][cat-config]                                             |
| [查找，满足给定范围的最新版本][ex-semver-latest]       | [![semver-badge]][semver] | [![cat-config-badge]][cat-config]                                             |
| [检查外部命令版本的兼容性][ex-semver-command]          | [![semver-badge]][semver] | [![cat-text-processing-badge]][cat-text-processing] [![cat-os-badge]][cat-os] |

## 构建时

| 食谱                                                   | 箱子              | 类别                                                    |
| ------------------------------------------------------ | ----------------- | ------------------------------------------------------- |
| [静态编译，并链接到捆绑的 C 库][ex-cc-static-bundled]  | [![cc-badge]][cc] | [![cat-development-tools-badge]][cat-development-tools] |
| [编译，并链接到捆绑的 C++库][ex-cc-static-bundled-cpp] | [![cc-badge]][cc] | [![cat-development-tools-badge]][cat-development-tools] |
| [自定义设置时，编译 C 库][ex-cc-custom-defines]        | [![cc-badge]][cc] | [![cat-development-tools-badge]][cat-development-tools] |

[ex-semver-increment]: development_tools/versioning.zh.html#parse-and-increment-a-version-string
[ex-semver-complex]: development_tools/versioning.zh.html#parse-a-complex-version-string
[ex-semver-prerelease]: development_tools/versioning.zh.html#check-if-given-version-is-pre-release
[ex-semver-latest]: development_tools/versioning.zh.html#find-the-latest-version-satisfying-given-range
[ex-semver-command]: development_tools/versioning.zh.html#check-external-command-version-for-compatibility
[ex-cc-static-bundled]: development_tools/build_tools.zh.html#compile-and-link-statically-to-a-bundled-c-library
[ex-cc-static-bundled-cpp]: development_tools/build_tools.zh.html#compile-and-link-statically-to-a-bundled-c-library-1
[ex-cc-custom-defines]: development_tools/build_tools.zh.html#compile-a-c-library-while-setting-custom-defines

{{#include links.zh.md}}
