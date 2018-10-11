
## 解析复杂的版本字符串.

[![semver-badge]][semver] [![cat-config-badge]][cat-config]

构造一个[`semver::Version`]从复杂的版本字符串使用[`Version::parse`].该字符串包含预定义的预发布和构建元数据[语义版本规范].

请注意,根据规范,解析构建元数据,但在比较版本时不予考虑.换句话说,即使它们的构建字符串不同,两个版本也可能相同.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate semver;

use semver::{Identifier, Version};
#
# error_chain! {
#     foreign_links {
#         SemVer(semver::SemVerError);
#     }
# }

fn run() -> Result<()> {
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
#
# quick_main!(run);
```

[`semver::version`]: https://docs.rs/semver/*/semver/struct.Version.html

[`version::parse`]: https://docs.rs/semver/*/semver/struct.Version.html#method.parse

[semantic versioning specification]: http://semver.org/
