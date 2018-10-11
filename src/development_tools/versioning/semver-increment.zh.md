
## 解析并递增版本字符串.

[![semver-badge]][semver] [![cat-config-badge]][cat-config]

构造一个[`semver::Version`]从字符串文字使用[`Version::parse`],然后逐个增加补丁,次要和主要版本号.

注意按照[语义版本规范],增加次要版本号会将修补程序版本号重置为0,并且增加主版本号会将次要版本号和修补程序版本号重置为0.

```rust
# #[macro_use]
# extern crate error_chain;
extern crate semver;

use semver::Version;
#
# error_chain! {
#     foreign_links {
#         SemVer(semver::SemVerError);
#     }
# }

fn run() -> Result<()> {
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
#
# quick_main!(run);
```

[`semver::version`]: https://docs.rs/semver/*/semver/struct.Version.html

[`version::parse`]: https://docs.rs/semver/*/semver/struct.Version.html#method.parse

[semantic versioning specification]: http://semver.org/
