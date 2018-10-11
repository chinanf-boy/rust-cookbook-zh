
# 文件系统

| 食谱 | 板条箱 | 类别 |
| --- | --- | --- |
| [从文件读取字符串行][ex-std-read-lines] | [![std-badge]][std] | [![cat-filesystem-badge]][cat-filesystem] |
| [避免从同一文件中读写][ex-avoid-read-write] | [![same_file-badge]][same_file] | [![cat-filesystem-badge]][cat-filesystem] |
| [使用内存映射随机访问文件][ex-random-file-access] | [![memmap-badge]][memmap] | [![cat-filesystem-badge]][cat-filesystem] |
| [过去24小时修改的文件名][ex-file-24-hours-modified] | [![std-badge]][std] | [![cat-filesystem-badge]][cat-filesystem] [![cat-os-badge]][cat-os] |
| [查找给定路径的循环][ex-find-file-loops] | [![same_file-badge]][same_file] | [![cat-filesystem-badge]][cat-filesystem] |
| [递归查找重复文件名][ex-dedup-filenames] | [![walkdir-badge]][walkdir] | [![cat-filesystem-badge]][cat-filesystem] |
| [递归查找给定谓词的所有文件][ex-file-predicate] | [![walkdir-badge]][walkdir] | [![cat-filesystem-badge]][cat-filesystem] |
| [跳过DOTFACK时遍历目录][ex-file-skip-dot] | [![walkdir-badge]][walkdir] | [![cat-filesystem-badge]][cat-filesystem] |
| [递归计算给定深度的文件大小][ex-file-sizes] | [![walkdir-badge]][walkdir] | [![cat-filesystem-badge]][cat-filesystem] |
| [递归查找所有PNG文件][ex-glob-recursive] | [![glob-badge]][glob] | [![cat-filesystem-badge]][cat-filesystem] |
| [查找给定模式的所有文件,忽略文件名的情况][ex-glob-with] | [![glob-badge]][glob] | [![cat-filesystem-badge]][cat-filesystem] |

[ex-std-read-lines]: file/read-write.html#read-lines-of-strings-from-a-file

[ex-avoid-read-write]: file/read-write.html#avoid-writing-and-reading-from-a-same-file

[ex-random-file-access]: file/read-write.html#access-a-file-randomly-using-a-memory-map

[ex-file-24-hours-modified]: file/dir.html#file-names-that-have-been-modified-in-the-last-24-hours

[ex-find-file-loops]: file/dir.html#find-loops-for-a-given-path

[ex-dedup-filenames]: file/dir.html#recursively-find-duplicate-file-names

[ex-file-predicate]: file/dir.html#recursively-find-all-files-with-given-predicate

[ex-file-skip-dot]: file/dir.html#traverse-directories-while-skipping-dotfiles

[ex-file-sizes]: file/dir.html#recursively-calculate-file-sizes-at-given-depth

[ex-glob-recursive]: file/dir.html#find-all-png-files-recursively

[ex-glob-with]: file/dir.html#find-all-files-with-given-pattern-ignoring-filename-case

{{包括链接.zh.md}}
