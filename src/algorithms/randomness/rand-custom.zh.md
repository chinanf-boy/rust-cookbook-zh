## 生成自定义类型的随机值

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

随机生成一个元组`(i32, bool, f64)`，和用户定义类型的变量`Point`。在 `Point` 类型之上，对[`Standard`]实现[`Distribution`] trait，为了(`Point`)允许随机生成(`gen`)。

> 这里，用得是，具象化泛型类型。

```rust
extern crate rand;

use rand::Rng;
use rand::distributions::{Distribution, Standard};

#[derive(Debug)]
struct Point {
    x: i32,
    y: i32,
}

// 把 泛型 具象化为 Point， (定义实现)
impl Distribution<Point> for Standard {
    fn sample<R: Rng + ?Sized>(&self, rng: &mut R) -> Point {
        let (rand_x, rand_y) = rng.gen();
        Point {
            x: rand_x,
            y: rand_y,
        }
    }
}

fn main() {
    let mut rng = rand::thread_rng();
    let rand_tuple = rng.gen::<(i32, bool, f64)>();
    let rand_point: Point = rng.gen(); 
    // 主要是 : Point，类型标签，让编译器知道 (调用上面的实现定义)
    println!("Random tuple: {:?}", rand_tuple);
    println!("Random Point: {:?}", rand_point);
}
```

[`distribution`]: https://docs.rs/rand/*/rand/distributions/trait.Distribution.html

[`standard`]: https://docs.rs/rand/*/rand/distributions/struct.Standard.html
