## 分析并增加版本字符串。

[![semver-badge]][semver] [![cat-config-badge]][cat-config]

构建一个[`semver::Version`]从字符串文本使用[`Version::parse`]，然后逐个递增补丁、次要版本和主要版本号。

注意，根据[语义版本规范]，递增次要版本号将补丁版本号重置为0，递增主要版本号将次要版本号和补丁版本号重置为0。

```rust
extern crate semver;

use semver::{Version, SemVerError};

fn main() -> Result<(), SemVerError> {
    let mut parsed_version = Version::parse("0.2.6")?;

    assert_eq!(
        parsed_version,
        Version {
            major: 0,
            minor: 2,
            patch: 6,
            pre: vec![],
            build: vec![],
        }
    );

    parsed_version.increment_patch();
    assert_eq!(parsed_version.to_string(), "0.2.7");
    println!("New patch release: v{}", parsed_version);

    parsed_version.increment_minor();
    assert_eq!(parsed_version.to_string(), "0.3.0");
    println!("New minor release: v{}", parsed_version);

    parsed_version.increment_major();
    assert_eq!(parsed_version.to_string(), "1.0.0");
    println!("New major release: v{}", parsed_version);

    Ok(())
}
```

[`semver::version`]: https://docs.rs/semver/*/semver/struct.Version.html

[`version::parse`]: https://docs.rs/semver/*/semver/struct.Version.html#method.parse

[semantic versioning specification]: http://semver.org/
