## 使用 HTTP range 标头，进行部分下载

[![reqwest-badge]][reqwest] [![cat-net-badge]][cat-net]

使用[`reqwest::Client::head`]，得到响应的[内容长度][content-length]。

然后，代码使用[`reqwest::Client::get`]，在打印进度消息的同时，下载 10240 字节的内容。这个[Range] 标头指定块的大小和位置。

Range 标头在[射频识别芯片][http range rfc7233]中定义。

```rust,no_run
# #[macro_use]
# extern crate error_chain;
extern crate reqwest;

use std::fs::File;
use std::str::FromStr;
use reqwest::header::{HeaderValue, CONTENT_LENGTH, RANGE};
use reqwest::StatusCode;

#
# error_chain! {
#     foreign_links {
#         Io(std::io::Error);
#         Reqwest(reqwest::Error);
#         Header(reqwest::header::ToStrError);
#     }
# }
#
# struct PartialRangeIter {
#     start: u64,
#     end: u64,
#     buffer_size: u32,
# }
#
# impl PartialRangeIter {
#     pub fn new(start: u64, end: u64, buffer_size: u32) -> Result<Self> {
#         if buffer_size == 0 {
#             Err("invalid buffer_size, give a value greater than zero.")?;
#         }
#
#         Ok(PartialRangeIter {
#             start,
#             end,
#             buffer_size,
#         })
#     }
# }
#
# impl Iterator for PartialRangeIter {
#     type Item = HeaderValue;
#
#     fn next(&mut self) -> Option<Self::Item> {
#         if self.start > self.end {
#             None
#         } else {
#             let prev_start = self.start;
#             self.start += std::cmp::min(self.buffer_size as u64, self.end - self.start + 1);
#             // 注意(unwrap): `HeaderValue::from_str` 仅在值不是 有效 ASCII 字符，才会失败
#             // 因为，这个格式字符串是静态的，两个值是整数，
#             // 也就是说，失败不会发生。
#             Some(HeaderValue::from_str(&format!("bytes={}-{}", prev_start, self.start - 1)).unwrap())
#         }
#     }
# }

fn run() -> Result<()> {
    let url = "https://httpbin.org/range/102400?duration=2";
    const CHUNK_SIZE: u32 = 10240;

    let client = reqwest::Client::new();
    let response = client.head(url).send()?;
    let length = response
        .headers()
        .get(CONTENT_LENGTH)
        .ok_or("response doesn't include the content length")?;
    let length = u64::from_str(length.to_str()?).map_err(|_| "invalid Content-Length header")?;

    let mut output_file = File::create("download.bin")?;

    println!("starting download...");
    for range in PartialRangeIter::new(0, length - 1, CHUNK_SIZE)? {
        println!("range {:?}", range);
        let mut response = client.get(url).header(RANGE, range).send()?;

        let status = response.status();
        if !(status == StatusCode::OK || status == StatusCode::PARTIAL_CONTENT) {
            bail!("Unexpected server response: {}", status)
        }

        std::io::copy(&mut response, &mut output_file)?;
    }

    println!("Finished with success!");
    Ok(())
}
#
# quick_main!(run);
```

[`reqwest::client::get`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html#method.get
[`reqwest::client::head`]: https://docs.rs/reqwest/*/reqwest/struct.Client.html#method.head
[content-length]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Length
[range]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range
[http range rfc7233]: https://tools.ietf.org/html/rfc7233#section-3.1
