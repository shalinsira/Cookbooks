Built-in Functions
==================


Built-in Functions
------------------

.. code-block:: python
    :linenos:

    print("This prints to the console/terminal!")

    # notice the space at the end!
    # it helps so that what you type isn't right next to the ?
    name = input("What is your name? ")

    # use input to get an integer
    age = input("How old are you?")
    # but it's still a string!
    # convert it
    age = int(age)

    # test the length of a list or string
    name_length = len(name)

    # get the absolute value of a number
    positive_number = abs(5 - 100)

    # get the max and min of two or more numbers
    num1 = 10**3
    num2 = 2**5
    num3 = 100003
    biggest_one = max(num1, num2, num3)
    smallest_one = min(num1, num2, num3)
    # can do any number of variables here
    #   max(num1, num2) works
    #   and max(num1, num2, num3,  num4)

    ## max/min with a list
    ages = [12, 15, 13, 10]
    min_age = min(age)
    max_age = max(age)

    # sum over the items in a list
    # more list stuff is below
    ages = [12, 15, 13, 10]
    sum_of_ages = sum(ages)
    number_of_ages = len(ages)
    average_age = sum_of_ages / number_of_ages

