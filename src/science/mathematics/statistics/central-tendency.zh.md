### 集中趋势度量

[![std-badge]][std] [![cat-science-badge]][cat-science]

这些例子计算了包含在一个 Rust 数组中，数据集的集中趋势度量。对于空数据集，可能没有要计算的平均值、中值或模式，因此，每个函数都返回一个给调用方处理的[`Option`]。

第一个示例，计算平均值(集合中，总和/数量)，通过生成对`data`引用的迭代器，并使用[`sum`]和[`len`]分别确定值的总值和计数。

```rust
fn main() {
    let data = [3, 1, 6, 1, 5, 8, 1, 8, 10, 11];

    let sum = data.iter().sum::<i32>() as f32;
    let count = data.len();

    let mean = match count {
       positive if positive > 0 => Some(sum /count as f32),
       _ => None
    };

    println!("Mean of the data is {:?}", mean);
}
```

第二个示例使用 QuickSelect 算法，计算中间值，这避免了[`sort`]的完整排序，只对已知可能包含中间值的数据集分区，进行排序。这用到[`cmp`]和[`Ordering`]，简洁决定下一个要检查的分区，以及在每个步骤中，[`split_at`]为下一个分区进行静态选择。

```rust
use std::cmp::Ordering;

fn partition(data: &[i32]) -> Option<(Vec<i32>, i32, Vec<i32>)> {
    match data.len() {
        0 => None,
        _ => {
            let (pivot_slice, tail) = data.split_at(1);
            let pivot = pivot_slice[0];
            let (left, right) = tail.iter()
                .fold((vec![], vec![]), |mut splits, next| {
                    {
                        let (ref mut left, ref mut right) = &mut splits;
                        if next < &pivot {
                            left.push(*next);
                        } else {
                            right.push(*next);
                        }
                    }
                    splits
                });

            Some((left, pivot, right))
        }
    }
}

fn select(data: &[i32], k: usize) -> Option<i32> {
    let part = partition(data);

    match part {
        None => None,
        Some((left, pivot, right)) => {
            let pivot_idx = left.len();

            match pivot_idx.cmp(&k) {
                Ordering::Equal => Some(pivot),
                Ordering::Greater => select(&left, k),
                Ordering::Less => select(&right, k - (pivot_idx + 1)),
            }
        },
    }
}

fn median(data: &[i32]) -> Option<f32> {
    let size = data.len();

    match size {
        even if even % 2 == 0 => {
            let fst_med = select(data, (even/2) - 1);
            let snd_med = select(data, even/2);

            match (fst_med, snd_med) {
                (Some(fst), Some(snd)) => Some((fst + snd) as f32/2.0),
                _ => None
            }
        },
        odd => select(data, odd/2).map(|x| x as f32)
    }
}

fn main() {
    let data = [3, 1, 6, 1, 5, 8, 1, 8, 10, 11];

    let part = partition(&data);
    println!("Partition is {:?}", part);

    let sel = select(&data, 5);
    println!("Selection at ordered index {} is {:?}", 5, sel);

    let med = median(&data);
    println!("Median is {:?}", med);
}
```

最后一个示例是计算常见值，使用可变的[`HashMap`]，从集合中，收集每个不同整数的计数，会用到一个[`fold`]以及[`entry`]API。[`HashMap`]中，会用[`max_by_key`]搞到最常见的值。

```rust
use std::collections::HashMap;

fn main() {
    let data = [3, 1, 6, 1, 5, 8, 1, 8, 10, 11];

    let frequencies = data.iter().fold(HashMap::new(), |mut freqs, value| {
        *freqs.entry(value).or_insert(0) += 1;
        freqs
    });

    let mode = frequencies
        .into_iter()
        .max_by_key(|&(_, count)| count)
        .map(|(value, _)| *value);

    println!("Mode of the data is {:?}", mode);
}
```

[option]: https://doc.rust-lang.org/std/option/enum.Option.html
[sum]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.sum
[len]: https://doc.rust-lang.org/std/primitive.slice.html#method.len
[sort]: https://doc.rust-lang.org/std/primitive.slice.html#method.sort
[cmp]: https://doc.rust-lang.org/beta/std/cmp/trait.Ord.html#tymethod.cmp
[ordering]: https://doc.rust-lang.org/beta/std/cmp/enum.Ordering.html
[split_at]: https://doc.rust-lang.org/std/primitive.slice.html#method.split_at
[hashmap]: https://doc.rust-lang.org/std/collections/struct.HashMap.html
[fold]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.fold
[entry]: https://doc.rust-lang.org/std/collections/hash_map/enum.Entry.html
[max_by_key]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.max_by_key
