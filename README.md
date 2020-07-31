# learning-python

Using Python packages Built in functions are at: https://docs.python.org/3/library/index.html
Need to import any packages you want to use
If you import a package you MUST use the package name as a prefix to its functions (equivalent to optional use use of namespace in R).
Can also import individual functions from a package eg. from numpy import arange, but for clarity not recomended.

```python
import numpy
# Option to give the package a custom name using eg. import numpy as np
# Could also do: from numpy import arange

x = numpy.arange(0, 5, 0.1)
print(x)
```

# To view all the functions available in a package press Tab after the .
# To see https://numpy.org/doc/stable/genindex.html

Python mixes up functions and methods eg. object.method() Nb. Some methods names have . in their names them object.methodroot.method()

```python
x = "test1"

# Strings have their own methods for certain operations eg. uppercase. methods can be chained.
print(x.upper())

# But to do other operations you need regular functions eg. string length
print(len(x))
```

List/Array (same notation as Javascript) Lists have methods.

```python
my_list = ["Mon", "Tues", "Weds", "Thurs", "Fri", "Sat"]

# Lists have their own methods for certain operations. Methods can be chained.

# Add a new item to the list
my_list.append("Sun")
print(my_list)

# Append 2 lists together  
my_list2 = ["A", "B", "C"]
my_list.extend(my_list2)
print(my_list)

print(len(my_list))
```

```python
# Join ordered lists (or tuples) together
numberList1 = [1, 2, 3]
numberList2 = ["A", "B", "C", "D"]
print(list(zip(numberList1, numberList2)))
```

Dictionaries (same notation as Javascript Object) Dictionaries have methods.

```python
dict = {x:150, y:21, z:"word"}
```

User defined Functions

```python
def myfunction(x):
    return (x**2)

myfunction(4)
```

Looping

```python
# Basic looping can be done using for .. in 
array = [1,2,3,5,8,13]
array2 = []
for i in array:
    array2.append(i**2)
print(array2)    

# Alternatively you might be able to use map() to apply a function to ecah item in an array 
def myfunction(x):
    return (x**2)
    
array2 = list(map(myfunction, array))
print(array2)
```

PANDAS Allows you to create dataframe including read/write A python dataframe is a collection of lists(arrays) Panda dataframes have their own methods (eg. .head())

```python
import pandas as pd

titanic = pd.read_csv('../Data/titanic.csv')
titanic.head()
```

```python
# Filtering a dataframe using base python syntax
titanic[(titanic['pclass'] == 1) & (titanic['sex']== 'female')]

# Alternatively this can be simplified using the .query method
titanic.query('pclass == 1 & sex == "female"')

#Nb. there is a dataframe method called .filter() but this is for selecting column
```

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
