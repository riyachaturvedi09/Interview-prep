## SumIfs & countIfs functions

#### Why Use SUMIFS & COUNTIFS?
##### UMIFS: Adds values based on multiple #####conditions.
##### COUNTIFS: Counts occurrences based on multiple conditions.

#### SUMIFS
##### Want to find the total sales for 'apple' in the 'north region'

```sh
=SUMIFS(B2:B5,A2:A5, 'APPLE',C2:C5,'NORTH')
# here B2:B5 refers to the SumRange then the If condition & A2:A5 refers to the Criterial-1 & C2:C5 refers to 2nd criteria. 
```

#### COUNTIFS
##### Want to find the no of transactions for 'apple'

```sh
=COUNTIFS(B2:B5, 'APPLE')
# here B2:B5 refers to the CountRange then the If condition. 
```

#### WHAT-IF
##### use to perform complex maths calculations

```sh
=COUNTIFS(B2:B5, 'APPLE')
# here B2:B5 refers to the CountRange then the If condition. 
```