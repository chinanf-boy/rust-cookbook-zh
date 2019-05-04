## 创建 sqlite 数据库

[![rusqlite-badge]][rusqlite] [![cat-database-badge]][cat-database]

使用`rusqlite`箱子打开 sqlite 数据库。见[机箱][documentation]用于在 Windows 上编译。

[`Connection::open`]如果数据库不存在，将创建该数据库。

```rust,no_run
extern crate rusqlite;

use rusqlite::{Connection, Result};
use rusqlite::NO_PARAMS;

fn main() -> Result<()> {
    let conn = Connection::open("cats.db")?;

    conn.execute(
        "create table if not exists cat_colors (
             id integer primary key,
             name text not null unique
         )",
        NO_PARAMS,
    )?;
    conn.execute(
        "create table if not exists cats (
             id integer primary key,
             name text not null,
             color_id integer not null references cat_colors(id)
         )",
        NO_PARAMS,
    )?;

    Ok(())
}
```

[`connection::open`]: https://docs.rs/rusqlite/*/rusqlite/struct.Connection.html#method.open
[documentation]: https://github.com/jgallagher/rusqlite#user-content-notes-on-building-rusqlite-and-libsqlite3-sys
