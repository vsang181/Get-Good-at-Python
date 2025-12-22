# Octal Numbers

Octal representation is less common, but it is still important to understand how to manipulate octal data. Octal numbers are declared with the `0o` prefix, have a base of **8**, and use digits **0–7**. Let us declare and check an octal number:

```
>>> o1 = 0o342127
>>> type(o1)
<class 'int'>

>>> o2 = o1 + 0o412661
>>> print(oct(o2))
0o755010

>>> print(o2)
252424
```

Octal numbers, like binary numbers, are stored internally as integers, so we can manipulate them using all standard integer operations. We can convert them back to their octal representation using the `oct()` function.

Continuing with the example above, if we want to obtain the octal value **without the** `0o` **prefix**, we can remove it as shown below:

```
>>> po1 = 0o755010
>>> print(oct(po1)[2:])
755010

>>> print(oct(po1).replace('0o', '', 1))
755010

>>> no1 = -0o4415
>>> print(oct(no1).replace('0o', '', 1))
-4415
```

Removing parts of a string is called **taking a slice**. This is common terminology when doing string operations.

While slicing off the first two characters works for **positive** octal numbers, using `replace()` is safer because it works for both **negative** and **positive** values.

## Converting Strings to Octal Integers

We can convert a string of digits into an integer using `int()`. By default, `int()` assumes **base 10**, but we can provide a second argument to specify another base. For octal numbers, the base is **8**. Including the `0o` prefix is optional.

```
>>> so1 = "0o755010"
>>> int1 = int(so1, 8)

>>> print(oct(int1))
0o755010

>>> so2 = "755010"
>>> int2 = int(so2, 8)

>>> print(oct(int2))
0o755010

>>> so3 = "-0o4415"
>>> int3 = int(so3, 8)

>>> print(oct(int3))
-0o4415
```

All three conversions produce correct Python octal integers.
