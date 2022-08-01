# Python Basics

## Operators

### Arithmetic Operators
1. Addition operator
```python
a + b
```
2. Subtraction operator
```python
a - b
```
3. Multiplication operator
```python
a * b
```
4. Division operator (returns quotient)
```python
a / b
```
5. Floor division operator (returns quotient without decimal part)
```python
a // b
```
6. Modulus operator (returns remainder)
```python
a % b
```
7. Exponential operator
```python
a ** b
```

### Comparison Operators

#### Comparison operators that compare the values of objects:
1. Equal to operator
```python
a == b
```
2. Not equal to operator
```python
a != b
```
3. Greater than operator
```python
a > b
```
4. Less than operator
```python
a < b
```
5. Greater than or equal to operator
```python
a >= b
```
6. Less than or equal to operator
```python
a <= b
```

#### Comparison operator that compares the identity of objects:
1. `is` keyword
```python
a is b
```

## Variables
- Variables are defined when they are to be used, they need to be assigned a value at the time of definition.
- Data type can not be explicitly specified, it is implied through the data type of the value assigned to the variable.
```python
variable_name1 = 'howdy' # string
variable_name2 = 8983 # int
variable_name3 = 34.88379 # float
variable_name4 = False # bool
variable_name5 = None; # None type
```
- Variable names can begin with letters or underscore (`_`).
- Variable names can contain letters, numbers and underscore; no other special characters are permitted.
- The convention is to use `snake_case` for variable names, `PascalCase` for class names and exception names and `SCREAMING_SNAKE_CASE` for constants

### Underscore (`_`) in Python
- Uses of single underscore:
  1. For accessing the result of last executed expression in python interpreter
  ```python
  >>> 8 + 2
  10
  >>> _ + 6
  16
  ```
  2. For ignoring values
  ```python
  a, b, _ = (1, 2, 3)
  ```
  3. For indicating a private member of a class
- Uses of double underscore:
  1. Python uses leading and trailing double underscores (`__name__`) to identify in-built attributes and methods

## Displaying Output and Accepting Input
- `print()` is used to display an output
```python
print("hello")
```
- `input()` is used to accept an input
```python
name = input("Enter your name: ")
```
- This stores the value entered by the user into the variable.
- Note that the input function returns the users input as a string.

## Modules
- Modules are also called libraries in other languages. They contain classes and functions which provide additional functionality.
- To use a module it has to be imported into the program using the `import` keyword.
- While using a class or function from within a library, you need to specify which module it belongs to using the dot operator (`.`)
```python
import math
print(math.sqrt(25)) # 5.0
```
- To import specific classes or functions from a module the `from` keyword can be used. This also means the imported class or function can be used without the dot operator (`.`)
```python
from math import pow
print(sqrt(25)) # 5.0
```
- To import everything from a module the `*` symbol is used.
```python
from math import *
print(sqrt(25)) # 5.0
```
- Modules or components of the module can also be imported under an alias name.
```python
import math as m
print(m.sqrt(16)) # 4.0
from math import sqrt as sr
print(sr(25)) # 5.0
```


## Strings
- String object is an immutable sequence.
- A string is enclosed in single quotes (`'`) or double quotes (`"`).
```python
my_string = 'hey there'
my_string = "he's a genius"
my_string = 'he\'s a genius'
```
- We can insert symbols and formatting using a backslash ( `\`) also known as escape character. `\'`, `\\`, `\n`, etc. are escape characters.

### Escape Characters
```python
print('what\'s up')
# what's up
print('\\ is an escape character')
# \ is an escape character
print('line one.\nline two.')
# line one.
# line two.
```

## Lists
- A list is a collection of elements in a sequence.
```python
list_name = [element_1,element_2,element_3]
```
- Lists are not homogeneous. Which means list elements can be of any data type - numeric, strings, even objects.
- Lists are dynamic and mutable. They can be changed after their definition. We can assign new values to list elements. We can also insert new elements into the list.

### Indexes
- List index starts from 0.
```python
my_list = [element_1,element_2,element_3,element_4]
```

| Elements: | element 1 | element 2 | element 3 | element 4 |
|:-----------:|:------------:|:------------:|:------------:|:------------:|
| Indexes:  |     0     |     1     |     2     |     3     |

- List elements can be referred to by using negative indexes as well.

| Elements: | element 1 | element 2 | element 3 | element 4 |
|:------------|:------------:|:------------:|:------------:|:------------:|
| Indexes:  |     -4     |     -3     |     -2     |     -1     |

```python
my_list = ['element1','element2','element3','element4']
print(my_list[0]) # element 1
print(my_list[2]) # element 3
print(my_list[-1]) # element 4
print(my_list[-3]) # element 2
```

### Slicing
- Creating a subsection of a sequence is called slicing.
```python
list_name[slice_beginning_index:slice_ending_index:index_jump]
```
- Default value of beginning index is 0, and default value of ending index is last index of the sequence plus 1.
- Default ending index can be thought of the as the length of the sequence (number of elements in the sequence).
- The element at the ending index is not included in the slice.
- Index jump is used to specify the step size, its default value is 1. Step size can also be negative.
- The index specified when slicing can be an index that is not present in the sequence. In such cases the default index is taken.
```python
my_list = [1,2,3,4,5]
print(my_list[0:4]) # [1, 2, 3, 4]
# Note that even though the last index in the list is 4, the above slice does not include the entire list.
print(my_list[1:3]) # [2, 3]
print(my_list[:3]) # [1, 2, 3]
print(my_list[2:]) # [3, 4, 5]
print(my_list[:9]) # [1, 2, 3, 4, 5]
# Note that 9 is not an index in the list.
```
- Slices can also be created using negative indexes.
```python
my_list = [1,2,3,4,5]
print(my_list[-4:-2]) # [2, 3]
print(my_list[:-1]) # [1, 2, 3, 4]
# Note that even in negative indexes the ending index is not included.
print(my_list[-8:]) # [1, 2, 3, 4, 5]
# Note that -8 is not an index in the list.
```
- All of the above examples work with strings as well.

#### Assigning list elements using slices:
- A slice of a list can be used to assign new data to the list elements.
```python
my_list = [1,2,3,4,5]
my_list[2:] = [6,7,8]
print(my_list) # [1, 2, 6, 7, 8]
my_list[-3:-1] = [4,6]
print(my_list) # [1, 2, 4, 6, 8]
my_list[:2] = [-4,-2,0]
print(my_list) # [-4, -2, 0, 4, 6, 8]
my_list[3:5] = []
print(my_list) # [-4, -2, 0, 8]
```

> **NOTE:** Assigning a value to an element or multiple elements using indexing or slicing like we have done above is not possible for strings. You will get such an error- `TypeError: 'str' object does not support item assignment`

### `in` Keyword
- `in` keyword has 2 purposes:
  1. to check if a value is present in a sequence (list, strings, etc.).
  2. to iterate through a sequence using for loop.
- `in` returns _True_ if the value is present and _False_ if the value is not present.
- `not in` is also a keyword, it returns _True_ if the value is not present and _False_ if the value is present.

### List Functions
- `len()`,`max()` and `min()` are inbuilt functions for sequences.
- `len()`: Finds the length of a sequence (number of elements in a sequence).
- `max()`: Finds the maximum value from the elements in a sequence.
- `min()`: Finds the minimum value from the elements in a sequence.
- `sum()`: Finds the sum of all elements in a sequence (the `+` operator for the datatypes should be supported).
```python
my_list = [1,2,3,4,5]
print(len(my_list)) # 5
print(len([23,643,32,743,52,21,53])) # 7
print(len('maggi noodles')) # 13
print(max(my_list)) # 5
print(max([23,643,32,743,52,21,53])) # 743
print(min('ABCXYZabcxyz')) # z
print(min(my_list)) # 1
print(min([23,643,32,743,52,21,53])) # 21
print(min('ABCXYZabcxyz')) # A
print(sum(my_list)) # 15
```
- When using `max()` and `min()` functions on strings, the _descending_ order (largest to smallest) is as follows:
  - Lowercase letters, from `z` to `a`.
  - Uppercase letters, form `Z` to `A`.
  - Special symbols, `.` then `,` then ` ` (space).

## Tuples
- A tuple is also a sequence similar to a list but it is immutable. Which means that once a tuple has been created it cannot be edited.
- Since they are immutable they only support 2 of the sequence methods, i.e., `count()` and `index()`.

## Sets
- A set is an unordered collection of unique elements.
- A set can be created using curly brackets (`{}`).
```python
my_set1 = {77, 20, 104, 65, -16, -16}
print(len(my_set1)) # 5
print(my_set1) # {65, 104, 77, -16, 20}
# Note that the duplicate value was omitted
my_set2 = {'jello', 'mellow', 'cello'}
print(my_set2) # {'cello', 'mellow', 'jello'}
my_set3 = set({0: "zero", 0.25: "quarter", 0.5: "half", 0.75: "three quarters", 1:"one"})
print(my_set3) # {0, 0.25, 0.5, 0.75, 1}
my_set4 = set('aeiou')
print(my_set4) # {'u', 'o', 'e', 'a', 'i'}
```
- Indexing and slicing doesn't work in sets.
```python
my_set = {1,2,3}
my_set[1] # TypeError: 'set' object is not subscriptable
```
- Note that when you print sets the output will not always be ordered in the same way since it is an unordered collection.

## Dictionaries
- A dictionary is an unordered collection of elements.
```python
dictionary_name = {key_1:value_1,key_2:value_2,key_3:value_3}
```
- Each element contains a `key:value` pair.
- A value can be of any datatype and can repeat, whereas a key needs to be of an immutable datatype (like `str`,`int`,`tuple`) and unique.
- key has the same function as indexes in lists.

## Concatenation
- `+` is the concatenation symbol.
- It is the operation of combining non-numeric data.
- Concatenation is usually done on strings and lists (or other sequences).
- Concatenation can be  performed on multiple operands.
```python
print('h' + 'i') # hi
txt1 = 'hey, '
txt2 = 'what\'s up'
print(txt1 + txt2) # hey, what's up
longTxt = '''How\'s it going?'''
print(longTxt + '''Thought we should catch up again..
Hope you have been well.''')
# How's it going?
# Thought we should catch up again..
# Hope you have been well.
```
```python
print([1,2,3]+[4]) # [1, 2, 3, 4]
my_list = [10,9,8,7,6]
another_list = [5,4,3,2,1]
print(my_list + another_list) # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
print(my_list + [5] + [4] + [3] + [2,1]) # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

## Methods
- Methods are used to modify and interact with objects, they are similar to functions but are always called using an object.
- When using a method belonging to an object, the object is specified using a dot (`.`).

### String Methods
- `split()`: splits the string into parts and returns a list containing the parts of the string. It takes 2 parameters - first the separator character to divide the string into parts (default is white spaces), second is the maximum number of splits to make.
```python
my_string = 'hilly woah:billy he:willy go:nilly yay'
print(my_string.split()) # ['hilly', 'woah:billy', 'he:willy', 'go:nilly', 'yay']
print(my_string.split(':')) # ['hilly woah', 'billy he', 'willy go', 'nilly yay']
print(my_string.split(':',2)) # ['hilly woah', 'billy he', 'willy go:nilly yay']
```

### List Methods
- `append(new_element)`: inserts an element at the end of the list.
- `insert(index, new_element)`: inserts an element into the list at a particular index.
- `remove(element_to_remove)`: finds and removes an element from the list.
- `count(element_to_search)`: counts the number of occurrences of an element in the list.
- `pop(index=-1)`: returns and removes the last element from the list by default, if an index is mentioned the element at that index is returned and removed instead.
- `extend(sequence)`: inserts all the elements of a specified sequence at the end of the list.
- `sort(reverse=False)`: sorts the elements of the list in ascending order by default.
```python
my_list = [1,2,3,4,5]
my_list.append(4)
print(my_list) # [1, 2, 3, 4, 5, 4]
my_list.insert(2, 4)
print(my_list) # [1, 2, 4, 3, 4, 5, 4]
my_list.remove(4)
print(my_list) # [1, 2, 3, 4, 5, 4]
print(my_list.count(3)) # 1
print(my_list.count(4)) # 2
my_list.extend([10,9,8])
print(my_list) # [1, 2, 3, 4, 5, 4, 10, 9, 8]
my_list.sort(reverse=True)
print(my_list) # [10, 9, 8, 5, 4, 4, 3, 2, 1]
```

### Dictionary Methods
- `get(key, default=None)`: searches a key in the dictionary and returns its value if found else returns `default`.
- `items()`: returns a set-like object containing the items of the dictionary as key-value pairs in tuples, like so, `(key_1, value_1)`.
- `keys()`: returns a set-like object containing the keys of the dictionary.
- `values()`: returns a set-like object containing the values of the dictionary.
```python
my_dict = {'a': 'apple', 'b': 'ball', 'c': 'cat'}
print(my_dict.get('a')) # apple
print(my_dict.get('d', "Invalid key")) # Invalid key
print(my_dict.items()) # dict_items([('a', 'apple'), ('b', 'ball'), ('c', 'cat')])
print(my_dict.keys()) # dict_keys(['a', 'b', 'c'])
print(my_dict.values()) # dict_values(['apple', 'ball', 'cat'])
```

## `del` keyword
- It is used for deleting an element or slice from a mutable sequence, or for deleting an object.
```python
my_str = "abcd"
del my_str[2] # TypeError: 'str' object doesn't support item deletion
del my_str
print(my_str) # NameError: name 'my_str' is not defined
my_lst = [1,2,3,4]
del my_lst[0]
print(my_lst) # [2, 3, 4]
del my_lst[1:]
print(my_lst) # [2]
my_dict = {'a':'apple', 'b':'ball', 'c':'cat', 'd':'dog'}
del my_dict['b']
print(my_dict) # {'a': 'apple', 'c': 'cat', 'd': 'dog'}
```

## Type Casting
- Type casting is the process of converting form one data type to another.
- Common type casting functions are:
  1. `int()`: to convert a string to an int.
  2. `str()`: to convert an object to a string.
  3. `list()`: to convert any iterable to a list.
```python
print(int('980') + int('6')) # 986
int('hi') # ERROR: Invalid literal for int().
print('I\'m ' + str(12) + ' years old.') # I'm 12 years old.
print('Go buy: ' + str(['apples','oranges','grapes'])) # Go buy: ['apples', 'oranges', 'grapes']
print(list([1,2,3,4,5])) # [1, 2, 3, 4, 5]
print(list('hey!')) # ['h', 'e', 'y']
```

## Control Flow Statements
- Control flow or flow of control is the order in which statements are executed. Control flow statements allow us to change the order based on conditions.
- There are 2 main types of control flow statements:
  1. Conditional statements: `if... elif... else` [python does not have an in-built `switch` case].
  2. Loops: `for`(definite iteration) and `while`(indefinite iteration) [python does not have an in-built `do... while` loop].
- Syntax of `if... elif... else`:
```python
if condition1:
	condition1_true_statements
elif condition2:
	condition2_true_statements
else:
	false_statements
```
- Syntax of `for` loop:
```python
for variable_name in sequence_name:
	looping_statements
```
- Syntax of `while` loop:
```python
while condition:
	looping_statements
```
- Blocks of control flow statements are identified by indentation.
- Control flow statements can be nested inside one another.

### Short Hand Statements
1. Short hand `if` statement
```python
if condition: true_statement
```
2. Short hand `if... else` statement
```python
true_statement if condition else false_statement
```

## User Defined Functions
```python
def function_name(arguments):
    statements
```
```python
def display(txt):
    print(txt)
display('hello') # hello
```

### Default Arguments
- It is used to specify a default value to be used when a value is not provided.
```python
def function_name(nondefault_arguments, default_arguments =  default_value):
    statements
```
```python
def add(x, y=2):
    print(x+y)
add(3,7) # 10
add(5) # 7
def display(txt = None):
    print(txt)
display() # None
```
- `None` is `Null`.

### Keyword Arguments
- Used to specify argument name when calling the function.
```python
def function_name(argument_1, argument_2):
    statements
function_name(argument_2 = value, argument_1 = value)
```
```python
def add(x=1, y=2):
    print(x,'+',y,'=',x+y)
add(y=4) # 1 + 4 = 5
add(y=7,x=2) # 2 + 7 = 9
```

<!--Doubts:
1. How do variables and references work in python?
  - For some commonly used integer and string values python keeps them stored indefinitely and whenever a variable is assigned one of these values it instead creates a reference to the value.
  - Also when we do something like `a = b` instead of assigning the value of `a` to `b` it makes `b` a reference to the value stored in `a`, but for some data types like lists it instead makes `b` a reference to `a`.
-->
