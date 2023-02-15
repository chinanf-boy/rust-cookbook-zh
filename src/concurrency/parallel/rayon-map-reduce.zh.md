## Map-reduce 并行

[![rayon-badge]][rayon] [![cat-concurrency-badge]][cat-concurrency]

这个例子使用[`rayon::filter`]，[`rayon::map`]，和[`rayon::reduce`]，计算年龄超过 30 岁的`Person`对象的平均年龄。

[`rayon::filter`]返回满足给定断言的集合，其中的元素。[`rayon::map`]对每个元素执行一个操作，创建一个新的迭代，然后[`rayon::reduce`]：执行带有一个当前元素，和前一个(执行结果)的操作。还显示了使用[`rayon::sum`]，与本例中的 reduce 操作，具有相同的结果。

```rust
extern crate rayon;

use rayon::prelude::*;

struct Person {
    age: u32,
}

fn main() {
    let v: Vec<Person> = vec![
        Person { age: 23 },
        Person { age: 19 },
        Person { age: 42 },
        Person { age: 17 },
        Person { age: 17 },
        Person { age: 31 },
        Person { age: 30 },
    ];

    let num_over_30 = v.par_iter().filter(|&x| x.age > 30).count() as f32;
    let sum_over_30 = v.par_iter()
        .map(|x| x.age)
        .filter(|&x| x > 30)
        .reduce(|| 0, |x, y| x + y);

    let alt_sum_30: u32 = v.par_iter()
        .map(|x| x.age)
        .filter(|&x| x > 30)
        .sum();

    let avg_over_30 = sum_over_30 as f32/num_over_30;
    let alt_avg_over_30 = alt_sum_30 as f32/ num_over_30;

    assert!((avg_over_30 - alt_avg_over_30).abs() < std::f32::EPSILON);
    println!("The average age of people older than 30 is {}", avg_over_30);
}
```

[`rayon::filter`]: https://docs.rs/rayon/*/rayon/iter/trait.ParallelIterator.html#method.filter
[`rayon::map`]: https://docs.rs/rayon/*/rayon/iter/trait.ParallelIterator.html#method.map
[`rayon::reduce`]: https://docs.rs/rayon/*/rayon/iter/trait.ParallelIterator.html#method.reduce
[`rayon::sum`]: https://docs.rs/rayon/*/rayon/iter/trait.ParallelIterator.html#method.sum
