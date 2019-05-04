## 从一组用户定义的字符，创建随机密码

[![rand-badge]][rand] [![cat-os-badge]][cat-os]

使用用户自定义的字节字符串，随机生成给定长度的 ASCII 字符串，运用[`gen_range`]。

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
            // 这是安全的，因为 `idx` 会在 `CHARSET` 的范围内。
            char::from(unsafe { *CHARSET.get_unchecked(idx) }) // 来自用户的所有输入，最好都定义为不安全的。
        })
        .collect();

    println!("{:?}", password);
}
```

[`gen_range`]: https://docs.rs/rand/*/rand/trait.Rng.html#method.gen_range
