
## 用矩阵将标量与向量相乘

[![ndarray-badge]][ndarray] [![cat-science-badge]][cat-science]

创建向量[`ndarray::arr1`]和一个矩阵[`ndarray::arr2`]. 首先,将标量乘以矢量以获得另一矢量.然后,将向量转换为列向量.[`ndarray::ArrayBase::reversed_axes`]将矩阵乘以列向量来计算一个新矩阵.

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

    let new_matrix = matrix * new_vector.reversed_axes();
    println!("{}", new_matrix);
}
```

[`ndarray::arr1`]: https://docs.rs/ndarray/*/ndarray/fn.arr1.html

[`ndarray::arr2`]: https://docs.rs/ndarray/*/ndarray/fn.arr2.html

[`ndarray::arraybase::reversed_axes`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#method.reversed_axes
