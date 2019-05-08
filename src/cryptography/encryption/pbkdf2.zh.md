<a name="ex-pbkdf2"></a>

## 用 PBKDF2 对密码，进行 加盐 和 哈希 操作

[![ring-badge]][ring] [![data-encoding-badge]][data-encoding] [![cat-cryptography-badge]][cat-cryptography]

[`ring::pbkdf2`]的用法是，使用 PBKDF2 密钥派生函数[`pbkdf2::derive`]，哈希 腌制的密码。 用[`pbkdf2::verify`]验证哈希是否正确。 盐是用[`SecureRandom::fill`]生成的，它用安全生成的随机数，填充 salt 字节数组。

> 这个在哈希中加入字符串的方式称为“加盐”。其作用是让加盐后的哈希结果和没有加盐的结果不相同，在不同的应用情景中，这个处理可以增加额外的安全性。

```rust
extern crate ring;
extern crate data_encoding;

use data_encoding::HEXUPPER;
use ring::error::Unspecified;
use ring::rand::SecureRandom;
use ring::{digest, pbkdf2, rand};

fn main() -> Result<(), Unspecified> {
    const CREDENTIAL_LEN: usize = digest::SHA512_OUTPUT_LEN;
    const N_ITER: u32 = 100_000;
    let rng = rand::SystemRandom::new();

    let mut salt = [0u8; CREDENTIAL_LEN];
    rng.fill(&mut salt)?;

    let password = "Guess Me If You Can!";
    let mut pbkdf2_hash = [0u8; CREDENTIAL_LEN];
    pbkdf2::derive(
        &digest::SHA512,
        N_ITER,
        &salt,
        password.as_bytes(),
        &mut pbkdf2_hash,
    );
    println!("Salt: {}", HEXUPPER.encode(&salt));
    println!("PBKDF2 hash: {}", HEXUPPER.encode(&pbkdf2_hash));

    let should_succeed = pbkdf2::verify(
        &digest::SHA512,
		N_ITER,
        &salt,
        password.as_bytes(),
        &pbkdf2_hash,
    );
    let wrong_password = "Definitely not the correct password";
    let should_fail = pbkdf2::verify(
        &digest::SHA512,
        N_ITER,
        &salt,
        wrong_password.as_bytes(),
        &pbkdf2_hash,
    );

    assert!(should_succeed.is_ok());
    assert!(!should_fail.is_ok());

    Ok(())
}
```

[`pbkdf2::derive`]: https://briansmith.org/rustdoc/ring/pbkdf2/fn.derive.html
[`pbkdf2::verify`]: https://briansmith.org/rustdoc/ring/pbkdf2/fn.verify.html
[`ring::pbkdf2`]: https://briansmith.org/rustdoc/ring/pbkdf2/index.html
[`securerandom::fill`]: https://briansmith.org/rustdoc/ring/rand/trait.SecureRandom.html#tymethod.fill
