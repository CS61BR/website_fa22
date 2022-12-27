---
parent: "Lab 01: Setup"
title: Instructions
nav_order: 2
---

After you've done the [setup](setup.md), you're ready to begin the lab!

## Task: Implement Collatz

In the lab folder, you should see the file `src/collatz.rs`. This program is supposed to print the [Collatz sequence](https://en.wikipedia.org/wiki/Collatz_conjecture) starting from a given number. The Collatz sequence is defined as follows:

 - If *n* is even, the next number is *n/2*. 
 - If *n* is odd, the next number is *3n + 1*.
 - If *n* is 1, the sequence ends.

For example, the Collatz sequence starting from 5 is 5, 16, 8, 4, 2, 1. 

Your task is to complete the implementation of the `next_number` function such that it returns the next number in the Collatz sequence. Once you have filled in the `next_number` function, you can run the program with the command: `cargo run --bin collatz`. If all goes well, you should see the Collatz sequence starting from 5 printed to the terminal.

## Optional Task: Implement Leap Year

In the lab folder, you should see the file `src/leap_year.rs`. Your task is to implement the `leap_year` function such that it returns `true` if and only if the given year is a leap year.

Leap years are defined as follows:
 - A year is a leap year if it is divisible by 400.
 - A year is also a leap year if it is divisible by 4 but not by 100.

For example, 2000 and 2004 are leap years. 1900, 2003, and 2100 are not leap years.

Once you have implemented the `leap_year` function, you can run the program with the command: `cargo run --bin leap_year`. 

