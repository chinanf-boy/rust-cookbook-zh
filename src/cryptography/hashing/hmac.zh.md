## 与HMAC Digest签署并验证消息

[![ring-badge]][ring] [![cat-cryptography-badge]][cat-cryptography]

使用[`ring::hmac`]创建一个[`hmac::Signature`]然后验证签名是否正确。

```rust
extern crate ring;

use ring::{digest, hmac, rand};
use ring::rand::SecureRandom;
use ring::error::Unspecified;

fn main() -> Result<(), Unspecified> {
    let mut key_value = [0u8; 48];
    let rng = rand::SystemRandom::new();
    rng.fill(&mut key_value)?;
    let key = hmac::SigningKey::new(&digest::SHA256, &key_value);

    let message = "Legitimate and important message.";
    let signature = hmac::sign(&key, message.as_bytes());
    hmac::verify_with_own_key(&key, message.as_bytes(), signature.as_ref())?;

    Ok(())
}
```

[`hmac::signature`]: https://briansmith.org/rustdoc/ring/hmac/struct.Signature.html

[`ring::hmac`]: https://briansmith.org/rustdoc/ring/hmac/
