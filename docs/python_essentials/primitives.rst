Primitive Variables
===================


Numbers
-------

Integers
^^^^^^^^

.. code-block:: python
    :linenos:

    # create an integer
    x = 5

    # convert an integer string
    x = str('5')

    # convert a float to an integer
    ## note: don't depend on this for rounding, it rounds in weird ways
    x = int(5.5)

    # convert a string of any number base
    # for example, binary
    x = int('1010101', base=2)

Floats
^^^^^^

.. code-block:: python
    :linenos:

    # create a float
    x = 5.5

    # convert a float string
    x = float("5.5")

    # convert an integer to a float
    x = float(5)

Basic math operations
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    x = 100

    # 1. Add
    x = x + 5
    x += 5

    # 2. Subtract
    x = x - 5
    x -= 5

    # 3. Multiply
    x = x * 5
    x *= 5

    # 4. Divide
    x = x / 5
    x /= 5

    # 5. Power
    x = x ** 2
    x **= 2


Advanced math operations
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    # 1. Integer Division
    x = x // 5
    x //= 5

    # 2. Modulo
    x = 84
    x = x % 5
    x %= 5

Use the math library
^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    import math

    x = 10

    # pow is power, same as x ** 2
    x = math.pow(x, 2)

    # ceil rounds up and floor rounds down
    x = 5.5
    y = math.ceil(x) # y is 6.0
    z = math.floor(x) # z in 5.0

    # some other useful ones:
    math.sqrt(x)
    math.cos(x)
    math.sin(x)
    math.tan(x)

    # this will give you pi:
    math.pi

Strings
-------

Add two strings together
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    first_name = "euclid "
    space = " "
    last_name = "von rabbitstein"
    full_name = first_name + space + last_name

Repeat a string
^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    message = "Repeat me!"
    repeated10 = message * 10

    # I like to use it for pretty printing code results
    line = "-" * 12
    print("   Title!   ")
    print(line)

Index into a string
^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    first_name = "Euclid"
    last_name = "Von Rabbitstein"
    first_initial = first_name[0]
    last_initial = last_name[0]
    initials = first_initial + last_initial

Slice a string
^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    # the syntax is
    #   my_string[start:stop]
    # this includes the start position but goes UP TO the stop
    # you can leave either empty to go to the front or end

    target = "door"
    last_three = target[1:]
    first_three = target[:3]
    middle_two = target[1:3]

    # you can use negatives to slice off the end!
    all_but_last = target[:-1]

    pig_latin = target[1:] + target[0] + "ay"


String's inner functions
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    full_name = "euclid von Rabbitstein"

    # all caps
    full_name_uppered = full_name.upper()

    # all lower
    full_name_lowered = full_name.lower()

    # use lower to make sure something is lower before you compare it
    user_command = "Exit"
    if user_command.lower() == "exit":
        print("now I can exit!")

    # first letter capitalized
    full_name_capitalized = full_name.capitalize()

    # split into a list
    full_name_list = full_name.split(" ")

    # strip off any extra spaces
    test_string = "   extra spaces everywhere   "
    stripped_string = test_string.strip()

    # replace things in a string
    full_name_replaced = full_name.replace("von", "rabbiticus")

    # use replace to delete things from a string!
    test_string = "annoying \t tabs in \t the string"
    fixed_string = test_string.replace("\t","")

