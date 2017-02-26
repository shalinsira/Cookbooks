Functions
---------

The syntax for a function
^^^^^^^^^^^^^^^^^^^^^^^^^

The first line of a function, called the function header, requires the following:

1. the :code:`def` keyword,
2. the name
3. parenthesis
4. a colon

For example:

.. code-block:: python
    :linenos:

    def some_name():

- Notice that there is a space between the :code:`def` and the function name, :code:`some_name`.
- There is also NO space between :code:`some_name` and the parenthesis.
- In the most basic version, there is nothing inside the parenthesis.
- Immediately following the parenthesis (with NO space!), there is a colon.

You are free to name functions whatever you want.  Everything else must remain the same!

Go to the next section to see how we put code inside a function.


No arguments and returns nothing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When there is nothing inside the parenthesis in a function header, we
say that the function takes no arguments.    When it doesn't
send back a value, we say it returns nothing.

For example:

.. code-block:: python
    :linenos:

    def say_hello():
        print("hello!")

Now, if you want to call the function, go to the next part!

Calling a function you wrote
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When you write a function, you give it a name.  For example, in the section
just before this one, the function name is :code:`say_hello`.

If you have a python file where you have defined that function, you can then
call it.  Calling a function looks just like the following:

.. code-block:: python
    :linenos:

    ### this is the definition! It does not call the function
    def say_hello():
        ## this comment is inside the function, because of the indentation!
        print("hello!")
        ## this comment is also inside the function

    ### this comment is outside the function!  The indentation is gone

    ### the function has to be called outside of the function!!
    ### We use its name plus parenthesis
    say_hello()


Notice a couple of things:

1. The name of the function is :code:`say_hello`.
2. At the end of the code above, on line 11, we use the function.
    - This is also known as **executing** or **calling** a function.
3. Python knew to call the function because of the parenthesis in line 11.
    - It is part of an agreement with Python and programmers that programmers will use
    parenthesis in this way, immediately after a function name, to tell it that it wants to call a function.


Takes one argument
^^^^^^^^^^^^^^^^^^

Now, let's look at how a function can have a single argument.
This is why there are parenthesis in the function header.
This lets specify what arguments a function will have.

.. code-block:: python
    :linenos:

    def say_something(the_thing):
        print("2. I will say something now!")
        print(the_thing)
        print("4. I just said something!")

    print("1. I am going to call the say_something function!")
    say_something("3. This is cool!")
    print("5. I just called the function!")

In this example, there are a lot of print statements!
Run the code and see the order in which they print out.
I have numbered the print statement so you can see the order.

**The important thing to know: **

- Once Python "enters" into the function to start running the code, it is
in a local context
- This means that the variable named :code:`the_thing` exists only inside the function
- It is a temporary variable Python makes to hold the value you pass in when you
call the function.


Returns a value
^^^^^^^^^^^^^^^

Now let's look at how you can **return** items from a function!


.. code-block:: python
    :linenos:

    def double(x):
        return 2*x


Takes two arguments
^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    def exp_func(x, y):
        result = x ** y
        return result

    final_number = exp_func(10, 3)

Takes keyword arguments
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    def say_many_times(message, n=10):
        print("Inside the say_many_times function!")
        for i in range(n):
            print(message)


    say_many_times("Hi!", 2)
    say_many_times("Yay!")
