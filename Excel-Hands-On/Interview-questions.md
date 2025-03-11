# Intermediate Level Excel Interview Questions

##### Wildcards
```sh
There 3 wildcards- 
* : refers to any number of characters
? : refer to single character
~ : use to identify wildcard character in the text
```

##### absolute, relative, and mixed cell references
```sh
Absolute ($A$1) remains fixed 
Relative (A1) changes
Mixed ($A1 or A$1) is partially fixed.
```

##### IFERROR function
```sh
IFError Func returns customized value whenever a error is occured
```

#####  difference between COUNT, COUNTA, COUNTIF, and COUNTIFS?

```sh
COUNT: Counts numbers
COUNTA: Counts non-empty cells
COUNTIF: Counts based on one condition
COUNTIFS: Counts based on multiple conditions
```

##### difference between SUM(), SUMIF(), and SUMIFS()?

```sh
SUM(A1:A10) - will add all the numbers from cells A1 to A10.
SUMIF(A1:A10, ">5") - will sum all numbers greater than 5 in the range A1 to A10
SUMIFS(A1:A10, B1:B10, "X", C1:C10, ">5") - will sum all numbers in the range A1 to A10 where the corresponding cells in range B1 to B10 equal "X" and those in C1 to C10 are greater than 5.
```

#####  difference SUBSTITUTE() and REPLACE()

```sh
SUBSTITUTE("Hello World", "World", "Excel") : will change "Hello World" to "Hello Excel"

REPLACE("Hello World", 7, 5, "Excel") : starts at the 7th character (W), replaces 5 characters ("World") with "Excel", also resulting in "Hello Excel"
```

##### Extract the domain name from an Email
```sh
=RIGHT(A1,LEN(A1)-FIND("@",A1))
```

##### OFFSET combined with SUM or Average
```sh
TOP4Salary= SUM(OFFSET(B1,0,0,E13))

```