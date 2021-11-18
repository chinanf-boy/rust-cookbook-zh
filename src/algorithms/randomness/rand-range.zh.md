## 生成范围内的随机数

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

用[`Rng::gen_range`]，在半开放`[0, 10)`范围（不包括`10`）生成随机值。

```rust
extern crate rand;

use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();
    println!("Integer: {}", rng.gen_range(0 .. 10));
    println!("Float: {}", rng.gen_range(0.0 .. 10.0));
}
```

[`Uniform`]可以用来获得[均匀分布][uniform distribution]的值。下面的代码是相同作用，但是当在相同范围内，重复生成数字时可能更快。

```rust
extern crate rand;


use rand::distributions::{Distribution, Uniform};

fn main() {
    let mut rng = rand::thread_rng();
    let die = Uniform::from(1..7);

    loop {
        let throw = die.sample(&mut rng);
        println!("Roll the die: {}", throw);
        if throw == 6 {
            break;
        }
    }
}
```

[`uniform`]: https://docs.rs/rand/*/rand/distributions/uniform/struct.Uniform.html

[`rng::gen_range`]: https://doc.rust-lang.org/rand/*/rand/trait.Rng.html#method.gen_range

[uniform distribution]: https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)
