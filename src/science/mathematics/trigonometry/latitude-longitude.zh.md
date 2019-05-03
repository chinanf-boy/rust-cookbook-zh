## 地球两点之间的距离

[![std-badge]][std]

默认情况下，rust提供数学[浮法]如三角函数、平方根、弧度和度数之间的转换函数等。

下面的示例使用[半正矢]. 点用经纬度对表示。然后，[`to_radians`]把它们转换成弧度。[`sin`]，[`cos`]，[`powi`]和[`sqrt`]计算中心角。最后，可以计算距离。

```rust
fn main() {
    let earth_radius_kilometer = 6371.0_f64;
    let (paris_latitude_degrees, paris_longitude_degrees) = (48.85341_f64, -2.34880_f64);
    let (london_latitude_degrees, london_longitude_degrees) = (51.50853_f64, -0.12574_f64);

    let paris_latitude = paris_latitude_degrees.to_radians();
    let london_latitude = london_latitude_degrees.to_radians();

    let delta_latitude = (paris_latitude_degrees - london_latitude_degrees).to_radians();
    let delta_longitude = (paris_longitude_degrees - london_longitude_degrees).to_radians();

    let central_angle_inner = (delta_latitude / 2.0).sin().powi(2)
        + paris_latitude.cos() * london_latitude.cos() * (delta_longitude / 2.0).sin().powi(2);
    let central_angle = 2.0 * central_angle_inner.sqrt().asin();

    let distance = earth_radius_kilometer * central_angle;

    println!(
        "Distance between Paris and London on the surface of Earth is {:.1} kilometers",
        distance
    );
}
```

[float methods]: https://doc.rust-lang.org/std/primitive.f64.html#methods

[`to_radians`]: https://doc.rust-lang.org/std/primitive.f64.html#method.to_radians

[`sin`]: https://doc.rust-lang.org/std/primitive.f64.html#method.sin

[`cos`]: https://doc.rust-lang.org/std/primitive.f64.html#method.cos

[`powi`]: https://doc.rust-lang.org/std/primitive.f64.html#method.powi

[`sqrt`]: https://doc.rust-lang.org/std/primitive.f64.html#method.sqrt

[haversine formula]: https://en.wikipedia.org/wiki/Haversine_formula
