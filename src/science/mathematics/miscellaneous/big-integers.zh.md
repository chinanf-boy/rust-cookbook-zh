## 大整数

[![num-badge]][num] [![cat-science-badge]][cat-science]

可以使用计算超过128位的整数[`BigInt`]。

```rust
extern crate num;

use num::bigint::{BigInt, ToBigInt};

fn factorial(x: i32) -> BigInt {
    if let Some(mut factorial) = 1.to_bigint() {
        for i in 1..(x+1) {
            factorial = factorial * i;
        }
        factorial
    }
    else {
        panic!("Failed to calculate factorial!");
    }
}

fn main() {
    println!("{}! equals {}", 100, factorial(100));
}
```

[`bigint`]: https://docs.rs/num/0.2.0/num/struct.BigInt.html
