# Exploring Complex Numbers

Python provides built-in support for working with **complex numbers**, which consist of both a real part and an imaginary part. Complex numbers commonly arise when performing square-root operations on negative values and are widely used in fields such as engineering, signal processing, and fluid dynamics. A complex number is represented in the form **x + yj**, where:

- **x** = real component
- **y** = imaginary component
- **j** = the imaginary unit (equivalent to √−1)

```
>>> a = 17 + 3j
>>> print(a)
(17+3j)

>>> type(a)
<class 'complex'>

>>> b = complex(17, 3)
>>> print(b)
(17+3j)
```

Python allows us to create complex numbers either through literal notation (using `j`) or via the `complex()` function.

We can access the real and imaginary components using built-in attributes:

```
>>> print(a.real)
17.0

>>> print(a.imag)
3.0

>>> print(a.conjugate())
(17-3j)
```

- `.real` returns the real part of the number.
- `.imag` returns the imaginary part.
- `.conjugate()` returns the complex conjugate, which negates the imaginary component.

Complex numbers support standard mathematical operators and can be used in many numerical functions. However, they **cannot** be directly converted into integers or floating-point values. If needed, you may convert either component individually:

```
int(a.real)     
float(a.imag)      
```

Complex numbers remain a powerful tool in advanced mathematical computation, and Python’s native support makes them easy to manipulate when required.
