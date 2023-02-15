## 在 Postgres 数据库中，创建表

[![postgres-badge]][postgres] [![cat-database-badge]][cat-database]

使用[`postgres`]在 Postgres 数据库中，创建表。

[`Connection::connect`]帮助连接到现有数据库。该食谱的`Connection::connect`使用一个 URL 字符串格式。它假定现有一个名为`library`的数据库，用户名是`postgres`，密码是`postgres`.

```rust,no_run
extern crate postgres;

use postgres::{Connection, TlsMode, Error};

fn main() -> Result<(), Error> {
    let conn = Connection::connect("postgresql://postgres:postgres@localhost/library",
                                    TlsMode::None)?;

     conn.execute("CREATE TABLE IF NOT EXISTS author (
                    id              SERIAL PRIMARY KEY,
                    name            VARCHAR NOT NULL,
                    country         VARCHAR NOT NULL
                  )", &[])?;

    conn.execute("CREATE TABLE IF NOT EXISTS book  (
                    id              SERIAL PRIMARY KEY,
                    title           VARCHAR NOT NULL,
                    author_id       INTEGER NOT NULL REFERENCES author
                )", &[])?;

    Ok(())

}
```

[`postgres`]: https://docs.rs/postgres/0.15.2/postgres/
[`connection::connect`]: https://docs.rs/postgres/0.15.2/postgres/struct.Connection.html#method.connect
