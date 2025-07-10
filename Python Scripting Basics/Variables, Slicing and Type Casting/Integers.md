# Integers

An integer (or `int`) variable in Python is used to store whole numbers that can be compared, calculated, or manipulated. Integer variables are defined by assigning a number without quotation marks to a variable name.

## Defining an Integer Variable

In the example below, we assign the value `420` to a variable named `randomInt` and then print it to the terminal:

```
~ % cat randomInt.py
#!/usr/bin/python3

randomInt = 420

print(randomInt)
```

When the script is executed:

```
~ % ./randomInt.py
420
```

As expected, the script outputs the value `420`.

## Strings vs Integers

If a number is enclosed in quotation marks, Python interprets it as a string rather than an integer. This distinction can lead to unexpected behaviour or runtime errors, particularly during mathematical operations or comparisons.

Consider the following example:

```
~ % cat randomInt_2.py
#!/usr/bin/python3

randomStr = "420"
randomInt = 420

print(randomInt)         # Integer
print(randomStr)         # String
print(randomInt + 1)     # Integer addition
print(randomStr + 1)     # Attempting to add an int to a string
```

When this script is run:

```
~ % ./randomInt_2.py
420
420
421
Traceback (most recent call last):
  File "/Users/victorsangwan/./randomInt_2.py", line 9, in <module>
    print(randomStr + 1)
TypeError: can only concatenate str (not "int") to str
```

Although the first two outputs appear identical, they are fundamentally different data types:

- `randomInt` is an integer (`int`)

- `randomStr` is a string (`str`)

The third line works as expected, adding `1` to the integer `420` and printing `421`.

However, the final line causes a `TypeError`, because Python cannot directly add an integer (`1`) to a string (`"420"`). The error message is clear: <em>"can only concatenate str (not 'int') to str"</em>.

Interpreting Errors

This is a good example of why understanding data types is essential. It also illustrates the importance of reading and understanding error messages. Becoming familiar with Python's traceback output will help you debug your code more efficiently.

When in doubt:

- Check the type of your variables using `type()`

- Avoid mixing incompatible types

- Use type casting (`int()`, `str()`, etc.) when needed
