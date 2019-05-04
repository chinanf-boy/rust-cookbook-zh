# 并发性

| 烹饪书                                                                 | 箱子                                                                                                              | 类别                                                                                                                  |
| ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [生成一个短命线程][ex-crossbeam-spawn]                                 | [![crossbeam-badge]][crossbeam]                                                                                   | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [保持全局可变状态][ex-global-mut-state]                                | [![lazy_static-badge]][lazy_static]                                                                               | [![cat-rust-patterns-badge]][cat-rust-patterns]                                                                       |
| [同时计算\*.iso 文件的 sha1 和][ex-threadpool-walk]                    | [![threadpool-badge]][threadpool] [![walkdir-badge]][walkdir] [![num_cpus-badge]][num_cpus] [![ring-badge]][ring] | [![cat-concurrency-badge]][cat-concurrency][![cat-filesystem-badge]][cat-filesystem]                                  |
| [将分形分派工作绘制到线程池][ex-threadpool-fractal]                    | [![threadpool-badge]][threadpool] [![num-badge]][num] [![num_cpus-badge]][num_cpus] [![image-badge]][image]       | [![cat-concurrency-badge]][cat-concurrency][![cat-science-badge]][cat-science][![cat-rendering-badge]][cat-rendering] |
| [并行改变数组的元素][ex-rayon-iter-mut]                                | [![rayon-badge]][rayon]                                                                                           | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [如果集合的任何或所有元素与给定谓词匹配，则并行测试][ex-rayon-any-all] | [![rayon-badge]][rayon]                                                                                           | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [并行使用给定谓词搜索项][ex-rayon-parallel-search]                     | [![rayon-badge]][rayon]                                                                                           | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [并行排序向量][ex-rayon-parallel-sort]                                 | [![rayon-badge]][rayon] [![rand-badge]][rand]                                                                     | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [平行地图缩小][ex-rayon-map-reduce]                                    | [![rayon-badge]][rayon]                                                                                           | [![cat-concurrency-badge]][cat-concurrency]                                                                           |
| [并行生成 JPG 缩略图][ex-rayon-thumbnails]                             | [![rayon-badge]][rayon] [![glob-badge]][glob] [![image-badge]][image]                                             | [![cat-concurrency-badge]][cat-concurrency][![cat-filesystem-badge]][cat-filesystem]                                  |

[ex-crossbeam-spawn]: concurrency/threads.html#spawn-a-short-lived-thread
[ex-global-mut-state]: concurrency/threads.html#maintain-global-mutable-state
[ex-threadpool-walk]: concurrency/threads.html#calculate-sha1-sum-of-iso-files-concurrently
[ex-threadpool-fractal]: concurrency/threads.html#draw-fractal-dispatching-work-to-a-thread-pool
[ex-rayon-iter-mut]: concurrency/parallel.html#mutate-the-elements-of-an-array-in-parallel
[ex-rayon-any-all]: concurrency/parallel.html#test-in-parallel-if-any-or-all-elements-of-a-collection-match-a-given-predicate
[ex-rayon-parallel-search]: concurrency/parallel.html#search-items-using-given-predicate-in-parallel
[ex-rayon-parallel-sort]: concurrency/parallel.html#sort-a-vector-in-parallel
[ex-rayon-map-reduce]: concurrency/parallel.html#map-reduce-in-parallel
[ex-rayon-thumbnails]: concurrency/parallel.html#generate-jpg-thumbnails-in-parallel

包含链接.md
