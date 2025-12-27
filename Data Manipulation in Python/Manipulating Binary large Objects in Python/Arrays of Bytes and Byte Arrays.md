# Arrays of Bytes and Byte Arrays

A byte array is a sequence of bytes, and in Python it can be created using the `b` prefix, the `bytes()` constructor, or the `bytearray()` constructor. Although these structures may look similar, their behaviour differs—most notably in whether the data is mutable.

Let us begin by creating a bytes object using the `b` prefix.

```
>>> ba1 = b'ABCDEFG'

>>> type(ba1)
<class 'bytes'>

>>> print(ba1)
b'ABCDEFG'

>>> print(ba1[0])
65

>>> type(ba1[0])
<class 'int'>
```

Notice that indexing into a bytes object returns the integer value of that byte.

We can also create a bytes object using the `bytes()` function:

```
>>> ba2 = bytes([1, 3, 5, 7, 11, 13, 17, 19, 23, 31, 37])

>>> type(ba2)
<class 'bytes'>

>>> print(ba2)
b'\x01\x03\x05\x07\x0b\x0d\x11\x13\x17\x1f%'
```

Here, Python displays values less than 32 (non-printable ASCII) using their hexadecimal escape sequences.

Another way to construct a bytes object is by encoding a string:

```
>>> ba3 = 'ABCDEFG'.encode()

>>> type(ba3)
<class 'bytes'>

>>> s3 = ba3.decode()

>>> type(s3)
<class 'str'>

>>> print(s3)
ABCDEFG
```

Encoding converts a string to bytes; decoding reverses the process.

The fourth approach is to create a **bytearray**:

```
>>> ba4 = bytearray([1, 3, 5, 7, 11, 13, 17, 19, 23, 31, 37])

>>> type(ba4)
<class 'bytearray'>

>>> print(ba4)
bytearray(b'\x01\x03\x05\x07\x0b\r\x11\x13\x17\x1f%')
```

A `bytearray` is similar to `bytes`, but it is **mutable**, meaning its elements can be changed.

We can also create a bytearray directly from a list:

```
>>> list3 = [1, 3, 5, 7, 11, 13, 17, 19, 23, 31, 37]

>>> ba5 = bytearray(list3)

>>> type(ba5)
<class 'bytearray'>

>>> print(ba5)
bytearray(b'\x01\x03\x05\x07\x0b\r\x11\x13\x17\x1f%')
```

## Bytes vs Bytearrays

These structures behave differently when we attempt to modify them.

```
>>> ba5[0] = 6

>>> print(ba5)
bytearray(b'\x06\x03\x05\x07\x0b\r\x11\x13\x17\x1f%')
```

This works because `bytearray` supports item assignment.

Now compare this with a `bytes` object:

```
>>> ba3[0] = 6
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'bytes' object does not support item assignment
```

Bytes objects are **immutable**—their contents cannot be altered after creation.

## Combining Bytes Objects

While bytes are immutable, we can concatenate them to produce a new bytes object:

```
>>> ba6 = bytes([1, 2, 3, 4, 5, 6, 7])
>>> ba7 = bytes([8, 9, 10, 11, 12])

>>> ba6 = ba6 + ba7

>>> print(ba6)
b'\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\x0c'
```

Note that:

- `\t` represents the byte value 9 (tab)
- `\n` represents the byte value 10 (newline)

## Modifying Bytearrays

Bytearrays are far more flexible:

```
>>> ba5.append(65)

>>> print(ba5)
bytearray(b'\x06\x03\x05\x07\x0b\r\x11\x13\x17\x1f%A')
```

Here we appended the integer 65, which corresponds to the ASCII character `'A'`.

We can also delete or slice-remove items:

```
>>> del ba5[0:2]

>>> print(ba5)
bytearray(b'\x05\x07\x0b\r\x11\x13\x17\x1f%A')
```

This removes the first two elements of the bytearray.

## Searching Within Byte Sequences

Both `bytes` and `bytearray` objects provide the `find()` method to locate the first occurrence of a byte sequence:

```
>>> ba6.find(b'\x05')
4
```

This tells us that the byte `0x05` appears at index 4.
