
## 从一组用户定义的字符创建随机密码

[![rand-badge]][rand] [![cat-os-badge]][cat-os]

使用自定义用户定义的字节字符串随机生成给定长度ASCII字符的字符串[`choose`].

```rust
extern crate rand;

use rand::{thread_rng, Rng};

fn main() {
    const CHARSET: &[u8] =  b"ABCDEFGHIJKLMNOPQRSTUVWXYZ\
    abcdefghijklmnopqrstuvwxyz\
    0123456789)(*&^%$#@!~";

    let mut rng = thread_rng();
    let password: Option<String> = (0..30)
        .map(|_| Some(*rng.choose(CHARSET)? as char))
        .collect();

    println!("{:?}", password);
}
```

[`choose`]: https://docs.rs/rand/*/rand/trait.Rng.html#method.choose
