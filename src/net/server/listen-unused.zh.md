
## 监听未使用的端口TCP/IP

[![std-badge]][std] [![cat-net-badge]][cat-net]

在这个例子中,端口显示在控制台上,程序将侦听直到请求被发出.`SocketAddrV4`将端口设置为0时分配一个随机端口.

```rust,no_run
# #[macro_use]
# extern crate error_chain;
#
use std::net::{SocketAddrV4, Ipv4Addr, TcpListener};
use std::io::Read;
#
# error_chain! {
#     foreign_links {
#         Io(::std::io::Error);
#     }
# }

fn run() -> Result<()> {
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
#
# quick_main!(run);
```
