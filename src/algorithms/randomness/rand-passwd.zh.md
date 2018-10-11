
## 从一组字母数字字符创建随机密码

[![rand-badge]][rand] [![cat-os-badge]][cat-os]

随机生成范围内给定长度ASCII字符的字符串`A-Z,
a-z, 0-9`,与[`Alphanumeric`]样品.

```rust
extern crate rand;

use rand::{thread_rng, Rng};
use rand::distributions::Alphanumeric;

fn main() {
    let rand_string: String = thread_rng()
        .sample_iter(&Alphanumeric)
        .take(30)
        .collect();

    println!("{}", rand_string);
}
```

[`alphanumeric`]: https://docs.rs/rand/*/rand/distributions/struct.Alphanumeric.html
