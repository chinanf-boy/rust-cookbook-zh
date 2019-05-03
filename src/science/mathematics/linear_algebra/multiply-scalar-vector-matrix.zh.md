## 用向量和矩阵相乘一个标量

[![ndarray-badge]][ndarray] [![cat-science-badge]][cat-science]

创建一个一维数组（向量），其中[`ndarray::arr1`]和二维数组（矩阵）[`ndarray::arr2`]. 首先，将一个标量乘以向量得到另一个向量。然后，矩阵乘以新的向量[`ndarray::Array2::dot`]. （`dot`执行矩阵乘法，而`*`运算符执行逐元素乘法。）in`ndarray`，根据上下文，一维数组可以解释为行或列向量。如果表示矢量方向很重要，则必须使用一行或一列的二维数组。在本例中，向量是右侧的一维数组，因此`dot`将其作为列向量处理。

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
