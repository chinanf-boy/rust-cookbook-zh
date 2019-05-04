## 从一组字母+数字的字符，创建随机密码

[![rand-badge]][rand] [![cat-os-badge]][cat-os]

随机生成，给定长度的 ASCII 字符串，字符范围是`A-Z, a-z, 0-9`，运用[`Alphanumeric`] （字母+数字）样品。

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
