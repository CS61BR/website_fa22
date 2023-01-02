---
parent: "Lab 07: BSTMap"
title: Instructions
nav_order: 1
---

## Starting the Lab

 - Open the `lab07/` folder in your preferred text editor.
 - Open the `lab07/` folder in your preferred terminal.
 - Run `git pull skeleton main` to get the latest version of the skeleton code for this lab.

## Implementing BSTMap

Today, you'll be writing a binary search tree implementation from scratch. In fact, the starter code doesn't even contain a `bstmap.rs` file - you'll need to create it yourself.

Create a `btsmap.rs` file in the `src/` folder, and create a `BSTMap<K, V>` type in it. The `BSTMap` type should implement the `Map61B` trait as following:
```
impl<K: Ord, V> Map61B for BSTMap<K, V> { ... }
```
You are required to implement the following methods:
 - `new`
 - `len`
 - `clear`
 - `contains_key`
 - `insert`
 - `get`
 - `get_mut`

The following methods are optional. If you don't implement them, just replace their bodies with `unimplemented!()`:
 - `remove`
 - `into_iter` (from the `IntoIterator` trait). If you don't plan on implementing this, you can use `std::vec::IntoIter<(K, V)>` as a placeholder for the trait's `IntoIter` type.

If you get stuck, read through some of the implementations in `ullmap.rs`. `BSTMap` should be very similar to `ULLMap`, except `BSTMap` uses a binary search tree and `ULLMap` uses a singly-linked list. 

Once you are finished, you can test the required methods with `cargo test map`. To test the optional methods as well, run `cargo test`.

## Benchmarking your Implementation

How does your implementation stack up to a naive implementation (`ULLMap`, from `ullmap.rs`) and industrial-strength implementations (`BTreeMap` and `HashMap`, from the standard library)? Let's find out!

Run the interactive benchmarks with `cargo run --release`. How well does each implementation scale when the keys are inserted randomly? How well do they scale when the keys are inserted in ascending order?