---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.10.3
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Introduction to Python Programming



By: Dr. Eric Godat and Dr. Rob Kalescky 


# Intro to Python Basics


*This section is designed to guide you from having never used Python before to feeling comfortable with basic operations.*

Python is a programming language capable of just about anything you could want to do. It is designed to be human readable and robust. This particular document is called a Jupyter Notebook. Notebooks are tools for developing Python code and running that code in small steps and see the intermediate results in line.


## Operating this notebook


To operate this notebook, you will need to execute boxes of code, called cells. To do this you can either click the *Run* button on the toolbar or use [Shift]+[Enter].

Throughout this notebook you will see cells that are not code (like this one). These cells contain text in a language called Markdown. You can execute these cells to render formatted text. A cheatsheet for Markdown can be found by clicking `Help -> Markdown Reference` or articles [like this](https://medium.com/analytics-vidhya/the-ultimate-markdown-guide-for-jupyter-notebook-d5e5abf728fd). There will also be comments with in the code itself that give additional information about the operation of the code, describe functions or show you places where you might want to make changes. These comments are always preceded by an octothorp (#) and in most cases be a different color from the surrounding text.

Notebooks save automatically, however if you have made big changes your code, you can checkpoint it. This allows you to roll back changes to this point (or any previous checkpoints) should something break in the future.

There are a few useful [keyboard shortcuts](https://gist.github.com/discdiver/9e00618756d120a8c9fa344ac1c375ac) for modifying the cells in a notebook. To use these, click on the far left side of the cell such that the outline changes color (to blue in most cases), press [Enter]] to return to editing the cell's contents.

-Add a cell **a**bove the current cell   [A]

-Add a cell **b**elow the current cell   [B]

-**D**elete the current cell   [D,D]

**Let's try it out!**


### Basic Math


Python can do simple mathematical operations just like a calculator. Try executing the following cells.

```python
1+1
```

```python
2.5-2.0
```

> Let's now add a cell and have it calculate the sum of the populations of Dallas (1,345,000) and Fort Worth (895,000).

```python
# Add a cell below this one to do your calculation
```

## Variables and Objects


Calculations are nice but we really want to be able to store our calculations in memory so that we can access them later. We do that by assigning variables. 

```python
a=2
b=3
```

```python
a+b
```

Variables can be named just about anything

```python
Dallas=2
SMU=7
texas_TX=3
```

```python
#Notice that if we assign a value to a variable, our notebook won't return that value to our screen.
#If we want it to show us the value, we can call that variable after it is assigned.
ouranswer = SMU*Dallas*texas_TX
ouranswer
```

So far we have been doing all of our operations on numbers, integers and floats (decimals), but there are other useful objects we can use in Python.

Strings allow us to store and operate on text data. Strings in Python are surrounded by either single quotes '' or double quotes "".

```python
ourstring = "Here is a string in Python!"
ourstring
```

> Try uncommenting the next cell and making a string of your own.

```python
#mystring = <put your string here>
#mystring
```

If we later want to see the value stored in a variable we can always use the built in **print** function. **Print** is recognized as a keyword by our notebook and so the color changes to make our lives as programmers easier.

```python
print(ourstring)
```

What if we want to have multiple strings stored at once but we don't want to assign a bunch of variables? Then we can use a list.

Lists are enclosed by brackets [] and separated by commas.

```python
ourlist = ['This', 'is', "a", "list", 'of', "strings"]
```

```python
print(ourlist)
```

To access individual elements in a list you call it by its reference number.

*__Note:__ In Python, counting starts with 0. Thus in the list [a,b,c], a is the 0th element and c is the 2nd*

```python
first = ourlist[0]
```

```python
# Notice we can call the last element by using a negative reference number. This lets us see the end without knowing how long the list is.
last = ourlist[-1]
```

```python
print(first,last)
```

```python
# If we did want to know the length of our list we can use the len() function
len(ourlist)
```

> Try making a list and printing the 2nd element from your list. Make sure to remove the #'s for comments.

```python
#mylist=
#
#
```

> How long is your list?

```python

```

### Dictionaries


Dictionaries are a different way of storing data than lists. They rely on a key and value system as opposed to the order of the entries.

Dictionaries are enclosed in curly braces {}, the key and value are separated by a colon : and entries are separated by commas ,

Values can then be accessed by referencing the key.

*__Note:__ Finding dictionary values does not go both ways, so using the value to find the key will cause an error.*

```python
ourdictionary = {"Dallas":1345000,"Taos":5668,'Houston':2326000}
ourdictionary
```

```python
ourdictionary["Taos"] 
#NOTE: ourdictionary[5668] will NOT give you "Taos", but an error.
```

Here are the word counts for the *Lord of the Rings* books ([citation](http://lotrproject.com/statistics/books/wordscount)). We will use this data for some exercises below.

|__Book__|__Word Count__|
|---|---|
|The Silmarillion|130115|
|The Hobbit|95506|
|The Fellowship of the Ring|187726|
|The Two Towers|156147|
|The Return of the King|137037|



>1) Can you build a dictionary of the information in the table above?
>2) Calculate the difference between the number of words in *The Fellowship of the Ring* and *The Hobbit*.
>3) Calculate the total number of words for books in the *Lord of the Rings* Trilogy.

```python

```

<!-- #raw -->
# Example Solution

tolkien = {"The Silmarillion":130115,"The Hobbit":95506,"The Fellowship of the Ring":187726, "The Two Towers":156147, "The Return of the King":137037}

bilbo=tolkien["The Hobbit"]

frodo=tolkien["The Fellowship of the Ring"]

print("The Fellowship of the Ring - The Hobbit")

print(frodo-bilbo)

print("Total Words for the Lord of the Rings Trilogy")

print(tolkien["The Fellowship of the Ring"]+tolkien["The Two Towers"]+tolkien["The Return of the King"])

<!-- #endraw -->

## Loops and Functions


Computers are much better at doing simple repeatable tasks than humans are so to leverage this advantage, we will cover two different ways of writing these kind of repeatable instructions.


### Loops


Loops are a way of having Python complete a task over and over.

The most common form if a **for** loop. A **for** loop completes a task a fixed number of times by iterating a variable over the members of a sequence in order.

```python
#Example for loop
for i in [0,1,2]:
    print(i)
```

*__Note__: The indention is important, it tells Python that the line *print(i)* belongs inside the loop.*


### Functions


Sometimes it would be nice to be able to save a group of instructions in a single block, that way we won't need to rewrite several lines of code each time we want to do that set of operations.

To do this we define a **function**.

Functions allow us to define a more complicated set of instructions as a single entity and call that entire block of code directly.

Functions are defined (*def*), named (lowercase is a standard practice) and accept arguments (). They then can return a value if needed (*return*).

Python has several built in functions (*print()* is a good example) and when you combine external packages and libraries, there are functions for just about everything you could think of.

```python
# Example function
def square_me(n):
    return n*n
```

```python
square_me(4)
```

>**Think**: What is something that you do over and over again?
>Is that task something you could use a *loop* for or a *function* for?


>Try to build your own loop that prints the individual letters in a string. *Hint: Python is clever enough to do this without making a list first*

```python
# for
```

>Try defining your own function that takes 2 arguments and adds them together.

```python
#def add_me
#
#
```

```python
#add_me(7,11)
```

Putting loops and functions together is where python can become very powerful.

```python
# Looping over a function
for i in [0,1,2,3]:
    print(square_me(i)) # note that this is still tabbed in within the for loop
```

```python
# A function with a loop
def print_numbers(start,stop):
    for i in range(start,stop): #Here the range() function gives us all the values from start up to but excluding the stop value
        print(i) # this is indented twice, so Python knows it is within the loop within the function
```

```python
print_numbers(0,4)
```

>Define a function that uses a loop to add the squares of the numbers 0 to n. (e.g. with n = 3, return 0+1+4+9 = 14)


# Libraries


Libraries are pre-written chunks of code designed to be integrated into projects for a specific purpose.  The idea is to keep people from having to reinvent the wheel every time they want to write a program.  When we encounter situations where a libary might be useful, we use the keyword *import* to tell the program that we want to use this pre-existing code.  As an example, in the next section you will use a library called Pandas which helps visualize data and make it easier to digest, which is very useful for us.  Because of this, we will import that code into this program simply by running the cell with the import that goes with that code.  Here is what you will see, only in commented code.

```python
#import pandas as pd

#by using the keyword *as* and giving pandas an alternative name (pd) in this program, it allows us to use the
#functions within pandas while only having to type our pd instead of pandas every time.
```

Most programming languages have libraries that allow you to import code this way, and it will save you a lot of time and allow you to quickly use many new functions that are highly polished.


# DataFrames and Pandas


Now it is time to use what we have learned to start doing some data science.

Pandas is the name of a library in which there are functions and tools for doing operations common in data analysis and data science. One particularly great feature is the DataFrame structure which allows us to work with an object similar to an Excel spreadsheet but with the flexibility and power of Python behind it.

First we will need to import the Pandas library and create a DataFrame. DataFrames are can also be created when you import files (like CSV's) or tables from a database (like SQL).

```python
import pandas as pd
```

```python
#Notice here the data is a dictionary, similar to the one we used above but with the titles and wordcounts as nested lists
d = {"Books":["The Silmarillion","The Hobbit","The Fellowship of the Ring","The Two Towers","The Return of the King"],
     "Words":[130115,95506,187726,156147,137037]
    }
df = pd.DataFrame(d)
df
```

Now we can operate on entire rows or columns in our DataFrame.

```python
df["Books"] #Selecting the column "Books"
```

```python
df[:2] #Selecting the first 2 rows
```

```python
df[2:4] #Selecting rows 2 up to 4
```

```python
df["Words"][2:4] #Selecting the second and third row from the "Words" column.
```

```python
df[2:4]["Words"] #Same result but from the opposite order
```

You can also operate on entire columns in your DataFrame. Just be careful because this can give you unexpected results. Rows are generally more consistent for elements within a DataFrame.

```python
total = sum(df["Words"])
total
```

> Use slicing to determine how much longer is the "Lord of the Rings" Trilogy than the other two books combined?


## More Complex Data


To look at slightly more complex data operations, we need more complex data.

Below we have all the chapters from the Hobbit and Lord of the Rings books along with their word counts. Notice that each chapter is a list of information and then each of those list is an element in a larger list.

```python
chapters = [[0,1,'An Unexpected Party',8638,0],
            [0,2,'Roast Mutton',5257,0],
            [0,3,'A Short Rest',2876,0],
            [0,4,'Over Hill and Under Hill',4034,0],
            [0,5,'Riddles in the Dark',6967,0],
            [0,6,'Out of the Frying Pan into the Fire',6703,0],
            [0,7,'Queer Lodgings',9027,0],
            [0,8,'Flies and Spiders',10223,0],
            [0,9,'Barrels Out of Bond',5833,0],
            [0,10,'A Warm Welcome',3930,0],
            [0,11,'On the Doorstep',3001,0],
            [0,12,'Inside Information',7132,0],
            [0,13,'Not At Home',3909,0],
            [0,14,'Fire and Water',3236,0],
            [0,15,'The Gathering of the Clouds',3362,0],
            [0,16,'A Thief in the Night',2153,0],
            [0,17,'The Clouds Burst',3949,0],
            [0,18,'The Return Journey',2815,0],
            [0,19,'The Last Stage',2461,0],
            [1,-4,'Concerning Hobbits',3406,1],
            [1,-3,'Concerning Pipeweed',600,1],
            [1,-2,'Of the Ordering of the Shire',2431,1],
            [1,-1,'Note on the Shire Records',914,1],
            [1,1,'A Long-expected Party',10012,1],
            [1,2,'The Shadow of the Past',11311,1],
            [1,3,'Three is Company',9763,1],
            [1,4,'A Short Cut to Mushrooms',5957,1],
            [1,5,'A Conspiracy Unmasked',5196,1],
            [1,6,'The Old Forest',6502,1],
            [1,7,'In the House of Tom Bombadil',5501,1],
            [1,8,'Fog on the Barrow-downs',6694,1],
            [1,9,'At the Sign of the Prancing Pony',6251,1],
            [1,10,'Strider',5905,1],
            [1,11,'A Knife in the Dark',9468,1],
            [1,12,'Flight to the Ford',8805,1],
            [1,1,'Many Meetings',9085,2],
            [1,2,'The Council of Elrond',16360,2],
            [1,3,'The Ring goes South',10656,2],
            [1,4,'A Journey in the Dark',11501,2],
            [1,5,'The Bridge of Khazad-dum',5428,2],
            [1,6,'Lothlorien',9387,2],
            [1,7,'The Mirror of Gladriel',6896,2],
            [1,8,'Farewell to Lorien',6174,2],
            [1,9,'The Great River',7218,2],
            [1,10,'The Breaking of the Fellowship',6305,2],
            [2,1,'The Departure of Boromir',3397,3],
            [2,2,'The Riders of Rohan',11133,3],
            [2,3,'The Uruk-hai',7854,3],
            [2,4,'Treebeard',12876,3],
            [2,5,'The White Rider',8856,3],
            [2,6,'The King of the Golden Hall',9303,3],
            [2,7,"Helm's Deep",7575,3],
            [2,8,'The Road to Isengard',7899,3],
            [2,9,'Flotsam and Jetsam',7789,3],
            [2,10,'The Voice of Saruman',5663,3],
            [2,11,'The Palantir',6325,3],
            [2,1,'The Taming of Smeagol',8375,4],
            [2,2,'The Passage of the Marshes',7357,4],
            [2,3,'The Black Gate is Closed',5881,4],
            [2,4,'Of Herbs and Stewed Rabbit',6975,4],
            [2,5,'The Window on the West',10120,4],
            [2,6,'The Forbidden Pool',5179,4],
            [2,7,'Journey to the Crossroads',4266,4],
            [2,8,'The Stairs of Cirith Ungol',6793,4],
            [2,9,"Shelob's Lair",5209,4],
            [2,10,'The Choices of Master Samwise',7322,4],
            [3,1,'Minas Tirith',13100,5],
            [3,2,'The Passing of the Grey Company',8586,5],
            [3,3,'The Muster of Rohan',6951,5],
            [3,4,'The Siege of Gondor',11793,5],
            [3,5,'The Ride of the Rohirrim',4358,5],
            [3,6,'The Battle of the Pelennor Fields',5225,5],
            [3,7,'The Pyre of Denethor',3736,5],
            [3,8,'The Houses of Healing',6731,5],
            [3,9,'The Last Debate',5416,5],
            [3,10,'The Black Gate Opens',5204,5],
            [3,1,'The Tower of Cirith Ungol',9721,6],
            [3,2,'The Land of Shadow',8446,6],
            [3,3,'Mount Doom',7777,6],
            [3,4,'The Field of Cormallen',4721,6],
            [3,5,'The Steward and the King',7639,6],
            [3,6,'Many Partings',7440,6],
            [3,7,'Homeward Bound',4106,6],
            [3,8,'The Scouring of the Shire',11296,6],
            [3,9,'The Grey Havens',4791,6]
           ]
```

Now we can turn the list of the lists into a dataframe. We have also named our columns. This isn't necessary but it does make things clearer to work with.

```python
cols = ['CollectionNum','ChapterNum','ChapterName','WordCount','BookNum']
data = pd.DataFrame(chapters, columns=cols)
```

```python
data
```

Now we might want to apply the names of each of the traditional "books" you might think of when you think about the Lord of the Rings. To do this we need to use a function that is very powerful and flexible: [apply](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html). This function will allow us to apply an operation or function to each value in a column and save it into a new column. In this example, our "function" is using our *CollectionNum* to reference a book name in our list *titles*.


The structure of the apply function is: `apply(lambda *variable* : *function*(*variable*) )`
Where the variable represents the value in each row and the opertaion of function will return a value that can be stored in our new column.

```python
titles = ['The Hobbit','The Fellowship of the Ring', 'The Two Towers', 'The Return of the King']
data['CollectionName']=data['CollectionNum'].apply(lambda x: titles[x])
```

> Can you use apply to estimate the time it takes to read each chapter? How long would it take to read all the chapters? Assume someone reads at 225 words per minute.

```python

```

## [GroupBy](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html)


Now that we have data for each of the chapters, we can group them using groupby. This lets us do aggregate operations like "add all the wordcounts for each book" or "count how many chapters there are in each book".

Groupby is a powerful tool but if you don't understand your data, it can quickly introduce errors.

```python
data.groupby(by='CollectionName').count()
```

> What happened here? Why are all the values in a row the same?

```python
data.groupby(by='CollectionName').sum()
```

> What happened here? Explain where these values came from.


## Selecting (Advanced Slicing)


You can select slices of your dataframe using conditional logic as well. Conditional logic means determining if a condition is `True` or `False` and often relies on operations like: equals `==`, not `!`, and `&`, or `|`.

```python
df
```

```python
# Select values based on exact matches
df[df['Books']=='The Hobbit']
```

```python
# Select values by negating a match
df[df['Books']!='The Hobbit']
```

```python
# Select values containing substrings
df[df['Books'].str.contains('ing')]
```

```python
# Select values on multiple conditions using different columns
df[(df['Books'].str.contains('ing')) & (df['Words']>150000)]
```

>Can you select the books with a lowercase 'r' in their name but not a capital 'R'? *Hint: you can use "~" to negate a function*

```python

```

## Joining


You can also merge 2 dataframes if you want. Merging allows you to combine datasets in new ways and is a great tool to have when working with complex datasets.


First we need a second dataframe to work with. Here, we have made a dataframe with the publication year of each of of our Tolkien books.

```python
df
```

```python
dates = pd.DataFrame({'Name':df['Books'],'Year':pd.Series([1977,1934,1954,1954,1954])})
dates
# NOTE: We named our column 'Name' for instructional purposes, but a better name would be 'Books' so that it matches my other dataframe.
#       Typically you want to use a unique identifier in your data and then merge based on that column.
```

Now we can merge our new dates dataframe with our existing dataframe.

We have done an inner join (only rows that match in both dataframes will appear in our join) where the column in the left dataframe is called "Books" and the column in the right dataframe is called "Name".

More documentation on merging dataframes can be found [here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html).

```python
pd.merge(df,dates, left_on="Books", right_on="Name", how = 'inner')
```

Notice that our merge duplicated our matching column because they had different names. This would not happen if we had the same name for columns in both dataframes. However, will not always be the case, so you can clean up your dataframe by dropping one of the redundant columns.

```python
merged = pd.merge(df,dates, left_on="Books", right_on="Name", how = 'inner').drop(columns=['Name'])
merged
```

> 1) Assuming Tolkien wrote consistently, how many words per year did he write between the publication of "The Hobbit" and the "The Lord of the Rings" trilogy?
> 2) The trilogy and the rlease of "The Silmarillion"?
> 3) Using those rates, predict when he might have started writing "The Hobbit".


# Plotting


Visualizing data is incredibly important when trying to convey findings. There are several libraries available for doing data visualization. Pandas has some built in plotting functionality, but we have provided access to MatPlotLib as well.

```python
# This is only needed in this case because we wanted to show the names of the books. You could make a similar plot in Pandas.
import matplotlib as plt
%matplotlib inline
# This allows the plot to be shown inline in the notebook
```

```python
plot = df.plot(kind='bar') # we are setting the type of plot to a bar graph
plot.set_xticklabels(df['Books']); #This lets us rename the x axis labels
```

## More Complex Plotting


Lastly, we can combine several of the things we have learned into a single plot. Here we can group each book together and then look at the word counts by chapter throughout the story.


First, we want to come up with a way to step through the books in a linear way. We have provided a few ways to do this in increasing complexity.

```python
# Simple - add the collection number to the chapter number divided by 10
#data['BookChapter'] = data['CollectionNum']+0.1*data['ChapterNum']

# Much better - add the book number to the chapter number divided by 10
#data['BookChapter'] = data['BookNum']+0.1*data['ChapterNum']

# Best but complicated - add the book number to the chapter number scaled by 1/n where n is the max number of chapters in that book.
data['BookChapter']=data.apply(lambda x: x['BookNum']+(1/data.groupby(by='BookNum').max()['ChapterNum'][x['BookNum']])*x['ChapterNum'], axis=1)
```

```python
groups = data.groupby("CollectionName")

for name, group in groups:

    plt.pyplot.plot(group["BookChapter"], group["WordCount"],label=name)

plt.pyplot.legend()

```

 Notice that the prologue materials in *The Fellowship of the Ring* cause it to overlap with the *Hobbit*. If we wanted to resolve this, we would need to revisit our conventions in our data.


> 1) Generate a bar graph showing the word length of each chapter in our data set.
> 2) Look in the documentation for [pandas visualization](https://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html) and learn how to change the color of the bars in your bar graph.

```python

```
