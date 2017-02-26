Boolean algebra
===============

Create a literal boolean variable
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    literal_boolean = True
    other_one = False

Create a boolean variable from comparisons
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    x = 9
    y = 3
    x_is_bigger = x > y # True
    x_is_even = x % 2 == 0 # False
    x_is_multiple_of_y = x % y == 0 # True

Combine two boolean variables with 'and' and 'or'
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    # example data
    card_suit = "Hearts"
    card_number = 7

    # save the results from comparisons!
    card_is_hearts = card_suit == "Hearts"
    card_is_diamond = card_suit == "Diamond"
    card_is_big = card_number > 8

    # only 1 of them needs to be true
    card_is_red = card_is_hearts or card_is_diamond

    # both need to be true
    card_is_good = card_is_red and card_is_big

    # creates the opposite!
    card_is_bad = not card_is_good
