Chatbot Tutorial
================

The goal of this tutorial is to introduce the idea of reflex-response agents and finite state automata. 


Reflex-Response Agents
----------------------

Agent is a word used in Artificial Intelligence to refer to programs that are meant to act on their own. 

There are several types of agents.  The one we will cover here is a reflex-response agent.
Our reflex-response agent will look at the world in turns.  Each turn, there is an input, and each turn, it has to choose an output.
This is what is meant by reflex-response.  It responds as a reflex to the input. 

There are some famous reflex-response agents. The most famous is `Eliza <https://en.wikipedia.org/wiki/ELIZA>`_. 
When you plan your chatbot, you should think about how it compares to Eliza.  In fact, it wouldn't be bad to try to recreate her. 

So, what does it take for a Reflex-Response Agent?  
There needs to a separation of the two major components: **the agent's brain** and **the agent's interface**. 
The brain handles the thinking, the interface handles the communication through the terminal.

Our reflex-response agent is going to be slightly more advanced than usual, however.
I will cover that in the **brain** section. 

Interace
********

So, begin by designing the interface.  How should it act?  
It should be a while loop that acts in the following steps:
1. Present information to the user about the task
2. Ask the agent what it wants to say
3. Show that to the user
4. Wait for the human to say something
5. Send the human's response to agent
6. Go back to Step 2.

For a pure turn based reflex-response agent, that is all that it takes to interface with the human.
Of course, it would be better if it were more like a chat room or text messaging interface where the agent didn't have to wait for the human to respond and vice versa.
However, that's more of a second stage project. 


Brain
*****

The brain needs to be able to take the input from the human and respond to it. 
You should do this so the agent's brain has an internal state.  This means that
it can keep track of different properties, such as the user's name or what it has previously said. 

For this, you need to design the agent's class.  
- What functions should it have? 
- What should it pay attention to?  
- What properties are important in the conversation?
- What do you want the agent to do? 

I have implemented an agent before that kept track of todo lists and reminded me of things.  
I have also had it so that it could check on things like the time.  

A basic agent class could look like
::
    class Agent:
        def __init__(self, important, properties):
            self.important = self.important
            self.properties = self.properties
            self.startup_stuff()
        
        def startup_stuff(self):
            ''' any complex startup logic should go here '''
        
        def observe(self, observation):
            ''' this is the incoming sentence. you could call it something else if you'd like.
                I call it observation just because I also deal with agents that see properties of the world
            '''
        
        def speak(self):
            ''' this should have the agent say something. this is the sentence shown to the user 
            '''
            

And that's about it.  You have to figure out how you want the agent to respond to sentences, now.
For this, you have to see if the incoming string matches something you know about. 
One possible way of doing this is think about it in the following sense:

1. Get the input string and process it by checking it for words or phrases
    - for example, maybe the user said "Hi! How are you" and you want to find the phrase "How are you"
2. Have your checking be a process which returns a number, perhaps 1-5, depending on what it found. 
3. Have a set of responses set up that respond to the numbers 1-5.

The reason this method could be good is that you're funneling the wide range of the ways people could say things 
into a smaller number.  Then, you write responses to that smaller number.  
The process of reducing the wide range of ways people could say things is called classification.  
By writing code that classifies, you are doing rule-based classification. 

You could even have a function which checks for things like: "My name is", "I am", "You are", "we will".
Then, you can take whatever is the in the rest of that sentence and use it in some way. 

Finite State Automata
---------------------

I will briefly cover finite state automata.  Today you should concentrate on the agent. 

In a conversation, we go through a series of states.  A state means a certain settings of the current situation. 
For example, when we first see someone, we are the "greeting" state. This means that the appropriate things to say are about greetings.
Then, we move to another state. In class, we move to a "checkpoint" state where I ask the students how their homework went. 

An agent that has states and has transitions between states is called a finite state automata.  For example:

.. image:: http://oldblogimages.metawrap.com/2008/WindowsLiveWriter/PracticalApplicationsOfFiniteStateMachin_C2DB/244px-Finite_state_machine_example_with_comments.svg_2.png

It is useful to represent the states explicitly.  
The reason is that you might have different responses to the same exact string given different states.
If you wanted into class and said "goodbye", I would be confused.  If the class is ending and you say "goodbye", that makes sense. 

The way you can represent states in an agent is to a separate class for states. 
Then, you would have a new copy for each new type of state.  
Each state copy would be setup with different variables so it could manage the things you want to do. 

Then, inside the agent, whenever it gets an input, it would use the current state to get its response.
It would then decide whether or not it should stay in the same state or move to a new state.
A good way of managing this is to have each state have a set of conditions. As soon as those conditions are met, 
it tells the agent that it should move on.

These are all very complex ideas.  
One nice blog post on these types of ideas are from `the gamasutra blog <http://www.gamasutra.com/blogs/ChrisSimpson/20140717/221339/Behavior_trees_for_AI_How_they_work.php>`_.
