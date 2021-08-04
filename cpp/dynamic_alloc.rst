Dynamic Allocation
==================

Dynamic allocation allows you to allocate memory on the heap, rather than
the stack. There are two benefits to doing this:

1. The heap is usually bigger than the stack, meaning you can allocate more
   memory without overflowing.

2. On the stack, you can only allocate pre-defined sizes. On the heap, you can
   allocate sizes that are defined at runtime (e.g. the user inputs a size).

Keep in mind that allocating on the heap will be a little bit slower than on
the stack. This is usually not noticeable, though.

Allocation
----------

To dynamically allocate, use the ``new`` keyword. This takes a type and, optionally,
a size. It returns a pointer to the newly allocated memory.

.. code-block:: cpp

    # Static size
    int *array = new int [10];

    # Dynamic size
    int size = some_input_function();
    int *array2 = new int [size];

    # Object on the heap
    int *car = new Car;

Deallocation
------------

Unlike on the stack, the dynamically allocated memory will be there until you
explicitly un-allocate it, called deallocation. Whenever you are using dynamic
allocation, **make sure to deallocate after you are done using it**. Failing to
do so will cause *memory leak*.

Use the ``delete`` and ``delete[]`` keywords to deallocate objects and arrays.

.. code-block:: cpp

    # continued from above
    delete[] array;
    delete[] array2;
    delete car;
