Interactive Stories and Games
=============================


Understanding State
-------------------

The word state refers to a specific setting of variables. In practice, there are
several different ways you could accomplish this.
It is important to think about it in the following way:
in the flow chart, you are defining how information flows from state to state, but in the code, you should
be trying to design code that works similarly for every state.

The simplest state, for example, is to have just a single number which represents
which state you are in. Then, when you need to have code that is conditional on the state, you could do:

.. code-block:: python
    :linenos:

    state = 1 # for example

    if state == 0:
        print("In state 0")
    if state == 1:
        print("In state 1")
    if state == 2:
        print("In state 2")


The Main Loop
--------------

When doing things like stories and games, you need to have a loop which manages the repeated behaviors.
In other words, you make code that handles all states, and you use a while loop
which keeps looping over the code.

Here is an example.  I used :code:`state` as an integer to keep track of
what point the user is in the story.

.. code-block:: python

    game_over = False
    state = 0

    while not game_over:

        if state == -1:
            game_over = True
        elif state == 0:
            print("Welcome to the dungeon..")
            print("You are in a dark room. Do you go left or right?")
            choice = input("> ")
            if choice == "left":
                state = 1
            elif choice == "right":
                state = -1
                print("You ran into a monster and died!")
            else:
                print("I don't understand that command!")
        elif state == 1:
            print("more code here and for other states!")



While the above code is good and you could write the entire game like that,
you have two choices for how to make it more compact, easier to write,
and easier to use. 

The first is to use functions. For this method, you would have a test
to see which state you are in and then call different functions based on that
state. 

The second is to use classes. For this method, you have objects can accomplish
the actions of the different states, but they have a shared function. 
That way, from the perspective of the main loop, the same function is being called every time. 

Using Functions
---------------

The game loop above could get really messy and long.  One way to manage
the top-level view without having too crazy of code is to break parts up into states.
For example, you could put the above first-state code into a function

.. code-block:: python
    :linenos:

    def state_0():
        print("Welcome to the dungeon..")
        print("You are in a dark room. Do you go left or right?")
        choice = input("> ")
        if choice == "left":
            state = 1
        elif choice == "right":
            state = -1
            print("You ran into a monster and died!")
        else:
            print("I don't understand that command!")

        return state

    ### the main game loop
    state = 0
    game_over = False
    while not game_over:
        if state == -1:
            game_over = True
        elif state == 0:
            state = state_0()
        elif state == 1:
            print("more stuff")


Notice how cleaner this code is!
Try to write state functions so that your code stays clean.
It is good practice to break code into chunks like this.

Notice that the function returns the :code:`state` integer.
The reason you'd want to return this is because then you're
letting each state decide whether the game ended.  You could do it another way,
if you wanted. For example, you could have player information like health.
And then, you pass that information into the function and pass it back out.
You could then check to see if player health was 0 and that would end the game.


More complex states
^^^^^^^^^^^^^^^^^^

You could also be writing more complex states.  For example, you could
be using a dictionary or a list with information in it.

.. code-block:: python

    euclid = {'location': 'kitchen', 'health': 10, 'name': 'Euclid'}


You could create classes for things like this:

.. code-block:: python

    class Bunny:
        def __init__(self, name, location, health):
            self.name = name
            self.location = location
            self.health = heatlh
            
    euclid = Bunny("Euclid", "kitchen", 10000)


An example
^^^^^^^^^^

.. code-block:: python
    :linenos:
    
    class Human:
        def __init__(self, name, health, location):
            self.name = name
            self.health = health
            self.location = location
            self.thing_type = 'human'
    
    
    class Animal:
        def __init__(self, name, health, location, animal_type):
            self.name = name
            self.location = location
            self.health = health
            self.thing_type = "animal"
            self.animal_type = animal_type
    
    def get_response(options):
        while True:
            print("Options: ")
            for option in options:
                print("\t{}".format(option))
            user_choice = input("What do you do? ") 
    
            if user_choice not in options:
                print("'{}' is not a valid option, try again".format(user_choice))
            else:
                return user_choice
    
    def kitchen(player, world):
        print("You are in the kitchen.. it is very spooky and very scary")
    
        animals_in_kitchen = list(world.animals['kitchen'].items())
        
        if len(animals_in_kitchen) == 0:
            print("Nothing in the kitchen.. how boring.")
            print("I wish you could go to other rooms now...")
    
        for animal_name, animal in animals_in_kitchen:
            print("Suddenly, a {} comes out of no where!".format(animal.animal_type))
    
            options = ['pet', 'run away', 'hide']
    
            choice = get_response(options)
    
            if choice == 'pet':
                print("You tried to pet him, but he bit your finger!")
                player.health = 0
            elif choice == "run away":
                print("You successfully ran away into the garage")
                player.location = "garage"
            elif choice == "hide":
                print("You hide under the table!")
                world.move_animal(animal, from_location="kitchen", to_location="hidden") 
    
    
    def garage(player, world):
        print("You are in the garage.. and you're locked in. whoops!")
        print("You are stuck here forever")
        player.health = 0
        
    class World:
        def __init__(self):
            self.locations = {"hidden": None}
            self.animals = {"hidden": {}}
            self.player = None
    
        def put_in_world(self, new_thing, thing_type):
            location = new_thing.location
            if location not in self.locations.keys():
                raise Exception("Location '{}' hasn't been added yet!!".format(location))
            if thing_type == 'animal':
                ## note: you can't have the same names, it will overwrite!
                self.animals[location][new_thing.name] = new_thing
            elif thing_type == 'player':
                self.player = new_thing
            else:
                raise Exception("Not supported yet: {}".format(thing_type))
    
        def add_location(self, location, location_function):
            self.locations[location] = location_function
            self.animals[location] = dict()
    
        def move_animal(self, animal, from_location, to_location):
            del self.animals[from_location][animal.name]
            self.animals[to_location][animal.name] = animal
            
    euclid = Animal(name="Euclid", health=10, location="kitchen", animal_type='bunny')
    player = Human(name="Mr. McMahan", health=100, location="kitchen")
    
    ### this is putting the function inside the dictionary!
    world = World()
    
    world.add_location('kitchen', kitchen)
    world.add_location('garage', garage)
    world.put_in_world(player, 'player')
    world.put_in_world(euclid, 'animal')
    
    
    game_active = True
    
    max_num_turns = 100
    
    while game_active:
        location = player.location
        location_function = world.locations[location]
    
        location_function(player, world)
    
        if player.health == 0:
            print("Player has passed out! The game was too much. game over")
            game_active = False
        else:
            options = ['leave', 'keep going']
    
            choice = get_response(options)
            
            if choice == 'leave':
                print("Goodbye!")
                game_active = False
            
            