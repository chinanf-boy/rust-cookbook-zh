## ANSI终端

[![ansi_term-badge]][ansi_term] [![cat-command-line-badge]][cat-command-line]

这个程序描述了[`ansi_term`箱子]的用法，以及它是如何用于控制ANSI终端上的颜色和格式，例如，蓝色粗体文本或带黄色下划线的文本。

[`ansi_term`]有两个主要的数据结构：[`ANSIString`]和[`Style`]。一个[`Style`]保存风格信息：颜色，文本应该是粗体，还是闪烁，或者其他什么的。还有`Colour`变体代表简单的前景色样式。一个[`ANSIString`]是与一个[`Style`]配对的字符串。

**注意：**英国英语，要使用*Colour*代替*Color*，不要混淆

### 将彩色文本打印到终端

```rust
extern crate ansi_term;

use ansi_term::Colour;

fn main() {
    println!("This is {} in color, {} in color and {} in color",
             Colour::Red.paint("red"),
             Colour::Blue.paint("blue"),
             Colour::Green.paint("green"));
}
```

### 终端中的粗体文字

比普通前景色更改更复杂的事情，相关代码需要构造`Style`结构。用[`Style::new()`]创建结构，和要链接的属性。

```rust
extern crate ansi_term;

use ansi_term::Style;

fn main() {
    println!("{} and this is not",
             Style::new().bold().paint("This is Bold"));
}
```

### 终端中的粗体和彩色文本

`Colour`实现了许多与`Style`类似的函数，并且可以链式方法。

```rust
extern crate ansi_term;

use ansi_term::Colour;
use ansi_term::Style;

fn main(){
    println!("{}, {} and {}",
             Colour::Yellow.paint("This is colored"),
             Style::new().bold().paint("this is bold"),
             Colour::Yellow.bold().paint("this is bold and colored"));
}
```

[documentation]: https://docs.rs/ansi_term/

[`ansi_term` crate]: https://crates.io/crates/ansi_term

[`ansistring`]: https://docs.rs/ansi_term/*/ansi_term/type.ANSIString.html

[`style`]: https://docs.rs/ansi_term/*/ansi_term/struct.Style.html

[`style::new()`]: https://docs.rs/ansi_term/0.11.0/ansi_term/struct.Style.html#method.new
