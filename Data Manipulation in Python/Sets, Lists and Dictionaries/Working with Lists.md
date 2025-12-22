# Working with Lists

A **list** is an ordered collection of items. Unlike sets, lists preserve order, allow duplicate values, and allow us to modify elements. Lists are one of the most flexible and commonly used data structures in Python.

Earlier, we used lists implicitly when treating strings as sequences of characters. Strings support indexing and slicing; lists support the same concepts but with mutable elements.

We can build a list by starting with an empty list and appending values, or by initialising it with predefined data:

```
>>> a = []
>>> print(a)
[]

>>> b = [69, 420, "Willy", 3.14159]
>>> print(b)
[69, 420, "Willy", 3.14159]
```

We can add items to a list using `append()`, modify items by index, and extend the list with multiple values:

```
>>> a.append(81)
>>> a[0] = 69
>>> a.extend([420, "Willy", 3.14159])

>>> print(a)
[69, 420, "Willy", 3.14159]

>>> print(len(a))
4
```

When working with lists, we must avoid accidentally overwriting the list itself. Methods such as `append()` modify the list in place and return `None`. Assigning their return value back to the list variable will destroy the list:

```
>>> a = a.append(4)
>>> print(a)
None
```

Lists are powerful because they can store mixed types, and even other lists. This allows for nested, multi-dimensional structures:

```
>>> a.append(b)

>>> print(a)
[69, 420, "Willy", 3.14159, [69, 420, "Willy", 3.14159]]

>>> print(a[2])
"Willy"

>>> print(a[4])
[69, 420, "Willy", 3.14159]

>>> print(a[4][3])
3.14159
```

We can remove elements using `del`, or replace a slice of items using subscript ranges:

```
>>> del b[2]

>>> print(b)
[69, 420, 3.14159]

>>> b[1:3] = [345, 678]

>>> print(b)
[69, 345, 678]
```

Lists preserve insertion order. If we wish to reorder elements, we may use `.sort()` to sort the list in place, or `sorted()` to produce a new list:

```
>>> a.sort()
>>> print(a)
[3.14159, 69, 420, "Willy"]
```

Sorting works best with consistent data types, though Python will attempt comparisons where possible.

We can insert new elements at specific positions using `insert()`:

```
>>> c = [1, 3, 5, 7, 13, 17, 19, 23]

>>> c.insert(4, 11)

>>> print(c)
[1, 3, 5, 7, 11, 13, 17, 19, 23]
```

Lists also make good lookup tables. For example, we can store hexadecimal digits and access them by index:

```
>>> hex_list = ['0','1','2','3','4','5','6','7','8','9','A','B','C','D','E','F']

>>> print(hex_list[12])
'C'
```

Lists can be concatenated simply by using the `+` operator:

```
>>> c = c + [29, 31, 37]

>>> print(c)
[1, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37]
```

With lists completed, let us now move on to another special form of ordered collection: **tuples**.
