Reading and Writing JSON Files
===============================

JSON files are really useful. They let you store not just plain text, but 
dictionaries!   You pronounce them as "Jay-Sawn" 
(Jason is more like "Jay-Sun", which isn't quite right here)

Writing a JSON file
--------------------

Writing a JSON file is called "dumping".

.. code-block:: python
    :linenos:
    
    import json
    
    bunny_dict = {"name": "Euclid", "age": 2}
    
    with open("bunny.json", "w") as fp:
        json.dump(bunny_dict, fp)
        
And that's it!  One nice part about JSON is it that you can dump a JSON dictionary
to a string instead of a file!  

.. code-block:: python
    :linenos:
    
    import json
    
    bunny_dict = {"name": "Euclid", "age": 2}
    
    new_str = json.dumps(bunny_dict)
    
    print(new_str)       
    
Notice that it is :code:`json.dumps` now.  The **s** in :code:`dumps` means "dump string". 


Reading a JSON file
-------------------

Loading a JSON file is called "loading"

.. code-block:: python
    :linenos:
    
    import json
    
    with open("bunny.json", "r") as fp:
        bunny_dict = json.load(fp)
        

Pretty easy!  The nice part about using JSON is that you can use dictionaries
to store information. This means you can store and load information which 
requires more structure than a plain string, like character information or save game state.