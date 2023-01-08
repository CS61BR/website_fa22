---
title: "Project 1.5: Percolation"
has_children: true
nav_order: 12
---


# Project 1.5: Percolation

## Project Demo

See the demo [here](https://sberkun.github.io/percolation/)!

## Differences from the Java version

 - `PercolationStats` includes the raw counts, for the purpose of making a histogram.
 - No statistics library is provided for `PercolationStats`; you have to do the math yourself.
 - Dependency injection is done via a trait (as opposed to a factory)
 - Percolation is generalized to non-square grids
 