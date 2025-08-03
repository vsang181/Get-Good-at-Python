# Importing a Module

One of the best aspects of Python is its large and active community. There are countless resources available to help solve problems, improve your code, or accomplish complex tasks more efficiently. Often, someone has already solved a problem you are facing and shared their solution as a Python module.

Examples of popular Python modules include:

- `json`

- `requests`

- `numpy`

You may also encounter situations where your own Python scripts become large or complex. In such cases, it is a good idea to split your code into multiple files (modules) and import functionality as needed. This helps keep your code clean, organized, and reusable in other projects.

## Creating and Importing a Custom Module

Let us begin by creating a custom module. Save the following as `importingModule.py`:

```
~ % cat importingModule.py
#!/usr/bin/python3

alcohol = ["Single Malt Whiskey", "Irish Cream", "Lager"]

snacks = ["peanuts", "crisps", "sausage rolls"]

def printItems(y):
    for x in y:
        print(x)
```

Now, create another script in the same directory, named `importingModule_1.py`, to import the module and use its contents.

```
~ % cat importingModule_1.py
#!/usr/bin/python3

import importingModule

print(importingModule.alcohol)
print(importingModule.snacks)

importingModule.printItems(importingModule.alcohol)
```

How It Works

- The `import` statement loads the entire module.

- You access the module's contents using `module_name.content_name`, e.g., `importingModule.alcohol`.

- Python first searches for the module in the current directory. If not found, it checks the system-wide locations listed in the `PYTHONPATH`.

## Importing Specific Items

Typing `importingModule`. every time can become tedious. You can import specific components instead:

```
~ % cat importingModule_2.py
#!/usr/bin/python3

from importingModule import alcohol, printItems

print(alcohol)
printItems(alcohol)
print(snacks)
```

Output:

```
["Single Malt Whiskey", "Irish Cream", "Lager"]
Single Malt Whiskey
Irish Cream
Lager
Traceback (most recent call last):
  File "/Users/victorsangwan/./importingModule_2.py", line 7, in <module>
    print(snacks)
NameError: name 'snacks' is not defined
```

As shown above, trying to use `snacks` results in an error because it was not imported. You must explicitly import anything you want to use.

## Importing Everything (Not Recommended)

You can also import everything using the asterisk (`*`), but this is discouraged in most cases because it can:

- Pollute the namespace

- Make it hard to trace where a variable or function came from

- Increase the chances of name collisions

```
from importingModule import *
```

Use this only when you are certain that there are no naming conflicts and the module is small and predictable.
