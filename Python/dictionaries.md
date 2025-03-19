# Dictionaries in Python
A Python dictionary is a data structure that stores the value in key: value pairs

```sh
d = {1:'Geeks', 2: 'For', 3:'Geeks'}
print(d) 

#output 
d= {1: 'Geeks', 2: 'For', 3: 'Geeks'}

print(d[1]) // print the
#output 
'Geeks'

```
## Removing Dictionary Items
We can remove items from dictionary using the following methods:

* del: Removes an item by key.
* pop(): Removes an item by key and returns its value.
* clear(): Empties the dictionary.
* popitem(): Removes and returns the last key-value pair.

```sh
d= {1: 'Geeks', 2: 'For', 3: 'Geeks'}
val = d.pop(1)
print(val)

#output
'Geeks'
```

## Iteration Through dict
```sh

# defaultly its going to give the key from the dictionary's from key:value pair
for i in d:
    print(i)

# to extract the value from the dictionary
for values in d.values():
    print(values)

# to extract both
for i,j in d.items():
    print(f"{key}: {value}")
```
