## 侦听，未使用的端口 TCP/IP

[![std-badge]][std] [![cat-net-badge]][cat-net]

在本例中，端口会显示在控制台。且程序会一直监听，直到一个请求发出。`SocketAddrV4`会在端口(第二参数)设为 0 时，分配一个随机端口。

```rust,no_run
use std::net::{SocketAddrV4, Ipv4Addr, TcpListener};
use std::io::{Read, Error};

fn main() -> Result<(), Error> {
    let loopback = Ipv4Addr::new(127, 0, 0, 1);
    let socket = SocketAddrV4::new(loopback, 0);
    let listener = TcpListener::bind(socket)?;
    let port = listener.local_addr()?;
    println!("Listening on {}, access this port to end the program", port);
    let (mut tcp_stream, addr) = listener.accept()?; //block  until requested
    println!("Connection received! {:?} is sending data.", addr);
    let mut input = String::new();
    let _ = tcp_stream.read_to_string(&mut input)?;
    println!("{:?} says {}", addr, input);
    Ok(())
}
```
