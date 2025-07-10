# Type Casting

Type casting refers to the process of converting a variable from one data type to another in Python. This is done using built-in casting functions such as `int()`, `str()`, or `float()`.

Type casting is particularly useful when dealing with user input or data sourced externally (e.g. from a text file, database, or webpage), which is often treated as a string—even if it represents numeric data.

## Problem with Implicit String Addition

Suppose we have two strings that each contain a numeric value. If we attempt to "add" them without casting, Python will not raise an error—but the result may not be what we expect:

```
~ % cat typeCasting.py
#!/usr/bin/python3

x = "420"
y = "69"

print(type(x))
print(type(y))

print(x + y)
```

When executed:

```
~ % ./typeCasting.py
<class 'str'>
<class 'str'>
42069
```

Explanation:

Python has concatenated the two strings (`"420"` and `"69"`) to produce `"42069"`, instead of performing a mathematical addition.

## Correcting with `int()` Casting

To perform actual arithmetic, we must first convert the strings to integers using the `int()` function:

```
~ % cat typeCasting_2.py
#!/usr/bin/python3

x = "420"
y = "69"

print(type(x))
print(type(y))

print(int(x) + int(y))
```

Output:

```
~ % ./typeCasting_2.py
<class 'str'>
<class 'str'>
489
```

Now the addition works as expected, because both values were type-cast to integers before being added.

## Casting an Integer to a String

Similarly, we can convert numeric data types (such as `int` or `float`) to strings using the `str()` function. This is particularly useful when combining numbers with text for display or formatting purposes.

Let us demonstrate:

```
~ % cat typeCasting_3.py
#!/usr/bin/python3

x = "420"
y = "69"

print(type(x))
print(type(y))

z = int(x) + int(y)
print(z)
print(type(z))
print(type(str(z)))
```

Output:

```
~ % ./typeCasting_3.py
<class 'str'>
<class 'str'>
489
<class 'int'>
<class 'str'>
```

## Summary

- Use `int()` to convert a string or float to an integer.

- Use `str()` to convert an integer or float to a string.

- Use `float()` to convert a string or integer to a floating-point number.

Type casting ensures that data is in the appropriate format for the operation you intend to perform, helping to prevent logic errors and type-related exceptions.
