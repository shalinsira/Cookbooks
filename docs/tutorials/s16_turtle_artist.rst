Turtle Artist
=============

The basics of a turtle artist are being able to make creations that are more complicated than a single function.

The goals you should have are:

1. Create a class which wraps around a turtle
    - This means that it has an internal variable that is a turtle (or multiple turtles)
    - All of the class functions will then use that single turtle to do things
2. Make it either interactive or periodic. 
    - Periodic means the Turtle Artist goes through phases and those phases repeat forever.
        + This does not mean a single looping turtle that draws the same thing forever.
        + You could think of a clock, for example, which constantly updates the time.
    - Interactive means that you can use the keyboard to influence how the turtle does things.
3. It should be a purposeful design.  Randomly doing things is not an acceptable solution. 


I recommend the interactive route.  There are a lot of cool things you can do!

For instance:
::
    import turtle
    class SuperTurtle:
        def __init__(self):
            self.grow_bigger = True
            
        def run(self):
            self.screen = turtle.Screen()
            self.inner_turtle = turtle.Turtle()
            self.screen.onkey(self.square, "s")
            self.screen.onkey(self.speed_up, "f")
            self.screen.onclick(self.hop)
            self.screen.ontimer(self.size_cycle, 50)
            self.screen.listen()
       
        def square(self):
            for i in range(4):
                self.inner_turtle.forward(100)
                self.inner_turtle.left(90)
        def speed_up(self):
            current_speed = self.inner_turtle.speed()
            if current_speed < 10:
                self.inner_turtle.speed(current_speed+1)
        def hop(self, x, y):
            self.inner_turtle.penup()
            self.inner_turtle.goto(x,y)
            self.inner_turtle.pendown()
            
        def size_cycle(self):
            s1, s2, s3 = self.inner_turtle.shapesize()
            if self.grow_bigger:
                self.inner_turtle.shapesize(s1+1, s2+1, s3)
            else:
                self.inner_turtle.shapesize(s1-1, s2-1, s3)
            if s1+1 > 20:
                self.grow_bigger = False
            elif s1-1 < 5:
                self.grow_bigger = True
            self.screen.ontimer(self.size_cycle, 50)
                
            
    
    bob = SuperTurtle()
    bob.run()
    turtle.done()

    