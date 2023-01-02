---
parent: "Lab 03: Testing and Timing"
title: Instructions
nav_order: 1
---

## Starting the Lab

 - Open the `lab03/` folder in your preferred text editor.
 - Open the `lab03/` folder in your preferred terminal.
 - Run `git pull skeleton main` to get the latest version of the skeleton code for this lab.

## Benchmarking a sub-optimal AList

In `AList.rs`, I've implemented a resizible array (aka Vec but worse). However, because I don't know much about asymptotics, I've given it a very naive resize strategy. Every time the `AList` runs out of space, it allocates a new slice with space for 1 more element.

Let's figure out how well this naive implementation performs. If you run `cargo run --release AList`, you should see something like this:
```
Took 8.972465ms to run 10000 AList::add_last calls
thread 'main' panicked at 'not implemented', src/benchmarks.rs:50:5
```

That sounds pretty fast! Let's run `cargo run --release Vec` to see how Vec performs:
```
Took 16.05µs to run 10000 Vec::push calls
thread 'main' panicked at 'not implemented', src/benchmarks.rs:50:5
```
Oh...maybe `AList` isn't so fast after all...

Let's try changing the `AList` resize strategy. In `alist.rs`, try changing the resize strategy to `+10000` instead of `+1`. If you run the program again, it should get much faster:
```
Took 13.766µs to run 10000 AList::add_last calls
thread 'main' panicked at 'not implemented', src/benchmarks.rs:50:5
```
Wow! That's even faster than Vec! Unfortunately, we can't just claim victory here: if we change the benchmark to run 1,000,000 calls instead of 10,000, Vec seems to be faster again. Clearly, we can't get the whole picture with just one data point.

## Implementing the benchmark function

Right now, the `benchmark` function in `benchmarks.rs` just creates one data point: it calls the `add` method of the given data structure 10000 times. Implement the `benchmark` function with the following behavior:
 - test several different sizes (N = 1000, 2000, ..., 128000)
 - at each N, 
     - call `add` N times to create a data structure of size N
     - call `get` 10,000 times to see how fast `get` is
 - print a timing table for the `add` method
 - print a timing table for the `get` method

Once you've implemented `benchmark`, you can run benchmarks for `AList` and `Vec` at the same time by running `cargo run --release AList Vec`.

## Benchmarking a better AList

In `alist.rs`, change the resize strategy to be *multiplicative* rather than *additive*. Some multiplicative factors you can try:
 - 2
 - 1.5 (use casting; i.e. `(self.len as f64 * 1.5).ceil() as usize`)
 - 1.01
 - 3
 - 10
 - 100

When you run the benchmarks, you should notice `AList` performing significantly better with a multiplicative strategy than an additive strategy. Which multiplicative factor performs the best?

## Benchmarking a Linked List

Are linked lists good? Absolutely not, and we can prove it.

Run `cargo run --release SLList`. You should notice that although `SLList::add_first` isn't terrible, `SLList::get_last` gets slower and slower as N (the size of the list) gets larger. Why might this be?

## Comparison Testing

In an alternate universe, I made a terrible bug when implementing `AList`. I couldn't find the bug, even after hours of searching, so I created a simpler implementation of `AList` to cross-check against. Since the simpler implementation (probably) doesn't have the bug, we can try to find situations where the two implementations behave differently in order to isolate the bug.

The buggy `AList` implementation is in `buggyalist.rs`, and the simple implementation is in `alistnoresizing.rs`. You might notice that the simple implementation can't handle more than 1000 elements; this is fine, because its sole purpose in life is for comparison testing. As long as our tests never create lists with more than 1000 elements, `AListNR` is perfectly adequate for helping us find the bug in `BAList`.

Start by implementing the test `test_add_3_remove_3` in `mod.rs`. This should add 3 elements to both `AListNR` and `BAList`, then check that 3 `remove_last` calls have the same result on each list.

You can run both tests with `cargo test`, or run `cargo test test_add_3_remove_3` if you want to run just this test.

## Randomized Comparison Testing

Unfortunately, `test_add_3_remove_3` probably wasn't enough to catch the bug. It's time to bring out the big guns: randomized testing.

In `randomized_test`, create a test that randomly switches between `len`, `add_last`, `get_last`, and `remove_last`. For example, one random sequence of calls might be
 - len
 - add_last
 - len
 - len
 - add_last
 - remove_last
 - get_last
 - add_last

The test should assert that the two implementations have the same result after each call (except for `add_last` calls, which don't return anything). A few thousand randomized calls should be enough to expose the bug.

Once you've created a failing test, use it to find the bug in `buggyalist.rs`. Fix the bug, and re-run the tests to verify that the bug is fixed.
