Decorators
==========

In Python, decorators are a convenient way to create a wrapper.

You have probably seen the ``classmethod`` or ``staticmethod`` decorator
before:

.. code-block:: python

    @staticmethod
    def hi():
        print("Hi")

    @classmethod
    def make_hi(cls):
        return cls("hi")

First, let's understand functions a bit more.

Functions as Objects
--------------------

In Python, functions are objects, meaning they can be assigned to another
variable, passed as arguments, and returned:

.. code-block:: python

    def func():
        pass

    def do_nothing(func):
        return func

    func_copy = func
    func_copy2 = do_nothing(func)

Your First Decorator
--------------------

The ``@decorator`` syntax is a shorter and cleaner way to apply a decorator.
It is actually doing:

.. code-block:: python

    # This
    @decorator
    def func():
        pass

    # is equivalent to
    def func():
        pass
    func = decorator(func)

Our decorator will take in one argument: the user-defined function.
In that decorator, we will define a second function that usually calls the input
function, but modifies the arguments and return values before doing so.
Then, our decorator will return the second function.

Let's say that we need a decorator that adds 1 to all arguments (assuming they are numerical).

.. code-block::

    def my_decorator(func):
        # "func" is the user defined function.

        def new_func(*args):
            # We use *args to take in any amount of arguments,
            # because we will eventually pass them to "func",
            # and we are unsure of how many arguments "func" takes.

            new_args = [a+1 for a in args]
            return func(*new_args)

        return new_func

    @my_decorator
    def add_args(a, b, c):
        return a + b + c

Remember, the ``@decorator`` syntax assigns the function to ``decorator(function)``.
Because ``my_decorator`` returns the internal function ``new_func``, ``add_args``
is assigned to ``new_func``.

When we call ``add_args`` (which is ``new_func``), it will *first* add one to all the
arguments and then call the original ``add_args`` function. Because ``add_args`` takes
3 arguments, the sum will be increased by 3.
