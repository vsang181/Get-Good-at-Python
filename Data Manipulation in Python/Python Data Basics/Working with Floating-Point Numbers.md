# Working with Floating-Point Numbers

Floating-point variables represent numbers that contain digits both before and after a decimal point. They provide a decimal-based method of representing fractional values. For example, dividing 3 by 2 yields **1.5**, which represents one and a half. In Python, any number that contains a decimal point—whether or not digits follow it—is treated as a floating-point value.
```
>>> a = 4.20
>>> type(a)
<class 'float'>

>>> b = 69.
>>> type(b)
<class 'float'>
```

Standard arithmetic operators behave as expected and return floating-point results. Integer division and modulo operations also operate on floating-point numbers, producing floating-point outputs.

```
>>> c = b / a
>>> print(c)
16.428571428571427

>>> type(c)
<class 'float'>

>>> a = 5
>>> b = 25
>>> d = b / a
>>> print(d)
25.0

>>> type(d)
<class 'float'>

>>> e = b % a
>>> print(e)
1.7999999999999972
```

The unusual behaviour shown in the final example above is due to how Python stores floating-point numbers internally. Floating-point values cannot always be represented with perfect accuracy, which often leads to small rounding discrepancies. Consider the following:

```
>>> a = 0.1
>>> b = 0.2
>>> c = a + b
>>> print(c)
0.30000000000000004

>>> c == 0.3
False
```

Here, the sum of 0.1 and 0.2 does not appear exactly as 0.3 due to binary floating-point precision limits. This behaviour is common across many programming languages.

In many cases, we do not need the full precision of a floating-point number. For example, dividing 5 by 3 yields an infinitely repeating value:

**- 1.66666…**

We often choose a fixed number of decimal places for practical purposes. Instead of manually trimming digits, we typically **round** the result. For example, rounding to four decimal places:

**- 1.667**

Python provides the `round()` function to simplify this:

```
>>> round (c,1)
0.3
```

Floating-point and integer values can be converted back and forth easily, and Python will often perform conversions automatically during arithmetic operations:

```
>>> a = 164
>>> b = 37
>>> a = a / b
>>> print(a)
4.4324324324324325

>>> type(a)
<class 'float'>

>>> c = int(a)
>>> print(c)
4

>>> type(c)
<class 'int'>

>>> d = float(c)
>>> print(d)
4.0
```

Very small floating-point values are displayed using scientific notation. Python will automatically format these numbers in exponential form, even when converted to strings:

```
>>> a =  0.002
>>> print(type(a),a)
<class 'float'> 0.002

>>> b = 0.000002
>>>print(type(b),b)
<class 'float'> 2e-06

>>> c = str(b)
>>> print(c)
2e-06
```

When handling extremely large or small values, scientific notation becomes practical. If we need to control the level of displayed precision in these cases, we can use format specifiers. In the example below, the value is rounded to three significant digits:

```
>>> a = 1.4966517743e17

>>> print("%.3g"%a)
1.5e+17
```

With floating-point concepts refreshed, we can now move forward to explore complex numbers.
