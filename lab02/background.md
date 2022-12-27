---
parent: "Lab 02: Debugging"
title: Background
nav_order: 0
---

## Linked Lists

For various technical reasons, linked lists are more challenging to implement in Rust than in most other languages. Before diving into the `IntList` implementation in this lab, you might want to review [enums](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html) and [boxing](https://doc.rust-lang.org/book/ch15-01-box.html).

The `IntList` implementation in this lab closely resembles "A Bad Singly-Linked Stack" from [Learning Rust With Entirely Too Many Linked Lists](https://rust-unofficial.github.io/too-many-lists/). I _highly_ suggest reading through that chapter; it is a great introduction to several Rust concepts.


## Looping with `while let`

One unusual structure you will see in this lab is the `while let` loop. For example, here's the `size_iterative` implementation from `int_list.rs`:

```rust
pub fn size_iterative(mut s: &Self) -> usize {
    let mut total = 0;
    while let IntList::More(_, next) = s {
        total += 1;
        s = next;
    }
    total
}
```
The `while let` is shorthand for a `loop` with a `match` statement. Here's an equivalent implementation of the above code:
```rust
pub fn size_iterative(mut s: &Self) -> usize {
    let mut total = 0;
    loop { // like "while true" in other languages
        match s {
            IntList::More(_, next) => {
                total += 1;
                s = next;
            },
            _ => break
        }
    }
    total // implicit return
}
```

