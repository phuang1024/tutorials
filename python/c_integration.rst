C Integration
=============

Calling a C function from Python.

Shared Library
--------------

First, we need to create a *Shared Library* from our C code. This is a
binary file that can be loaded and called by Python.

A shared library can be produced by GCC (file name is ``utils.c``):

.. code-block:: bash

    gcc -Wall -O3 -c -fPIC utils.c
    gcc -shared utils.o -o libutils.so

Void Functions
--------------

C (``utils.c``):

.. code-block:: c

    #include <stdio.h>

    void print_hello(void) {
        printf("Hello world!");
    }

Python (``main.py``)

.. code-block:: python

    import ctypes

    lib = ctypes.CDLL("libutils.so")
    lib.print_hello()

This prints ``"Hello world!"`` to the terminal.

Numerical Arguments
-------------------

C:

.. code-block:: c

    int add_ints(int a, int b) {
        return a + b;
    }

    float add_floats(float a, float b) {
        return a + b;
    }

Python:

.. code-block:: python

    import ctypes

    INT = ctypes.c_int
    FLOAT = ctypes.c_float

    lib = ctypes.CDLL("libutils.so")

    lib.add_ints.argtypes = (INT, INT)
    lib.add_ints.restype = INT

    lib.add_floats.argtypes = (FLOAT, FLOAT)
    lib.add_floats.restype = FLOAT

    print(lib.add_ints(3, 19))
    print(lib.add_floats(1.5, 6.2))

If we pass arguments and use the return value, we need to declare the argument and
return value type.

For each function, set the ``argtypes`` attribute to a tuple of argument types, and
the ``restype`` attribute to the return types.

In this example, the variables ``INT`` and ``FLOAT`` were defined for convenience.

Running ``main.py`` prints:

.. code-block:: text

    22
    7.699999809265137

as expected. The float error is due to limited precision.

C++
---

Calling C++ is very similar. All we need to do is declare our functions as C:

.. code-block:: cpp

    #include <iostream>

    extern "C" void print_hello(void) {
        std::cout << "Hello world!" << std::endl;
    }

and use ``g++`` when compiling.
