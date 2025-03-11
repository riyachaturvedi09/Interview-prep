## Lookups-Index-Match functions

##### INDEX MATCH – a combination of lookup functions that are more powerful than VLOOKUP
=VLOOKUP – a lookup function that searches vertically in a table
=HLOOKUP – a lookup function that searches horizontally in a table
=INDEX – a lookup function that searches vertically and horizontally in a table
=MATCH – returns the position of a value in a series
=OFFSET – moves the reference of a cell by the number of rows and/or columns specified

#### Index-Match

```sh
=INDEX(Return-col, MATCH(lookupvalue,lookupArray,0))
```
#### XLOOKUP - works left to right & viceversa

```sh
=XLOOKUP(lookup_value,lookup_column,return_column)
```

#### VLOOKUP - works left to right but not viceversa

```sh
=VLOOKUP(lookup_value,lookup_array,return_array,0)
```
