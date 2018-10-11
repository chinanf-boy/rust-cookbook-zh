
## 使用HMAC摘要签名并验证消息

[![ring-badge]][ring] [![cat-cryptography-badge]][cat-cryptography]

用途[`ring::hmac`]创造一个[`hmac::Signature`]然后验证字符串是否正确.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate ring;
#
# error_chain! {
#     foreign_links {
#         Ring(ring::error::Unspecified);
#     }
# }

use ring::{digest, hmac, rand};
use ring::rand::SecureRandom;

fn run() -> Result<()> {
    let mut key_value = [0u8; 48];
    let rng = rand::SystemRandom::new();
    rng.fill(&mut key_value)?;
    let key = hmac::SigningKey::new(&digest::SHA256, &key_value);

    let message = "Legitimate and important message.";
    let signature = hmac::sign(&key, message.as_bytes());
    hmac::verify_with_own_key(&key, message.as_bytes(), signature.as_ref())?;

    Ok(())
}
#
# quick_main!(run);
```

[`hmac::signature`]: https://briansmith.org/rustdoc/ring/hmac/struct.Signature.html

[`ring::hmac`]: https://briansmith.org/rustdoc/ring/hmac/
