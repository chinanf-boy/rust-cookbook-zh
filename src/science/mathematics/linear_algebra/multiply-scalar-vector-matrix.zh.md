## 用 vector 和 矩阵，乘一个标量

[![ndarray-badge]][ndarray] [![cat-science-badge]][cat-science]

用[`ndarray::arr1`]创建一个，一维数组（vector），二维数组（矩阵）就用[`ndarray::arr2`]。 首先，将一个标量乘以 vector ，得到另一个 vector。然后，矩阵用[`ndarray::Array2::dot`]，乘以这个新的 vector。 （`dot`会执行矩阵乘法，而`*`运算符`scalar * vector`，执行逐个元素的相乘。）在`ndarray`中，一维数组根据上下文，可以解释为行或列 vector。如果 vector 表示的方向很重要，则要用二维数组的一行或一列。在本例中，vector 是右手边的一维数组，因此，`dot`将其作为列 vector 处理。

```rust
extern crate ndarray;

use ndarray::{arr1, arr2, Array1};

fn main() {
    let scalar = 4;

    let vector = arr1(&[1, 2, 3]);

    let matrix = arr2(&[[4, 5, 6],
                        [7, 8, 9]]);

    let new_vector: Array1<_> = scalar * vector;
    println!("{}", new_vector);

    let new_matrix = matrix.dot(&new_vector);
    println!("{}", new_matrix);
}
```

[`ndarray::array2::dot`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#method.dot-1
[`ndarray::arr1`]: https://docs.rs/ndarray/*/ndarray/fn.arr1.html
[`ndarray::arr2`]: https://docs.rs/ndarray/*/ndarray/fn.arr2.html
