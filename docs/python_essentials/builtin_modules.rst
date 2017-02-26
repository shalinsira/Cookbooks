Built-in Modules
================


Time module
-----------

Using time.time() to count how long something takes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    import time

    start = time.time()

    for i in range(10000):
        continue

    new_time = time.time()
    total_time = new_time - start
    print(total_time)


Using time.sleep(n) to wait for n seconds
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    import time

    start = time.time()

    time.sleep(10)

    end = time.time()

    print(start - end)


Random Module
-------------

Generate a random number between 0 and 1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    import random

    num = random.random()
    print("the random number is {}".format(num))

Generate a random number between two integers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    import random

    num = random.randint(5, 100)
    print("the random integer between 5 and 100 is {}".format(num))

Select a random item from a list
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    import random

    my_pets = ['euclid', 'leta']
    fav_pet = random.choice(my_pets)
    print("My randomly chosen favorite pet is {}".format(fav_pet))

