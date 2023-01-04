---
title: "Project 0: 2048"
has_children: true
nav_order: 10
---


# Project 0: 2048

## Project Demo

Play the demo [here](https://sberkun.github.io/2048/)!

## Differences from the Java version

 - The game has been generalized to an N * M grid (rather than just 4 * 4)
 - The game does not end at 2048 (the "max tile"). Just like most other implementations, the game continues until moves can no longer be made, so 4096 and beyond are valid tiles.
 - You are encouraged, but not forced to, make helper methods for `game_over`.
 - Not as many tests are needed, since there is no longer a stateful "model" object to test. Also tests relating to the "max tile" have been removed.
 