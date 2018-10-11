
# 为Rust Cookbook做贡献

食谱需要贡献者,并且易于贡献.欢迎帮助.

-   [Building and testing](#building-and-testing)
-   [Finding what to contribute](#finding-what-to-contribute)
-   [Adding an example](#adding-an-example)
-   [Example guidelines](#example-guidelines)

## 建设和测试

首先,从git克隆cookbook并导航到该目录:

```
git clone https://github.com/rust-lang-nursery/rust-cookbook.git
cd rust-cookbook
```

Cookbook是用[mdBook],所以先用Cargo安装:

```
cargo install --version 0.1.8 mdbook
```

要在本地构建和查看cookbook,请运行:

```
mdbook serve
```

然后打开`http://localhost:3000`在网络浏览器中浏览食谱.您对cookbook源所做的任何更改都将在浏览器中自动重建并显示,因此在编辑时保持此窗口打开会很有帮助.

烹饪书中的所有示例都经过测试[怀疑论者],一种用于以类似于rustdoc的样式测试任意markdown文档的工具.

要运行cookbook测试套件:

```
cargo test
```

## 棉短绒

Rust Cookbook附带了在持续集成服务器上运行的链接检查和拼写检查.在提交拉取请求之前,应在本地运行这些短绒,以确保没有死链接或拼写错误.

要安装链接检查程序,请查看文档[蟒蛇]安装python 3.6和pip3.使用pip3完成依赖关系后安装链接检查器.

```
[sudo] pip3 install link-checker==0.1.0
```

或者,添加用户安装目录(可能`~/.local/bin`)到您的PATH变量并为您的用户安装链接检查器.

```
pip3 install --user link-checker==0.1.0
```

首先在本地检查本书的链接需要使用mdBook构建本书.从cookbook的根目录,以下命令运行链接检查器.

```
mdbook build
link-checker ./book
```

aspell二进制文件提供拼写检查.Apt包在基于Debian的操作系统上提供安装.

```
[sudo] apt install aspell -y
```

在其他Linux发行版上,您可能还需要安装`aspell-en`包裹或类似物.

要在本地检查Rust Cookbook的拼写,请从Cookbook的根目录运行以下命令.

```
./ci/spellchecker.sh

# or, if you're using a different locale
LANG=en_US.UTF-8 ./ci/spellchecker.sh
```

如果拼写检查器找到拼写错误的单词,您可以使用数字键更正拼写错误.如果拼写错误是错误的,请将单词添加到位于的字典中`ci/dictionary.txt`.紧迫`a`要么`l`不会将该单词添加到自定义词典中.

[mdbook]: http://azerupi.github.io/mdBook/index.html

[python]: https://packaging.python.org/tutorials/installing-packages/#install-pip-setuptools-and-wheel

[skeptic]: https://github.com/brson/rust-skeptic

## 寻找贡献的东西

该项目旨在简化,并始终提供明显的下一个工作项目.如果在任何时候没有明显的贡献,这是一个错误.随意请求额外的支持[Rust Ecosystem Working Group](https://gitter.im/rust-lang/WG-ecosystem).

该烹饪书的开发过程目前围绕着板条箱:我们决定在食谱中代表哪些板条箱,然后提出示例用例来编写,然后编写示例.这些是所需的三种基本的,经常性的贡献类型.

今天的食谱开发过程与之相关[利兹兹闪电战],一个改善Rust crate生态系统的更广泛的项目,目前该食谱代表了那里正在考虑的板条箱.找到烹饪书所需的最直接工作的最简单方法是遵循该主题顶部的"下一步"部分,该部分应始终链接到为烹饪书做出贡献的内容.

否则,请查看GitHub问题[例]标签.最简单的贡献方式是声明其中一个示例,然后提交PR添加它.如果您确实声明了一个,请发表评论,这样,其他人不会意外地复制您的工作.

如果您对某个特定板条箱的示例有所了解,请在相关板条上进行建议[跟踪问题].

请不要提交尚未在食谱中表示的包装箱的示例,除非它是libz闪电战箱包计划的一部分.未来将对更广泛的板条箱做出贡献.有关在食谱中表示哪些包装箱的更多信息,请参阅["关于箱子表示的说明"][which-crates]在食谱中.

[example]: https://github.com/rust-lang-nursery/rust-cookbook/issues?q=is%3Aissue+is%3Aopen+label%3Aexample

[tracking issue]: https://github.com/rust-lang-nursery/rust-cookbook/issues?q=is%3Aissue+is%3Aopen+label%3A%22tracking+issue%22

[which-crates]: https://rust-lang-nursery.github.io/rust-cookbook/about.html#a-note-about-crate-representation

[libz blitz]: https://internals.rust-lang.org/t/rust-libz-blitz/5184

## 添加一个例子

添加示例涉及:

-   决定哪个*部分*它所属的书
-   决定哪个*类别*适用于它
-   将示例添加到intro.zh.md中的节索引
-   将示例添加到相应的部分markdown文件中
-   根据需要更新徽章和超链接
-   写一个有用的例子描述

完成的提交看起来像[这个].

[this one]: https://github.com/rust-lang-nursery/rust-cookbook/commit/e698443f2af08d3106d953c68c1977eba3c3526c

目前的例子有三种方式:

-   书籍部分 - 食谱是一本书,在逻辑部分就像一本书,如"基础","编码","并发".
-   类别标签 - 每个示例都标有一个或多个类别标签,如"filesystem","debugging".
-   Crate标签 - 每个示例都标有一个或多个crate标签,指示示例中表示了哪些crate.那些不使用额外板条箱的人只需标记为'std'.

有关该书组织的更多信息,请参阅["怎么读这本书"]在食谱中.

希望你的例子属于一个明显的部分和类别,但由于食谱是如此新,很可能不是.在线程上询问.

对于大多数步骤,您可以简单地遵循现有示例的主角.艺术来自写作有效的例子.

["how to read this book"]: https://rust-lang-nursery.github.io/rust-cookbook/about.html#how-to-read-this-book

## 示例指南

食谱中的例子有这些目标和品质:

-   它们可以用一句话来描述它们的效用.
-   完整的初学者可以阅读和理解它们.
-   它们是独立的示例,可以复制到学习者自己的工作区中,并进行编译和修改以进行实验.
-   它们展示了真实的任务,经验丰富的开发人员可以将其用作参考.
-   他们遵循最佳实践,不采取捷径.
-   他们使用一致的错误处理.

#### 标题

示例应该有一个简单的单句标题,描述典型的Rust用户通常想要做的事情.

> ## 生成具有给定分布的随机数

#### 描述

描述导入的特征和使用的方法.考虑哪些信息支持用例,对于新用户可能并不明显.将描述保持为1-4个句子,避免在代码范例之外的解释.

使用代码执行的第三人称叙述,借此机会链接到API文档.一直用[active voice](https://www.plainlanguage.gov/guidelines/conversational/use-active-voice/).在doc.rust-lang.org/std或docs.rs上对API的所有引用进行超链接,并将其设置为`code`.使用通配符版本说明符进行包链接.

执行不明显的代码的任何要求,例如传递环境标志或配置`Cargo.toml`应该在代码示例之后添加.

> 默认情况下,生成随机数[均匀分布].要使用其他分布生成数字,您需要实例化分布,然后使用该分布进行采样[`Distribution::sample`]借助随机数生成器[`rand::Rng`].
>
> 该[可用的分发在此记录][rand-distributions].一个使用的例子[`Normal`]分布如下所示.

[uniform distribution]: https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)

[`distribution::sample`]: https://docs.rs/rand/*/rand/distributions/trait.Distribution.html#tymethod.sample

[`rand::rng`]: https://docs.rs/rand/*/rand/trait.Rng.html

[rand-distributions]: https://docs.rs/rand/*/rand/distributions/index.html

[`normal`]: https://docs.rs/rand/*/rand/distributions/struct.Normal.html

#### 码

示例旨在由完整的初学者阅读,并复制到项目中进行实验.他们应该遵循最佳做法,而不是走捷径.

该示例应具有最少的代码,该代码不直接支持该示例的描述.将额外的功能和类型保持在最低限度.

如果示例必须处理错误的可能性,请按照错误处理模板进行操作["关于错误处理的说明"][errors].示例始终正确设置错误处理并传播错误`?`(不`try!`,`urwrap`, 要么`expect`).如果示例中不需要错误处理,请选择`main()`.

避免进口水珠(`*`),即使是前奏,以便用户可以看到所谓的特征.(有些板条箱可能会考虑使用glob导入作为前奏最佳实践,这使得这很尴尬.)

示例应该简单明了,经验丰富的开发人员不需要评论.

示例应该在没有警告,clippy lint警告或恐慌的情况下编译.代码应该由rustfmt格式化.隐藏所有未完成示例主题的错误样板和样本部分.

标记依赖于外部系统的示例`no_run`如果示例不需要,则删除它们.避免内联注释,更喜欢说明中的解释.

> ```rust
> extern crate rand;
>
> use rand::distributions::{Normal, Distribution};
>
> fn main() {
>    let mut rng = rand::thread_rng();
>    let normal = Normal::new(2.0, 3.0);
>    let v = normal.sample(&mut rng);
>    println!("{} is from a N(2, 9) distribution", v)
> }
> ```

最后,本书旨在展示可以很好地协同工作的板条箱的集成.我们正在寻找能够明智地展示多个箱子的例子.

[errors]: https://rust-lang-nursery.github.io/rust-cookbook/about.html#a-note-about-error-handling
