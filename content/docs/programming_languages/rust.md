+++
title = 'Rust'
date = 2024-11-24T00:45:35+05:30
draft = false
description = 'Information on Rust programming language'
+++

# Hello world

```rust
fn main() {
    println!("Hello world!")
}
```

# rustc

- `rustc FILE_NAME.rs`
  - create a new compiled binary with same filename without `rs` extention

# Cargo

- `cargo build`
  - `cargo build --release`
- `cargo run`
- `cargo check`
- `cargo update`
  - update dependencies

# Comments

- `//`

# Functions

## Associated functions

- An associated function is a function that’s implemented on a type.
  - Invoked like this `String::new()`

# Variables

```rust
// without type annotation
let cars = 2;

// with type annotation
let cars: i32 = 2;

// multiple variables
let (cars, trucks) = (2,4);
```

- by default variables are immutable
	- reason safety, concurrency and speed
		- lot of bugs cannot happen if value is not changed, hence safety improved
		- data shared between threads and processes does not change and required less locks, hence concurrency is improved
		- compiler can do compile time optimization if it knows data does not change, he speed of application is improved

```rust
// make variable mutable by adding 'mut' keyword before variable name
let mut cars = 2;
```

## const

```rust
const PI: f64: 3.14
```

- `const` keyword is used to define constant variable which can be used across module scope, which is defined outside the functions
- shake case is the convention for const variable name
- inline to compiple time, they are fast to access in program.
