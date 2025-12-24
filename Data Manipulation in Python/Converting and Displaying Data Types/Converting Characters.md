# Converting Characters

A character in Python is simply a string of length one. Although it behaves like a normal string, there are several useful conversion operations we can apply to single-character values.

## Converting a Character to an Integer

We can convert a single character into its corresponding integer (ASCII or Unicode code point) using the `ord()` function:

```
>>> ch1 = 'c'
>>> print(type(ch1))
<class 'str'>

>>> print(ord(ch1))
99
```

`ord()` works only on single characters. It will raise an error if you attempt to pass a longer string.

## Converting a Character to Bytes

Characters can be converted into byte values using `.encode()`. This method works for strings of any length but is frequently used with single characters:

```
>>> ch1 = 'c'
>>> b1 = ch1.encode()
>>> print(type(b1), b1)
<class 'bytes'> b'c'
```

The resulting bytes object uses Python's standard `b'...'` representation.

## Converting a Character to Hexadecimal

Because characters are strings, we must first encode them into bytes before obtaining a hexadecimal representation. The `.hex()` method returns a hex string without the `0x` prefix:

```
>>> ch1 = 'c'
>>> hex1 = ch1.encode().hex()
>>> print(hex1)
63
```

The output `"63"` is the hexadecimal representation of the ASCII code for `'c'`.

## Converting Hexadecimal Back to a Character

Python 2 previously supported a `"hex"` decoding mode, but Python 3 does not. To convert a hexadecimal string back into a character, we use `bytearray.fromhex()` followed by `.decode()`:

```
>>> hex1 = '63'
>>> print(bytearray.fromhex(hex1).decode())
c
```

This approach works for any valid hex string representing one or more bytes.
