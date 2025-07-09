# Data Types

Python is relatively flexible when it comes to handling data types, especially when compared to lower-level programming languages. It allows for dynamic typing, meaning that variables do not need to be explicitly declared with a type. Additionally, variables can be converted from one data type to another through a process known as type casting—which we will cover in more detail later.

That said, it is still essential to understand the basic data types available in Python, particularly when writing scripts that handle user input, perform calculations, or process data.

## Assigning Values to Variables

We assign values to variables using the equals sign (`=`). If the value is enclosed in quotation marks, Python treats it as a string. This distinction is important because the way Python handles the variable depends on its data type.

## Using `print()` in Python

The `print()` function is used to display output to the terminal. It functions similarly to the `echo` command in Bash scripting. The syntax for Python 3 is as follows:

```
myName = "Victor"
print(myName)

# or simply:
print("Victor")
```

## Checking a Variable’s Data Type

While debugging or validating logic in your script, you may wish to verify the type of a variable. This can be done using Python’s built-in `type()` function, which returns the data type of the value passed to it:

```
~ % cat example.py
#!/usr/bin/python3

x = "Victor"
print(x)
print(type(x))

y = 2025
print(y)
print(type(y))
```

## Output

```
~ % ./example.py
Victor
<class 'str'>
2025
<class 'int'>
```

## Explanation

In this example, we created two variables: `x` and `y`.

- `x` is a string with the value `Victor`. This is confirmed by the output `<class 'str'>`.

- `y` is an integer with the value `2025`, confirmed by `<class 'int'>`.

By printing both the value and its data type, we can easily inspect and validate how Python is interpreting each variable.
