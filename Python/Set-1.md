# Set-1
---

###      **1. Reverse a String**
```python
def reverse_string(s):
    return s[::-1]

print(reverse_string("NAB"))
```

---

###      **2. Check if a Number is Prime**
```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, n):
        if n % i == 0:
            return False
    return True

print(is_prime(7))
```

---

###      **3. Find Duplicate Elements in a List**
```python
def find_duplicate(list):
    list1 = []
    for i in list:
        if i not in list1:
            list1.append(i)
        else:
            return i
    return "No duplicate"
print(find_duplicate([1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,20]))
```

---

###      **4. Count Vowels in a String**
```python
def count_vowels(s):
    return sum(1 for char in s.lower() if char in 'aeiou')

print(count_vowels("Hello NAB"))
```

---

###      **5. Merge Two Sorted Lists**
```python
def merge_lists(lst1, lst2):
    return sorted(lst1 + lst2)

print(merge_lists([1, 3, 5], [2, 4, 6]))
```

---

###      **6. Find Factorial Using Recursion**
```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

print(factorial(5))
```

---

###      **7. Remove Duplicates from a List**
```python
def remove_duplicates(lst):
    return list(set(lst))

print(remove_duplicates([1, 2, 2, 3, 4, 4, 5]))
```

---

###      **8. Check for Palindrome**
```python
def is_palindrome(s):
    s = s.lower().replace(" ", "")
    return s == s[::-1]

print(is_palindrome("NAB BAN"))
```

---

###      **9. Find Missing Number in a List**
```python
def find_missing_number(lst, n):
    return n * (n + 1) // 2 - sum(lst)

print(find_missing_number([1, 2, 4, 5, 6], 6))
```

---

###      **10. Fibonacci Sequence Using Recursion**
```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(7))
```

---

###      **11. Count Occurrences of Elements in a List**
```python
from collections import Counter

def count_elements(lst):
    return Counter(lst)

print(count_elements([1, 2, 3, 4, 2, 1, 5, 2]))
```

---

###      **12. Find Second Largest Number**
```python
def second_largest(lst):
    unique_lst = list(set(lst))
    unique_lst.remove(max(unique_lst))
    return max(unique_lst)

print(second_largest([10, 20, 4, 45, 99]))
```

---

###      **13. Find Intersection of Two Lists**
```python
def intersection(lst1, lst2):
    return list(set(lst1) & set(lst2))

print(intersection([1, 2, 3, 4], [3, 4, 5, 6]))
```

---

###      **14. Find Maximum Consecutive 1s in a Binary Array**
```python
def max_consecutive_ones(nums):
    return max(map(len, ''.join(map(str, nums)).split('0')))

print(max_consecutive_ones([1, 1, 0, 1, 1, 1, 0, 1]))
```

---

###      **15. Validate an Email Address**
```python
import re

def is_valid_email(email):
    pattern = r'^[a-z0-9]+[\._]?[a-z0-9]+[@]\w+[.]\w+$'
    return bool(re.match(pattern, email))

print(is_valid_email("user@nab.com"))
```

---

###      **16. Check Anagram**
```python
def is_anagram(s1, s2):
    return sorted(s1) == sorted(s2)

print(is_anagram("listen", "silent"))
```

---

###      **17. Count Words in a String**
```python
def word_count(s):
    return len(s.split())

print(word_count("Hello NAB World"))
```

---

###      **18. Find Longest Word in a Sentence**
```python
def longest_word(s):
    words = s.split()
    return max(words, key=len)

print(longest_word("Data analyst interview preparation"))
```

---

###      **19. Reverse Words in a String**
```python
def reverse_words(s):
    return ' '.join(s.split()[::-1])

print(reverse_words("Hello NAB"))
```

---

###      **20. Remove Non-Alphanumeric Characters from a String**
```python
import re

def clean_string(s):
    return re.sub(r'[^a-zA-Z0-9]', '', s)

print(clean_string("Hello, NAB! 2025"))
```

---

###      **21. Flatten a Nested List**
```python
def flatten(lst):
    flat_list = []
    for item in lst:
        if isinstance(item, list):
            flat_list.extend(flatten(item))
        else:
            flat_list.append(item)
    return flat_list

print(flatten([1, [2, [3, 4]], 5]))
```

---

###      **22. Find Common Elements in Multiple Lists**
```python
def common_elements(*lists):
    return list(set.intersection(*map(set, lists)))

print(common_elements([1, 2, 3], [2, 3, 4], [3, 4, 5]))
```

---

###      **23. Sort Dictionary by Values**
```python
def sort_dict(d):
    return dict(sorted(d.items(), key=lambda x: x[1]))

print(sort_dict({'a': 3, 'b': 1, 'c': 2}))
```

---

###      **24. Calculate Sum of Digits in a Number**
```python
def sum_of_digits(n):
    return sum(int(digit) for digit in str(n))

print(sum_of_digits(12345))
```

---

###      **25. Generate All Permutations of a String**
```python
from itertools import permutations

def all_permutations(s):
    return [''.join(p) for p in permutations(s)]

print(all_permutations("NAB"))
```

---

###      **26. Remove Elements from a List**
```python
def remove_elements(lst, val):
    return [x for x in lst if x != val]

print(remove_elements([1, 2, 3, 4, 2, 5], 2))
```

---

###      **27. Convert a String to Title Case**
```python
def to_title_case(s):
    return s.title()

print(to_title_case("hello nab"))
```

---

###      **28. Generate Prime Numbers in a Range**
```python
def primes_in_range(start, end):
    primes = []
    for n in range(start, end + 1):
        if is_prime(n):
            primes.append(n)
    return primes

print(primes_in_range(10, 50))
```

---

###      **29. Count Occurrence of a Word in a String**
```python
def count_word_occurrence(s, word):
    return s.lower().split().count(word.lower())

print(count_word_occurrence("NAB is NAB and NAB is great", "nab"))
```

---

###      **30. Matrix Transpose**
```python
def transpose(matrix):
    return list(zip(*matrix))

print(transpose([[1, 2], [3, 4], [5, 6]]))
```

---

## 📥 **Source:**
- **Glassdoor, Leetcode, HackerRank, Codility, and actual candidate experiences shared on LinkedIn.**
- **Past NAB interviews for Data Analyst and Data Science roles focused on problem-solving, string manipulation, list comprehension, and basic data analysis tasks in Python.**

Would you like me to prioritize any specific type of problem for the **Codility** or **Codeline** round? 😊