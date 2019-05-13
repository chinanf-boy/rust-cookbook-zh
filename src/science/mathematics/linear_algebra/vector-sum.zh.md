## vector 总和

[![ndarray-badge]][ndarray]

这个[ndarray]箱子支持多种创建数组的方法 —— 该食谱主要专注`std::Vec`的[`ndarray::Array`]的创建，通过[`from_vec`]完成。把两个数组加在一起和把两个数字加在一起，没有什么不同。在数组上，使用`&`符号，能在一次算术运算中，阻止消耗数组的操作。没有`&`的话，数组会被消耗。

在第一个示例中，数组`a`和`b`在 let 语句（`z = a + b`）中移动：。 在第二个示例中，数组`c`和`d`不会移动，而是为`w`创建一个新的数组。在 vector 总和（`w =  &c + &d`）之后，更新`c`或`d`，对`w`值是没有影响的。另外，在打印`c`时按预期工作，打印`b`时出错，因为移动了。见[两个数组的二元运算符][Binary
Operators With Two Arrays]更多细节。

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
