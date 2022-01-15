

## Speed

https://news.ycombinator.com/item?id=17161168  
https://github.com/dyu/ffi-overhead

# C FFI

NodeJS  - N-API

Python

R

Java - project panama

Rust

# LIBFFI - Calling compiled code from interpreted languages at runtime

* https://sourceware.org/libffi/ and https://github.com/libffi/libffi
* Provides a portable, high level programming interface to various calling conventions. This allows a programmer to call any function specified by a call interface description at run-time. Provides only part of the picture, developers must write the type conversion to go with it.
* Widely used in OpenJDK, Ruby, CPython and more


# Language Bindings to C/C++

* SWIG - http://www.swig.org/. Now deprecated by it's creator - https://code.activestate.com/lists/python-dev/109281

* CLIF - generate Python language bindings to C/C++ - from Google (their alternative to SWIG). Uses LLVM https://github.com/google/clif 
* cppyy: Automatic Python-C++ bindings - create bindings at runtime to CPP using Cling the CPP interpreter https://cppyy.readthedocs.io/en/latest/


# Python Bindings 

* HPy (alpha) - a better set of bindings for Python. https://hpyproject.org/ and https://github.com/hpyproject/hpy and https://hpyproject.org/talks/2021/05/hpy-present-and-future.pdf
  * What are the advantages of HPy?
    * Zero overhead on CPython: extensions written in HPy runs at the same speed as "normal" extensions.
    * Much faster on alternative implementations such as PyPy, GraalPython.
    * Debug Mode: in debug mode, you can easily identify common problems such as memory leaks, invalid lifetime of objects, invalid usage of APIs. Have you ever forgot a Py_INCREF or Py_DECREF? The HPy debug mode will detect these mistakes for you.
    * Universal binaries: extensions built for the HPy Universal ABI can be loaded unmodified on CPython, PyPy, GraalPython, etc.
    * Nicer API: the standard Python/C API shows its age. HPy is designed to overcome some of its limitations, be more consistent, produce better quality extensions and to make it harder to introduce bugs.

