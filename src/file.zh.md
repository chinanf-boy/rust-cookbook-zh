# 文件系统

| 烹饪书                                                     | 箱子                            | 类别                                                                |
| ---------------------------------------------------------- | ------------------------------- | ------------------------------------------------------------------- |
| [从文件中，读取字符串行][ex-std-read-lines]                  | [![std-badge]][std]             | [![cat-filesystem-badge]][cat-filesystem]                           |
| [避免写入和读取，同一文件][ex-avoid-read-write]              | [![same_file-badge]][same_file] | [![cat-filesystem-badge]][cat-filesystem]                           |
| [随机使用内存映射，访问文件][ex-random-file-access]          | [![memmap-badge]][memmap]       | [![cat-filesystem-badge]][cat-filesystem]                           |
| [过去 24 小时内，修改过的文件名][ex-file-24-hours-modified]  | [![std-badge]][std]             | [![cat-filesystem-badge]][cat-filesystem] [![cat-os-badge]][cat-os] |
| [查找给定路径的循环][ex-find-file-loops]                   | [![same_file-badge]][same_file] | [![cat-filesystem-badge]][cat-filesystem]                           |
| [递归查找，重复的文件名][ex-dedup-filenames]                 | [![walkdir-badge]][walkdir]     | [![cat-filesystem-badge]][cat-filesystem]                           |
| [递归查找，具有给定断言的所有文件][ex-file-predicate]        | [![walkdir-badge]][walkdir]     | [![cat-filesystem-badge]][cat-filesystem]                           |
| [跳过点(隐藏)文件，遍历目录][ex-file-skip-dot]                   | [![walkdir-badge]][walkdir]     | [![cat-filesystem-badge]][cat-filesystem]                           |
| [在给定深度(目录)，递归计算文件大小][ex-file-sizes]                | [![walkdir-badge]][walkdir]     | [![cat-filesystem-badge]][cat-filesystem]                           |
| [递归查找，所有 PNG 文件][ex-glob-recursive]                 | [![glob-badge]][glob]           | [![cat-filesystem-badge]][cat-filesystem]                           |
| [查找具有给定模式的所有文件，忽略文件名大小写][ex-glob-with] | [![glob-badge]][glob]           | [![cat-filesystem-badge]][cat-filesystem]                           |

[ex-std-read-lines]: file/read-write.zh.html#read-lines-of-strings-from-a-file
[ex-avoid-read-write]: file/read-write.zh.html#avoid-writing-and-reading-from-a-same-file
[ex-random-file-access]: file/read-write.zh.html#access-a-file-randomly-using-a-memory-map
[ex-file-24-hours-modified]: file/dir.zh.html#file-names-that-have-been-modified-in-the-last-24-hours
[ex-find-file-loops]: file/dir.zh.html#find-loops-for-a-given-path
[ex-dedup-filenames]: file/dir.zh.html#recursively-find-duplicate-file-names
[ex-file-predicate]: file/dir.zh.html#recursively-find-all-files-with-given-predicate
[ex-file-skip-dot]: file/dir.zh.html#traverse-directories-while-skipping-dotfiles
[ex-file-sizes]: file/dir.zh.html#recursively-calculate-file-sizes-at-given-depth
[ex-glob-recursive]: file/dir.zh.html#find-all-png-files-recursively
[ex-glob-with]: file/dir.zh.html#find-all-files-with-given-pattern-ignoring-filename-case

{{#include links.zh.md}}
