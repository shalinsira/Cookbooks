Classes Cookbook
================

Design patterns and examples for classes!  Use these to help you solve problems.


Defining a class
----------------

.. code-block:: python
    :linenos:

    class Dog:
        def __init__(self, name, age):
            self.name = name
            self.age = age


Instantiating an object
-----------------------

.. code-block:: python
    :linenos:

    # create the object!
    fido = Dog("Fido", 7)


Writing a method
----------------

A method is the name of a function when it is part of a class.

You always have to include :code:`self` as a part of the method arguments.

.. code-block:: python
    :linenos:

    class Dog:
        def __init__(self, name, age):
            self.name = name
            self.age = age

        def bark(self):
            print("Bow wow!")


    fido = Dog("Fido", 7)
    fido.bark()

Using the self variable
-----------------------

You can access object variables through the :code:`self` variable.
Think of it like a storage system!

.. code-block:: python
    :linenos:

    class Dog:
        def __init__(self, name, age):
            self.name = name
            self.age = age

        def bark(self):
            print("{}: Bow Wow!".format(self.name))


    fido = Dog("Fido", 7)
    fido.bark()

    odie = Dog("Odie", 20)
    odie.bark()

Using the property decorator
----------------------------

You can have complex properties that compute like methods but act like properties.
Properties cannot accept arguments.

.. code-block:: python
    :linenos:

    class Dog:
        def __init__(self, name, age):
            self.name = name
            self.age = age

        def bark(self):
            print("{}: Bow Wow!".format(self.name))

        @property
        def human_age(self):
            return self.age * 7

    fido = Dog("Fido", 7)
    fido.bark()
    print("Fido is {} in human years".format(fido.human_age))

Inheriting properties and methods
---------------------------------

You can inherit properties and methods from the ancestors!
For example, the initial function below is inherited.

.. code-block:: python
    :linenos:

    class Animal:
        def __init__(self, name, age):
            self.name = name
            self.age = age

    class Dog(Animal):
        def bark(self):
            print("{}: Bow Wow!".format(self.name))

        @property
        def human_age(self):
            return self.age * 7

    class Cat(Animal):
        def meow(self):
            print("{}: Meow!".format(self.name))

    fido = Dog("Fido", 7)
    fido.bark()
    print("Fido is {} in human years".format(fido.human_age))

You can also override certain things and call the methods of the ancestor!


.. code-block:: python
    :linenos:

    class Animal:
        def __init__(self, name, age, number_legs, animal_type):
            self.name = name
            self.age = age
            self.number_legs = number_legs
            self.animal_type = animal_type

        def make_noise(self):
            print("Rumble rumble")

    class Dog(Animal):
        def __init__(self, name, age):
            super(Dog, self).__init__(name, age, 4, "dog")

        def make_noise(self):
            self.bark()

        def bark(self):
            print("{}: Bow Wow!".format(self.name))

        @property
        def human_age(self):
            return self.age * 7

    class Cat(Animal):
        def __init__(self, name, age):
            super(Dog, self).__init__(name, age, 4, "cat")

        def make_noise(self):
            self.meow()

        def meow(self):
            print("{}: Meow!".format(self.name))


    fido = Dog("Fido", 7)
    fido.make_noise()
    print("Fido is {} in human years".format(fido.human_age))

    garfield = Cat("Garfield", 5, 4, "cat")
    garfield.make_noise()



Using the classmethod decorator
-------------------------------

There is a nice Python syntax which lets you define custom creations for your objects.

For example, if you wanted certain types of dogs, you could do this:

.. code-block:: python
    :linenos:

    class Animal:
        def __init__(self, name, age, number_legs, animal_type):
            self.name = name
            self.age = age
            self.number_legs = number_legs
            self.animal_type = animal_type

        def make_noise(self):
            print("Rumble rumble")

    class Dog(Animal):
        def __init__(self, name, age, breed):
            super(Dog, self).__init__(name, age, 4, "dog")
            self.breed = breed
            
    
    fido = Dog("Fido", 5, "Labrador")
            

But you could also do this:

.. code-block:: python
    :linenos:

    class Animal:
        def __init__(self, name, age, number_legs, animal_type):
            self.name = name
            self.age = age
            self.number_legs = number_legs
            self.animal_type = animal_type

        def make_noise(self):
            print("Rumble rumble")

    class Dog(Animal):
        def __init__(self, name, age, breed):
            super(Dog, self).__init__(name, age, 4, "dog")
            self.breed = breed

        @classmethod
        def labrador(cls, name, age):
            return cls(name, age, "Labrador")
            
    fido = Dog.labrador("Fido", 5)
    
    
Important parts:

1. Instead :code:`self`,  it has :code:`cls` as its first argument.
    - This is a variable which points to the class being called. 
2. :code:`@classmethod` is right above the definition of the class.
    - It absolutely has to be exactly like this
    - No spaces in between, just sitting on top of the class definition
    - It's called a decorator.
3. It returns :code:`cls(name, age, "Labrador")`.  
    - This is exactly the same as :code:`Dog("Fido", 5, "Labrador")` in this instance
    - Overall, it is letting you shortcut having to put in the labrador string. 


This is a simple example, but it is useful for more complex classes