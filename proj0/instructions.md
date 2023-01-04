---
parent: "Project 0: 2048"
title: Instructions
nav_order: 1
---

## Starting the Project

 - Open the `lab08/` folder in your preferred text editor.
 - Open the `lab08/` folder in your preferred terminal.
 - Run `git pull skeleton main` to get the latest version of the skeleton code for this lab.

## Running the Starter Code

To allow you to focus on the game logic, the UI for this game has already been written. Let's run it!

 - Open two terminals (or split your terminal, if it has that feature)
 - In one terminal, run `wasm-pack build --target web` to compile your code.
 - In the other terminal, run `python3 -m http.server` to start the server.
 - Go to [http://0.0.0.0:8000/](http://0.0.0.0:8000/) (or whichever address the server says to go to) in your browser to view the project.

You should see a beautiful-looking game of 2048. However, if you press an arrow key (or WASD), the game will just freeze, and not do anything. What happened?

Open up your browser's Javascript console (you can get to it by right-clicking, clicking "inspect", and clicking the "console" tab at the top of the opened window). You should see an error message that says
```
panicked at 'not implemented', src/game.rs:152:5
```
If you go to `game.rs` and look at line 152, you should see the problem. The game logic hasn't been written yet!

## Game Over

The first part of the game you'll be implementing is the `game_over` function in `game.rs`. This function should return `true` if the game is over, which happens when there are no possible moves left on the board.

There are two ways a move might exist:
 - If there is an empty space on the board (that tile is zero)
 - If there are two adjacent tiles with the same value.

Here are three examples:
```
   (A)            (B)            (C)
2  0  2  0     2  4  2  4     2  4  2  4 
4  4  2  2     8  2  4  2     8  2  4  2
0  4  0  0     2  4  2  4     2  4  2  8
2  4  4  8     4  2  4  2     4  2  4  8
```
Example A has empty spaces, so `game_over` should return `false`. Example B has no empty spaces, and no adjacent tiles with the same value, so `game_over` should return `true`. Example C has no empty spaces, but it has two adjacent 8s, so `game_over` should return `false`.

Once you've implemented `game_over`, you can run the tests for it by running `cargo test game`.

## Tilt

The final piece needed to make the game work is the `tilt` function in `game.rs`. This function calculates what should happen if the board is tilted in a certain direction. For example, if we start with the following board:
```
4  0  0  0
0  0  2  0
0  0  2  0
0  0  0  0
```
and tilted North (up), we would get the following result:
```
4  0  4  0      2 tile: (2, 1) -> (2, 0)
0  0  0  0      2 tile: (2, 2) -> (2, 0)
0  0  0  0      4 tile: (0, 0) -> (0, 0)
0  0  0  0      add 4 to score
```
Note that the `tilt` method returns not just the resulting board, but also the movements of all the tiles. This is so the UI can create sliding animations on every move.

Make sure to read the [background](background.md) before you start writing code; it contains some tips that may help you avoid some major pitfalls.

Once you've implemented `tilt`, you can run the full test suite with `cargo test`.

## Fruits of Your Labor

Once you've implemented `game_over` and `tilt`, the game should be playable. Repeat the steps in [Running the Starter Code](#running-the-starter-code), and enjoy the game!