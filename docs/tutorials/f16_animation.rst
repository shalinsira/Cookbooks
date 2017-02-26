Animation
=========

The tools we are going to use for animation are going to be PyGame and Python.
There is information on how to install pygame linked here.

PyGame
------

PyGame provides you with a couple core things:

1. A way to interact with a canvas
2. A set of ways to draw shapes and images to the canvas
3. A procedure for repeating the code and updating the screen to make things animated

There are a couple initial things for pygame.

I have outlined the basic code here:

.. code-block:: python
    :linenos:

    import pygame

    ##### INIT SECTION
    # Define some colors
    BLACK = (0, 0, 0)
    WHITE = (255, 255, 255)
    GREEN = (0, 255, 0)
    RED = (255, 0, 0)

    size = (700, 500)
    done = False

    pygame.init()

    screen = pygame.display.set_mode(size)
    clock = pygame.time.Clock()

    pygame.display.set_caption("My Animation")

This is the header code for pygame.  It does the following things:

1. Imports the pygame library
2. Defines some basic colors.  These are in the RGB format in tuples.
3. Define the size of the screen as a tuple.
4. Create a boolean variable to represent whether the animation is done yet.
5. :code:`pygame.init()` starts the pygame engine.
6. After the engine is started, you can set the screen size and get the clock.
    - the clock is useful for setting and changing the frames per second.
7. You can also optionall set the title of the screen

With this part, you are not quite done.  You now need to have the game loop!

Game Loop
---------

.. code-block:: python
    :linenos:

    # -------- Main Program Loop -----------
    while not done:
        #### EVENT CHECK SECTION
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                done = True

        #### CLEAR THE SCREEN
        screen.fill(WHITE)

        #### DRAWING SECTION

        # empty

        #### TELL THE SCREEN TO UPDATE
        pygame.display.flip()

        #### TELL THE CLOCK YOU WANT 60 FRAMES PER SECOND
        clock.tick(60)


    # Close the window and quit.
    pygame.quit()


You should combine this code with the code from the last second.
When run together, it should open a blank white screen.
Let me know if it doesn't, because then there is something wrong.

Drawing Objects
---------------

Pygame has several different objects it can draw.
There is a specific format to them.
There are complete docs `at the pygame docs <https://www.pygame.org/docs/ref/draw.html>`_, but I will
describe a couple things here.

The screen object created in the initial section is very important.
It is used to reference the screen for drawing!
Inside the drawing section in the while loop, add the following:

.. code-block:: python
    :linenos:

    pygame.draw.rect(screen, BLACK, (0, 0, 100, 100))


This code does the following:

1. It uses the :code:`pygame.draw.rect` function draw a rectangle
2. It uses the :code:`screen` object to draw to the screen
3. It uses the :code:`BLACK` color to pick the rectangle's color
4. It uses a 4-length tuple :code:`(0,0,100,100)` to define the shape of the rectangle.
    - The format of this tuple is: :code:`(left_x, top_y, width, height)`

The pygame website describes this code as: :code:`rect(Surface, color, Rect, width=0) -> Rect`.
This means that the :code:`rect(...)` function takes as input the :code:`Surface`, which we call :code:`screen`,
a color, a capital-R :code:`Rect`, and optionally the width.  The arrow means it returns back a
capital-R :code:`Rect`.

The capital-R :code:`Rect` is a specific PyGame variable type.  I will show
how to use that in the next section.  But, you can also just use tuples in this case.
We also aren't saving the :code:`Rect` that it produces.


Explore the code on the pygame docs.  Explore the different shapes.
To list them here:

.. code-block:: python

    rect(Surface, color, Rect, width=0) -> Rect
    polygon(Surface, color, pointlist, width=0) -> Rect
    circle(Surface, color, pos, radius, width=0) -> Rect
    ellipse(Surface, color, Rect, width=0) -> Rect
    arc(Surface, color, Rect, start_angle, stop_angle, width=1) -> Rect
    line(Surface, color, start_pos, end_pos, width=1) -> Rect
    lines(Surface, color, closed, pointlist, width=1) -> Rect


We are not importing the functions completely, so we are calling them as
:code:`pygame.draw.*` where the * is polygon, circle, rect, etc.

Keeping track of state
----------------------

The structure of the pygame code is:

::

    create variables and initialize them

    start loop
        draw and update things inside the loop
        the loop ends when the animation ends

    close the window


In order to keep track of the state of things, you have to create variables
to represent the state in the first part.

An easy way to play with this is to create :code:`x` and :code:`y` variables and
set them to some number like 0

.. code-block:: python

    x = 0
    y = 0

then use them to draw the object inside the loop.

.. code-block:: python

    ## inside the loop
    pygame.draw.rect(surface, BLACK, (x, y, 100, 100))


Finally, you can then change the x and y inside the loop!

.. code-block:: python

    x += 1
    y += 1

Now, the object will move!


The core elements of the game loop
----------------------------------

The game loop follows this pattern:

1. Handle Events
2. Update states
3. Draw everything


Where you should go from here
-----------------------------

Your goal now is to make an animation.  You can continue to use variables like above
and use functions to modify those variables. You can also use classes, 
which are described elsewhere and in the cookbooks linked below. 

You should work on doing the following: 

1. Putting the game loop inside a function or inside a class
2. Put the event handling, state updating, and drawing inside functions or classes.

You should also answer the following questions:

1. What is the overall goal of your animation?
2. What are the pieces of your animation?
3. How do those pieces change over time?
4. What variables do you need to represent those changes?
5. What python syntax is really useful for all of these things?

In addition to the main cookbooks, there are a couple additional cookbooks which you can use:

- :doc:`Simple PyGame cookbook <simple_pygame_cookbook>`
    - covers pygame examples without using classes
- :doc:`PyGame with Classes cookbook <pygame_classes_cookbook>` 
    - covers pygame using classes 
    - has a lot of functionality explained!




