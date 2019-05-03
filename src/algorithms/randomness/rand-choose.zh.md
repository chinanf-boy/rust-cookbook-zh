## 从一组用户定义的字符创建随机密码

[![rand-badge]][rand] [![cat-os-badge]][cat-os]

使用自定义用户定义的字节字符串随机生成给定长度ASCII字符的字符串[`gen_range`]。

```rust
extern crate rand;

fn main() {
    use rand::Rng;
    const CHARSET: &[u8] = b"ABCDEFGHIJKLMNOPQRSTUVWXYZ\
                            abcdefghijklmnopqrstuvwxyz\
                            0123456789)(*&^%$#@!~";
    const PASSWORD_LEN: usize = 30;
    let mut rng = rand::thread_rng();

    let password: String = (0..PASSWORD_LEN)
        .map(|_| {
            let idx = rng.gen_range(0, CHARSET.len());
            // This is safe because `idx` is in range of `CHARSET`
            char::from(unsafe { *CHARSET.get_unchecked(idx) })
        })
        .collect();

    println!("{:?}", password);
}
```

[`gen_range`]: https://docs.rs/rand/*/rand/trait.Rng.html#method.gen_range
