
## 向量和

[![ndarray-badge]][ndarray]

这个[恩达雷]CRATE支持创建数组的多种方法——这个配方着重于创建[`ndarray::Array`]来自于`std::Vec`通过[`from_vec`]. 将两个数组相加与将两个数字相加没有什么不同.使用`&`算术运算中数组的操作数防止操作消耗数组.没有`&`数组被消耗掉.

在第一个示例中,数组`a`和`b`在LET语句中移动`z = a +
b`. 在第二个示例中,数组`c`和`d`不移动,而是创建一个新数组`w`. 更新任一`c`或`d`在向量和之后没有影响的值`w`. 另外,在印刷时`c`如预期的那样工作,打印错误`b`由于移动.见[二元二元算子]更多细节.

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
