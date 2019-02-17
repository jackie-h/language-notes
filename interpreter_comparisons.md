# Dynamic Language Interpreter Research

Understanding optimizations and approaches in existing dynamic languages

## Javascript

### V8:
A Tale of Turbofan - explains Inlining nicely
https://docs.google.com/presentation/d/1UXR1H2elTdAYJJ0Eed7lUctCVUserav9sAYSidxp8YE

https://ponyfoo.com/articles/an-introduction-to-speculative-optimization-in-v8
https://medium.com/dailyjs/understanding-v8s-bytecode-317d46c94775

Interesting - that typescript does not 

## Python

https://medium.com/@dawran6/getting-started-with-python-internals-a5474ccb8022

Inside the python virtual machine
https://leanpub.com/insidethepythonvirtualmachine/read

https://hackernoon.com/why-is-python-so-slow-e5074b6fe55b

Efforts to make python faster
https://faster-cpython.readthedocs.io/index.html

How fast can we make interpreted Python? - looks at register based and stack based
https://arxiv.org/pdf/1306.6047v2.pdf


## Self

## Lua
Register-based rather than stack-based

## Techniques

### Inlining or Inline Expansion
https://en.wikipedia.org/wiki/Inline_expansion
Increases memory but reduces function call overhead
Enables further whole program optimizations

### Loop unrolling
http://www2.cs.uh.edu/~jhuang/JCH/JC/loop.pdf

https://en.wikipedia.org/wiki/Loop_unrolling

## General Research Papers

Stack-based vs Register-based
https://arxiv.org/pdf/1611.00467.pdf

New Research
Typed incremental computation with names - 
https://arxiv.org/pdf/1808.07826.pdf
