## 使用事务

[![rusqlite-badge]][rusqlite] [![cat-database-badge]][cat-database]

[`Connection::open`]将打开`cats.db` —— 来自之前食谱的数据库。

用[`Connection::transaction`]开始一个事务（transaction）。事务将回滚，除非明确使用[`Transaction::commit`]提交。

> 一次事务，就是一系列对数据库的操作，且明确`commit`后才会执行。

在下面的示例中，将颜色添加表，该表对颜色名称要唯一，进行约束。当尝试插入重复的颜色时，事务将回滚。

```rust,no_run
extern crate rusqlite;

use rusqlite::{Connection, Result, NO_PARAMS};

fn main() -> Result<()> {
    let mut conn = Connection::open("cats.db")?;

    successful_tx(&mut conn)?;

    let res = rolled_back_tx(&mut conn);
    assert!(res.is_err());

    Ok(())
}

fn successful_tx(conn: &mut Connection) -> Result<()> {
    let tx = conn.transaction()?;

    tx.execute("delete from cat_colors", NO_PARAMS)?;
    tx.execute("insert into cat_colors (name) values (?1)", &[&"lavender"])?;
    tx.execute("insert into cat_colors (name) values (?1)", &[&"blue"])?;

    tx.commit()
}

fn rolled_back_tx(conn: &mut Connection) -> Result<()> {
    let tx = conn.transaction()?;

    tx.execute("delete from cat_colors", NO_PARAMS)?;
    tx.execute("insert into cat_colors (name) values (?1)", &[&"lavender"])?;
    tx.execute("insert into cat_colors (name) values (?1)", &[&"blue"])?;
    tx.execute("insert into cat_colors (name) values (?1)", &[&"lavender"])?;

    tx.commit()
}
```

[`connection::transaction`]: https://docs.rs/rusqlite/*/rusqlite/struct.Connection.html#method.transaction
[`transaction::commit`]: https://docs.rs/rusqlite/*/rusqlite/struct.Transaction.html#method.commit
