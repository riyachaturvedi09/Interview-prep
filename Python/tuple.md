# Tuples in Python
Python Tuple is a collection of objects separated by commas. A tuple is similar to a Python list in terms of indexing, nested objects, and repetition
```sh
(10, 20, 30)
<class 'tuple'>
```
## Immutable in Tuples?

* Like lists, tuples are ordered and we access using index value
* once craeted, No UPDATE
* In Tuple - NO Append & can not be extended
* Can't remove item from tuple once created

```sh

examples:

t = (1,4,7,2,9,4,2)
print(t[1]) // prints '4' as its @ index 1
print(t)   // prints the tuple
t[1] = 100 // this will through error
print(t)
```

## Different Operations Related to Tuples

### Traversing 
```sh
for i in t:
    print(i, end="")

#output
1472942
```

### concatenation
concat operation using '+'
```sh
t1 = (1,4,7,2,9,4,2)
t2 = ('python','geeks')
print(t1+t2)

#output
(1, 4, 7, 2, 9, 4, 2, 'python', 'geeks')
```

### Nesting of tuple

```sh
t1 = (1,4,7,2,9,4,2)
t2 = ('python','geeks')
t3 = (t2, t1)
print(t3)

#output
(('python', 'geeks'), (1, 4, 7, 2, 9, 4, 2))
```

### deleting tuple

t= (0,1)
del t

### Converting a List to a Tuple

```sh
a= [0,1,2]
t = tuple(a)

#output
(0,1,2)
```
