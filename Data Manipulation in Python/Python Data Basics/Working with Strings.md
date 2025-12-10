# Working with Strings

One of the most frequently used data types in Python is the string object, which consists of zero or more characters concatenated together. A string may be of any length and can contain spaces, punctuation, and special characters such as newline symbols. Strings can be stored in variables or written directly as quoted text. Because basic string manipulation was covered in the introductory Python Scripting topic, we will briefly review the key functions used to manipulate strings.

```
>>> a = "Hello I am Willy Wonka, "
>>> b = "Would you like to taste my Cholate?"

>>> a = a + b

>>> print(a.upper())
HELLO I AM WILLY WONKA, WOULD YOU LIKE TO TASTE MY CHOCOLATE?

>>> print(a.lower())
hello i am willy wonka, would you like to taste my cholate?
```

n this example, we assign two separate strings to the variables `a` and `b`, and then concatenate them using the `+` operator. The `upper()` and `lower()` methods are used to convert the full sentence into upper-case or lower-case text respectively.

When handling multiple items, we can store them inside a larger data structure and access them using indexes. A string behaves similarly to a list (or array) of characters, where each character can be accessed individually. We can use `len()` to find the length of the string, and indexing begins at 0 for the first character. Let us extract the first and last characters, along with a slice from within the sentence.

```
>>> print(len(a))
59
>>> print(a[0])
H
>>> print(a[21])
a
>>> print(a[-1])
?
>>> print(a[17:21])
Wonk
```

In the above listing, we use positive indexing to reference characters from the beginning of the string, and negative indexing to reference characters starting from the end (`-1` representing the final character). The portion of the string that we extract is known as a substring or slice. A slice includes the start index and excludes the end index.

Strings in Python are immutable, which means we cannot directly modify an element or a slice of a string. Attempting to do so results in an error:

```
>>> a[11:22] = "Umpa Lumpa"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

Instead, we can create an updated version of the string using methods such as replace()``:

```
>>> a = a.replace("Willy Wonka", "Umpa Lumpa")
>>> print(a)
Hello I am Umpa Lumpa, Would you like to taste my Cholate?
```

Python also allows string multiplication using the asterisk (`*`) operator:

```
>>> a = "A" * 6
>>> print(a)
AAAAAA
```

Strings may be declared using either single (`' '`) or double (`" "`) quotes. This flexibility is especially useful when embedding quotes inside a string. Alternatively, we can use escape sequences, such as `\"`, to include quote characters.

```
>>> a = 'Hello I am "Willy Wonka".'
>>> print(a)
Hello I am "Willy Wonka".

>>> a = "Hello I am \"Willy Wonka\"."
>>> print(a)
Hello I am "Willy Wonka".
```

Python provides additional escape sequences, including newline (`\n`) and tab (`\t`):

```
a = "Hello\tI\tam\nWilly\tWonka\n"

>>> print(a)
Hello	I	am
Willy	Wonka
```

With this brief refresher on strings completed, we can now move on to working with integers.
