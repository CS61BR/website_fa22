---
parent: "Lab 03: Testing and Timing"
title: Background
nav_order: 0
---


## AList

Vec is written in Rust; you can read the [source code](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#400) if you're interested. 

If you're even more interested, you might find [implementing Vec from scratch](https://doc.rust-lang.org/nomicon/vec/vec.html) fun. The fundamental idea is to use pointers and `unsafe` magic to manage the memory where the elements get stored.

The idea behind `AList` is essentially to make a home-grown Vec implementation. However, pointers are a bit too in-depth for this assignment, so `AList` uses `Box<[T]>` instead. It's almost the same thing, but `Box<[T]>` is safe to interact with, and can essentially be treated as a fixed size array. And as the benchmarks will show, it's not that much worse (performance-wise) than the pointer approach.


## What is `cargo run --release`?

When you run a program with `cargo run`, it defaults to running the _debug_ binary. This is a version of the program with:
 - debug symbols enabled: these are things like variable names and line numbers, so that debuggers can tell you what line you're on and can print variables for you
 - no optimizations: the compiler won't optimize your code, so most code will run much much slower.

However, there's also a _release_ binary, which is the "final" version of the compiled program which has:
 - no debug symbols: debuggers won't be very useful
 - optimized: code go speedy

When running benchmarks, we're interested in how fast the _release_ code will go, since that's where performance actually matters. This is why we run `cargo run --release` rather than just `cargo run` in this lab.

## Black box

Compilers are very smart, and this can sometimes mess up benchmarks. For example, consider the following program:

```rust
fn addition(a: usize, b: usize) -> usize {
    a + b
}

fn main() {
    let start = std::time::Instant::now();
    for _ in 0..1000000 {
        addition(10, 20);
    }
    println!("{:?}", start.elapsed());
}
```
Surprisingly, this only takes a few nanoseconds. Increasing the number of loops doesn't affect the time at all: 10 additions seem to take the same amount of time as 10,000,000 additions. Why?

The compiler has essentially noticed that the result of `addition` is never being used, so it never even bothers to do the work in the first place. In fact, the compiler can just treat the above program as this:
```rust
fn main() {
    let start = std::time::Instant::now();
    println!("{:?}", start.elapsed());
}
```
which is indeed a lot faster, but not what we wanted.

Is there a way to tell the compiler that we want it to do useless work? There is! We can use `std::hint::black_box` to tell the compiler "I don't actually care about this result, but please pretend that I do".
```rust
fn addition(a: usize, b: usize) -> usize {
    a + b
}

fn main() {
    let start = std::time::Instant::now();
    for _ in 0..1000000 {
        std::hint::black_box(addition(10, 20));
    }
    println!("{:?}", start.elapsed());
}
```
Now, the compiler will actually perform 1000000 additions, so the benchmarks will actually be useful.