## 静态编译并链接到捆绑的 C 库

[![cc-badge]][cc] [![cat-development-tools-badge]][cat-development-tools]

为了适应项目中需要附加 C、C++或程序集的场景，[**复写的副本**][cc]CRATE 提供了一个简单的 API，用于将捆绑的 C/C++/ASM 代码编译成静态库（**A**）可以通过静态链接到**鲁斯特**.

下面的示例包含一些绑定的 C 代码（**SRC/Hello C**）那将用在铁锈上。在编译 rust 源代码之前，“build”文件（**建筑工人**）指定**卡莫尔**跑。使用[**复写的副本**][cc]箱子，将生成静态库文件（在这种情况下，**李碧**见[`compile`文档][cc-build-compile]）然后，可以通过在`extern`块。

由于绑定的 C 非常简单，因此只需要将一个源文件传递给[`cc::Build`][cc-build]. 对于更复杂的构建需求，[`cc::Build`][cc-build]提供一整套用于指定[`include`][cc-build-include]路径和额外的编译器[`flag`][cc-build-flag]s.

### `Cargo.toml`

```toml
[package]
...
build = "build.rs"

[build-dependencies]
cc = "1"

[dependencies]
error-chain = "0.11"
```

### `build.rs`

```rust,no_run
extern crate cc;

fn main() {
    cc::Build::new()
        .file("src/hello.c")
        .compile("hello");   // outputs `libhello.a`
}
```

### `src/hello.c`

```c
#include <stdio.h>


void hello() {
    printf("Hello from C!\n");
}

void greet(const char* name) {
    printf("Hello, %s!\n", name);
}
```

### `src/main.rs`

```rust,ignore
# #[macro_use] extern crate error_chain;
use std::ffi::CString;
use std::os::raw::c_char;
#
# error_chain! {
#     foreign_links {
#         NulError(::std::ffi::NulError);
#         Io(::std::io::Error);
#     }
# }
#
# fn prompt(s: &str) -> Result<String> {
#     use std::io::Write;
#     print!("{}", s);
#     std::io::stdout().flush()?;
#     let mut input = String::new();
#     std::io::stdin().read_line(&mut input)?;
#     Ok(input.trim().to_string())
# }

extern {
    fn hello();
    fn greet(name: *const c_char);
}

fn run() -> Result<()> {
    unsafe { hello() }
    let name = prompt("What's your name? ")?;
    let c_name = CString::new(name)?;
    unsafe { greet(c_name.as_ptr()) }
    Ok(())
}
#
# quick_main!(run);
```

[`cc::build::define`]: https://docs.rs/cc/*/cc/struct.Build.html#method.define
[`option`]: https://doc.rust-lang.org/std/option/enum.Option.html
[cc-build-compile]: https://docs.rs/cc/*/cc/struct.Build.html#method.compile
[cc-build-cpp]: https://docs.rs/cc/*/cc/struct.Build.html#method.cpp
[cc-build-flag]: https://docs.rs/cc/*/cc/struct.Build.html#method.flag
[cc-build-include]: https://docs.rs/cc/*/cc/struct.Build.html#method.include
[cc-build]: https://docs.rs/cc/*/cc/struct.Build.html
