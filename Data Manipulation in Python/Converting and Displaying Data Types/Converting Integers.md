# Converting Integers

Python provides several convenient methods for converting integers into other data representations, such as bytes, characters, strings, and hexadecimal formats. These conversions are fundamental when working with files, network protocols, or low-level data structures.

## Converting Integers to Bytes

An integer can be converted to a `bytes` object in two primary ways:

**1. Using the** `.to_bytes()` **method**
**2. Using the** `bytes()` **constructor with a single-item list**

```
>>> i1 = 99

>>> b1 = i1.to_bytes(1, 'big')
>>> print("to_bytes:", type(b1), b1)
to_bytes: <class 'bytes'> b'c'

>>> b2 = bytes([i1])
>>> print("In list:", type(b2), b2)
In list: <class 'bytes'> b'c'
```

The `.to_bytes()` method requires two arguments:

- **The number of bytes** to use for the representation.
- **Byte order**, either `'big'` (most significant byte first) or `'little'`.

For values larger than 255, you must specify enough bytes to contain the integer.
The list-based form (`bytes([i])`) only supports values from 0–255 (i.e., a single byte).

## Converting Integers to Characters

The `chr()` function converts an integer into its corresponding Unicode character.

```
>>> i1 = 99
>>> print(chr(i1))
c
```

For values above 255, Python returns the appropriate Unicode character. For example, the integer **468** corresponds to a character used in several non-English languages:

```
>>> i2 = 468
>>> print(chr(i2))
ǔ
```

## Converting Integers to and from Strings

Converting an integer to its decimal string form is straightforward:

```
>>> print(str(i1))
99
```

To convert a numeric string back into an integer, use `int()`:

```
>>> i2 = int("42")
>>> print(i2)
42
```

## Converting Integers to and from Hexadecimal

The `hex()` function displays an integer in hexadecimal format:

```
>>> i1 = 99
>>> print(hex(i1))
0x63

>>> i2 = 333
>>> print(hex(i2))
0x14d
```

To convert a hexadecimal string back to an integer, pass the string to `int()` with base 16:

```
>>> h1 = "0x01ff"
>>> i2 = int(h1, 16)
>>> print(i2)
511
```

The same approach applies for other bases:

- Use base `8` for octal.
- Use base `2` for binary.
