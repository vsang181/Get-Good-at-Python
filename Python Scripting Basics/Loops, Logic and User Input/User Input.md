# User Input

So far, we have set variables directly inside our scripts, which works for basic examples. However, this approach does not make our programs very interactive. Prompting the user for input can greatly enhance a script's flexibility, allowing different values to be entered at runtime.

Let us consider the following code:

```
~ % cat userInput.py
#!/use/bin/python3

x = Victor
y= 25

print("Hi" + x + ".")

if y >= 100:
    print("You appears to be about century old, did you personally knew any dinosaurs in your time?")
elif y >= 50:
    print("you appears to be half a century old, damn you are old ")
elif y >= 20:
    print("You appears to be few decades old, why do you still not have a job?")
elif y >= 18:
    print("You appears to be an adult, why do you still nto have a driving license?")
else:
    print("How to does it feel to still live with your parents?")
```

Here, we create two variables, print a greeting, and run conditional statements based on the value of the `y` variable.

Output:

```
~ % ./userInput.py
Hi Victor.
You appears to be few decades old, why do you still not have a job?
```

The script works, but it is not flexible. Each time we want to change the name or age, we must edit the script manually. This can be tedious and inefficient. Instead, we can make the script interactive by using the `input()` function.

The syntax for the `input()` function is:

```
input("Your prompt message here")
```

Let us improve the script using `input()`:

```
~ % cat userInput_1.py
#!/use/bin/python3

x = input("Would you please provide me your name: ")
y= input("May I ask how old are you: ")

print("Hi" + x + ".")

if y >= 100:
    print("You appears to be about century old, did you personally knew any dinosaurs in your time?")
elif y >= 50:
    print("you appears to be half a century old, damn you are old ")
elif y >= 20:
    print("You appears to be few decades old, why do you still not have a job?")
elif y >= 18:
    print("You appears to be an adult, why do you still nto have a driving license?")
else:
    print("How to does it feel to still live with your parents?")
```

Output:

```
~ % ./userInput_1.py
Would you please provide me your name: Victor
May I ask how old are you: 25
HiVictor.
Traceback (most recent call last):
  File "/Users/victorsangwan/./slicing.py", line 8, in <module>
    if y >= 100:
TypeError: '>=' not supported between instances of 'str' and 'int'
```

The script fails. This error occurs because the `input()` function always returns a string, and we are trying to compare it to an integer in the conditional statements.

To resolve this, we need to use type casting to convert the age input from a string to an integer:

```
~ % cat userInput_2.py
#!/use/bin/python3

x = input("Would you please provide me your name: ")
y= int(input("May I ask how old are you: "))

print("Hi" + x + ".")

if y >= 100:
    print("You appears to be about century old, did you personally knew any dinosaurs in your time?")
elif y >= 50:
    print("you appears to be half a century old, damn you are old ")
elif y >= 20:
    print("You appears to be few decades old, why do you still not have a job?")
elif y >= 18:
    print("You appears to be an adult, why do you still nto have a driving license?")
else:
    print("How to does it feel to still live with your parents?")
```

Output:

```
~ % ./userInput_2.py
Would you please provide me your name: Victor
May I ask how old are you: 25
HiVictor.
You appears to be few decades old, why do you still not have a job?
```

This works correctly.

## A Note on Input Validation

While we have fixed the type error using `int()`, users may still enter invalid values. For example:

```
~ % ./userInput_2.py
Would you please provide me your name: Victor
May I ask how old are you: twenty five
Traceback (most recent call last):
  File "/Users/victorsangwan/./userInput_2.py", line 4, in <module>
    y= int(input("May I ask how old are you: "))
```

This error occurs because Python cannot convert a non-numeric string to an integer.

Handling such issues is out of scope for this module, but it is important to note that input validation is a critical concept in programming. It helps protect against:

- Invalid data types
- Special characters
- Excessively long inputs
- And other security vulnerabilities

In future lessons, we will explore how to properly validate and sanitize user input.
