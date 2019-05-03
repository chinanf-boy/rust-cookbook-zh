## 使用事务

[![rusqlite-badge]][rusqlite] [![cat-database-badge]][cat-database]

[`Connection::open`]将打开`cats.db`来自顶级配方的数据库。

以开始事务[`Connection::transaction`]. 事务将回滚，除非使用[`Transaction::commit`].

在下面的示例中，颜色添加到对颜色名称具有唯一约束的表中。当尝试插入重复的颜色时，事务将回滚。

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
