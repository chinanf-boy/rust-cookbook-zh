## vector 范数

[![ndarray-badge]][ndarray]

这个食谱演示了[`Array1`]类型，[`ArrayView1`]类型，[`fold`]方法，以及[`dot`]方法，它计算给定 vector 的[l1]和[l2]范数。l2 范数的计算是两者中，比较简单的一个，因为它是一个 vector 的点乘积的平方根，如`l2_norm`函数所示。而 l1 范数，在`l1_norm`函数，由`fold`方法完成，它是元素绝对值的总和。（这也可以用`x.mapv(f64::abs).scalar_sum()`执行，但这将为`mapv`的结果分配一个新的数组。）

注意`l1_norm`和`l2_norm`都拿了[`ArrayView1`]类型。这个食谱考虑了 vector 范数，因此范数函数，只需要接受一维 view（就是[`ArrayView1`]）。当这个函数换成接受一个`&Array1<f64>`类型参数，这将要求调用者具有，所有权数组的一个引用，这比仅对一个 view 的访问，更为严格（因为一个 view，是可以通过任何 array 或 view 创建的，而不仅仅是所有权数组）。对调用者来说，最方便的参数类型是`&ArrayBase<S, Ix1> where S: Data`，因为调用者可以使用`&array`或`&view`，而不是`x.view()`。 如果该函数是你公共 API 的一部分，那么对于用户来说，这可能是一个更好的选择，但是对于内部函数来说，简洁的`ArrayView1<f64>`可能更好。

```rust
#[macro_use(array)]
extern crate ndarray;

use ndarray::{Array1, ArrayView1};

fn l1_norm(x: ArrayView1<f64>) -> f64 {
    x.fold(0., |acc, elem| acc + elem.abs())
}

fn l2_norm(x: ArrayView1<f64>) -> f64 {
    x.dot(&x).sqrt()
}

fn normalize(mut x: Array1<f64>) -> Array1<f64> {
    let norm = l2_norm(x.view());
    x.mapv_inplace(|e| e/norm);
    x
}

fn main() {
    let x = array![1., 2., 3., 4., 5.];
    println!("||x||_2 = {}", l2_norm(x.view()));
    println!("||x||_1 = {}", l1_norm(x.view()));
    println!("Normalizing x yields {:?}", normalize(x));
}
```

[l1]: http://mathworld.wolfram.com/L1-Norm.html
[l2]: http://mathworld.wolfram.com/L2-Norm.html
[`array1`]: https://docs.rs/ndarray/*/ndarray/type.Array1.html
[`arrayview1`]: https://docs.rs/ndarray/*/ndarray/type.ArrayView1.html
[`dot`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#method.dot
[`fold`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#method.fold
