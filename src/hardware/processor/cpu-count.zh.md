
## 逻辑CPU核的校验数

[![num_cpus-badge]][num_cpus] [![cat-hardware-support-badge]][cat-hardware-support]

显示当前计算机使用的逻辑CPU核数[`num_cpus::get`].

```rust
extern crate num_cpus;

fn main() {
    println!("Number of logical cores is {}", num_cpus::get());
}
```
