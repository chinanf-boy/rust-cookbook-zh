## 编译并链接到捆绑的C++库

[![cc-badge]][cc] [![cat-development-tools-badge]][cat-development-tools]

链接捆绑的C++库非常类似于链接捆绑的C库。编译和静态链接捆绑的C++库时的两个核心区别是通过Builder方法指定C++编译器。[`cpp(true)`][cc-build-cpp]通过添加C++编译器防止名称篡改`extern "C"`节在我们的C++源文件的顶部。

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
