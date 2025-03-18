# Python Lists

#### built-in dynamic sized array (automatically grows and shrinks)
#### A list may contain mixed type of items, this is possible because a list mainly stores references at contiguous locations and actual items maybe stored at different locations.

'''sh
- list can contain duplicate items
- list in python are mutable. 
- items in List can be done directly using their position (index), starting from 0.
- list are maintained in order of added.
```

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

