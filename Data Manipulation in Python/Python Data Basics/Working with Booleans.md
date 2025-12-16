# Working with Booleans

Boolean values represent one of two possible states: **True** or **False**. These values are foundational in programming, as they allow us to make decisions, evaluate conditions, and control program flow.

A Boolean value may be assigned directly using the predefined names `True` and `False`, or it may be produced as the result of a comparison operation.

```
>>> a = True
>>> print(a)
True

>>> if a:
...     print("It is True!")
...
It is True!
```

In the next example, Boolean values are created as a result of comparing numerical values:

```
>>>> a = 164
>>> b = 37
>>> if a > b:
...     print(a, "is greater than", b)
...
164 is greater than 37
```

Python provides three primary Boolean operators:

- **and**
- **or**
- **not**

Additionally, the bitwise operators `&` and `|` can function as shorthand for logical and and or, respectively, when used with Boolean values.

```
>>> a = True
>>> b = False

>>> print(a and b)
False

>>> print(a & b)
False

>>> print(a or b)
True

>>> print(a | b)
True

>>> print(not b)
True
```

These operators allow us to combine Boolean expressions and build more complex conditions that control how our programs behave.
