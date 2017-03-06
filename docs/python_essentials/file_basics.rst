Read and Write Files
====================

It is common to read and write files to store and process data and information.
This could the saving of a game or processing a file. 

There are a couple new syntax items we haven't talked about yet.

1. :code:`with` is Python syntax that temporarily creates variables and handles
the creation and closing.  We use it with files so Python makes sure the file
closes when we are done and doesn't corrupt the file.  :code:`with` will
create a new code block, so it's important to note that as soon as the code block ends
(a line of code starts that isn't indented the 4 spaces needed to be in the 
:code:`with` code block), then Python closes the file.

2. :code:`open` is a Python command to open a file.  With only one argument,
that argument is assumed to be the filepath.  There are optional arguments. The
important one is a second argument which will tell Python whether you are
reading or writing the file.  When you don't put in the second argument, 
Python assumes it is :code:`'r'` for reading. 

3. :code:`as` is Python syntax only used with the :code:`with` command.  You should
keep note of the syntax as a whole and follow that pattern. 


Reading the file
----------------

.. code-block:: python
    :linenos:
    
    filepath = "file_location.txt"
    with open(filepath) as file_obj:
        data = file_obj.read()
        

in this example, we knew where the location of the file is.  This is vital and there are
two different ways to think about this. 

1. The **relative path** is based on the file that's running the code (or where 
        the iPython console thinks it is currently at)
2. You have to know the **absolute path**, which is the fully path to the file. 

I recommend trying this out with a file that's in the same folder as the python
file. This is the **relative path** style.  Then the filepath is just the filename. 

The hidden second argument to :code:`open`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As mentioned above, :code:`open` can have a second argument. In this 
example, the second argument is not there and Python has a default value for it.
To explicitly put it there so we can see the value, it would look like:

.. code-block:: python
    :linenos:
    
    filepath = "file_location.txt"
    with open(filepath, 'r') as file_obj:
        data = file_obj.read()
        
The :code:`'r'` stands for **read**

Variations on read
^^^^^^^^^^^^^^^^^^

There are a couple of different ways you can read in the file. 
The example above showed the function :code:`file_obj.read()`. This gets
the entire file in as a string.  Another way is to use :code:`file_obj.read_lines()`.
If you're doing line by line processing, I recommend the second. If not, I recommend the first.

Things to be careful of
^^^^^^^^^^^^^^^^^^^^^^^

Strings can be tricky. They can include characters that you don't want. 
For example, with :code:`file_obj.read()`, all of the new lines (the characters that
give new lines when printed) are still in there (as :code:`\n`). 
You can fix this by removing them from the string using the replace function:


.. code-block:: python
    :linenos:

    x = "this has \n\tweird characters"
    
    x = x.replace("\n", "")
    x = x.replace("\t, "")
    print(x)
    assert x == "this has weird characters"
    

Writing to files
----------------

Writing to files is very similar. The important things to notice:

1. There is now an :code:`'w'` in the syntax: :code:`with open(filepath, 'w') as file_obj`.
   This means Python is now writing to the file.  Be careful though! 
   **This will always overwrite any file that is already there!**
2. You have to write the new lines yourself (otherwise everything will be on
one line!)


.. code-block:: python
    :linenos:
    
    
    filepath = "file_location.txt"
    with open(filepath, 'w') as file_obj:
    
        file_obj.write("This is in the file")
        file_obj.write("So is this! But this one has the new line\n")
        file_obj.write("Here is some more stuff")
        