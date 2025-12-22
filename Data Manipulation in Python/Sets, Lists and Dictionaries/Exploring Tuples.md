# Exploring Tuples

A **tuple** is very similar to a list, but with one crucial difference: **tuples are immutable**. Once the values inside a tuple have been defined, they cannot be altered. This makes tuples useful for storing fixed collections of related data.

Tuples are declared using parentheses:

```
>>> a = (1, 2, 3)

>>> type(a)
<class 'tuple'>

>>> print(a)
(1, 2, 3)
```

Just like lists, tuples may contain mixed data types, including lists, bytes, and even other tuples. They support indexing and nested indexing just as lists do:

```
>>> b = (1, 2, ['mango', 'banana'], b'APPLE')

>>> type(b[0])
<class 'int'>

>>> type(b[2])
<class 'list'>

>>> type(b[3])
<class 'bytes'>

>>> type(b[2][1])
<class 'str'>
```

Although the tuple itself is immutable, **mutable objects inside the tuple (such as lists) can still be modified**, because immutability applies only to the tuple structure, not to the objects it contains.

Tuples provide a clean and efficient way to represent structured, related information that should not change throughout program execution.
