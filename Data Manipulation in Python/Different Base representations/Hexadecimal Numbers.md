# Hexadecimal Numbers

Hexadecimal numbers are integers represented in **base 16**, where the digits 10–15 are written using the characters **A–F** (lowercase is equally valid). In Python, hexadecimal values use the prefix `0x`, and integers can be displayed in hexadecimal form using the `hex()` function.

<img width="1008" height="1111" alt="image" src="https://github.com/user-attachments/assets/971e610f-82a7-4565-a5e5-061fa0375107" />

The figure above illustrates hexadecimal addition and subtraction. As with other number bases, these operations are standard integer operations in Python, and results may be displayed in decimal, hexadecimal, or any other desired base. Below is an example of working with hexadecimal values:

```
>>> hex1 = 0x13A7
>>> hex2 = 0x26FF

>>> print(hex(hex1 + hex2))
0x3aa6

>>> hex3 = 0xF00D
>>> hex4 = 0xBAAD

>>> print(hex(hex3 - hex4))
0x3560
```

Hexadecimal manipulation is especially important when working with memory, binary data, and low-level protocols. It is often necessary to work with the two hexadecimal digits that make up a single byte. Each byte consists of two **nibbles**:

- H**igh-order nibble** → bits 7–4
- **Low-order nibble** → bits 3–0

We can isolate the low-order nibble using a bitwise **AND** with `0x0F`, and we can obtain the high-order nibble by shifting the byte right by four bits:

```
>>> hexbyte = 0xBE
>>> low_nibble = hexbyte & 0x0F
>>> print(hex(low_nibble))
0x0e

>>> high_nibble = hexbyte >> 4
>>> print(hex(high_nibble))
0x0b
```

When working with binary files, navigation is done using hexadecimal offsets, not line numbers. These offsets represent the position (in bytes) from the beginning of the file. A typical hex editor displays 16 bytes per line, meaning the offset increments by 0x10 for each row.

<img width="1228" height="705" alt="Screenshot 2025-12-23 at 22 40 09" src="https://github.com/user-attachments/assets/b33642f2-0e6c-4e90-ab87-b0e43e30614a" />

Below, we will create a simple Python script that replicates the behaviour of a very basic hex viewer.

## Building a Hex Dump Script in Python

```
1. fname = input("Filename: ")
2. f = open(fname, "rb")
3. offset = 0x0
```

- Line 1 prompts the user for a filename.
- Line 2 opens the file in **binary** mode.
- Line 3 initialises an offset variable to zero since we begin at the start of the file.

Next, we prepare the per-line loop:

```
4. infile = True
5. while infile:
6.     addr = str(hex(offset)[2:].zfill(8))
7.     hexline = ""
8.     ascline = ""
```

- `infile` is a flag used to signal end-of-file processing.
- Line 6 converts the offset to a zero-padded 8-digit hexadecimal address (without the `0x` prefix).
- `hexline` and `ascline` hold the hexadecimal and ASCII representations respectively.

We now construct the **inner loop**, which processes 16 bytes per line:

```
9.     for x in range(0x10):
10.         byte = f.read(1)
11.         if len(byte) == 0:
12.             hexline = hexline.ljust(48)
13.             infile = False
14.             break
15.         if byte[0] > 29:
16.             aschr = chr(byte[0])
17.         else:
18.             aschr = "."
19.         ascline = ascline + aschr
20.         hexline = hexline + hex(byte[0])[2:].zfill(2) + " "
```

Explanation

- Line 10 reads a single byte from the file.
- Line 11 checks for end-of-file.
- Line 12 pads the hex portion to maintain formatting if fewer than 16 bytes remain.
- Lines 15–18 determine whether the byte is printable ASCII (greater than decimal 29). Non-printable bytes are replaced with `"."`.
- Line 20 converts the byte to a two-digit hexadecimal value.

Finally, we print each line and update the offset:

```
21.     print(addr + " " + hexline + " " + ascline)
22.     offset = offset + 0x10
23. f.close()
```

A full version of the script is shown below:

```
fname = input("Filename: ")
f = open(fname, "rb")
offset = 0x0
infile = True

while infile:
    addr = str(hex(offset)[2:].zfill(8))
    hexline = ""
    ascline = ""
    for x in range(0x10):
        byte = f.read(1)
        if len(byte) == 0:
            hexline = hexline.ljust(48)
            infile = False
            break
        if byte[0] > 29:
            aschr = chr(byte[0])
        else:
            aschr = "."
        ascline = ascline + aschr
        hexline = hexline + hex(byte[0])[2:].zfill(2) + " "
    print(addr + " " + hexline + " " + ascline)
    offset += 0x10

f.close()
```

## Converting Between Bytes, Integers, and Strings

We frequently need to convert between raw bytes, integers, and strings. Python gives us several convenient mechanisms:

```
>>> b1 = b'A'
>>> type(b1)
<class 'bytes'>

>>> type(b1[0])
<class 'int'>

>>> type(ord(b1))
<class 'int'>
```

Strings and bytes can be converted using `.encode()` and `.decode()`:

```
>>> str1 = "Wanna see my chocolate?"
>>> type(str1)
<class 'str'>

>>> type(str1.encode())
<class 'bytes'>

>>> b1 = b"Wanna see my chocolate?"
>>> type(b1)
<class 'bytes'>

>>> type(b1.decode())
<class 'str'>
```

Python can also convert floating-point values into hexadecimal notation using `float.hex()`:

```
>>> f1 = 3.14159
>>> print(float.hex(f1))
0x1.921f9f01b866ep+1
```

Hexadecimal floating-point notation is rarely required in typical scripting tasks but is useful in low-level numerical analysis.
