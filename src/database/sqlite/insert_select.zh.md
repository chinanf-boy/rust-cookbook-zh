## 插入并选择数据

[![rusqlite-badge]][rusqlite] [![cat-database-badge]][cat-database]

[`Connection::open`]将打开数据库`cats`在早期配方中创建。此配方将数据插入`cat_colors`和`cats`表使用[`execute`]方法`Connection`. 首先，将数据插入`cat_colors`表。插入颜色记录后，[`last_insert_rowid`]方法`Connection`用于获取`id`最后插入的颜色。这个`id`在将数据插入到`cats`表。然后，使用[`prepare`]方法，给出[`statement`]结构。然后，使用[`query_map`]方法[`statement`].

```
eextern crate rusqlite;

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
