# Python Lists

#### built-in dynamic sized array (automatically grows and shrinks)
#### A list may contain mixed type of items, this is possible because a list mainly stores references at contiguous locations and actual items maybe stored at different locations.

- list can contain duplicate items
- list in python are mutable. 
- items in List can be done directly using their position (index), starting from 0.
- list are maintained in order of added.


```sh

a = [10,20,"gfg",True,40]
print(a[0]) #10
print(a[2]) #gfg
print(type(a[2])) # str

```

#### Adding Elements into List

* append(): Adds an element at the end of the list.
* extend(): Adds multiple elements to the end of the list.
* insert(): Adds an element at a specific position.

```sh
a =[]
# Adding 10 at the end of list
a.append(10)

# Inserting 5 at index 0
a.insert(0,5)

# Adding multiple elements  [15, 20, 25] at the end
a.extend([15,20,25])

```

#### Removing Elements from List
* remove(): Removes the first occurrence of an element.
* pop(): Removes the element at a specific index or the last element if no index is specified.
* del statement: Deletes an element at a specified index.

```sh
a= [10,30,40,50,"gfg"]

a.remove(30)   # Remove 30 @the 1st occurance
a.pop(1)       # Remove value @ index 1 i.e 30
del a[0]       # Remove value @ index 0 i.e 10
```

### Iterating Over Lists

<!-- Using for loop -->
```sh
a= [1,2,3]

for item in a:
    print(item)
# output
1
2
3

```
### Nested Lists in Python
```sh

matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Access element at row 2, column 3
print(matrix[1][2]) 
#output
6
```
## Examples

### Remove duplicate 
Which Method to Choose?
* reverse(): Use for in-place modification when we don’t need the original list
* List Slicing ([::-1]): Use to quickly create a reversed copy without modifying the original list
* reversed(): Ideal for creating an iterator to reverse without modifying the original list and if we need an iterable for further operations.
* Loop (In-Place): Use for more control during in-place reversal and especially if additional conditions are involved.


```sh
a=[1,2,3,3,4,5,5,6]
#Create an empty list to store unique values
res = []
for  i in a:
    if i not in res:
        res.append(i)
print(res)

#output
# Remove duplicates by converting to a set
[1, 2, 3, 4, 5]
```
### Reversing a list in python
```sh
a=[1,2,3,3,4,5,5,6]
a.reverse()
print(a)
```

### Merge Two List
```sh
a= [1,2,3]
b= [4,5,6]
c= a+b
```
### Sort a list in python

```sh
a= [5,3,8,10,4]
* a.sort() - sorts the list
* a.sort(reverse= True)  - Sorts the list in reverse order
* s= sorted(a,reverse=True) - - Sorts the list in reverse order

print(s)
```