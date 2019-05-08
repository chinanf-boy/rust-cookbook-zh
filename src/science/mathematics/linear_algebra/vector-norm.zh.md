## 向量范数

[![ndarray-badge]][ndarray]

这个食谱演示了[`Array1`]类型，[`ArrayView1`]类型，[`fold`]方法，以及[`dot`]计算的方法[l1]和[l2]给定向量的范数。l2 范数的计算是两者中比较简单的一个，因为它是一个向量的点积的平方根，如函数所示。`l2_norm`. 函数中显示的 l1 范数`l1_norm`，由`fold`对元素的绝对值求和的运算。（这也可以用`x.mapv(f64::abs).scalar_sum()`，但这将为`mapv`）

注意这两者`l1_norm`和`l2_norm`拿[`ArrayView1`]类型。这个方法考虑了向量范数，因此范数函数只需要接受一维视图（因此[`ArrayView1`]）函数可以接受类型为的参数`&Array1<f64>`相反，这将要求调用者具有对拥有的数组的引用，这比仅具有对视图的访问更为严格（因为可以从任何数组或视图创建视图，而不仅仅是拥有的数组）。调用方最方便的参数类型是`&ArrayBase<S, Ix1> where S: Data`，因为调用方可以使用`&array`或`&view`而不是`x.view()`. 如果函数是公共 API 的一部分，那么对于用户来说，这可能是一个更好的选择，但是对于内部函数来说，更简洁`ArrayView1<f64>`可能更好。

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
