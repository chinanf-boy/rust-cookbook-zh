## 排序结构的 vector

[![std-badge]][std] [![cat-science-badge]][cat-science]

对 Person 结构的 Vector 进行排序，通过属性`name`和`age`的自然顺序（按名称和年龄）。为了使 Person 可排序，你需要四个 trait[`Eq`]，[`PartialEq`]，[`Ord`]和[`PartialOrd`]。可以简单地`derive`出这些特征。您还可以使用一个[`vec:sort_by`]方法，提供自定义比较函数：只按年龄排序。

```rust
#[derive(Debug, Eq, Ord, PartialEq, PartialOrd)]
struct Person {
    name: String,
    age: u32
}

impl Person {
    pub fn new(name: String, age: u32) -> Self {
        Person {
            name,
            age
        }
    }
}

fn main() {
    let mut people = vec![
        Person::new("Zoe".to_string(), 25),
        Person::new("Al".to_string(), 60),
        Person::new("John".to_string(), 1),
    ];

    // 自然顺序，排序 people  (名字 和 年龄)
    people.sort();

    assert_eq!(
        people,
        vec![
            Person::new("Al".to_string(), 60),
            Person::new("John".to_string(), 1),
            Person::new("Zoe".to_string(), 25),
        ]);

    // 用 年龄 排序
    people.sort_by(|a, b| b.age.cmp(&a.age));

    assert_eq!(
        people,
        vec![
            Person::new("Al".to_string(), 60),
            Person::new("Zoe".to_string(), 25),
            Person::new("John".to_string(), 1),
        ]);

}
```

[`eq`]: https://doc.rust-lang.org/std/cmp/trait.Eq.html
[`partialeq`]: https://doc.rust-lang.org/std/cmp/trait.PartialEq.html
[`ord`]: https://doc.rust-lang.org/std/cmp/trait.Ord.html
[`partialord`]: https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html
[`vec:sort_by`]: https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_by
