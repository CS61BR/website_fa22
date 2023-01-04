---
parent: "Project 0: 2048"
title: Background
nav_order: 0
---



## Gameplay

If you're not familar with the game, you can play the [original version here](https://play2048.co/). On each move, the player will tilt the board towards one of the 4 sides, and tiles will slide towards that side.

Tiles may merge if they are adjacent and have the same value, creating one tile with double the value. This seems simple enough, but there are some corner cases to consider:
 - A tile that is the result of a merge will not merge again on that tilt. For example, if the row `[0 2 2 4]` is slid to the left, the result will be `[4 4 0 0]`, not `[8 0 0 0]`. 
 - When there are three or more adjacent tiles, the leading tiles in the direction of motion merge first. For example, if the row `[2 2 2 0]` is slid left, the result will be `[4 2 0 0]`. If the row `[2 2 2 2]` is slid left, the result will be `[4 4 0 0]`.

Every time a merge happens, the total value of the tiles should be added to the score. For example, if two 2s merge into a 4, the score should be incremented by 4.

Here are some examples that illustrate these rules. All examples slide to the left:
```
before: [0 2 0 2] after: [4 0 0 0] (score: +4)
before: [0 2 4 2] after: [2 4 2 0] (score: +0)
before: [4 2 0 2] after: [4 4 0 0] (score: +4)
before: [0 2 0 2 2 2 4 4] after: [4 4 8 0 0 0 0 0] (score: +16)
before: [8 4 4 4 4 0 0 8] after: [8 8 8 8 0 0 0 0] (score: +16)
```




## Tilt: Board Rotations


When writing `tilt`, you might be tempted to write something like:
```rust
match dir {
    Direction::North => {
        ... // calculate tilt to the north
    },
    Direction::East => {
        ... // calculate tilt to the east
    },
    Direction::South => {
        ... // calculate tilt to the south
    },
    Direction::West => {
        ... // calculate tilt to the west
    },
}
```
Don't do this! You would be writing very similar code for each direction, which makes it four times harder. Instead, use the `rotate` methods to your advantage. The logic should roughly go:
 - rotate the board such that the given direction faces up. For example, if `dir` is East, this should rotate it 90 degrees counter-clockwise.
 - calculate the tilt (given that the tiles "fall" upwards)
 - rotate the `MovingTile`s to the perspective of the original board (for example, if `dir` is East, this should rotate the movements 90 degress clockwise)
 - rotate the board back to North facing up (for example, if `dir` is East, this should rotate it 90 degrees clockwise).
