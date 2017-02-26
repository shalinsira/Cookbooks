Loops
=====


For Loops
---------

Write a for loop
^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    for i in range(10):
        print("do stuff here")

Use the for loop's loop variable
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    for i in range(10):
        new_number = i * 100
        print("The loop variable is i.  It equals {}".format(i))
        print("I used it to make a new number. That number is {}".format(new_number))


Use range inside a for loop
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    start = 3
    stop = 10
    step = 2

    for i in range(stop):
        print(i)

    for i in range(start, stop):
        print(i)

    for i in range(start, stop, step):
        print(i)

Use a list inside a for loop
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    my_pets = ['euclid', 'leta']

    for pet in my_pets:
        print("One of my pets: {}".format(pet))

Nest one for loop inside another for loop
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    for i in range(4):
        for j in range(4):
            result = i * j
            print("{} times {} is {}".format(i, j, result))

While Loops
-----------

Use a comparison
^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    response = ""

    while response != "exit":
        print("Inside the loop!")
        response = input("Please provide input: ")


Use a boolean variable
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    done = False

    while not done:
        print("Inside the loop!")
        response = input("Please provide input: ")
        if response == "exit":
            done = True


Loop forever
^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    while True:
        print("Don't do this!  It is a bad idea.")

Special Loop Commands
---------------------

Skip the rest of the current cycle in the loop
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    for i in range(100):
        if i < 90:
            continue
        else:
            print("At number {}".format(i))


Break out of the loop entirely
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    while True:
        response = input("Give me input: ")
        if response == "exit":
            break
