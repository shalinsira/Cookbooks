Cookbook
========


A set of common recipes and design patterns for pygame with classes



Game Loop
---------

The main game logic can be divided into two parts: 

1. Initialize the variables
2. Run the game loop which does the following steps:
    1. Handle Events
    2. Update objects
    3. Draw 
    
    
.. code-block:: python
    :linenos:
    
    import pygame
    
    class Game:

        def initialize(self):    
        
            ## start pygame's engines
            pygame.init()
        
            ## get a screen 
            self.screen = pygame.display.set_mode(WINDOW_SIZE)
            
            ## get a clock used for FPS control
            self.clock = pygame.time.Clock()
            
            self.example_box = pygame.Rect(0, 0, 100, 100)
    
        def run(self):    
            ## a simple flag variable for the loop
            done = False
            
            ## the main game loop
            while not done:
                    
                ### 1. Events
                
                ## the event loop; used to check for events that occurred since the last time around
                for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        done = True
        
                ### 2. Updates
                ## update the example box with whatever you want
                self.example_box.x += 1
                
                
                ## 3.  Drawing
                pygame.draw.rect(self.screen, BLACK, self.example_box)
        
                #### update the display and move forward 1 frame
                pygame.display.flip()
                # --- Limit to 60 frames per second
                self.clock.tick(FPS)


Basic Sprites
-------------

There are several ways to include objects, monsters, obstacles, etc in your pygame code.
The best way is to define your own classes that inherit from pygame's Sprite class. 

You should think of this as defining recipes for different objects in your game. 
In this section, there are the following recipes:

1. A basic sprite
    - the core components of a sprite and how to use them
2. Adding the drawing function to the basic sprite
    - You can put the logic for the sprites inside the class, so it makes the game logic cleaner
    - Your game shouldn't have to worry about how sprites get drawn!
3. Colliding with one other sprite
    - Colliding with another sprite is handled just like in the simple case
    - The trick is to correctly identify how the collision happened so you can fix it!
4. Using Groups of sprites
    - Group is a special pygame object that gives us extra shortcuts!
5. Colliding with many sprites
    - Using a Group, we can easily get the list of sprites our main sprite is colliding with
6. Adding an image to your sprite
    - Usually you will want to draw more than basic shapes.  This will show you how!
7. Adding event handling to your sprite
    - If you want your sprite to do things, it should handle its own event logic!
    - This means that the game just gives the events to the sprite and the sprite does what it needs to do.
8. Making an animated sprite
    - This will show you how the basic animation happens


Basic Sprite
^^^^^^^^^^^^

For our basic sprite, we will **subclass** pygame's sprite class.  
Subclassing means that we will tell python that our new class is the exact same
as pygame's sprite class. Then, whatever we can specialize any parts we want. 

.. code-block:: python
    :linenos:
    
    class BasicSprite(pygame.sprite.Sprite):
    
        # by defining this function, we are overriding the parent class's function
        def __init__(self, color, width, height):
            
            # this is a special command which tells python to execute the parent's function
            # the pattern is 
            # super(ThisClassName, self).func_to_call()
            super(BasicSprite, self).__init__()
        
            ### When you sublcass the sprite, you need two things
            
            #  1. self.image
            
            self.image = pygame.Surface([width, height])
            self.image.fill(color)
            
            #  2. self.rect
            
            self.rect = self.image.get_rect()
            
            # self.rect starts out at 0,0. if you want to change the location, you have to update these coordinates
            # this hard codes the BasicSprite to start at the coordinates 50,50
            self.rect.x = 50
            self.rect.y = 50 



You can use this class in the same places you would before:

1. **Instantiate** (create) the object at the beginning of the game
2. **Update** the coordinates inside the game loop
3. **Draw** the coordinates inside the game loop


One of the nice features about using sprites is that we only have to draw the
sprite's :code:`self.image` property. We do this with the following: 

.. code-block:: python
    :linenos:
    
    class Game:
        
        def initialize(self):
            # other code was here
            
            # just remember that our screen is made here
            self.screen = pygame.display.set_mode(WINDOW_SIZE)
            
            self.example_object = BasicSprite(BLACK, 100, 100)
    
        def run(self):
            done = False
            
            ## the main game loop
            while not done:
                
                # other code was here
                
                
                ## the way to read this dot notation is:
                ## inside this Game object access (using "self") a variable called example_object 
                ## inside example_object is the property "image" (which we defined just above)
                ## inside image is a function called blit
                ## blit takes two arguments:
                ##      1. the surface it should draw on, this is our screen.
                ##      2. the coordinates of where to draw it. this is the rect inside example_object
                ## overall, the syntax is:
                ##      surface_variable.blit(screen_variable, rect_variable)
                
                self.example_object.image.blit(self.screen, self.example_object.rect)
            
                
                ## then don't forget the rest of the code here

So, to summarize:

1. Subclass pygame's :code:`Sprite` class and define the :code:`self.image` and :code:`self.rect`. 
2. Inside the :code:`Game` object's initialize function, use the class to make a new object
    - save this object to the :code:`self` variable so we can access it later
3. Inside the :code:`Game` object's run function, use the saved object to draw
    - the syntax for drawing a sprite is showing above. 
    - You are calling :code:`blit` to draw the sprite's surface onto the main surface.



Adding the drawing function to the basic sprite
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Doing that drawing logic inside the game loop is a bit messy.
Also, maybe we want to change how we draw the object based on some situation.
We don't want to have the main game loop get all messy with that code. 

To solve this problem, we put a :code:`draw` function inside the :code:`BasicSprite` class

.. code-block:: python
    :linenos:
    
    class BasicSprite(pygame.sprite.Sprite):
    
        # by defining this function, we are overriding the parent class's function
        def __init__(self, color=BLACK, width=100, height=100):
            # notice it has default values for its paremeters!
            
            # this is a special command which tells python to execute the parent's function
            # the pattern is 
            # super(ThisClassName, self).func_to_call()
            super(BasicSprite, self).__init__()
        
            ### When you sublcass the sprite, you need two things
            
            #  1. self.image
            
            self.image = pygame.Surface([width, height])
            self.image.fill(color)
            
            #  2. self.rect
            
            self.rect = self.image.get_rect()
            
            # self.rect starts out at 0,0. if you want to change the location, you have to update these coordinates
            # this hard codes the BasicSprite to start at the coordinates 50,50
            self.rect.x = 50
            self.rect.y = 50 
            
        
            
        def draw(self, screen):
            # draw this object's image onto the passed in screen variable
            self.image.blit(self.screen, self.rect)
            
Moving a sprite
^^^^^^^^^^^^^^^

Moving a sprite is really easy!  Everytime through the game loop, the sprite is drawn
using its internal :code:`rect` object, which stores the location coordinates.

To move it, we just change those coordinates before it is drawn! 

We are going to have a theme with this code. Any functionality we want our 
:code:`BasicSprite` to have, we will put it inside that class!

To illustrate how you can subclass and keep specializing, let's subclass our previous
:code:`BasicSprite` to make a :code:`MovingSprite`:

.. code-block:: python
    :linenos:
    
    class MovingSprite(BasicSprite):
        # MovingSprite has all the functions and properties that 
        # BasicSprite has
        
        def move(self, dx, dy):
            ## move dx units in the x direction
            ## move dy units in the y direction
            
            self.rect.x += dx
            self.rect.y += dy
            
Now, let's change one more thing about this. Let's alter the :code:`__init__` function
so that the dx and dy are internal!  

.. code-block:: python
    :linenos:
    
    class MovingSprite(BasicSprite):
        # MovingSprite has all the functions and properties that 
        # BasicSprite has
        def __init__(self, color=BLACK, width=100, height=100):
            super(MovingSprite, self).__init__(color, width, height)
            
            self.dx = 0
            self.dy = 0
        
        def move(self):
            ## move dx units in the x direction
            ## move dy units in the y direction
            
            self.rect.x += self.dx
            self.rect.y += self.dy

            
Colliding with one other sprite
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pygame provides several ways to handle collisions with sprite objects.

From the documentation, it says the following thing:
::
    pygame.sprite.collide_rect()
    
    Collision detection between two sprites, using rects.
    
    collide_rect(left, right) -> bool
    
    Tests for collision between two sprites. Uses the pygame rect colliderect function to calculate the collision. 
    Intended to be passed as a collided callback function to the *collide functions. Sprites must have a “rect” attributes.

Basically, this means that you can give this function two sprites and it will tell
you :code:`True` or :code:`False`.

We are going to have a theme with this code. Any functionality we want our 
sprite objects to have, we will put it inside that class!

To illustrate how you can subclass and keep specializing, let's subclass our previous
:code:`BasicSprite` to make a :code:`CollisionSprite`:

.. code-block:: python
    :linenos:
    
    class CollisionSprite(BasicSprite):
        # CollisionSprite has all the functions and properties that 
        # BasicSprite has, which has all of the functions BasicSprite has!

        
        def handle_collision(self, other_sprite, dx, dy):
            # we are going to define the logic for handling the collision with
            # one other sprite
            
            # there are two extra variables this function is taking.
            # they are the dx and dy. we need these so we know which direction
            # the sprite is moving!
            # Note: we want to make sure we only move x or y. 
            # if we are moving both, then we don't know whether the collision
            # is from the top/bottom or from the sides.
            
            if dx != 0 and dy != 0:
                # this syntax is:
                #   "raise" is a way of manually throwing errors and exceptions
                #   "Exception" is the default exception
                # by doing
                #   raise Exception(some_message)
                # we are stopping the program and causing an error.
                raise Exception("ERROR: don't move both x and y at the same time; Collision checking is impossible if you do this!")
            
            
            if pygame.sprite.collide_rect(self, other_sprite):
                ## if this "if" is true, then this means a collision is happening!
                ## let's check and see which direction it is

                ## check if the sprite is moving in the x direction:
                # if dx is positive, it is moving right
                # if the right side is past the other rect's left, snap them together
                if dx > 0 and self.rect.right > other_sprite.rect.left:
                    self.rect.right = other_sprite.rect.left
                    
                # if dx is negative, it is moving up
                # if the left side is past the other rect's right, snap them together
                elif dx < 0 and self.rect.left < other_sprite.rect.right:
                    self.rect.left = other_sprite.rect.right

                # if dy is positive, it is moving down
                # if the bottom is past the other rect's top, snap them together
                if dy > 0 and self.rect.bottom > other_sprite.rect.top:
                    self.rect.bottom = other_sprite.rect.top
                    
                # if dy is negative, it is moving up
                # if the top is past the other rect's bottom, snap them together
                elif dy < 0 and self.rect.top < other_sprite.rect.bottom:
                    self.rect.top = other_sprite.rect.bottom
                    
                    
                    
                
        
        ## Let's re-write the move function from before to handle collisions
        def move(self, other_sprite=None):
            ## we will assume that we are given access to a single other sprite
            ## as an argument to this function
            ## we will give it a default value of None though, so it's only optional
            
            ## move dx units in the x direction
            self.rect.x += self.dx
            
            if other_sprite is not None:
                # handle the x collision!
                self.handle_collision(other_sprite, self.dx, 0)
            
            ## move dy units in the y direction            
            self.rect.y += self.dy

            if other_sprite is not None:            
                # handle the y collision!
                self.handle_collision(other_sprite, 0, self.dy)
                
                
                

Using Groups of sprites
^^^^^^^^^^^^^^^^^^^^^^^

Pygame's :code:`Group` class is really useful for storing objects. 
We would use it inside the :code:`initialize` function of :code:`Game` so store
each of the sprites that we create.

.. code-block:: python
    :linenos:
    
    class Game:
        
        def initialize(self):
            # other code was here
            
            # just remember that our screen is made here
            self.screen = pygame.display.set_mode(WINDOW_SIZE)
            
            ## use group to manage a list of basic sprites
            self.basic_sprites = pygame.sprite.Group()
            
            # let's create a couple basic sprites
            for i in range(5):
                # create the new sprite
                # notice no self variable
                # that's because I know I'm not saving this inside self
                # instead, I'm saving this inside self.basic_sprites
                new_sprite = BasicSprite(BLACK, 100, 100)
                
                # doing this to offset the sprites so we can see them
                new_sprite.rect.x += i * 50
                new_sprite.rect.y += i * 50
                
                # save it to self.basic_sprites
                self.basic_sprites.add(new_sprite)
                
            
        def run(self):
            done = False
            
            ## the main game loop
            while not done:
                
                # other code was here
                
                # because you used a group to handle the basic sprites, you 
                # can shortcut the drawing of them by using group's draw function:
                
                self.basic_sprites.draw(self.screen)

  
Colliding with many sprites
^^^^^^^^^^^^^^^^^^^^^^^^^^^

First, we are going to add some functionality to our :code:`CollisionSprite` to handle group collisions!


.. code-block:: python
    :linenos:
    
    class GroupCollisionSprite(CollisionSprite):
        # CollisionSprite has all the functions and properties that 
        # CollisionSprite has, which has all of the functions CollisionSprite has!
        
        def handle_group_collision(self, sprite_group, dx, dy):
            # we pass in the "sprite_group", and the movements again
            
            # the False here is the option to remove all sprites being collided with
            # from the group. 
            # if True, sprite_group will no longer have them and they won't be drawn anymore
            # the returned object, colliding_sprites, is a list of sprites!
            colliding_sprites = pygame.sprite.spritecollide(self, sprite_group, False)

            # go through each of the sprites in this list
            for sprite in colliding_sprites:
                
                # use the function from CollisionSprite to handle this!
                
                self.handle_collision(sprite, dx, dy)
                
                
                
        ## Let's re-write the move function from before to handle group collisions
        def move(self, collision_group=None):
            ## we will assume that we are given access to a single other sprite
            ## as an argument to this function
            ## we will give it a default value of None though, so it's only optional
            
            ## move dx units in the x direction
            self.rect.x += self.dx
    
            # make sure it's not the default value        
            if collision_group is not None:
                # handle the x collision!
                self.handle_group_collision(collision_group, self.dx, 0)
            
            ## move dy units in the y direction            
            self.rect.y += self.dy
            
            # make sure it's not the default value
            if collision_group is not None:
                # handle the y collision!
                self.handle_group_collision(collision_group, 0, self.dy)
                

Now that we have :code:`GroupCollisionSprite` which can handle colliding with a group
of sprites, let's add it into :code:`Game`.

.. code-block:: python
    :linenos:
    
    class Game:
        
        def initialize(self):
            # other code was here
            
            # just remember that our screen is made here
            self.screen = pygame.display.set_mode(WINDOW_SIZE)
            
            ## use group to manage a list of basic sprites
            self.basic_sprites = pygame.sprite.Group()
            
            # let's create a couple basic sprites
            for i in range(5):
                # create the new sprite
                # notice no self variable
                # that's because I know I'm not saving this inside self
                # instead, I'm saving this inside self.basic_sprites
                new_sprite = BasicSprite(BLACK, 100, 100)
                
                # doing this to offset the sprites so we can see them
                new_sprite.rect.x += i * 50
                new_sprite.rect.y += i * 50
                
                # save it to self.basic_sprites
                self.basic_sprites.add(new_sprite)
                
            
            # it has the same __init__ function as BasicSprite
            self.hero = GroupCollisionSprite(BLACK, 100, 100)
            
                    
                    
        def run(self):
            done = False
            
            ## the main game loop
            while not done:
                
                # other code was here
                
                # remember the loop order:
                # Events, Updates, and then Draw
                
                # Updates is where collisions and movement goes
                # let's move the hero and have it handle sprite collision!
                self.hero.move(self.basic_sprites)
                
                # because you used a group to handle the basic sprites, you 
                # can shortcut the drawing of them by using group's draw function:
                
                self.basic_sprites.draw(self.screen)
                self.hero.draw(self.screen)


Adding an image to your sprite
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Adding an image is super easy!  The main thing is to change how :code:`self.image` gets defined!

Since our class, :code:`GroupCollisionSprite` has so much functionality now, let's just subclass it
and override the :code:`__init__` function:

.. code-block:: python
    :linenos:
    
    class ImageSprite(GroupCollisionSprite):
        
        def __init__(self, image_filename, colorkey=WHITE):
            
            # because all of the arguments in BasicSprite were optional, we
            # can just call the init function
            super(ImageSprite, self).__init__()
            
            # now, we overwrite image
            self.image = pygame.image.load(image_filename).convert()
            
            # Set our transparent color
            self.image.set_colorkey(colorkey)
            
            # refresh the rect now 
            self.rect = self.image.get_rect()
            
And that's it! 

If you wanted to do this without subclassing :code:`GroupCollisionSprite`, you 
could just subclass :code:`pygame.sprite.Sprite` again and define :code:`self.image` in this way.


Adding event handling to your sprite
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It's really useful to be able to handle keyboard input! In fact, if you want
people to play your game, it has to be able to handle input. 


There are two ways you could do this.  You could add code inside :code:`Game` which will
manually update the :code:`hero`.  But we don't want :code:`Game` to care about such things!

So, instead, we will let :code:`Game` just give every single event to the hero!

.. code-block:: python
    :linenos:
    
    class Game:
    
            
                    
                    
        def run(self):
            done = False
            
            ## the main game loop
            while not done:
                
                ## the event loop
                
                ## the event loop; used to check for events that occurred since the last time around
                for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        done = True
                    else:
                        # if the event isn't a quitting event, give it to the hero!
                        self.hero.handle_event(event)
                
                

And that's it! Now, writing this code creates an expectation from python that
our :code:`hero` will have this function implemented. So, let's do that.

.. code-block:: python

    class EventHandlingSprite(ImageSprite):
        # I inherited from the ImageSprite
        # if you don't want to do this, you can replace ImageSprite with GroupCollisionSprite
        # since that was our second most advanced sprite so far
        
        # remember, because we are inheriting, we get all of the functionality from before!
        
        def handle_event(self, event):
            # there are a couple of different pygame events:
            if event.type == pygame.KEYDOWN:
                # this is a keydown event
                # this means a key is pressed
                
                if event.key == pygame.K_LEFT:
                    self.dx = -5
                elif event.key == pygame.K_RIGHT:
                    self.dx = 5
            elif event.type == pygame.KEYUP:
                # this is a keyup event
                # this means a key was let go 
            
                if event.key == pygame.K_LEFT:
                    self.dx = 0
                elif event.key == pygame.K_RIGHT:
                    self.dx = 0
                    
Thsi is really simple event handling.  For instance, if you press two keys at once, 
this will have some weird results.  But at least it will handle some input!

To overcome the two-keys-at-once problem, you will have to do something a bit more complicated.
For instance, you could have the left key subtract 5 from :code:`self.dx` and then
use :code:`min` to make sure it is never smaller than -5.  You could also have some
boolean variables that are internal to the sprite which keep track of which keys have been pressed.


Making an animated sprite
^^^^^^^^^^^^^^^^^^^^^^^^^
        

Basic Game Physics
------------------

Physics is very important to games!  Since you are telling the game how each object
updates, you have to use math to update the objects to match how physics works. 
This can sometimes be hard, but there are plenty of ways to make it easier. 


In this section, there are the following recipes:

1. Bouncing off walls
    - If an object is moving in a direction and encounters an obstacle, it could bounce
    - Bouncing in certain ways looks and feels weird
    - So, you should bounce in a way that feels real!
2. Gravity
    - Instead of letting objects freely move in both x and y directions, gravity constantly affects the y!
    - You can think of this as making so that your object always wants to be moving down at 9 units at a time
3. Jumping
    - Jumping is just the opposite of gravity
    - When the jump happens, there is a force which makes the object want to move up at 9 units!
    - In other words, the y speed is set to -9
    - Then, every frame, the speed slowly goes back to +9. 


Handling Keyboard Input
-----------------------

1. Basic keyboard input
    - handle single keys
    - do specialized things
2. Continuous keyboard input
    - continue to do something until key is released
    - this is basically the example in the earlier section!
3. Advanced continuous keyboard input
    - use extra variables to keep track of which key was pressed!


Scoreboards
-----------

1. Drawing an extra surface that never moves
    - In the same logic as the sprite, except that it doesn't move and is always drawn last.

Menus
-----

1. Use a "card" concept to draw different viewpoints
    - A "card" is a certain way the game is
    - The standard one is your actual game
    - The menu one handles menu inputs and draws the menu
    - Inside the game loop, you check which card is active and give all event, update, and draw information to it.
    - The card then gives all up the information to its members. 



