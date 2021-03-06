[![Crates.io](https://img.shields.io/crates/v/minifb.svg)](https://crates.io/crates/minifb)
[![Build Status](https://travis-ci.org/emoon/rust_minifb.svg)](https://travis-ci.org/emoon/rust_minifb)
[![Build Status](https://ci.appveyor.com/api/projects/status/sfvgqq4d4sjulkbx?svg=true)](https://ci.appveyor.com/project/emoon/rust-minifb)

rust_minifb (Mini FrameBuffer) is a small cross platform library written in [Rust](https://www.rust-lang.org) and that makes it easy to render (32-bit) pixels in a window. An example is the best way to show how it works:

[Documentation](http://prodbg.com/minifb/minifb/index.html)

Usage
-----

```toml
# Cargo.toml
[dependencies]
minifb = "0.2.7"
```

Example
-------

```rust
extern crate minifb;

const WIDTH: usize = 640;
const HEIGHT: usize = 360;

fn main() {
    let mut buffer: Vec<u32> = vec![0; WIDTH * HEIGHT];

    let mut window = match minifb::Window::new("Test - ESC to exit", WIDTH, HEIGHT, Scale::X1) {
        Ok(win) => win,
        Err(err) => {
            println!("Unable to create window {}", err);
            return;
        }
    };

    while window.is_open() && !window.is_key_down(Key::Escape) {
        for i in buffer.iter_mut() {
            *i = 0; // write something more funny here!
        }

        window.update(&buffer);
    }
}
```

Status
------
Currently Mac, Linux and Windows (64-bit and 32-bit) are the current supported platforms. X11 (Linux/FreeBSD/etc) support has been tested on Ubuntu (x64). Bug report(s) for other OSes/CPUs are welcome! 


Build instructions
------------------

```
cargo build
cargo run --example noise 
```

This will run the [noise example](https://github.com/emoon/rust_minifb/blob/master/examples/noise.rs) which should look something like this (Mac screenshot)

![mac_screenshot](https://dl.dropboxusercontent.com/u/5205843/rust_minifb/noise_screen.png)

## License

Licensed under either of

 * Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.
