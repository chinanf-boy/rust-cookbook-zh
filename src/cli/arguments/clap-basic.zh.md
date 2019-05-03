## 解析命令行参数

[![clap-badge]][clap] [![cat-command-line-badge]][cat-command-line]

该应用程序描述了其命令行界面的结构`clap`的建设者风格。该[文件]提供了另外两种可能的实例化应用程序的方法。

在构建器样式中，`with_name`是唯一的标识符`value_of`将用于检索传递的值。该`short`和`long`options控制用户将要键入的标志;短旗看起来像`-f`和长旗看起来像`--file`。

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

使用信息由生成`clap`。示例应用程序的用法如下所示。

```
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

我们可以通过运行如下命令来测试应用程序。

```
$ cargo run -- -f myfile.txt -n 251
```

输出是：

```
The file passed is: myfile.txt
Your favorite number must be 256.
```

[documentation]: https://docs.rs/clap/
