# Using Dictionaries

A **dictionary** is a data structure that stores paired entries, where one element serves as a **key** and the other element is its corresponding **value**. Keys must be unique, but values may be duplicated or of any data type.

Let us begin by creating a simple dictionary that maps the first four letters of the English alphabet to their NATO phonetic equivalents. We will then access a value and add additional entries.

```
>>> a = {"A": "Alfa", "B": "Bravo", "C": "Charlie", "D": "Delta"}

>>> print(a["C"])
Charlie

>>> a.update({"E": "Echo"})

>>> print(a)
{'A': 'Alfa', 'B': 'Bravo', 'C': 'Charlie', 'D': 'Delta', 'E': 'Echo'}

>>> type(a)
<class 'dict'>
```

In this example, each letter is a **key**, and each corresponding phonetic word is its **value**. The `update()` method allows us to insert new key–value pairs into the dictionary.

Keys must be unique and immutable (e.g., strings, numbers, or tuples). Values, however, may contain **any** data type—including lists or even other dictionaries. This makes dictionaries a powerful tool for modelling structured information.

Let us demonstrate a dictionary that stores employee details, with each key representing an employee ID and each value containing a list of attributes:

```
>>> b = {
...     "108679": ["Victor", "Sangwan", "Security Engineer", "25/12/2025"],
...     "104569": ["Willy", "Wonka", "Chocolate Factory", "12/08/1971"]
... }

>>> for empid in b:
...     print(empid, b[empid][1], b[empid][0])
...
108679 Sangwan Victor
104569 Wonka Willy

```

In the loop above, we iterate through the dictionary using the employee ID as the key and display the surname and first name for each entry.

Dictionaries therefore provide a highly flexible and efficient way to structure and retrieve related information.
