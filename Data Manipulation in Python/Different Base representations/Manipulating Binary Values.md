# Manipulating Binary Values

Binary numbers take the values `0` and `1`. While `0` and `1` are still equal to their face values, the binary equivalent of `2` is `10`, `3` is `11`, and `4` is `100`. Instead of each position in the number representing a decimal digit `0–9`, it represents a binary digit `0–1`. Binary numbers work in base `2`.

We can do maths with binary numbers as we would with our normal decimal system, but we need to remember to carry over at `2` instead of `10`. For example, adding `1001` (which is `9` in decimal) to `1010` (which is `10` in decimal) gives `10011` (which is the binary representation of `19`).

Binary numbers can be declared in Python using the `0b` prefix. Let us declare a binary variable and check its type.

```
>>> x = 0b01000001

>>> print(chr(x))
'A'

>>> type(x)
<class 'int'>
```

Now we know binary numbers in Python are manipulated as integers, and we can treat them as such using all the standard integer operations. We might still want to declare a value in binary form, for example, if we are using it as a mask to pick out a certain bit in a set of flags. This often happens when dealing with system and network activity, such as manipulating the header fields in a TCP packet with a set of flags, as shown below.

<img width="1194" height="714" alt="image" src="https://github.com/user-attachments/assets/3e32ca2a-cdfb-48d0-b877-6ebe582586bc" />

In order to know whether this transmission was an acknowledgement, we have to check whether the ACK flag is set. To isolate and check that bit, we will need to carry out some bitwise operations.

Bitwise operations are used to manipulate binary numbers. There are four basic bitwise logic operators:

- AND
- OR
- XOR
- NOT

AND, OR, and XOR operate on two inputs, while NOT operates on one.

- **AND** returns `1` where **both** bits are `1`.
- **OR** returns `1` where **at least one** of the bits is `1`.
- **XOR** returns `1` where **exactly one** of the two bits is `1` (but not both).
- **NOT** returns the opposite of the bit (`0` becomes `1`, `1` becomes `0`).

There are two additional bitwise operators, `<<` and `>>`, which shift the bits to the left or right by a specified number of bit positions. These operations are demonstrated below.

<img width="1228" height="582" alt="image" src="https://github.com/user-attachments/assets/bf81b10b-9a9e-4234-859c-76c794de0cf6" />

We can use bitwise operations on integer variables:

```
>>> x = 0b01001011
>>> y = 0b00011101
>>> z = x & y
>>> print(z)
9
```

`z` is `9` because `0b01001011` & `0b00011101` is `0b00001001`, which is `9` in decimal.

Computers work at the binary level, but often display their work in terms of bits and bytes.
Some common terms:

- 8 bits = 1 byte
- 16 bits (2 bytes) = a **word**
- 32 bits (4 bytes) = a **double word** (DWORD)

Let us do some bitwise manipulation using bytes. We will use a flag byte to extract the ACK bit from the TCP header by AND-ing the flag byte with the bit sequence `00010000`. If the result is not zero, the ACK bit is set. The bit sequence used to extract a bit is often called a **mask**, while the process of AND-ing with it is known as **masking**.

In Python, bitwise AND is written as `&` (do not confuse this with the logical `and` keyword, which operates on boolean values, not individual bits).

```
>>> flag = 0b00011000
>>> ack = flag & 0b00010000

>>> if ack:
...     print("ACK set")
...
ACK set
```

We also might want to set or unset a bit. Let us set the ACK bit using the OR operator. The ACK bit is in position 4, with the lowest-order bit being position 0. We can use the left shift operator in conjunction with OR (`|`) to set it.

```
>>> flag = 0b00000000
>>> flag = flag | (1 << 4)
>>> print(bin(flag))
0b10000
```

Here `1 << 4` is `0b10000`, so the ACK bit (bit 4) is now set.

We can clear a bit using a similar technique with AND and a negated mask:

```
>>> flag = 0b00010000      # ACK bit set
>>> flag = flag & ~(1 << 4)
>>> print(bin(flag))
0b0
```

Now the ACK bit is cleared.

XOR is a commonly used operator with a very useful characteristic: when it is applied twice with the same key, the original value is recovered. This makes XOR ideal for simple cryptographic functions.

Let us create a cipher and then recover it:

```
>>> plaintext = 0b01101010
>>> key = 0b10101010
>>> ciphertext = plaintext ^ key

>>> print(bin(ciphertext))
'0b11000000'

>>> decode = ciphertext ^ key

>>> print(bin(decode))
'0b1101010'
```

The value `'0b1101010'` is equivalent to the original `0b01101010`; the leading `0` is simply omitted when Python prints the binary representation.

In the example above we used the `bin()` function to display an integer in its binary form.

Because of its use in cryptography, XOR is also useful for manipulating plaintext in the form of Python strings. Let us code up a variation on an `sxor()` function to perform string XOR.

```
>>> def sxor(s1, s2):
...     # Repeat the key so it is at least as long as the message
...     tkey = (s2 * (len(s1) // len(s2) + 1))[:len(s1)]
...     # XOR each character of the message with the key
...     return "".join(chr(ord(a) ^ ord(b)) for a, b in zip(s1, tkey))
```

We provide the `sxor()` function with two parameters: a string to encrypt and a key to encrypt it with. The first thing we do is repeat the key so it is at least as long as the string. We use the ratio of the string lengths to determine how many times to repeat it and use the multiply operator to concatenate the key.

The return line builds the result by looping over the pairs of characters produced by `zip(s1, tkey)`, XOR-ing their integer values, and converting each result back to a character with `chr()`.

The core of the operation is the exclusive OR (`ord(a) ^ ord(b)`), in which the integer value of the message character is XORed with the integer value of the key character at the corresponding position.

The `zip()` function takes two iterables as arguments and returns an iterator that generates a sequence of character pairs. It generates pairs until it reaches the end of one of its inputs, which is why we made the key at least as long as the string.

Now that we understand the function, let us use it to encrypt and recover a message.

```
>>> msg = 'Wanna taste my chocolate?'
>>> key = 'WillyWonka'
>>> cipher = sxor(msg, key)

>>> print(cipher.encode().hex())
0008020218771b0f18153249011559340701080e3b08180946

>>> recovery = sxor(cipher, key)

>>> print(recovery)
Wanna taste my chocolate?
```

This is a pretty useful function to add to our toolbox. We can code up a very similar function for byte strings:

```
>>> def bxor(b1, b2):
...     tkey = (b2 * (len(b1) // len(b2) + 1))[:len(b1)]
...     return bytes([a ^ b for a, b in zip(b1, tkey)])

>>> b1 = b'Wanna taste my chocolate?'
>>> b2 = b'WillyWonka'
>>> cipher = bxor(b1, b2)

>>> print(cipher)
b'\x00\x08\x02\x02\x18w\x1b\x0f\x18\x152I\x01\x15Y4\x07\x01\x08\x0e;\x08\x18\tF'

>>> recovery = bxor(cipher, b2)

>>> print(recovery)
b'Wanna taste my chocolate?'
```

Here, `bxor()` operates directly on bytes, which is usually what you want for real-world cryptography and when displaying hex output.
