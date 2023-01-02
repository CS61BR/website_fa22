---
title: "Lab 08: HashMap"
has_children: true
nav_order: 7
---


# Lab 08: HashMap

## Lab Goals

 - To implement a hashmap from scratch
 - To learn about and compare different hashmap implementations


## Differences from the Java version

The Java version has an emphasis on polymorphism, and testing different bucket types. However, the bucket choice ends up being inconsequential, because they're all being used in the same way; the exotic bucket types just end up being worse `ArrayList`s. This makes the extra complexity feel a bit pointless.

In this version of the lab, there are three unique hashmap implementations to compare (two external chaining and one open addressing). Each implementation has different performance characteristics, so the design choices actually matter.

Other minor differences:
 - The methods to implement are a bit different.
 - The "speed tests" have all been combined into `benchmark.rs`

