## 解析命令行参数

[![clap-badge]][clap] [![cat-command-line-badge]][cat-command-line]

通过使用`clap`的构建样式，该应用程序描述了其命令行界面的结构。该[文档][documentation]提供了，另外两种可能的方法，去实例化应用程序。

在构建样式中，`with_name`是唯一标识符，而`value_of`则用于检索传递的值。该`short`和`long`选项控制用户将要键入的标志; `short`标志`-f`和`long`标志`--file`是同个标志。

```rust
extern crate clap;

use clap::{Arg, App};

fn main() {
    let matches = App::new("My Test Program")
        .version("0.1.0")
        .author("Hackerman Jones <hckrmnjones@hack.gov>")
        .about("Teaches argument parsing")
        .arg(Arg::with_name("file")
                 .short("f")
                 .long("file")
                 .takes_value(true)
                 .help("A cool file"))
        .arg(Arg::with_name("num")
                 .short("n")
                 .long("number")
                 .takes_value(true)
                 .help("Five less than your favorite number"))
        .get_matches();

    let myfile = matches.value_of("file").unwrap_or("input.txt");
    println!("The file passed is: {}", myfile);

    let num_str = matches.value_of("num");
    match num_str {
        None => println!("No idea what your favorite number is."),
        Some(s) => {
            match s.parse::<i32>() {
                Ok(n) => println!("Your favorite number must be {}.", n + 5),
                Err(_) => println!("That's not a number! {}", s),
            }
        }
    }
}
```

`help`信息，由`clap`生成。该示例应用程序的用法，如下所示。

```bash
My Test Program 0.1.0
Hackerman Jones <hckrmnjones@hack.gov>
Teaches argument parsing

USAGE:
    testing [OPTIONS]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -f, --file <file>     A cool file
    -n, --number <num>    Five less than your favorite number
```

我们可以通过运行如下命令，来测试应用程序。

```
$ cargo run -- -f myfile.txt -n 251
```

输出是：

```
The file passed is: myfile.txt
Your favorite number must be 256.
```

[documentation]: https://docs.rs/clap/
