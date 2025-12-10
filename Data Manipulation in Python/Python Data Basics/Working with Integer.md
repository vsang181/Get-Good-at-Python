# Working with Integers

We can create an integer variable in Python using a simple assignment statement. Python supports integers of unlimited length, and an integer may be either positive or negative. We can perform arithmetic using the standard operators, as demonstrated below:

```
>>> a = 123
>>> b = 231
>>> c = a + b
>>> print(c)
354

>>> c = c + 1
>>> print(c)
355

>>> type(c)
<class 'int'>

>>> d = c / 5
>>> print(d)
71

>>> type(d)
<class 'int'>

>>> e = c % 2
>>> print(e)
1

>>> c += 1
>>> print(c)
356
```

In this example, notice how the division operator (`/`) results in an integer answer because the result is whole. Any remainder from division can be retrieved using the modulo operator (`%`). We also use the `type()` function to confirm the data type of our variables. Additionally, the `+=` operator is demonstrated as shorthand for adding a fixed value to an existing variable.

Python provides many mathematical functions for working with integers. Two functions that will be especially important later in this Topic are:

- `int()` — converts a string into an integer
- `str()` — converts an integer into a string

These are particularly useful when reading numeric input from the console, since user input is always interpreted as a string. We can convert this input using `int()`, or convert the result back into a string when constructing output. Both approaches are shown below:

```
>>> a = input("Enter a number please: ")
Enter a number please: 69

>>> type(a)
<class 'str'>

>>> b = int(a)
>>> print(b)
69

>>> c = int(input("Enter a number please: "))
Enter a number please: 420

>>> print(c)
420

>>> type(c)
<class 'int'>

>>> d = str(c+1)+" chocolates"
>>> print(d)
421 chocolates
```

Now that we have revisited integer operations, let us move on to floating point numbers.

