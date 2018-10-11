
## 静态编译并链接到捆绑的C ++库

[![cc-badge]][cc] [![cat-development-tools-badge]][cat-development-tools]

链接捆绑的C ++库与链接捆绑的C库非常相似.编译和静态链接捆绑的C ++库时,两个核心差异是通过构建器方法指定C ++编译器[`cpp(true)`][cc-build-cpp]并通过添加.阻止C ++编译器进行名称修改`extern "C"`我们的C ++源文件顶部的部分.

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
