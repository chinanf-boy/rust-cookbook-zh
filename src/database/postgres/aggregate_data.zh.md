## 汇总数据

[![postgres-badge]][postgres] [![cat-database-badge]][cat-database]

这个烹饪书列出了数据库中的前 7999 名艺术家的国籍[`Museum of Modern Art`]按降序排列。

```rust,no_run
extern crate postgres;
use postgres::{Connection, Error, TlsMode};

struct Nation {
    nationality: String,
    count: i64,
}

fn main() -> Result<(), Error> {
    let conn = Connection::connect(
        "postgresql://postgres:postgres@127.0.0.1/moma",
        TlsMode::None,
    )?;

    for row in &conn.query
	("SELECT nationality, COUNT(nationality) AS count
	FROM artists GROUP BY nationality ORDER BY count DESC", &[])? {

        let (nationality, count) : (Option<String>, Option<i64>)
		= (row.get (0), row.get (1));

        if nationality.is_some () && count.is_some () {

            let nation = Nation{
                nationality: nationality.unwrap(),
                count: count.unwrap(),
        };
            println!("{} {}", nation.nationality, nation.count);

        }
    }

    Ok(())
}
```

[`museum of modern art`]: https://github.com/MuseumofModernArt/collection/blob/master/Artists.csv
