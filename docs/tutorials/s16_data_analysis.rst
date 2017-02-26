Data Analysis Tutorial
======================


More datasets
-------------

1. `Simpler Datasets <https://vincentarelbundock.github.io/Rdatasets/datasets.html>`_
2. `A huge list of datasets <https://github.com/caesar0301/awesome-public-datasets>`_
3. `538's datasets <https://github.com/fivethirtyeight/data>`_

Overview
--------

The goal of this tutorial is to talk about the important parts of beginning data analysis.

The typical analysis pipeline goes through the following stages:

1. Think about the data you would like
2. Either find a way to collect that data, or find data that already exists
    - sometimes you might have to compromise on data because it's easier to just use stuff that exists already
    - I have provided links to datasets above. 
    - For this tutorial, there is a titanic dataset
3. Write code that takes the data from a file or database and loads it into a data structure
    - We will be using Pandas, a data management library
    - Pandas makes manipulating data really easy
4. Write code that puts the data into different forms that match the task you want to do.
    - For instance, if you want to view interesting properties of your data as a scatter plot, you need to get two lists: one for the x positions and 1 for the y positions
    - You should be thinking about what kinds of things the data can tell you

I will be writing this tutorial while looking at the titanic dataset. 
The titanic dataset is a list of passengers, information about them, and whether they survived or not.


Getting the Data
----------------

I have made the data easy to get:
::
    from urllib import request
    import pandas as pd
    filepath = 'https://gist.githubusercontent.com/braingineer/5d15057ac482ee0130b6d0e6f9cc9311/raw/d4eefaecc98b342ec578cf3512184556e8856750/titanic.csv'
    response = request.urlopen(filepath)
    df = pd.read_csv(response)
    df = df.fillna(0)


Using Pandas and Matplotlib
---------------------------

Some example tutorials
**********************
1. `Simple Graphics <http://pbpython.com/simple-graphing-pandas.html>`_
2. `Beautiful Plots <https://datasciencelab.wordpress.com/2013/12/21/beautiful-plots-with-pandas-and-matplotlib/>`_

Some simple operations
**********************

Selecting a column
::
    age_column = df['Age']
    
Selecting a subset 
::
    df2 = df[age_column > 0]
    
View the columns
::
    print(df2.columns)

Visualize a scatter plot
::
    plt.scatter(df2['Survived'], df2['Age']);
    # or with columns out
    surv_col = df2['Survived']
    age_col = df2['Age']
    
Seaborn
*******

If you don't already have it, to install seaborn, type in a single cell in your Jupyter Notebook:
::
    !pip install seaborn

Then, you can do the following:
::
    import seaborn as sns
    sns.barplot(data=df, x='Pclass', y='Survived')

You can see more examples of seaborn plots at the `seaborn website <https://stanford.edu/~mwaskom/software/seaborn/examples/index.html>`_

Some examples to get you started:
::
    sns.countplot(data=df, x='Sex', hue='Survived')
    
    ### do these in different cells otherwise they will try to plot on top of each other
    sns.factorplot(data=df, x='Pclass', y='Age', col='Sex', kind='swarm', hue='Survived', x_order=[1, 2, 3])


Science
-------

To use data for science, you want to get summarize what happened.  
In other words, you want to tell a story with the data.  
To do this, you have to look at the different properties: counts, means, proportions, etc.

A good way to formulate a scientific question is to think about different groups. 
If the rate at which something happens is different between the two groups, then there is an effect of group. 

Some terminology
****************

1. **Proportion**: A proportion is a number between 0 and 1 that signifies the part to whole relationship.
   - If you eat half of a cake, the proportion you ate is 0.5
2. **Percentage**: A percentage is a number between 0 and 100 that signifies the part to whole relationship
   - If you eat half of a cake, the percentage is 50%

Questions you can ask
*********************

1. How many people were on the Titanic?
2. What percentage of the passengers did not survive?
3. How many of the passengers were male? How many were female?
4. How many male passengers survived?  How many female? Is there an interesting relationship?
5. What is the proportion of 3rd class passengers who survived?   
6. Is there an effect of class on the survivability of the gender?
7. What is the mean age per class?  



Additional setup
----------------

A version I was working that renames and cleans a version of the dataset:
::
    from urllib import request
    import pandas as pd
    import seaborn as sns
    %matplotlib inline
    filepath = 'https://gist.githubusercontent.com/braingineer/5d15057ac482ee0130b6d0e6f9cc9311/raw/d4eefaecc98b342ec578cf3512184556e8856750/titanic.csv'
    response = request.urlopen(filepath)
    df = pd.read_csv(response)
    df = df.fillna(0)
    cols = df.columns.values
    idx = list(cols).index('Pclass')
    cols[idx] = "Class"
    df.columns = cols
    df_clean = df[df['Age']>0]

And a couple extra plots I was looking at:
::
    ### super fancy
    sns.factorplot(data=df_clean, kind='violin', split=True, inner='stick', scale='count', x='Class', y='Age', hue='Survived', col='Sex')

    ### really sad
    sns.factorplot(data=df_clean, kind='bar', col='Class', x='SibSp', y='Age', hue='Survived', row='Sex')

.. 
    Old versions below
    ==================
    
    I have changed the page to reflect the use of pandas. the old stuff is below. 
    
    
    
    Getting the Data
    ----------------
    
    
    I have made the data easy to get:
    ::
        from urllib import request
        filepath = 'https://gist.githubusercontent.com/braingineer/5d15057ac482ee0130b6d0e6f9cc9311/raw/d4eefaecc98b342ec578cf3512184556e8856750/titanic.csv'
        response = request.urlopen(filepath)
        data = response.readlines()
        
    The data that is input here is a list of rows for the dataset.  Try and print out a couple.
    
    
    Cleaning the Data
    -----------------
    
    Take this raw data and turn it into a cleaner version. 
    
    To do this, you have to go through each line, replace the newline character with 
    the empty string (so it is removed), and split on the comma.  
    
    Since the first line is the headers, you know the name of each column. 
    
    So, you can take this information and make a dictionary per line which uses the 
    column names in the header as the keys and the values of each row as the values.  
    I have made a function which does this for one line.  You have to figure out how to 
    get the headers into a cleaned list, and how to apply this to every line in the file. 
    
    This should involve:
    
    1. to make the headers, replacing and splitting the first line in the data (``data[0]``) 
    2. then, use a for loop over the rest of the data (``data[1:]``) an apply the function
        - You will need another list to save things to (``clean_data.append(...)`` where ``...`` is a place holder for code you should write)
    example:
    ::
        def clean_one_line(line, headers):
            line = line.replace("\n", "")
            line = line.split(",")
            ### this is a fancy line.  play around with zip on your own. 
            ### zip lets you take two lists and make them into a list with them paired
            ### just like a zipper =)
            temp_dict = dict(zip(headers, line))
            should_be_ints = ['PassengerId']
            should_be_floats = []
            out_dict = dict()
            for key, value in temp_dict.items():
                if key in should_be_ints:
                    out_dict[key] = int(value)
                elif key in should_be_floats:
                    out_dict[key] = float(value)
                else:
                    out_dict[key] = value
            return out_dict
    
    Viewing the Data
    ----------------
    
    Now that you have data in a list of dictionaries, you can view it!
    Matplotlib is the python plotting library. You can import it like:
    ::
        import matplotlib.pyplot as plt
        
    If you are using Jupyter notebook (which I highly recommend), you should also type this in:
    ::
        %matplotlib inline
    
    If you are in the terminal, you should do the following. If you don't, every plot will take over the terminal and not let you type.
    ::
        plt.ion()
    
    If you are running a file, you should do the following after every plot. 
    ::
        plt.show()
    
    The reason it's shortcutted like this is because the alternative is too long. 
    It's called ``plt`` because it's just what everyone does (and it's good to use a common convention)
    
    There are a couple easy plots you can do:
    ::
        plt.plot
        plt.hist
        plt.scatter
    
    You can see some basics at `this pyplot tutorial <http://matplotlib.org/users/pyplot_tutorial.html>`_.
    But, you need to get your data into a certain form for this. 
    Let's take the ``plt.hist`` for example.  This requires you to have a single list of numbers.
    To do this, we now just iterate over our cleaned data:
    ::
        age_view = []
        for datum in cleaned_data:
            age_view.append(datum['Age'])
        plt.hist(age_view)
        
        