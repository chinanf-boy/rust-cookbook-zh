### 标准偏差

[![std-badge]][std] [![cat-science-badge]][cat-science]

此示例计算一组测量集合的标准偏差，和 z 分数。

标准偏差，定义为方差的平方根。此处()用 `f32` 的 [`sqrt`]计算，方差则是，每次测量与平均值[`mean`]之间差的平方的总和[`sum`]。

z 分数是（单个测量值 - 数据集的[`mean`] / 标准方差）。

```rust
fn mean(data: &[i32]) -> Option<f32> {
    let sum = data.iter().sum::<i32>() as f32;
    let count = data.len();

    match count {
        positive if positive > 0 => Some(sum/count as f32),
        _ => None,
    }
}

fn std_deviation(data: &[i32]) -> Option<f32> {
    match (mean(data), data.len()) {
        (Some(data_mean), count) if count > 0 => {
            let variance = data.iter().map(|value| {
                let diff = data_mean - (*value as f32);

                diff * diff
            }).sum::<f32>()/count as f32;

            Some(variance.sqrt())
        },
        _ => None
    }
}

fn main() {
    let data = [3, 1, 6, 1, 5, 8, 1, 8, 10, 11];

    let data_mean = mean(&data);
    println!("Mean is {:?}", data_mean);

    let data_std_deviation = std_deviation(&data);
    println!("Standard deviation is {:?}", data_std_deviation);

    let zscore = match (data_mean, data_std_deviation) {
        (Some(mean), Some(std_deviation)) => {
            let diff = data[4] as f32 - mean;

            Some(diff/std_deviation)
        },
        _ => None
    };
    println!("Z-score of data at index 4 (with value {}) is {:?}", data[4], zscore);
}
```

[sqrt]: https://doc.rust-lang.org/std/primitive.f32.html#method.sqrt
[sum]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.sum
[mean]: science/mathematics/statistics/central-tendency.html
