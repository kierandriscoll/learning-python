# learning-python

## Packages
Built-in functions are at: https://docs.python.org/3/library/index.html
If you import a package you MUST use the package name as a prefix to its functions (equivalent to optional use of namespace in R).
You can import individual functions from a package eg. `from numpy import arange` but for clarity not recommended.

```python
import numpy
# Option to give the package a custom name using eg. import numpy as np

x = numpy.arange(0, 5, 0.1)
print(x)
```

To view all the functions available in a package press Tab after the `numpy.`  
To see https://numpy.org/doc/stable/genindex.html
matplotlib
seaborn
bokeh
numpy
scipy
pandas
tkinter
nltk
gensim
sklearn


## Functions and methods
Some Python objects (like in Javascript) can have methods eg. `object.method()`. Methods can be chained together eg. `object.method1().method2()`
Nb. Some methods names have . in their names.

```python
x = "test1"

# Strings have their own methods for certain operations eg. uppercase. methods can be chained.
x.upper()

# But to do other operations you need regular functions eg. string length
len(x)
```

## Lists (a.k.a array/vector)
A Python list has the same notation as an array in Javascript.
Lists have their own methods for certain operations, and they can be chained.

```python
my_list = ["Mon", "Tues", "Weds", "Thurs", "Fri", "Sat"]
```

Methods `.append` and `.extend` cna be used to add item to a list:
```python
# Add a new item to the list
my_list.append("Sun")
print(my_list)

# Append 2 lists together  
my_list2 = ["A", "B", "C"]
my_list.extend(my_list2)
print(my_list)

len(my_list)
```

```python
# Join ordered lists (or tuples) together
numberList1 = [1, 2, 3]
numberList2 = ["A", "B", "C", "D"]
print(list(zip(numberList1, numberList2)))
```

## Dictionaries
A Python dictionary has the same notation as Javascript Object.
Dictionaries have their own methods for certain operations, and they can be chained.
```python
dict = {x:150, y:21, z:"word"}
```

## User defined Functions

```python
def myfunction(x):
    return (x**2)

myfunction(4)
```

## Looping
Basic looping can be done using `for .. in` 
```python

array = [1,2,3,5,8,13]
array2 = []
for i in array:
    array2.append(i**2)
print(array2)    
```

You may also be able to use the `map()` function to apply a function to each item in an array. 
```python
def myfunction(x):
    return (x**2)
    
array2 = list(map(myfunction, array))
print(array2)
```

## Calling other scripts
If you have modular scripts (eg. myscript.py) and want to run them in regular Python: 
```python
import myscript
```
If you are using a Jupyter notebook then use:
```python
%run myscript
```


## PANDAS
The PANDAS package allows you to create dataframes - A dataframe is a collection of lists.  
Panda dataframes have their own methods eg. `.head()`

### Import data as a dataframe
```python
import pandas as pd

titanic = pd.read_csv('../Data/titanic.csv')
titanic.head()
```

### Accessing columns
You can use bracket notation to reference columns (this is clearer to read but longer to type):
```python
titanic["pclass"]
```
Columns are also attributes of the dataframe so you can also use dot notation (although this may be confusing if chaining with other methods):
```python
titanic.pclass
```

### Renaming
```python
titanic.rename(columns = {
  "parch" : "Parents_Children"
})
```
### Drop columns
```python
titanic = titanic.drop(columns=["cabin","boat"])
```

### Filtering
```python
# Filtering a dataframe using base python syntax
titanic[(titanic.pclass == 1) & (titanic.sex == 'female')]

# Alternatively this can be simplified using the .query method
titanic.query('pclass == 1 & sex == "female"')

#Nb. there is a dataframe method called .filter() but this is for selecting columns
```

### Creating new variables
```python
# Creating new variables using base python syntax - Always use [] for the new variable name:
cond = titanic.sex == 'female'
titanic['female'] = cond.astype(int)
titanic['family_size'] = titanic.sibsp + titanic.parch + 1
titanic['embarked_city'] = titanic.embarked.map({'S':'Southampton','C':'Cherbourg','Q':'Queenstown'})

# Alternatively use .assign() for similar syntax to mutate
titanic = titanic.assign(
    female2 = titanic.sex == 'female',
    family_size2 = titanic.sibsp + titanic.parch + 1,
    embarked_city2 = titanic.embarked.map({'S':'Southampton','C':'Cherbourg','Q':'Queenstown'})
)

titanic.head()
```

### Changing values with conditions
```python
titanic.loc[titanic.id == 5, 'existing_var'] = "value if 5"
```

### String methods
String columns have string functions/methods under the **.str** namespace. 
```python
titanic.pclass.str.lower()
titanic.pclass.str.strip()
titanic.pclass.str.split()
```

**.str** can be used to extract substrings (Nb. Python indexing starts with 0):
```python
# Extract the first 4 characters
titanic.embarked.str[0:4] 

# Extract the first 4th, 5th and 6th characters
titanic.embarked.str[3:6] 
```

**.str.replace** will replace one string with another. 
```python
titanic.embarked.str.replace('-', '')

# You can include regex in the argument to match multiple characters/strings:
titanic.embarked.str.replace("[.,:;'()?!]", "") 
titanic.embarked.str.replace("red|blue", "green") 
```

### Summary stats
Dataframe columns have a `.value_counts()` method that producing a freuency count:  
```python
titanic.embarked.value_counts()
```

### apply functions to a column
Pandas adds an **apply** function that can be applied to each item in a column   
```python
titanic.embarked.apply(lambda x: x.lower())  # In this case it would be simpler to use titanic.embarked.str.lower()
```
**apply** is most useful if you want to apply a user-defined function:
```python
def myfunction(x):
    # x = process1
    # x = process2
    # x = process3
    return x

titanic.embarked.apply(lambda x: myfunction(x))
```


### Saving a dataframe
A dataframe has various **methods** that will save it in different formats including:
```python
titanic.to_csv('savetitanic.csv')
titanic.to_excel('savetitanic.xlsx')
titanic.to_feather('savetitanic.ft')
titanic.to_json("titanic.json", orient='records')
```
