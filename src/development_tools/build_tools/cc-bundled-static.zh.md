## 编译，并静态链接到捆绑的 C 库

[![cc-badge]][cc] [![cat-development-tools-badge]][cat-development-tools]

为了适应项目，需要附加 C、C++ 或 ASM 的场景，[**cc**][cc]箱子，提供了一个简单的 API，用于将捆绑的 C/C++/ASM 代码编译成静态库（**.a**），这样就可以静态链接到**rustc**.

下面的示例，包含一些绑定的 C 代码（**src/hello.c**），会用在 Rust 上。在编译 rust 源代码之前，“构建”文件（**build.rs**）可通过**Cargo.toml**指定运行。若使用[**cc**][cc]箱子，一个静态库文件将被生成（在这情况下，就是**libhello.a**，若想知道更多，请看[`compile`文档][cc-build-compile]）然后，在 Rust 中想使用该库，可以通过在`extern`块中，定义外部函数签名。

由于绑定的 C 非常简单，因此只需要将一个源文件，传递给[`cc::Build`][cc-build]。 对于更复杂的构建需求，[`cc::Build`][cc-build]为指定的[`include`][cc-build-include]的路径，和额外的编译器[`flag`][cc-build-flag]标志们，提供了一整套构建器方法。

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
