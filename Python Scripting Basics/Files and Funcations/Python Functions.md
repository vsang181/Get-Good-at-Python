# Python Functions

A function is a block of code that can be reused later in the same script or in another external script or program. Functions must be defined before they can be called. To define a function, we use the def keyword followed by the function name. The function definition line ends with parentheses and a colon.

The value of using functions lies in how they help organize code into small, manageable blocks. This makes programs easier to understand, maintain, and debug. Rather than writing a long, monolithic script, you can divide your code into smaller, reusable pieces that can be assembled together. We will explore this idea further in the final section of this documentation.

## Function Structure

As a general guideline, it is a good idea to keep functions under 30 lines of code. While this number is arbitrary, smaller functions are easier to manage, test, and debug. If possible, strive for even fewer lines per function.

Here is an example of a simple function:

```
~ % cat pythonFunction.py
#!/usr/bin/python3

def helloThere():
    print("General Kenobi!")
```

This function is named `helloThere()` and simply prints a line of text to the terminal.

Now let us run this script:

```
~ % ./pythonFunction.py
```

Despite defining a function, nothing is shown in the terminal. Why? Because we never called the function. Defining a function does not execute it—it only makes it available to be called. If you try to call a function before it is defined, the script will raise an error because, at that point, the function "does not exist" to the interpreter.

## Calling a Function

Let us now call the function in the same script:

```
~ % cat pythonFunction_1.py
#!/usr/bin/python3

def helloThere():
    print("General Kenobi!")

helloThere()
```

Now run the updated script:

```
~ % ./pythonFunction_1.py
General Kenobi!
```

Perfect! This time the function was defined and then called, which executed the instructions inside the function—printing the message to the terminal.

This was a basic example, but even simple functions like this will prove useful later in this module.

## Function Arguments and Return Values

To make functions more dynamic, we can supply arguments. Arguments (also called parameters or variables, though technically they differ in scope) are passed within the parentheses when calling the function. Functions can also return values using the `return` statement, allowing us to use the output elsewhere in our script.

Let us look at an example function that adds two numbers and returns the result:

```
def addNumbers(numberA, numberB):
    sresult = numberA + numberB
    return result
```

We have defined a function `addNumbers` that takes two arguments: `numberA` and `numberB`. Inside the function, we add the two values and store the sum in the `result` variable. Then, we return `result` to the caller.

Now let us call the function in a script:

```
~ % cat pythonFunction_2.py
#!/usr/bin/python3

def addNumbers(numberA, numberB):
    sresult = numberA + numberB
    return result

x = addNumbers(6, 9)

print(x)
```

Run the script:

```
~ % ./pythonFunction_2.py
15
```

As expected, the output is `15` because `6 + 9 = 15`.

> Note: The `return` statement does not print the result to the terminal—it simply sends the value back to the part of the script that called the function. In this case, we printed the result manually using `print(x)`.
