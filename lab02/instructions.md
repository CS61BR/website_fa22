---
parent: "Lab 02: Debugging"
title: Instructions
nav_order: 1
---

## Starting the Lab

 - Open the `lab02/` folder in your preferred text editor.
 - Open the `lab02/` folder in your preferred terminal.
 - Run `git pull skeleton main` to get the latest version of the skeleton code for this lab.

## Debug Exercise 1

I've created an amazing program to do my math homework for me; unfortunately, it has a bug in it! It's supposed to round each calculation to the nearest whole number, but sometimes it gives incorrect results.

Run `cargo run --bin debug_exercise_1`. You should notice an incorrect result; let's figure out why.

 - First, run `cargo build`. This will build binaries/executables for every program in the current project. This step happens automatically whenever you run `cargo run`, but we're doing it again for good measure.
 - `cargo build` puts the executables in the `target/` folder. Open `target/debug/`. You should see a `debug_exercise_1` file; that's the executable we want to debug!
 - Run `rust-gdb target/debug/debug_exercise_1`. This will open a GDB prompt. GDB is a powerful tool for debugging low-level programs: [this cheatsheet](https://darkdust.net/files/GDB%20Cheat%20Sheet.pdf) lists several helpful commands you can use. If anything goes wrong in the next few steps, you can run `quit` in the GDB prompt to exit GDB, and re-run this command to start from here. 
 - In the GDB prompt, run `layout src`. This will let you see the source code for `debug_exercise_1` as you debug, which will be very useful in the following steps. If things don't look right, run `refresh`, which often fixes graphical issues in GDB.
 - We should now set a breakpoint, which is a place where we want to pause the program. Run `break rounded_division`, which will set a breakpoint at the beginning of the `rounded_division` method. Alternatively, you can run `break 24` or `b 24`, which sets a breakpoint on line 24.
 - Now that we've set a breakpoint, we can start the program. Run `run` in the GDB prompt.
 - The program should stop at the first line of `rounded_division`. Let's print some variables: Run `print top` and `print bot`. These will tell you the valies of the `top` and `bot` variables. Now try to run `print quotient`: this should give an error, because line 24 has not run yet.
 - Run `next` (or `n`) to advance to the next line. Then press enter again: GDB interprets a blank line as "run the last command again", so it should advance again, to line 26.
 - Print the values of the `quotient` and `result` variables.
 - Run `continue` (or `c`) to resume the program; it should stop on line 24 again, the second time `rounded_division` is called.
 - Using the `next` and `continue` commands, go to the point in execution where you think the bug is. Use the `print` command to confirm your suspicions.
 - Once you are done debugging, run `quit` to exit the GDB prompt (It may ask if you are sure; press `y` to confirm).

Now you know how to use `rust-gdb`! Optionally, you can fix the bug in `rounded_division`, and re-run the program to see the (now correct) answers to my math homework.

## Debug Exercise 2

I've created another amazing program, this time to take the sum of elementwise maxes of two arrays. However, this one also has a bug in it.

Run `cargo run --bin debug_exercise_2`. It will print out `Ok(-17)`, even though the answer should be 15, not -17. 

Using `rust-gdb`, locate the bug and fix it! Here are some GDB commands you might find useful:
 - `break [line number]` to set a breakpoint
 - `run` to start the program
 - `next` to advance to the next line (skipping over function calls)
 - `step` to advance to the next line (stepping into function calls)
 - `continue` to resume execution to the next breakpoint
 - `print [variable name]` to print variables
 - `finish` to jump to the end of the current function

Once you have fixed the bug, re-run the program and verify that it prints `Ok(15)`.

## Arithmetic

I've learned my lesson from the first two programs; now I always write tests to verify that my code is correct. Unfortunately, my code is not always correct.

Run `cargo test arithmetic`, which will run the tests in `arithmetic.rs`. Note that `test_sum` is failing; something might be wrong with the `sum` function. Let's figure out why.
 - At the top of the test output, there should be a line like
   ```
   Running unittests src/lib.rs (target/debug/deps/lab02-0e9653381300a9a7)
   ```
   In parenthesis is the file name of the test binary; this the executable running under the hood when we run `cargo test`. Copy that file name.
 - Run `rust-gdb [filename]`, using the file name you copied above (i.e. `rust-gdb target/debug/deps/lab02-0e9653381300a9a7`). This should open a familiar-looking GDB prompt.
 - In the GDB prompt, run `layout src`, and `refresh` if necessary.
 - Run `break test_sum` to set a breakpoint, then run `run` to start execution.
 - Debug the test!
 - When you've located the bug, run `quit` to exit GDB.

Fix the bug, and re-run `cargo test arithmetic` to verify that the tests pass.

## IntList

Now that we know how to debug tests, it's time to incorperate everyone's favorite data structure: the linked list. I've been magically handed a bug-free `IntList` implementation (see [Background](background.md)), but unfortuately, the code I've written using `IntList`s is not quite so bug-free.

Run `cargo test int_list`, which will run all the tests in `tests.rs`. Your task is to fix the following methods in `int_list_exercises.rs`:
 - `add_constant`
 - `set_to_zero_if_max_fel`
 - `square_primes`

Note that `set_to_zero_if_max_fel` uses several helper methods; the bug(s) may be in the helper methods. If a bug is in a helper method, you should fix the helper method.

Note that `square_primes` doesn't fail any tests. Does this mean that it's bug free? No, it means that there aren't enough tests. Write a test that `square_primes` fails, then find and fix the bug in `square_primes`.




