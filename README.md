# learning-python

## Packages
Built-in functions are at: https://docs.python.org/3/library/index.html
If you import a package you MUST use the package name as a prefix to its functions (equivalent to optional use of namespace in R).
You can import individual functions from a package eg. `rom numpy import arange` but for clarity not recommended.

```python
import numpy
# Option to give the package a custom name using eg. import numpy as np

x = numpy.arange(0, 5, 0.1)
print(x)
```

To view all the functions available in a package press Tab after the `numpy.`  
To see https://numpy.org/doc/stable/genindex.html

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

## PANDAS
The PANDAS package allows you to create dataframes - A dataframe is a collection of lists.  
Panda dataframes have their own methods eg. `.head()`

### Import data as a dataframe
```python
import pandas as pd

titanic = pd.read_csv('../Data/titanic.csv')
titanic.head()
```

### Filtering
```python
# Filtering a dataframe using base python syntax
titanic[(titanic['pclass'] == 1) & (titanic['sex']== 'female')]

# Alternatively this can be simplified using the .query method
titanic.query('pclass == 1 & sex == "female"')

#Nb. there is a dataframe method called .filter() but this is for selecting column
```

### Creating new variables
```python
# Creating new variables using base python syntax
cond = titanic['sex'] == 'female'
titanic['female'] = cond.astype(int)
titanic['family_size'] = titanic['sibsp'] + titanic['parch'] + 1
titanic['embarked_city'] = titanic['embarked'].map({'S':'Southampton','C':'Cherbourg','Q':'Queenstown'})

# Alternatively use .assign() for similar syntax to mutate
titanic = titanic.assign(
    female2 = titanic['sex'] == 'female',
    family_size2 = titanic['sibsp'] + titanic['parch'] + 1,
    embarked_city2 = titanic['embarked'].map({'S':'Southampton','C':'Cherbourg','Q':'Queenstown'})
)

titanic.head()
```
