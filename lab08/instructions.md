---
parent: "Lab 08: HashMap"
title: Instructions
nav_order: 1
---

## Starting the Lab

 - Open the `lab08/` folder in your preferred text editor.
 - Open the `lab08/` folder in your preferred terminal.
 - Run `git pull skeleton main` to get the latest version of the skeleton code for this lab.

## Implementing MyHashMap

Today, you'll be implementing your very own hashmap. Specifically, your hashmap will be an external chaining hashmap, using a bucketing scheme. In this scheme, the hashmap stores a list of buckets. Each "bucket" is a `Vec<(K, V)>` that stores all the key-value pairs corresponding to a specific hash code (modulo the list length).

Implement `MyHashMap<K, V>` in `myhashmap.rs`. The `MyHashMap` type should implement the `Map61B` trait as following:
```
impl<K: Hash + Eq, V> Map61B for MyHashMap<K, V> { ... }
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


Once you are finished, you can test the required methods with `cargo test map`. To test the optional methods as well, run `cargo test`.

## Benchmarking your Implementation

Run the interactive benchmarks with `cargo run --release`. Experiment with different loading factors: can you improve the performance of `MyHashMap`? What about the other hashmaps implementations?