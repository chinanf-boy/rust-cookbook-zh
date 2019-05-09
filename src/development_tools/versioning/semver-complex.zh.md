## 分析复杂的版本字符串。

[![semver-badge]][semver] [![cat-config-badge]][cat-config]

使用[`Version::parse`]从复杂版本字符串，构建一个[`semver::Version`]。 该字符串包含预发布和构建的元数据，正如[语义版本规范]所定义的。

注意，根据规范，构建元数据虽然解析了，但在比较版本时，不考虑。换句话说，即使构建字符串不同，两个版本也可能相同。

```rust
extern crate semver;

use semver::{Identifier, Version, SemVerError};

fn main() -> Result<(), SemVerError> {
    let version_str = "1.0.49-125+g72ee7853";
    let parsed_version = Version::parse(version_str)?;

    assert_eq!(
        parsed_version,
        Version {
            major: 1,
            minor: 0,
            patch: 49,
            pre: vec![Identifier::Numeric(125)],
            build: vec![],
        }
    );
    assert_eq!(
        parsed_version.build,
        vec![Identifier::AlphaNumeric(String::from("g72ee7853"))]
    );

    let serialized_version = parsed_version.to_string();
    assert_eq!(&serialized_version, version_str);

    Ok(())
}
```

[`semver::version`]: https://docs.rs/semver/*/semver/struct.Version.html
[`version::parse`]: https://docs.rs/semver/*/semver/struct.Version.html#method.parse
[semantic versioning specification]: http://semver.org/
