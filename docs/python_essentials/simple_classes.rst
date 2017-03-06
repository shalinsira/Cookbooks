Class Basics
============

First class
^^^^^^^^^^^

Defining class is a recipe.  Take a look at the syntax:

.. code-block:: python
    :linenos:
    
    class Dog:
        name = 'default name'
        age = 0
        

The important part to notice is the :code:`class Dog:`.  This is what indicates the beginning of the code block.
After the class is defined, two variables are declared.  These variables are inside the class. Think of them like files in a folder. 


.. code-block:: python
    :linenos:

    class Dog:
        name = 'default name'
        age = 0

    fido = Dog()
    

This code **instantiates** the class.  This means you are using the recipe to create a new object. 

To repeat the vocabulary:

- **instantiate**: use the recipe to create an object
- **object**: a specific instance of a class. think of this like a cookie from a cookie recipe. 


Using the first class
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:

    class Dog:
        name = 'default name'
        age = 0

    fido = Dog()
    
    print("1. Fido's name: ", fido.name)
    fido.name = "Fido"
    
    print("2. Fido's name: ", fido.name)
    
    george = Dog()
    print("3. George's name: ", george.name)
    print("3. Fido's name: ", fido.name)
    
    george.name = "George"
    print("4. George's name: ", george.name)
    print("4. Fido's name: ", fido.name)
    
    
Run this example.

You will see that changing the internal properties of fido and george stay inside fido and george!
This is another example of scope. Just like inside functions are local scope, inside objects are local scope!

Getting access to internal variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python
    :linenos:
    
    class Dog:
        name = 'default name'
        age = 0
        
    def speak(some_dog):
        print("My name is {}. Bow wow!".format(some_dog.name))

    fido = Dog()
    speak(fido)
    
We can write functions which use the :code:`fido` object as its argument and 
access the internal variables!

Getting access to internal variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can see from the last example that you access the internal variables using the dot notation. 
But, what if you wanted to write a function *inside* the object?  How can you access the variables?

Let's try this:

.. code-block:: python
    :linenos:
    
    class Dog:
        name = 'default name'
        age = 0
        
        def speak():
            print("My name is {}. Bow wow!".format(name))

    fido = Dog()
    fido.speak()
    
Do you think this will work?  Nope!  Scope doesn't let us do that!

There is a second reason why the code above won't work and that reason is also what solves things!


.. code-block:: python
    :linenos:
    
    class Dog:
        name = 'default name'
        age = 0
        
        def speak(self):
            print("My name is {}. Bow wow!".format(self.name))

    fido = Dog()
    fido.speak()


When you use the function that is inside an object, python adds a variable without you having to do anything!
That variable is called the :code:`self` variable.   This is just like having the
function outside of the :code:`class`, except that Python puts the :code:`self` variable
there automatically, so we don't have to. 
    
    

:code:`def __init__(self)`
^^^^^^^^^^^^^^^^^^^^^^^^^^

The :code:`__init__` function is one of Python's special functions - 
this is indicated by the double underscore (__) on either side of the function name. 
:code:`init` is a keyword (like :code:`print` or :code:`if``) and Python already knows what it's used for.

When you write your own class, sometimes it's helpful to have a kind of setup
function that runs whenever you make a new copy of the class. For example, 
if you write the :code:`Door` class we've been using as an example, you might
want the :code:`Door` to print out "Hello!" the first time someone makes it. And,
every new :code:`Door` that gets made will also say "Hello!"

This is what the :code:`__init__` function is for: it's a special function that 
runs once every time an object of that type (in our example, :code:`Door`) is made.

So, for example:

.. code-block:: python
    :linenos:
    
    class Door:
        def __init__(self):
            print("Hello!")
      
    first_door = Door()
    second_door = Door()
  
The code above will print out "Hello!" twice - once for :code:`first_door`, and again for :code:`second_door`.

That's an example of an :code:`__init__` function that doesn't take any arguments. Usually, this isn't the case - because :code:`__init__` is a setup function, you want the user to provide certain information about the object when they make it. 

Here's an example:


.. code-block:: python
    :linenos:

    class Door:
        def __init__(self, in_name, in_height):
            self.name = in_name
            self.height = in_height
            print("Hello! My name is " + self.name)
    
    first_door = Door("Gerald", 10)
    second_door = Door("Geraldina", 12)

In this code, when a :code:`Door` object is created, 
it takes two arguments: the name, and the height. 
These arguments are then used for setting up the Door object 
(i.e., they set up the properties :code:`self.name` and :code:`self.height`)
