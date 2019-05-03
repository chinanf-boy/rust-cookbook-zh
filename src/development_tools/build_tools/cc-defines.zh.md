## 在设置自定义定义时编译C库

[![cc-badge]][cc] [![cat-development-tools-badge]][cat-development-tools]

使用自定义定义构建捆绑的C代码很简单[`cc::Build::define`]. 该方法采用[`Option`]值，因此可以创建定义，例如`#define APP_NAME "foo"`以及`#define WELCOME`（通过）`None`作为值减去定义）。这个例子构建了一个带有动态定义集的捆绑C文件`build.rs`印刷品**欢迎使用foo-版本1.0.2**“跑步的时候。货装一些[环境变量][cargo-env]这对于某些自定义定义可能很有用。

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
