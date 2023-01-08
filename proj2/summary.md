---
parent: "Project 2: NGordnet"
title: Summary and Deliverables
nav_order: 4
---

## Assignment Overview

In part A, you will be implementing the `TimeSeries` and `NGramMap` types, and part of `NGordNetHandler`. By the end of this part, your server should be able to respond to history queries.

In part B, you will be implementing the `WordNet` type, and completing `NGordNetHandler`. By the end of this part, your server should be able to respond to synonyms and hyponyms queries.

In part C, you will be adding a "hyponyms history" feature, and then refactoring the project to include an SQLite database.

## Running the Project

To test your code, run `cargo test --release`.

To run the project, run `cargo run --release`. You can then view the project at [http://127.0.0.1:8000](http://127.0.0.1:8000) (or whichever address the server says to go to).

## Submitting Your Code

Before submitting your code, make sure to:
 - Run `cargo clippy` and fix any warnings that appear.
 - Run `cargo fmt` to format your code according to the Rust style guidelines.
 - Commit and push your code to your repository.

Then, submit your code to the [Gradescope assignment](https://cheese.com/).


