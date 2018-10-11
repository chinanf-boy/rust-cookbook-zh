
<a name="ex-pbkdf2"></a>

## 使用PBKDF2加密并哈希密码

[![ring-badge]][ring] [![data-encoding-badge]][data-encoding] [![cat-cryptography-badge]][cat-cryptography]

用途[`ring::pbkdf2`]使用PBKDF2密钥派生函数散列盐渍密码[`pbkdf2::derive`].验证哈希是否正确[`pbkdf2::verify`].使用生成盐[`SecureRandom::fill`],用安全生成的随机数填充salt字节数组.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate data_encoding;
extern crate ring;
#
# error_chain! {
#   foreign_links {
#     Ring(ring::error::Unspecified);
#   }
# }

use data_encoding::HEXUPPER;
use ring::{digest, pbkdf2, rand};
use ring::rand::SecureRandom;

fn run() -> Result<()> {
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
#
# quick_main!(run);
```

[`pbkdf2::derive`]: https://briansmith.org/rustdoc/ring/pbkdf2/fn.derive.html

[`pbkdf2::verify`]: https://briansmith.org/rustdoc/ring/pbkdf2/fn.verify.html

[`ring::pbkdf2`]: https://briansmith.org/rustdoc/ring/pbkdf2/index.html

[`securerandom::fill`]: https://briansmith.org/rustdoc/ring/rand/trait.SecureRandom.html#tymethod.fill
