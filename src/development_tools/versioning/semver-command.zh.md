
## 检查外部命令版本是否兼容

[![semver-badge]][semver] [![cat-text-processing-badge]][cat-text-processing] [![cat-os-badge]][cat-os]

运行`git --version`运用[`Command`],然后将版本号解析为[`semver::Version`]运用[`Version::parse`].[`VersionReq::matches`]比较[`semver::VersionReq`]到解析版本.命令输出类似于"git version x.y.z".

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate semver;

use std::process::Command;
use semver::{Version, VersionReq};
#
# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#         Utf8(std::string::FromUtf8Error);
#         SemVer(semver::SemVerError);
#         SemVerReq(semver::ReqParseError);
#     }
# }

fn run() -> Result<()> {
    let version_constraint = "> 1.12.0";
    let version_test = VersionReq::parse(version_constraint)?;
    let output = Command::new("git").arg("--version").output()?;

    if !output.status.success() {
        bail!("Command executed with failing error code");
    }

    let stdout = String::from_utf8(output.stdout)?;
    let version = stdout.split(" ").last().ok_or_else(|| {
        "Invalid command output"
    })?;
    let parsed_version = Version::parse(version)?;

    if !version_test.matches(&parsed_version) {
        bail!("Command version lower than minimum supported version (found {}, need {})",
            parsed_version, version_constraint);
    }

    Ok(())
}
#
# quick_main!(run);
```

[`command`]: https://doc.rust-lang.org/std/process/struct.Command.html

[`semver::version`]: https://docs.rs/semver/*/semver/struct.Version.html

[`semver::versionreq`]: https://docs.rs/semver/*/semver/struct.VersionReq.html

[`version::parse`]: https://docs.rs/semver/*/semver/struct.Version.html#method.parse

[`versionreq::matches`]: https://docs.rs/semver/*/semver/struct.VersionReq.html#method.matches
