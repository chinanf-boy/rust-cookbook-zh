
## 向量范数

[![ndarray-badge]][ndarray]

这个食谱演示了如何使用[`Array1`]类型,[`dot`],[`map`]和[`scalar_sum`]在计算中[l1]和[l2]给定向量的范数.L2范数的计算是简单的两个,因为它是一个矢量的点积的平方根,所示的功能`l2_norm`. 函数中所示的L1范数`l1_norm`通过将输入向量的元素映射到它们的绝对值来计算,然后调用`scalar_sum`通过求和来减少元素.

注意这两者`l1_norm`和`l2_norm`拿[`Array1`]类型.这个公式考虑向量范数,因此范数函数只需要接受一维数组(因此)[`Array1`])

```rust
extern crate ndarray;

use ndarray::{Array, Array1};

fn l1_norm(x: &Array1<f64>) -> f64 {
  x.mapv(|e| e.abs()).scalar_sum()
}

fn l2_norm(x: &Array1<f64>) -> f64 {
  x.dot(x).sqrt()
}

fn normalize(mut x: Array1<f64>) -> Array1<f64> {
  let norm = l2_norm(&x);
  x.mapv_inplace(|e| e/norm);
  x
}

fn main() {
  let x = Array::from_vec(vec![1., 2., 3., 4., 5.]);
  println!("||x||_2 = {}", l2_norm(&x));
  println!("||x||_1 = {}", l1_norm(&x));
  println!("Normalizing x yields {:?}", normalize(x));
}
```

[l1]: http://mathworld.wolfram.com/L1-Norm.html

[l2]: http://mathworld.wolfram.com/L2-Norm.html

[`array1`]: https://docs.rs/ndarray/0.12.0/ndarray/type.Array1.html

[`dot`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#method.dot

[`map`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#method.map

[`scalar_sum`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#method.scalar_sum
