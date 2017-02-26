Conditionals
============

If, elif, and else
------------------


Use an if to test for something
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    power_level = 1000
    min_power_level = 500
    max_power_level = 1000

    # one thing is larger than another
    if power_level > minimum_power_level:
        print("We have enough power!")

    if power_level == max_power_level:
        print("You have max power!")


Create conditional logic
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    selected_option = 2

    if selected_option == 1:
        print("Doing option 1")
    elif selected_option == 2:
        print("Doing option 2")
    elif selected_option == 3:
        print("doing option 3")
    else:
        print("Doing the default option!")

Nest one if inside another if
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    name = "euclid"
    animal = "bunny"

    if animal == "bunny":
        if name == "euclid":
            print("Euclid is my bunny")
        elif name == "leta":
            print("Leta is my bunny")
        else:
            print("this is not my bunny..")
    else:
        print("Not my animal!")
