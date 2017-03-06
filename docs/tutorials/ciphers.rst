Ciphers
=======


Substitution Cipher
-------------------


There are many different kinds of ciphers. A simple one is a substitution cipher.
This is where you create a dictionary that maps one letter to another. 
Then, you can loop over the message and make a new one!

Since we are programmers, we don't always want to make things from scratch.
Let's look at some shortcuts too. 

.. code-block:: python
    :linenos:

    import string
    
    print("the string package has a bunch of useful things for strings in Python")
    print("We are going to use it to get all of our letters")
    
    letters = string.ascii_lowercase
    
    print(letters)
    
    cipher = dict() ## an empty dictionary
    
    n_letters = len(letters)
    
    for i in range(n_letters):
        from_letter = letters[i]
        
        ### now, let's get the opposite letter
        ## n_letters is 26, and i starts at 0
        ## but we want the first to_letter_index to be 25. so let's subtract 1. 
        ## what is the last number i will be?  what will this index be then? 
        to_letter_index = n_letters - i - 1
        to_letter = letters[to_letter_index] ### this will start at n_letters and work backwards!
        
        cipher[from_letter] = to_letter
        
    print("We have now made our cipher, let's use it to encrypt a message!")    
    
    message = "this is a test Message"
    
    print("Because we only made our cipher with lowercase letters, let's make sure the message is lowercase too")
    
    message = message.lower()
    
    print("Now we are going to use the accumulator pattern.")
    print("This means we start with an empty string and add onto it, one letter at a time")
    
    encrypted_message = ""
    for letter in message:
    
        ### make sure to test to see if the letter is even in the cipher. if it's not
        ### it is a space or a number. let's leave them along and just add them into
        ### the resulting string!
        if letter in cipher.keys():
            new_letter = cipher[letter]
        else:
            new_letter = letter ## just set it equal it self
            
        encrypted_message += new_letter ## remember the += is a shortcut!
        
    print("We have encrypted the message {} and it has become {}".format(message, encrypted_message))
    
    
Decrypting
^^^^^^^^^^

Decrypting is the opposite of encrypting: you just map backwards.  

One way to do this is to just use the dictionary we made and reverse it!

.. code-block:: python
    :linenos:

    import string
    letters = string.ascii_lowercase
    n_letters = len(letters)

    cipher = dict() ## an empty dictionary
    decrypt = dict() ## an empty dictionary
    
    for i in range(n_letters):
        from_letter = letters[i]
        ### now, let's get the opposite letter
        ## n_letters is 26, and i starts at 0
        ## but we want the first to_letter_index to be 25. so let's subtract 1. 
        ## what is the last number i will be?  what will this index be then? 
        to_letter_index = n_letters - i - 1
        to_letter = letters[to_letter_index] ### this will start at n_letters and work backwards!
        
        cipher[from_letter] = to_letter    
        decrypt[to_letter] = from_letter
    
    ## you could have also done this:
    decrypt = dict()
    for from_letter, to_letter in cipher.items():
        decrypt[to_letter] = from_letter
    
    ### and now you use it as we did with the cipher above
    
    
Caesar Cipher
-------------

A really awesome fact is that the Caesar Cipher is named after Ceasar himself.

From the `Wikipedia page <https://en.wikipedia.org/wiki/Caesar_cipher#History_and_usage>`_:

> The Caesar cipher is named after Julius Caesar, who, according to Suetonius, 
> used it with a shift of three to protect messages of military significance. 
> While Caesar's was the first recorded use of this scheme, other substitution ciphers are known to have been used earlier.[4][5]

> "If he had anything confidential to say, he wrote it in cipher, 
> that is, by so changing the order of the letters of the alphabet,
> that not a word could be made out. If anyone wishes to decipher these, 
> and get at their meaning, he must substitute the fourth letter of the alphabet, namely D, for A, and so with the others."
>   - Suetonius, Life of Julius Caesar 56

> His nephew, Augustus, also used the cipher, but with a right shift of one, and it did not wrap around to the beginning of the alphabet:
> "Whenever he wrote in cipher, he wrote B for A, C for B, and the rest of the letters on the same principle, using AA for Z."
>   - Suetonius, Life of Augustus 88

> Evidence exists that Julius Caesar also used more complicated systems,[6] and one writer, Aulus Gellius, refers to a (now lost) treatise on his ciphers:
> "There is even a rather ingeniously written treatise by the grammarian Probus concerning the secret meaning of letters in the composition of Caesar's epistles."
>   - Aulus Gellius, Attic Nights 17.9.1–5


A Caesar Cipher is just a substitution cipher which has a specific shift of letters!

So, let's assume we will use the exact same code above, but let's change how
we make the cipher dictionary.  The following code should only
replace the :code:`for loop` above that makes the cipher dictionary. 


.. code-block:: python
    :linenos:

    import string
    letters = string.ascii_lowercase
    n_letters = len(letters)
    
    caesar_cipher = dict() ## an empty dictionary
    shift_number = 3 ### Let's shift like Caesar!
    
    for i in range(n_letters):
        from_letter = letters[i]
        
        ### now, let's get the encrypting letter
        ### but this time, let's use the cipher!
        to_letter_index  = i + 3
        
        ### but what if other_index is larger than 26 now?  We need to make sure
        ### it wraps back around to the length of the alphabet:
        to_letter_index = to_letter_index % 26
        
        ### now store it!
        to_letter = letters[to_letter_index] ### this will start at n_letters and work backwards!
        
        cipher[from_letter] = to_letter
        
    print("We have now made the Caesar Cipher, let's use it to encrypt a message!")    
    
    message = "this is a test Message"
    
    print("Because we only made our cipher with lowercase letters, let's make sure the message is lowercase too")
    
    message = message.lower()
    
    print("Now we are going to use the accumulator pattern.")
    print("This means we start with an empty string and add onto it, one letter at a time")
    
    encrypted_message = ""
    for letter in message:
    
        ### make sure to test to see if the letter is even in the cipher. if it's not
        ### it is a space or a number. let's leave them along and just add them into
        ### the resulting string!
        if letter in cipher.keys():
            new_letter = cipher[letter]
        else:
            new_letter = letter ## just set it equal it self
            
        encrypted_message += new_letter ## remember the += is a shortcut!
        
    print("We have encrypted the message {} and it has become {}".format(message, encrypted_message))
            
    
ROT-13
^^^^^^

When the shift is 13, it is called **ROT-13** for "rotation 13".  
Although not that secure (it can be decoded easily), it does provide a nice
example because both the encryption and decryption dictionaries would be the same,
at least for English because we have 26 letters.  

To read more about it, `check out the wikipedia entry <https://en.wikipedia.org/wiki/ROT13>`_.
You should try the ROT-13 in your Caesar Cipher. 