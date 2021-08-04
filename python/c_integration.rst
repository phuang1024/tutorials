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
