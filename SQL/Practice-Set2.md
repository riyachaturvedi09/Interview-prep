## Medium Difficult

### Problem 1- 
Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output should consist of four columns (Doctor, Professor, Singer, and Actor) in that specific order, with their respective names listed alphabetically under each column.
Note: Print NULL when there are no more names corresponding to an occupation

```sql
SELECT [DOCTOR],[PROFESSOR],[SINGER],[ACTOR] FROM 

-- from the below partition query will get the name & occupation sorted and partitioned.
(
    SELECT NAME, OCCUPATION,
    ROW_NUMBER() OVER(PARTITION BY OCCUPATION ORDER BY NAME) AS RN
    FROM OCCUPATIONS
) AS TB


-- to show the output in the pivot from -
PIVOT(
    MAX(NAME)
    FOR OCCUPATION IN ([DOCTOR],[PROFESSOR],[SINGER],[ACTOR])
) AS PVT

```

### Problem 2- 
You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.
```sh 
BST Table Structure:
+----+------+
| N  |  P  |
+----+------+
| 1  | 2   |  -- 
| 3  | 2   |  -- 
| 2  | 5   |  -- 
| 6  | 8   |  -- 
| 9  | 8   |
| 8  | 5   |  
| 5  | Null| -- Root node
+----+-----
```

```sql
SELECT N, CASE
    WHEN P IS NULL THEN "Root" 
    WHEN N NOT IN (SELECT DISTINCT P FROM BST WHERE P IS NOT NULL) THEN "Leaf" 
    ELSE "Inner"
    END
FROM BST
ORDER BY N

-- root is always be null cause it doesn't any parent
-- here creating a set of unique parents from P, if N is not there then its a leaf else its a inner
-- output

N -ROL
1 -leaf
3 -leaf
2 -Inner
6 -Leaf
9 -Leaf
8 -Inner
5 -root

```