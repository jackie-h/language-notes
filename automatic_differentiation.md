# Automatic Differentiation

A set of techniques to evaluate the derivative of a function specified by a computer program. AD exploits the fact that every computer program, no matter how complicated, executes a sequence of elementary arithmetic operations (addition, subtraction, multiplication, division, etc.) and elementary functions (exp, log, sin, cos, etc.). By applying the chain rule repeatedly to these operations, derivatives of arbitrary order can be computed automatically, accurately to working precision, and using at most a small constant factor more arithmetic operations than the original program.

Automatic differentiation is distinct from symbolic differentiation and numerical differentiation. Symbolic differentiation faces the difficulty of converting a computer program into a single mathematical expression and can lead to inefficient code. Numerical differentiation (the method of finite differences) can introduce round-off errors in the discretization process and cancellation. Both of these classical methods have problems with calculating higher derivatives, where complexity and errors increase. Finally, both of these classical methods are slow at computing partial derivatives of a function with respect to many inputs, as is needed for gradient-based optimization algorithms. Automatic differentiation solves all of these problems.

* Nice explanation of autodiff and Julia - https://marksaroufim.medium.com/automatic-differentiation-step-by-step-24240f97a6e6
* Explains auto diff with Julia examples - https://github.com/MikeInnes/diff-zoo

# Programming Language Implementations

* Engineering Trade-Offs in Automatic Differentiation: from TensorFlow and PyTorch to Jax and Julia - December 2021 - https://www.stochasticlifestyle.com/engineering-trade-offs-in-automatic-differentiation-from-tensorflow-and-pytorch-to-jax-and-julia/
* Enzyme LLVM - https://proceedings.neurips.cc/paper/2020/file/9332c513ef44b682e9347822c2e457ac-Paper.pdf - https://enzyme.mit.edu/ - https://github.com/wsmoses/Enzyme

# Papers

* A Review of Automatic Differentiation and its Efficient Implementation - 2019 - https://arxiv.org/pdf/1811.05031.pdf 

# Use in Finance

* Automatic Differentiation for the Greeks - DR. SIMON BYRNE AND DR. ANDREW GREENWELL ON FAST AND ACCURATE PRICE SENSITIVITIES USING JULIA https://wilmott.com/automatic-for-the-greeks/
