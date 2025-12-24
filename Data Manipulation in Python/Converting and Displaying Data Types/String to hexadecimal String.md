# String to hexadecimal String

We can convert ordinary strings—of any length—into their hexadecimal representation using the same method we applied to single-character strings. The process is straightforward: encode the string into bytes, then convert those bytes into a hexadecimal string.

```
>>> str1 = "Gothic"
>>> print(str1.encode().hex())
476f74686963
```

The output is the hexadecimal representation of each character in the string `"Gothic"`.

To convert a hexadecimal string back into its original text, we use `bytearray.fromhex()` followed by `.decode()`. Note that Python requires the hex string to contain only valid hexadecimal characters and must represent complete bytes.

```
>>> hex1 = "47655E7265"
>>> print(bytearray.fromhex(hex1).decode())
Genre
```

This recovers the original string `"Genre"` from its hexadecimal form.
