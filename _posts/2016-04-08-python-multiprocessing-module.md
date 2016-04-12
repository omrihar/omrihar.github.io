---
title: Using Python's multiprocessing module to perform parameter sweeps
link: http://kmdouglass.github.io/posts/learning-pythons-multiprocessing-module.html
share: false
comments: true
---

I recently wanted to perform a parameter sweep on a simple simulation in python
and found [this post][post] about how to use python's `multiprocessing` module
very useful.

In short you define a function that you want to run with multiple parameters,
let's call it `run_simulation`. It should accept one argument which could be a
tuple or an object or whatever you need to run your simulation. You then create
an iterable that contains these parameters, call it `params`. We then simply
create a pool and apply a map function to run the simulations on multiple
cores.

~~~ python
import multiprocessing

def run_simulation(param):
  # my simulation code

pool = multiprocessing.Pool()
results = pool.map(run_simulation, params)
~~~

The `results` variable will contain a list of results, ordered in the same way
as the provided `params` iterable. There might be some pitfalls when using on
linux with `numpy`, see [the abovementioned blogpost][post] for a much better
explanation and discussion of pitfalls.

[post]: http://kmdouglass.github.io/posts/learning-pythons-multiprocessing-module.html
{:target="_blank"}
