Interactive Stories
===================

Flow charts and structure
-------------------------

You should decide on the structure and topic of your story pretty early.
Are you going to be writing fiction or non-fiction?
What is the context and background?

For an interactive story, there should be some actions that the reader can take.
For example, maybe they are entering into a house and need to choose rooms.
Or, they could be walking through a forest.

Once you have these details at least partially determined, you should start making
a flow chart for your ideas.  It's ok if the flow chart changes over time.

A flow chart starts with the initial point---the beginning of the story.
The information of the story will flow from this initial point.
You can use either paper to draw this or you can use an online website
(for example, `draw.io is an ok one <https://www.draw.io/>`_).

Any specific point in the story is sometimes called the "state".
The state is a specific setting of variables.  And since this is a story
you are programming, the set of variables are the variables you will be using
to keep track of the story.

Remember that you are drawing hte information flow.
There are several kinds of shapes in the flow charts:

Ovals are start/end points
^^^^^^^^^^^^^^^^^^^^^^^^^^

Ovals are either the starting or ending points.  They are where the story starts and stops.

Rectangles/Boxes are processing points
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Boxes represent the processing of information. Into the box flows some information and
out flows other information.  You draw this as a line flowing into a box and a line flowing out.
You could think about representing different rooms or states with boxes.

Diamonds are decision points
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you have a choice the user can make, you draw that as a diamond. Since the information
flow is being drawn as lines, a line connect to the diamond.  It is good to draw an arrow on the line to show
which direction it is flowing.

Each choice is a different path from the diamond.
I usually try to keep my diamonds as True/False and have a path come off one side of the diamond
and off the point opposite from where the information flow entered the diamond.

Other shapes
^^^^^^^^^^^^

There are a lot of shapes people use and slightly different ways to use them.
You have complete freedom to represent other types of information flow with other shapes.
Just make sure you use them the same way everywhere.  I personally only work with these three shapes.

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

In a flow chart, you could do:

.. raw:: html

    <iframe frameborder="0" style="width:100%;height:363px" src="https://www.draw.io/?chrome=0&lightbox=1&edit=https%3A%2F%2Fwww.draw.io%2F%23G0B_EznX5XVKAiSXQ4bzRsR3dBb28&nav=1#G0B_EznX5XVKAiSXQ4bzRsR3dBb28"></iframe>


The Story Loop
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



Breaking up your code
---------------------

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
-------------------

You could also be writing more complex states.  For example, you could
be using a dictionary or a list with information in it.

.. code-block:: python

    state = {'location': 'kitchen', 'health': 10, 'name': 'Euclid'}


Optional: Using functional programming
--------------------------------------

Remember, functions are values too.  You can use this to your advantage.

.. code-block:: python

    def get_name(state_dictionary):
        name = input("What is your name? ")
        state_dictionary['name'] = name

    def say_hello(state_dictionary):
        print("Hello {}".format(state_dictionary))

    def state_0(state_dictionary):
        print("in state 0!")

    def state_1(state_dictionary):
        print("in state 1!")

    def go_to_next(state_dictionary):
        if state_dictionary['position'] == 'first':
            state_dictionary['position'] = 'second'

    all_states = {'first': get_name, 'second': state_0, 'third': say_hello, 'fourth': state_1}

    state = {'position': 'first', 'name': 'unknown'}

    game_over = False
    while not game_over:
        # retrieve the state_function using the key to the state function
        state_name = state['position']
        state_function = all_states[state_name]

        # this updates state in place, since it's a dictionary
        # so, you can just pass it in and modify it
        state_function(state)

        go_to_next(state)


Optional: Use classes to handle state
-------------------------------------

The basic idea is to create a generic class which will handle the current information.
It is also useful to have it handle the transition information: which state should it go to next.
You can do this in several different ways. One way is shown below. 

.. code-block:: python
    :linenos:
    
    class State:
        def __init__(self, room):
            ## create all initial forms of the variables here
            self.room = room
            self.next_room = None
            
        def set_next_room(self, next_room)
            self.next_room = next_room

    kitchen = State("kitchen")
    hallway = State("hallway")
    kitchen.set_next_room(kitchen)

    
    current_place = kitchen
    
    game_over = False
    while not game_over:
        print("You are in the {}".format(current_place.room))
        some_input = input("What do you say? ")    
        
        
        ## do something that changes stuff and maybe go to the next room
        if current_place.next_room is not None:
            current_place = current_place.next_room
        
        
        


