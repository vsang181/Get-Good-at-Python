# Setting Variables

Before exploring the various types of variables available in Python, let us first understand how to define and use them. To demonstrate this, we will use the `print()` function to display the values of variables in the terminal.

## How to Set a Variable

In Python, setting a variable is straightforward. You assign a value to a variable name using the equals sign (`=`). Here's a simple example:

```
~ % cat variables.py
#!/usr/bin/python3

firstName = "Victor"
currentYear = 2025

print(firstName)
print(currentYear)
```

In this script:

- We define two variables:

  - `firstName` holds the string value `Victor`.
  - `currentYear` holds the integer value `2025`.

- We then use the `print()` function to output their values to the terminal.

## Executing the Script

Once the script has executable permissions, running it will produce the following output:

```
~ % ./variables.py
Victor
2025
```

As expected, the `print()` function displays the values assigned to each variable. This illustrates how Python stores and accesses variable data during execution.
