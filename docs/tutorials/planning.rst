Planning with Flow Charts and Structure
=======================================


Flow charts and structure
-------------------------

You should decide on the structure and topic of your project pretty early.

For example: 

- if you are doing a story, what is the context and background?
- if you are doing a game, what is the goal? what are the parts? 
- similar to a game, if you are doing a library (like encryption), what is the goal? 


A flow chart starts with the initial point.
For an interactive story or game, this is the beginning of the game.
For a library, it will be the beginning of the algorithm. 
The logic of the code will flow from this initial point.
You can use either paper to draw this or you can use an online website
(for example, `draw.io is an ok one <https://www.draw.io/>`_).

Any specific point in the story is sometimes called the "state".
The state is a specific setting of variables.  And since this is a story
you are programming, the set of variables are the variables you will be using
to keep track of the story.

Remember that you are drawing the information flow.
`Here is a real life example. <https://pbs.twimg.com/media/C6A7smLUsAAzJeS.jpg>`_.
Though, they don't use the dimaonds I recommend below, but instead use colors. 
You can do whichever you want.  

`This page has really good, simple examples of flow charts <https://www.programiz.com/article/flowchart-programming>`_ 

There are several kinds of shapes in the flow charts:

Ovals are start/end points
^^^^^^^^^^^^^^^^^^^^^^^^^^

Ovals are either the starting or ending points.  They are where the story starts and stops.

Rectangles/Boxes are processing points
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Boxes represent the processing of information. Into the box flows some information and
out flows other information.  You draw this as a line flowing into a box and a line flowing out.

Diamonds are decision points
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If there is a condition in your code, you draw that as a diamond. Since the information
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
