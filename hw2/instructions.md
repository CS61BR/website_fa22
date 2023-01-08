---
parent: "Project 1.5: Percolation"
title: Instructions
nav_order: 1
mathjax: true
---

## Starting the Project

 - Open the `percolation/` folder in your preferred text editor.
 - Open the `percolation/` folder in your preferred terminal.
 - Run `git pull skeleton main` to get the latest version of the skeleton code for this lab.

## Running the Starter Code

To allow you to focus on the core logic, the UI for this project has already been written. Let's run it!

 - Open two terminals (or split your terminal, if it has that feature)
 - In one terminal, run `wasm-pack build --target web` to compile your code.
 - In the other terminal, run `python3 -m http.server` to start the server.
 - Go to [http://0.0.0.0:8000/](http://0.0.0.0:8000/) (or whichever address the server says to go to) in your browser to view the project.

The UI probably won't look like much: it should just say "loading...". Over the course of the project, the UI will get progressively more interesting.

## Percolation

Your first task is to implement the `Percolation` data type, which models a percolation system. The methods are as follows:

 - `new` constructs a new percolation system, with all the sites initially blocked. 
 - `width` returns the width.
 - `height` returns the height.
 - `open` opens the specified site, doing nothing if the site is already open.
 - `is_open` returns whether the specified site has been opened.
 - `is_full` returns whether the specified site is filled with water (in other words, if it has an open path to the top).
 - `number_of_open_sites` returns how many sites have been opened.
 - `percolates` returns whether the system has an open path from top to bottom.

The `new` method must run in $$O(NM)$$ time, where $$N$$ is the width and $$M$$ is the height. Every other method must run in $$O(\log(MN))$$ time.

Once you've implemented all the methods, you should be able to use the interactive model in the UI. Make sure your model doesn't suffer from backwash (see [background](background.md#backwash)).

## Stats

The second part of this project is to implement a Monte Carlo simulation to estimate the [percolation threshold](background.md#indiana-jones-and-the-percolation-threshold). Consider the following computational experiment:
 - Initialize an N by M grid of blocked sites
 - repeat until the system percolates:
     - choose a random open site
     - open the site
 - count how many open sites there are. If we call this count C, then $$C / NM$$ is an estimate of the percolation threshold.

 
If we repeat this experiment $$T$$ times and average the results, we can obtain a more accurate estimate of the percolation threshold.

Complete the `calculate_stats` method in `percolationstats.rs` such that it returns a `PercolationStats` struct with the following information:
 - a `counts` vector, where `counts[i]` represents how many of the trials percolated after opening exactly `i` sites. For example, if you run 4 trials, that percolate after 6, 7, 7, and 9 trials respectively, the counts array would be `[0 0 0 0 0 0 1 2 0 1 0 0...]`.
 - the mean estimate of the percolation threshold. If we let $$x_i$$ be the ratio of open sites for trial $$i$$, the formula for the mean $$\mu$$ is

$$
\mu = \frac{x_1 + x_2 + \ldots + x_T}{T}
$$

 - the standard deviation of the $$x_i$$ set. The formula for the standard deviation $$\sigma^2$$ is
 
$$
\sigma^2 = \frac{(x_1 - \mu)^2 + (x_2 - \mu)^2 + \ldots + (x_T - \mu)^2}{T - 1}
$$

 - the 95% confidence interval, which can be calculated with

$$
c_L = \mu - \frac{1.96\sigma}{\sqrt{T}}, c_H = \mu + \frac{1.96\sigma}{\sqrt{T}}
$$

Once you've implemented this function, the "statistics" button in the UI should work. You should see a beautiful S-curve on the graph, and a mean close to 0.59.
