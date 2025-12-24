# Converting Bytes

Bytes are one of the most frequently used data types in low-level programming, networking, and file handling. Understanding how to convert between bytes and other data types is essential when analysing protocols or manipulating binary data.

## Converting Bytes to Integers

To convert a single byte into an integer, we use the `int.from_bytes()` method:

```
>>> b1 = b'c'
>>> i2 = int.from_bytes(b1, 'big')
>>> print(i2)
99
```

The second argument (`'big'` or `'little'`) specifies the byte order. For a single byte, the order does not affect the result.

## Converting Bytes to Characters

A bytes object can be converted into a character string using `.decode()`:

```
>>> b1 = b'c'
>>> print(b1.decode())
c
```

The `.decode()` method interprets the byte sequence using UTF-8 by default unless another encoding is specified.

## Converting Bytes to Strings (and Back)

The `str()` function produces Python’s native string representation of a bytes object—including the leading `b'...'`:

```
>>> b1 = b'c'
>>> print(str(b1))
b'c'
```

To convert a character back into bytes, we use `.encode()`:

```
>>> b2 = 'c'.encode()
>>> print(type(b2), b2)
<class 'bytes'> b'c'
```

The `.encode()` method converts a string into its byte representation without requiring the `b' '` prefix.

## Converting Bytes to Hexadecimal

Bytes cannot be passed directly to the `hex()` function. Instead, bytes provide their own `.hex()` method, which returns a hexadecimal string **without** the `0x` prefix:

```
>>> b1 = b'c'
>>> b2 = b1.hex()
>>> print(type(b2), b2)
<class 'str'> 63
```

The string "63"`` represents the hexadecimal form of the ASCII value for `'c'`.

## Converting Hexadecimal Strings to Bytes

To convert hexadecimal into a bytes object, use `bytes.fromhex()`. This method expects a string containing only hexadecimal digits, with no `0x` prefix:

```
>>> h1 = '01FF'
>>> b2 = bytes.fromhex(h1)
>>> print(type(b2), b2)
<class 'bytes'> b'\x01\xff'
```

The resulting bytes object is shown using Python’s standard notation with the `b'...'` prefix and `\x` escape sequences.



