Cookbook
========


A set of common recipes and design patterns



Game Loop
---------

.. code-block:: python
    :linenos:
    
    import pygame
    
    ## start pygame's engines
    pygame.init()
    
    ## set the screen size
    WINDOW_SIZE = (700, 500)
    
    ## get a screen 
    screen = pygame.display.set_mode(WINDOW_SIZE)
    
    ## get a clock used for FPS control
    clock = pygame.time.Clock()
    
    ## a simple flag variable for the loop
    done = False
    
    
    ## the main game loop
    while not done:
    
        ## the event loop; used to check for events that occurred since the last time around
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                done = True


        #### update the display and move forward 1 frame
        pygame.display.flip()
        # --- Limit to 60 frames per second
        self.clock.tick(FPS)

Drawing
-------

Using Rect to draw
^^^^^^^^^^^^^^^^^^

Rect is a useful PyGame class that is a wrapper around the standard rectangle information.

.. code-block:: python

    x = 0
    y = 0
    width = 100
    height = 100
    r1 = pygame.Rect(x, y, width, height)
    
The variable :code:`r1` now has access to a variety of different properties
::
    x,y
    top, left, bottom, right
    topleft, bottomleft, topright, bottomright
    midtop, midleft, midbottom, midright
    center, centerx, centery
    size, width, height
    w,h
    
You can also update :code:`r1` using any of those variables. For example:

.. code-block:: python
    :linenos:
    
    r1.center = (50,50)
    r1.right = 10
    r1.bottomright = 75
    

Bouncing off obstacles
----------------------

Basic collision detection with screen boundaries
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the simplest case, we are testing to see if our rect is over some threshold.
This happens in the case of bouncing off the edges of the screen. 
For this example, we assume we know the height and width of the window as well. 

.. code-block:: python
    :linenos:
    
    # W, H are window width and window height
    
    if r1.right > W:
        print("Over right side")
    elif r1.left < 0:
        print("over left side")
    
    if r1.top < 0:
        print("Over top")
    elif r1.bottom > H:
        print("Over bottom")
        
Changing direction based on screen boundary collision
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let's assume that the object in question is moving at some speed.  In other words,
the :code:`x` and :code:`y` properties are being updated by some variable 
:code:`dx` and :code:`dy`.  Then, when the object bounces, 
it should flip the signs of those speeds. 

.. code-block:: python
    :linenos:
    
    # W, H are window width and window height
    r1.x += dx
    
    if r1.right > W or r1.left < 0:
        dx *= -1

    r1.y += dy    
    if r1.top < 0 or r1.bottom > H:
        dy *= -1

Colliding with another Rect
^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you wanted to collide with another Rect, there are several different
ways you could it.  The easiest way is to use the built in functions which test for collision.
However, these functions don't tell you which parts collided. 
An example of why this is a problem:

- There is a collision with a Rect and an obstacle from the bottom
- The Rect's right side is technically past the obstacle's left
- But, the issue is the y-movement, not the x-movement. 

The first part of the solution is to update the X and Y parts separately.  
With this method, one dimension is changed and checked for collisions.
Then, the other is changed and checked for collisions. 

The second part of the solution is to "snap" the edges of the object and the obstacle together.
This just means making them line up exactly so no more collision is taking place. 

The below code illustrates the Rect collision code, 
the separate x and y movements, and the edge snapping. 

.. code-block:: python
    :linenos:
    
    '''
    in this example, self.rect is the rect of the object you are moving
    '''
    
    
    def move(self, dx, dy, other_rects):
    
        # move this object in the x direction
        self.rect.x += dx
        
        # go over each obstacle
        for other_rect in other_rects:
    
            
            # if there is a collision
            # since we moved only the x, we know it has to be this object's left or right
            if self.rect.colliderect(other_rect):
            
                # if dx is positive, it is moving right
                # if the right side is past the other rect's left, snap them together
                if dx > 0 and self.rect.right > other_rect.left:
                    self.rect.right = other_rect.left
                    
                # if dx is negative, it is moving left
                # if the left side is past the other rect's right, snap them together
                elif dx < 0 and self.rect.left < other_rect.right:
                    self.rect.left = other_rect.right
                    
        
        # move this object in the y direction
        self.rect.y += dy  
        
        # go over each obstacle
        for other_rect in other_rects:
            
            # if there is a collision
            # since we moved only the y, we know it has to be this object's top or bottom
            if self.rect.colliderect(other_rect):
                
                # if dy is positive, it is moving down
                # if the bottom is past the other rect's top, snap them together
                if dy > 0 and self.rect.bottom > other_rect.top:
                    self.rect.bottom = other_rect.top
                    
                # if dy is negative, it is moving up
                # if the top is past the other rect's bottom, snap them together
                elif dy < 0 and self.rect.top < other_rect.bottom:
                    self.rect.top = other_rect.bottom

