## Python Variables- STRING

####  variables are used to store data that can be referenced and manipulated during program execution. A variable is essentially a name that is assigned to a value.

```sh
#  variables are used to store data that can be referenced and manipulated during program execution. A variable is essentially a name that is assigned to a value.

age = 21
_colour = "lilac"
total_score = 90

```
#### Multiple Assignments
```sh
a = b = c = 100
print(a, b, c) 
```

#### Assigning Assignments

```sh
x, y, z = 1, 2.5, "Python"
print(x, y, z) 
```
#### Type Casting a Variable

```sh
int() – Converts compatible values to an integer.
float() – Transforms values into floating-point numbers. ex. 5.0
str() – Converts any data type into a string.

# Casting variables
s = "10"  # Initially a string
n = int(s)  # Cast string to integer
cnt = 5
f = float(cnt)  # Cast integer to float
age = 25
s2 = str(age)  # Cast integer to string

# Display results
print(n)  
print(f)  
print(s2)  
```

## DATATYPE

```sh
Numeric – int, float, complex
Sequence Type – string, list, tuple
Mapping Type – dict Syntax: 'd = {1: 'Geeks', 2: 'For', 3: 'Geeks'}'
Boolean – bool
Set Type – set, frozenset
Binary Types – bytes, bytearray, memoryview

```

### Sequence Data Types in Python
#### String Data Type

```sh
# Single Line String
S = 'str' or S = "str"

# Multi Line String
S= ''' I am Learning
Python String on GeeksforGeeks''' 

OR

S= """ I am Learning
Python String on GeeksforGeeks """
```

#### Accessing characters in Python String
<!-- Strings are indexed starting from 0 and -1 from end -->
```sh
s = "GeeksforGeeks"

# Accesses first character: 'G'
print(s[0])  

# Accesses 5th character: 's'
print(s[4]) 

```

#### Accessing characters in Python String

```sh
s = "GeeksforGeeks"

# Accesses first character: 'G'
print(s[0])  

# Accesses 5th character: 's'
print(s[4]) 

```

#### String Slicing - extracting a portion of string

```sh
s= "geeksforgeeks"
# Retrieves characters from index 1 to 3: 'eek'
print(s[1:4]) 

# Reverse a string
print(s[::-1])
```

#### Updating a String

```sh
s = "hello geeks"
s1 = s.replace("geeks","geeksforgeeks")

print(s)
print(s1)

# output 
Hello geeks
hello GeeksforGeeks

```

### Formatting Strings

#### Using f-strings - The simplest and most preferred way to format strings is by using f-strings.
```sh
name = "riya"
age = 22
print(f"Name: {name}, Age: {age}")

# Output
Name: Alice, Age: 22
```

#### Using format()

```sh
s= "my name is {} & I'm {} years old".format("Riya","27")
print(s)

#output
My name is Alice and I am 22 years old.
```

#### Using IN 

```sh
s = "hello GeeksforGeeks"
print("Geeks" IN s)
print("Gfg" IN s)

# output 
True
False
```
