### No-std friendly fork

This fork has been patched to stop the 'std' flag being default. This fixes
no_std builds where both the main dependency tree, and the dev-dependency tree
use this crate (see Cargo 5730).

Add this to your Cargo.toml to use:

```
[patch.crates-io]
# Use a special copy of byteorder, which has std support disabled
# This is a work around for Cargo bug 5730
byteorder = { git = "https://github.com/rust-embedded-community/byteorder" }
```

### Original Readme

This crate provides convenience methods for encoding and decoding
numbers in either big-endian or little-endian order.

[![Build status](https://api.travis-ci.org/BurntSushi/byteorder.svg)](https://travis-ci.org/BurntSushi/byteorder)
[![](http://meritbadge.herokuapp.com/byteorder)](https://crates.io/crates/byteorder)

Dual-licensed under MIT or the [UNLICENSE](http://unlicense.org).


### Documentation

https://docs.rs/byteorder


### Installation

This crate works with Cargo and is on
[crates.io](https://crates.io/crates/byteorder). Add it to your `Cargo.toml`
like so:

```toml
[dependencies]
byteorder = "1"
```

If you want to augment existing `Read` and `Write` traits, then import the
extension methods like so:

```rust
extern crate byteorder;

use byteorder::{ReadBytesExt, WriteBytesExt, BigEndian, LittleEndian};
```

For example:

```rust
use std::io::Cursor;
use byteorder::{BigEndian, ReadBytesExt};

let mut rdr = Cursor::new(vec![2, 5, 3, 0]);
// Note that we use type parameters to indicate which kind of byte order
// we want!
assert_eq!(517, rdr.read_u16::<BigEndian>().unwrap());
assert_eq!(768, rdr.read_u16::<BigEndian>().unwrap());
```

### `no_std` crates

This crate has a feature, `std`, that is enabled by default. To use this crate
in a `no_std` context, add the following to your `Cargo.toml`:

```toml
[dependencies]
byteorder = { version = "1", default-features = false }
```


### Alternatives

Note that as of Rust 1.32, the standard numeric types provide built-in methods
like `to_le_bytes` and `from_le_bytes`, which support some of the same use
cases.
