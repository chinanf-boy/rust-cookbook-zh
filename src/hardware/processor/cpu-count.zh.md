## 检查逻辑 CPU 的核数

[![num_cpus-badge]][num_cpus] [![cat-hardware-support-badge]][cat-hardware-support]

[`num_cpus::get`]会显示当前计算机中，使用的逻辑 CPU 核数。

```rust
extern crate num_cpus;

fn main() {
    println!("Number of logical cores is {}", num_cpus::get());
}
```
