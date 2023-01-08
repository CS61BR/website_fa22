---
parent: "Project 1.5: Percolation"
title: Background
nav_order: 0
mathjax: true 
---



## Indiana Jones and the Percolation Threshold

Go find some copper wire.

Seriously, this is important. If you need to, take apart a USB cable and extract the copper. Don't have any spare cables? Melt some pennies in the microwave and *make* some copper wire.[^1] Do whatever it takes. 

Got some wire? Great!

Look at your wire very closely. If you have the eyesight of a scanning electron microscope, you might be able to see the atomic impurities in your copper wire; most wire is only around 99.95% copper. Despite this, your wire is still conductive: there exists a path of pure copper atoms from one end of the wire to the other. 

Your wire would probably still be conductive even if it was only 95% copper; as long as the material is homogenous, there would still be an extremely high probability of a conductive path. In fact, you could probably decrease the purity to 90%, or even 80%, and the wire would probably still be conductive. However, somewhere between 80% and 50%, the material will go from "extremely likely to be conductive" to "extremely likely to be an insulator". Where is that threshold?

This behavior is not unique to the conductivity of copper. In fact, there's an entire field, [percolation theory](https://en.wikipedia.org/wiki/Percolation_theory), dedicated to this subject. There is no known way to calculate the [percolation threshold](https://en.wikipedia.org/wiki/Percolation_threshold) for most models, but a lot of people have tried really hard (as evidenced by all the fancy math stuff on the wikipedia page).

In this project, we're going to investigate a model of water in a porous material. We'll model the material as a square lattice (a.k.a. a grid), and assume that water comes from the top. We'll say the system *percolates* if there's a path for water to reach the bottom of the model.

In the following examples, black sites (grid spaces) are *closed*, white sites are *open* but *empty*, and blue sites are *open* and *full*. 

<div style="display: flex;">

<div style="margin-right: 1em;">
<div>
Does not percolate:
</div>
<svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg" style="background: white; height: 10em;">
  <defs></defs>
  <rect x="10" y="10" width="480" height="480" style="stroke: rgb(0, 0, 0);"></rect>
  <rect x="15" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="395" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="110" width="90" height="90" style="fill: white;"></rect>
  <rect x="110" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="110" width="90" height="90" style="fill: white;"></rect>
  <rect x="300" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="205" width="90" height="90" style="fill: white;"></rect>
  <rect x="110" y="205" width="90" height="90" style="fill: white;"></rect>
  <rect x="205" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="395" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="300" width="90" height="90" style="fill: white;"></rect>
  <rect x="205" y="300" width="90" height="90" style="fill: white;"></rect>
  <rect x="300" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="395" width="90" height="90" style="fill: white;"></rect>
  <rect x="300" y="395" width="90" height="90" style="fill: white;"></rect>
  <rect x="395" y="395" width="90" height="90" style="fill: black;"></rect>
</svg>
</div>

<div style="margin-right: 1em;">
<div>
Does not percolate:
</div>
<svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg" style="background: white; height: 10em;">
  <defs></defs>
  <rect x="10" y="10" width="480" height="480" style="stroke: rgb(0, 0, 0);"></rect>
  <rect x="15" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="110" width="90" height="90" style="fill: white;"></rect>
  <rect x="15" y="205" width="90" height="90" style="fill: white;"></rect>
  <rect x="110" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="300" width="90" height="90" style="fill: white;"></rect>
  <rect x="300" y="300" width="90" height="90" style="fill: white;"></rect>
  <rect x="395" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="395" width="90" height="90" style="fill: white;"></rect>
  <rect x="110" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="395" width="90" height="90" style="fill: white;"></rect>
</svg>
</div>


<div style="margin-right: 1em;">
<div>
Percolates:
</div>
<svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg" style="background: white; height: 10em;">
  <defs></defs>
  <rect x="10" y="10" width="480" height="480" style="stroke: rgb(0, 0, 0);"></rect>
  <rect x="15" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="395" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="300" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="300" width="90" height="90" style="fill: white;"></rect>
  <rect x="110" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="300" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="395" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="395" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="395" y="395" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
</svg>
</div>

<div style="margin-right: 1em;">
<div>
Percolates:
</div>
<svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg" style="background: white; height: 10em;">
  <defs></defs>
  <rect x="10" y="10" width="480" height="480" style="stroke: rgb(0, 0, 0);"></rect>
  <rect x="15" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="300" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="395" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="300" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="300" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="15" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="395" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
</svg>
</div>

</div>





## Backwash

Observe the following percolation system:

<div style="display: flex;">

<div style="margin-right: 1em;">
<div>
Correct:
</div>
<svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg" style="background: white; height: 10em;">
  <defs></defs>
  <rect x="10" y="10" width="480" height="480" style="stroke: rgb(0, 0, 0);"></rect>
  <rect x="15" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="395" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="395" width="90" height="90" style="fill: white;"></rect>
  <rect x="395" y="395" width="90" height="90" style="fill: white;"></rect>
</svg>
</div>

<div style="margin-right: 1em;">
<div>
Incorrect:
</div>
<svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg" style="background: white; height: 10em;">
  <defs></defs>
  <rect x="10" y="10" width="480" height="480" style="stroke: rgb(0, 0, 0);"></rect>
  <rect x="15" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="15" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="15" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="110" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="110" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="110" y="205" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="205" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="300" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="205" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="395" y="300" width="90" height="90" style="fill: black;"></rect>
  <rect x="15" y="395" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="110" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="205" y="395" width="90" height="90" style="fill: black;"></rect>
  <rect x="300" y="395" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
  <rect x="395" y="395" width="90" height="90" style="fill: rgb(103, 198, 243);"></rect>
</svg>
</div>

</div>

Note that even through the system percolates (has a path from top to bottom), there is no path from the top to the bottom right squares. Therefore, those two squares should not be filled.

Many implementations have a problem with "backwash" - water flowing "up" from the bottom of the world into those two squares. Solving this problem is challenging, but rewarding.



## WQU

The Weighted Quick Union (WQU for short) is an efficient implementation of the [union-find data structure](https://en.wikipedia.org/wiki/Disjoint-set_data_structure). It starts with N disjoint elements, and as elements are connected, it can efficiently tell you which elements are connected to each other.

For your convience, here are the runtimes of the methods for a WQU with N initial elements:
 - `new`: $$O(N)$$
 - `count`: $$O(1)$$
 - `find`: $$O(\log(N))$$
 - `connected`: $$O(\log(N))$$
 - `union`: $$O(\log(N))$$

A WQU implementation is provided in `wqu.rs`. You should use it.

## Extra: Why is calculate_stats Generic?

For testing purposes. Imagine a world where `calculate_stats` looks like this:
```rust
pub fn calculate_stats(...) {
    for t in 0..trials {
        let p = Percolation::new(width, height);
        ... // do stuff until p percolates
    }
    ... // math stuff
}
```

 Since `calculate_stats` depends on a `Percolation` implementation, if tests for `calculate_stats` fail, we have no clue whether its because `calculate_stats` is broken or if `Percolation` is broken.

Making `calculate_stats` generic alleviates this problem. For testing purposes, we don't have to run `calculate_stats` on an actual `Percolation` implementation; we can run it on types that *pretend* to be `Percolation` implementations. For example, we might have:
```rust
pub struct PercolatesHalfway {
    width: usize,
    height: usize,
    open_sites: usize
}

impl Percolatable for PercolatesHalfway {
    fn percolates(&self) -> bool {
        self.open_sites * 2 >= self.width * self.height
    }
    ... // rest of the methods
}
```
Now, we can test `calculate_stats::<PercolatesHalfway>()`. We know that it should have a mean of exactly 50% and a standard deviation of 0, which is a good sanity check for `calculate_stats`.

This idea of "make a thing generic so it can be tested easier" is part of a bag of tricks collectively known as [dependency injection](https://en.wikipedia.org/wiki/Dependency_injection). When used well, dependency injection can be a great tool for isolating components and writing unit tests. When not used well, it makes interns cry. 


[^1]: Most pennies aren't made of copper, and most microwaves aren't powerful enough for copper smelting, but hey, it doesn't hurt to try.