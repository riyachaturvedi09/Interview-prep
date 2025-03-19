# Python OOPs Concepts

## Python Classes and Objects

class in python is user defined template for creating objects. 
It binds data & functions together

```sh
class Employee:
    name = "harry"  #class attribute
    language = "py"
    def getinfo(self):
        print(f"The language is {self.language} and the name is {self.name}")

    @staticmethod
    def greet(self):
        print("Good Morning, Sir")
Anshul = Employee()

Anshul.name = "anshu" #instance attribute
Anshul.language = "java" #instance attribute

# Anshul.getinfo() 

Anshul.greet(Anshul)
print(Anshul.name) 
print(Anshul.language)

#output
Good Morning, Sir
anshu
java
```

### Using __init__() function
These methods with '__' called as dunder method  & are called automatically

```sh
    def __init__(self):
        print("this is init method")
```
