## 带自定义设置，编译 C 库

[![cc-badge]][cc] [![cat-development-tools-badge]][cat-development-tools]

使用[`cc::Build::define`]自定义构建，捆绑的 C 代码很简单。 该方法采用[`Option`]值，因此可以创建如下定义：`#define APP_NAME "foo"`，以及`#define WELCOME`（传递 `None`作为一个缺乏值的定义）。这个例子构建了一个动态定义集的捆绑 C 文件，而定义集在`build.rs`中，并会在运行使，打印**欢迎使用 foo-版本 1.0.2**“。Cargo 会设置一些[环境变量][cargo-env]，这对于某些自定义设置可能很有用。

### `Cargo.toml`

```toml
[package]
...
version = "1.0.2"
build = "build.rs"

[build-dependencies]
cc = "1"
```

### `build.rs`

```rust,no_run
extern crate cc;

fn main() {
    cc::Build::new()
        .define("APP_NAME", "\"foo\"")
        .define("VERSION", format!("\"{}\"", env!("CARGO_PKG_VERSION")).as_str())
        .define("WELCOME", None)
        .file("src/foo.c")
        .compile("foo");
}
```

### `src/foo.c`

```c
#include <stdio.h>

void print_app_info() {
#ifdef WELCOME
    printf("Welcome to ");
#endif
    printf("%s - version %s\n", APP_NAME, VERSION);
}
```

### `src/main.rs`

```rust,ignore
extern {
    fn print_app_info();
}

fn main(){
    unsafe {
        print_app_info();
    }
}
```

[cargo-env]: https://doc.rust-lang.org/cargo/reference/environment-variables.html
