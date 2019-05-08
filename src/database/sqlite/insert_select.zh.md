## 插入并查询数据

[![rusqlite-badge]][rusqlite] [![cat-database-badge]][cat-database]

[`Connection::open`]将打开在早期食谱中，创建的数据库`cats`。此食谱将数据插入到`cat_colors`，还有和`cats`表用到`Connection`的[`execute`]方法。 首先，将数据插入`cat_colors`表。插入颜色(color)记录后，`Connection`的[`last_insert_rowid`]方法，能获取最后插入(color)的`id`。这个`id`能用来，把数据插入到`cats`表。然后，使用[`prepare`]方法准备查询，它会返回[`statement`]结构。然后，再使用[`statement`]的[`query_map`]方法（进行查询）.

```rust
extern crate rusqlite;

use rusqlite::{Connection, Result};
use rusqlite::NO_PARAMS;
use std::collections::HashMap;


#[derive(Debug)]
struct Cat {
    name: String,
    color: String
}

fn main() -> Result<()> {
    let conn = Connection::open("cats.db")?;

    let mut cat_colors = HashMap::new();
    cat_colors.insert(String::from("Blue"), vec!["Tigger", "Sammy"]);
    cat_colors.insert(String::from("Black"), vec!["Oreo", "Biscuit"]);

    for (color, catnames) in &cat_colors{
        conn.execute(
            "INSERT INTO cat_colors (name) values (?1)",
            &[&color.to_string()],
        )?;
    let last_id : String = conn.last_insert_rowid().to_string();

    for cat in catnames{
        conn.execute(
            "INSERT INTO cats (name, color_id) values (?1, ?2)",
            &[&cat.to_string(), &last_id],
        )?;
        }
    }
    let mut stmt = conn.prepare("SELECT c.name, cc.name from cats c
                                 INNER JOIN cat_colors cc ON cc.id = c.color_id;")?;

	let cats = stmt
        .query_map(NO_PARAMS, |row|
			Ok(
                Cat {
					name: row.get(0)?,
					color: row.get(1)?,
				}
			)
		)?;

    for cat in cats {
        println!("Found cat {:?}", cat);
    }

    Ok(())
}
```

[`connection::open`]: https://docs.rs/rusqlite/*/rusqlite/struct.Connection.html#method.open
[`prepare`]: https://docs.rs/rusqlite/*/rusqlite/struct.Connection.html#method.prepare
[`statement`]: https://docs.rs/rusqlite/*/rusqlite/struct.Statement.html
[`query_map`]: https://docs.rs/rusqlite/*/rusqlite/struct.Statement.html#method.query_map
[`execute`]: https://docs.rs/rusqlite/*/rusqlite/struct.Connection.html#method.execute
[`last_insert_rowid`]: https://docs.rs/rusqlite/*/rusqlite/struct.Connection.html#method.last_insert_rowid
