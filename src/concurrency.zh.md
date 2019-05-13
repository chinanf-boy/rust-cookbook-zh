# 并发性

| 烹饪书                                                                 | 箱子                                                                                                              | 类别                                                                                                                  |
| ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [生成一个短命线程][ex-crossbeam-spawn]                                 | [![crossbeam-badge]][crossbeam]                                                                                   | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [保持全局可变状态][ex-global-mut-state]                                | [![lazy_static-badge]][lazy_static]                                                                               | [![cat-rust-patterns-badge]][cat-rust-patterns]                                                                       |
| [并发计算所有 `*.iso` 文件的 SHA1 和][ex-threadpool-walk]              | [![threadpool-badge]][threadpool] [![walkdir-badge]][walkdir] [![num_cpus-badge]][num_cpus] [![ring-badge]][ring] | [![cat-concurrency-badge]][cat-concurrency][![cat-filesystem-badge]][cat-filesystem]                                  |
| [将绘制分形工作，分派到线程池][ex-threadpool-fractal]                  | [![threadpool-badge]][threadpool] [![num-badge]][num] [![num_cpus-badge]][num_cpus] [![image-badge]][image]       | [![cat-concurrency-badge]][cat-concurrency][![cat-science-badge]][cat-science][![cat-rendering-badge]][cat-rendering] |
| [并行，改变数组的元素][ex-rayon-iter-mut]                              | [![rayon-badge]][rayon]                                                                                           | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [如果集合的任何或所有元素，与给定物匹配，则并行测试][ex-rayon-any-all] | [![rayon-badge]][rayon]                                                                                           | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [并行，使用给定物搜索项][ex-rayon-parallel-search]                     | [![rayon-badge]][rayon]                                                                                           | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [并行，排序 vector][ex-rayon-parallel-sort]                            | [![rayon-badge]][rayon] [![rand-badge]][rand]                                                                     | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [并行，缩小地图][ex-rayon-map-reduce]                                  | [![rayon-badge]][rayon]                                                                                           | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [并行，生成 JPG 缩略图][ex-rayon-thumbnails]                           | [![rayon-badge]][rayon] [![glob-badge]][glob] [![image-badge]][image]                                             | [![cat-concurrency-badge]][cat-concurrency][![cat-filesystem-badge]][cat-filesystem]                                  |

[ex-crossbeam-spawn]: concurrency/threads.zh.html#spawn-a-short-lived-thread
[ex-global-mut-state]: concurrency/threads.zh.html#maintain-global-mutable-state
[ex-threadpool-walk]: concurrency/threads.zh.html#calculate-sha1-sum-of-iso-files-concurrently
[ex-threadpool-fractal]: concurrency/threads.zh.html#draw-fractal-dispatching-work-to-a-thread-pool
[ex-rayon-iter-mut]: concurrency/parallel.zh.html#mutate-the-elements-of-an-array-in-parallel
[ex-rayon-any-all]: concurrency/parallel.zh.html#test-in-parallel-if-any-or-all-elements-of-a-collection-match-a-given-predicate
[ex-rayon-parallel-search]: concurrency/parallel.zh.html#search-items-using-given-predicate-in-parallel
[ex-rayon-parallel-sort]: concurrency/parallel.zh.html#sort-a-vector-in-parallel
[ex-rayon-map-reduce]: concurrency/parallel.zh.html#map-reduce-in-parallel
[ex-rayon-thumbnails]: concurrency/parallel.zh.html#generate-jpg-thumbnails-in-parallel

{{#include links.zh.md}}
