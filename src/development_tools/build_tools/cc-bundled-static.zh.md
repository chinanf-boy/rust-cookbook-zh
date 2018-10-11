
## 静态编译并链接到捆绑的C库

[![cc-badge]][cc] [![cat-development-tools-badge]][cat-development-tools]

为了适应项目中需要额外的C,C ++或程序集的场景,[**cc**][cc]crate提供了一个简单的api,用于将捆绑的C / C ++ / asm代码编译成静态库(**.一个**)可以静态链接到**rustc**.

以下示例包含一些捆绑的C代码(**SRC / hello.c中**)将用于生锈.在编译生锈源代码之前,"构建"文件(**build.rs**)中指定的**Cargo.toml**运行.使用[**cc**][cc]crate,将生成一个静态库文件(在这种情况下,**libhello.a**,见[`compile`文档][cc-build-compile])然后可以通过声明外部函数签名来生锈`extern`块.

由于捆绑的C非常简单,因此只需要传递一个源文件[`cc::Build`][cc-build].对于更复杂的构建要求,[`cc::Build`][cc-build]提供了一整套用于指定的构建器方法[`include`][cc-build-include]路径和额外的编译器[`flag`][cc-build-flag]秒.

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
