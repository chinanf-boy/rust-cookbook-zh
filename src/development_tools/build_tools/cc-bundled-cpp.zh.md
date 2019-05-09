## 编译，并静态链接到捆绑的 C++库

[![cc-badge]][cc] [![cat-development-tools-badge]][cat-development-tools]

链接捆绑的 C++库，非常类似于链接捆绑的 C 库。编译和静态链接捆绑的 C++库的两个核心区别，是通过构建器方法[`cpp(true)`][cc-build-cpp]指定 C++编译器。通过在我们的 C++源文件的顶部，添加`extern "C"`部分，防止 C++编译器的名称篡改。

### `Cargo.toml`

```toml
[package]
...
build = "build.rs"

[build-dependencies]
cc = "1"
```

### `build.rs`

```rust,no_run
extern crate cc;

fn main() {
    cc::Build::new()
        .cpp(true)
        .file("src/foo.cpp")
        .compile("foo");
}
```

### `src/foo.cpp`

```cpp
extern "C" {
    int multiply(int x, int y);
}

int multiply(int x, int y) {
    return x*y;
}
```

### `src/main.rs`

```rust,ignore
extern {
    fn multiply(x : i32, y : i32) -> i32;
}

fn main(){
    unsafe {
        println!("{}", multiply(5,7));
    }
}
```

[cc-build-cpp]: https://docs.rs/cc/*/cc/struct.Build.html#method.cpp
