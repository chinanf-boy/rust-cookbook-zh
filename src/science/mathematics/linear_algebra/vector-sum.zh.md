## 向量和

[![ndarray-badge]][ndarray]

这个[恩达雷]板条箱支持多种创建数组的方法——这个方法主要是创建[`ndarray::Array`]来自于`std::Vec`通过[`from_vec`]. 把两个数组加在一起和把两个数字加在一起没有什么不同。使用`&`算术运算中数组上的操作数阻止该运算使用数组。没有`&`，数组被消耗。

在第一个示例中，数组`a`和`b`在let语句中移动`z = a +
b`. 在第二个示例中，数组`c`和`d`不会移动，而是为`w`. 正在更新`c`或`d`在矢量和不起作用后，`w`. 另外，在打印时`c`按预期工作，打印时出错`b`因为搬家。见[带两个数组的二元运算符]更多细节。

```rust
extern crate ndarray;
use ndarray::Array;

fn main() {
  let a = Array::from_vec(vec![1., 2., 3., 4., 5.]);
  let b = Array::from_vec(vec![5., 4., 3., 2., 1.]);
  let mut c = Array::from_vec(vec![1., 2., 3., 4., 5.]);
  let mut d = Array::from_vec(vec![5., 4., 3., 2., 1.]);

  let z = a + b;
  let w =  &c + &d;

  let epsilon = 1e-8;
  for elem in z.iter() {
    let diff: f32 = *elem - 6.;
    assert!(diff.abs() < epsilon);
  }

  println!("c = {}", c);
  c[0] = 10.;
  d[1] = 10.;

  for elem in w.iter() {
    let diff: f32 = *elem - 6.;
    assert!(diff.abs() < epsilon);
  }

}
```

[binary operators with two arrays]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#binary-operators-with-two-arrays

[`from_vec`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html#method.from_vec

[ndarray]: https://docs.rs/crate/ndarray/*

[`ndarray::array`]: https://docs.rs/ndarray/*/ndarray/struct.ArrayBase.html
