Minecraft Architect Tutorial
============================

The goal of this tutorial is walk you through how to be a minecraft architect.

The first steps are going to be:

1. Get the correct setup going (see :doc:`../installminecraft`)
2. Start interacting with the world

This tutorial will cover a few of the basic information and then some techniques for building things in minecraft.

To start:

1. Start the minecraft server
2. Log into the minecraft client (make sure you set the version under the profile settings to 1.9.2!)
3. connect to a world at the address ``localhost`` or ``127.0.0.1``
4. Open up an iPython terminal to test the connection and type in
::
    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    mc.postToChat("hello world!")
5. From now on, you should use a file and do the first following lines so that you have access to the ``mc`` object and the ``Vec3`` class.
::
    from mcpi.minecraft import Minecraft
    from mcpi.vec3 import Vec3
    mc = Minecraft.create()

Information: User-Centric Positioning
-------------------------------------

The first thing you should think about is that everything you do is based around the user.
The user is located at a specific place in the world, which are the set of (x,y,z) coordinates.
So, when you construct anything, you are constructing relative to them.

You get the positions by:
::
    pos = mc.player.getPos()
    ### to see what this looks like, you can do
    print(pos, type(pos))
    ### you can also get the x,y,z individually:
    print(pos.x, type(pos.x))
    print(pos.y, type(pos.y))
    print(pos.z, type(pos.z))

It is best to draw things out on paper and plan them.
For instance, if you want to make a wall next to the user, you should figure out what the adjustments to the x and z would be.
One spot away from the user would be ``pos.x-1`` or ``pos.z-1``


Information: Placing Blocks
---------------------------

You can place either a single block or multiple blocks of the same type.

Single Blocks
*************

For a single block, you either specify a ``Vec3`` object, or the 3 coordinates.
You also specify the block number.  You will have a book looking these up.
::
    pos = mc.player.getPos()
    ### set by the Vec3
    mc.setBlock(pos, 42)
    ### set by each spot individually
    mc.setBlock(pos.x, pos.y, pos.z, 42)

    ### but probably set in front of user, not where they are
    mc.setBlock(pos.x+1, pos.y, pos.z+1, 42)

Vectors can add, so instead of typing out the 1 away with each spot individually, you can do
::
    pos = mc.player.getPos()
    offset = Vec3(1,0,1)
    new_pos = pos + offset
    mc.setBlock(new_pos, 42)
    ### you could have also done:
    mc.setBlock(pos + offset, 42)
    ### or even
    mc.setBlock(pos + Vec3(1,0,1), 42)

Multiple Blocks
***************

For multiple blocks, you are specifying a **cube**.  For this, you have to give the two corners of the cube.
For example, you could do:
::
    mc.setBlocks(0,0,0, 3, 3, 3, 42)

This would create a 3 by 3 by 3 cube.  Note, because I didn't use relative coordinates, you won't be able to find this cube.
To make it relative to the player:
::
    pos = mc.player.getPos()
    mc.setBlocks(pos.x, pos.y, pos.z, pos.x+3, pos.y+3, pos.z+3, 42)
    ### or more easily:
    mc.setBlocks(pos, pos+Vec3(3,3,3), 42)

Let's make a giant box around the player. You will probably have to break your way out.
::
    pos = mc.player.getPos()
    mc.setBlocks(pos-Vec3(5,5,5), pos+Vec3(5,5,5), 42)

Technique: Layers
-----------------

When you're placing blocks, if you want to have a unique shape, you can play the blocks in layers.
Imagine building a pirate ship, for example.  Each layer starting from the bottom would get longer and longer and slightly wider.
This would create a oval-type shape that ships have on their bottom.

You could do the layer technique for faces, buildings, triangles, etc.

How could you use the layer technique to build a four-sided pyramid?

Technique: Negative Space
-------------------------

One thing you can do is think about building things with negative space.

For example, let's say I wanted to build a box around the player, but I didn't want them to suffocate.
Well, you could create the cube first, and then replace the inner part of the cube with a smaller cube of air.
::
    pos = mc.player.getPos()
    cube_size = Vec(5,5,5)
    air_size = Vec(4,4,4)
    mc.setBlocks(pos-cube_size, pos+cube_size, 42)
    mc.setBlcoks(pos-air_size, pos+air_size, 0)

Technique: Block Collections
----------------------------

Another thing you can do is create collections of blocks using lists and then
have a function which can iterate over them and place them one at a time.
::
    def set_points(points, mc, block_type):
        for point in points:
            mc.setBlock(point, block_type)

    ### example usage
    pos = mc.player.getPos()
    points = list()
    for i in range(10):
        points.append(pos+Vec3(-1*(i%5), i%5, i%5))
    set_points(points, mc, 42)


Technique: Circles
------------------

You could also do a block collection that uses sin or cos to create a circle. I will explicitly give this one to you.
Here I am using a set because it enforces uniqueness. No point can exist twice.
::
    def taxicab_circle_x(r):
        point_set = set()
        x = 0
        for angle in range(360):
            theta = math.radians(angle)
            y = math.floor(r*math.sin(theta))
            z = math.floor(r*math.cos(theta))
            point_set.add(Vec3(x, y, z))
        return point_set
