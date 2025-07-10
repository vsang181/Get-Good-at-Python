# Floats

If we want a variable to hold a number with a decimal point, we cannot use an integer (`int`). Instead, we use a floating-point number, or simply a float.

The good news is that Python handles this conversion automatically in many cases, allowing us to work with floats much like integers. For example, if we add a float to an integer, Python will implicitly convert the result to a float.

## Demonstration

Let us explore what happens when we add a decimal number to an integer:

```
~ % cat randomFloat.py
#!/usr/bin/python3

x = 420

print(x)
print(type(x))

x = x + 6.9

print(x)
print(type(x))
```

When we execute the script:

```
~ % ./randomFloat.py
420
<class 'int'>
426.9
<class 'float'>
```

## Explanation

In this example:

- The variable `x` initially holds the integer value `420`.

- We then add `6.9` (a float) to `x`.

- Python automatically promotes the result to a float (`426.9`) without any additional instructions.

- The `type()` function confirms the change in data type from `int` to `float`.

This automatic type handling is part of what makes Python easy to work with—especially for those new to programming or scripting.

<br>

Having explored strings, integers, and floats, the next essential data type to understand is the Boolean, which represents true or false values and is commonly used in logic and control flow.
