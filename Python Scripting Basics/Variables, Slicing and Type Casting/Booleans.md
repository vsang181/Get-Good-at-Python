# Booleans

Boolean variables are used to represent one of two possible values: `True` or `False`. These are not strings (i.e., not `"True"` or `"False"` in quotation marks), but distinct data types in Python, and are fundamental in control flow and decision-making.

Boolean values are most commonly used in conditional statements, which we will explore in more detail later. For now, it is important to understand that Booleans allow a script to make logical decisions based on whether a condition is met.

## Example

Let us look at a simple example involving a Boolean variable:

```
~ % cat booleanExample.py
#!/usr/bin/python3

admin = False

if admin:
    print("Congratulations, you are Admin")
else:
    print("Better luck next time, buddy")
```

Output:

```
~ % ./booleanExample.py
Better luck next time, buddy
```

## Explanation

In this example:

- The variable `admin` is set to `False`.

- The `if` statement checks the value of `admin`. Since it is not `True`, the code inside the `else` block is executed.

- The result is the message: "Better luck next time, buddy".

If you were to change the value of `admin` to `True`, the script would print the admin message instead.

## Summary

- Booleans are written as `True` or `False` (note the capital letters).

- They are used to evaluate logic and make decisions in scripts.

- Avoid using quotation marks around Boolean values—doing so would make them strings, not Boolean types.

<br>

So far, we have covered:

- Strings – for text

- Integers and Floats – for numbers

- Booleans – for logic

We have also discussed how to convert between these types using type casting. Up next, you may wish to explore conditional statements or comparison operators to see how Booleans are used in real-world logic.
