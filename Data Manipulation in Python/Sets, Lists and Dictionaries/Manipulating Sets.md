# Manipulating Sets

A **set** is a one-dimensional collection of items, which may be of different data types. A set is **unordered**, **unindexed**, and contains **unique** values. While we can add or remove items from a set, we cannot modify an existing element in place. Since sets are unordered, we also cannot access elements by index; instead, we loop through them, check for membership, or perform set-based operations such as unions and intersections.

Sets are useful when we want to store multiple values without duplicates. For example, we might create a set named `a` to store fruit names. We can initialise an empty set as follows:

```
>>> a = set()
```

Because `{}` creates an empty dictionary, we must use `set()` to initialise an empty set.

We can also initialise a set with values:

```
>>> a = set(['Apple', 'Banana', 'Mango'])
```

Let us add Grapes to the set:

```
>>> a.add('Grapes')

>>> print(a)
set(['Apple', 'Banana', 'Mango', 'Grapes'])
```

Alternatively, we can create a set using curly braces when it is **not** empty:

```
>>> b = {"a", "e", "i", "o", "u"}

>>> type(b)
<class 'set'>
```

To remove values, we may use `remove()` or `discard()`. The `remove()` method raises an error if the value does not exist, whereas `discard()` does not. Let us remove Mango:

```
>>> a.discard('Mango')

>>> print(a)
set(['Apple', 'Banana', 'Grapes'])
```

We can loop through a set to access its elements:

```
>>> fruits = set(['Apple', 'Banana', 'Grapes'])
>>> for item in fruits:
...     print(item)
...
Apple
Banana
Grapes
```

Let us now define another set and perform **union** and **intersection** operations:

```
>>> a1 = set(['Apple', 'Banana', 'Grapes'])
>>> a2 = set(['Mango', 'Pear', 'Apple'])

>>> b = a1.union(a2)
>>> b
set(['Apple', 'Banana', 'Grapes', 'Mango', 'Pear'])

>>> a1 | a2
set(['Apple', 'Banana', 'Grapes', 'Mango', 'Pear'])
```

The `union()` method returns a set containing all unique elements from both sets.
Using the `|` operator performs the same operation.

Similarly, intersection identifies values present in both sets:

```
>>> c = a1.intersection(a2)
>>> c
set(['Apple'])

>>> a1 & a2
set(['Apple'])
```

The `&` operator is shorthand for `intersection()`.
