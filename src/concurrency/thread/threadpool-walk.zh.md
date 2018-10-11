
## 同时计算iso文件的SHA1总和

[![threadpool-badge]][threadpool] [![num_cpus-badge]][num_cpus] [![walkdir-badge]][walkdir] [![ring-badge]][ring] [![cat-concurrency-badge]][cat-concurrency][![cat-filesystem-badge]][cat-filesystem]

此示例计算当前目录中具有iso扩展名的每个文件的SHA1.线程池生成的线程数等于系统中存在的核心数[`num_cpus::get`].[`Walkdir::new`]迭代当前目录并调用[`execute`]执行读取和计算SHA1哈希的操作.

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate walkdir;
extern crate ring;
extern crate num_cpus;
extern crate threadpool;

# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#     }
# }
#
use walkdir::WalkDir;
use std::fs::File;
use std::io::{BufReader, Read};
use std::path::Path;
use threadpool::ThreadPool;
use std::sync::mpsc::channel;
use ring::digest::{Context, Digest, SHA1};

# // Verify the iso extension
# fn is_iso(entry: &Path) -> bool {
#     match entry.extension() {
#         Some(e) if e.to_string_lossy().to_lowercase() == "iso" => true,
#         _ => false,
#     }
# }
#
fn compute_digest<P: AsRef<Path>>(filepath: P) -> Result<(Digest, P)> {
    let mut buf_reader = BufReader::new(File::open(&filepath)?);
    let mut context = Context::new(&SHA1);
    let mut buffer = [0; 1024];

    loop {
        let count = buf_reader.read(&mut buffer)?;
        if count == 0 {
            break;
        }
        context.update(&buffer[..count]);
    }

    Ok((context.finish(), filepath))
}

fn run() -> Result<()> {
    let pool = ThreadPool::new(num_cpus::get());

    let (tx, rx) = channel();

    for entry in WalkDir::new("/home/user/Downloads")
        .follow_links(true)
        .into_iter()
        .filter_map(|e| e.ok())
        .filter(|e| !e.path().is_dir() && is_iso(e.path())) {
            let path = entry.path().to_owned();
            let tx = tx.clone();
            pool.execute(move || {
                let digest = compute_digest(path);
                tx.send(digest).expect("Could not send data!");
            });
        }

    drop(tx);
    for t in rx.iter() {
        let (sha, path) = t?;
        println!("{:?} {:?}", sha, path);
    }
    Ok(())
}
#
# quick_main!(run);
```

[`execute`]: https://docs.rs/threadpool/*/threadpool/struct.ThreadPool.html#method.execute

[`num_cpus::get`]: https://docs.rs/num_cpus/*/num_cpus/fn.get.html

[`walkdir::new`]: https://docs.rs/walkdir/*/walkdir/struct.WalkDir.html#method.new
