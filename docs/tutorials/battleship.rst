Battleship Requirements
=======================

1. Start a new game, randomize the locations of the ships
2. Make sure they aren't overlapping
3. At each turn, get the user's selection of place
4. At each turn, get the computer's random choice
5. Update the game and see if the player or computer have died
6. Repeat



Making the game board
---------------------

.. code-block:: python
    :linenos:
    
    def make_gameboard():
        game_board = dict()
        
        for letter in available_letters:
            for number in available_numbers:
                cell_string = "{}{}".format(letter, number)
                print("adding {} to the game board".format(cell_string))
                game_board[cell_string] = "o"
        return game_board
    

Starting a game and Randomizing
-------------------------------

.. code-block:: python
    :linenos:
    
    import random
    
    available_letters = "abcd..." ## fill this in
    min_num = 1 ## or whatever you want
    max_num = 10 ## or whatever you want
    
    game_board = make_gameboard()
    
    letter = random.choice(letter)
    number = random.randint(min_num, max_num)
    cell_string = "{}{}".format(letter, number)
    
    ## now that you have a letter and a number, how do you place the ships?
    ## it might be
    
    
Testing with a dictionary
-------------------------




.. code-block:: python
    :linenos:
    
    def get_userchoice(game_board):
        while True:
            user_choice = input("What's your next move...")
            ## test for existance first
            if user_choice not in game_board:
                print("{} is not a valid option".format(user_choice))
            ## test to see if it's good or bad, we are keeping track with x and o in this example
            elif game_board[user_choice] == "x":
                print("Already been done!")
            else:
                ## this escapes the while loop
                return user_choice
                
    