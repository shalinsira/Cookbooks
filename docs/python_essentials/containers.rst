Containers
==========

Lists
-----

Create an empty list
^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    new_list = list()
    # or
    new_list = []

Create a list with items
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    my_pets = ['euclid', 'leta']

Add onto a list
^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    my_pets.append('socrates')

Index into a list
^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    first_pet = my_pets[0]
    second_pet = my_pets[1]
    third_pet = my_pets[2]

Slice a list into a new list
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    # the syntax is
    #   my_list[start:stop]
    # this includes the start position but goes UP TO the stop
    # you can leave either empty to go to the front or end

    first_two_pets = my_pets[:2]
    last_two_pets = my_pets[1:]

Test if a value is inside a list
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    ## with any collection, you can test if an item is inside the collection
    ## it is with the "in" keyword

    my_pets = ['euclid', 'leta']
    if 'euclid' in my_pets:
        print("Euclid is a pet!")

Sets
----

Create a set or convert a list to a set
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    my_pet_list = ['euclid', 'leta']

    # you can convert lists to sets using the set keyword
    my_pet_set = set(my_pet_list)

    # sets are like lists but you can't index into them or slice them
    # they are used for fast membership testing

    # you can create a new set by:
    my_pet_set = set(['euclid', 'leta'])


Add an item to a set
^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    my_new_set = set()

    # instead of append, like a list, you use 'add'
    my_new_set.add("Potatoes")


Using sets to enforce uniqueness
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    my_grocery_list = ['potatoes', 'cucumbers', 'potatoes']

    # now if you want to make sure items only appear once, you can convert it to a set
    # it will automatically do this for you, because items are only allowed to be in sets one time

    my_grocery_set = set(my_grocery_list)
