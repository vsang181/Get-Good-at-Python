# Conditional Statements

When scripting, there are often sections of code that we want to run only under specific conditions. To achieve this, we can use conditional statements such as `if`, `elif`, and `else`.

In Python, indentation (tabs or spaces) and newlines are essential for defining blocks of code. If an `if` statement evaluates to `True`, the indented code underneath it will be executed. As with loops, a colon (`:`) and a newline are required after the condition.

```
~ % cat conditionalStatement.py
#!/use/bin/python3

if numChoclates > 100:
    print("We got enough chocolate at home!")
```

As long as the value of `numChocolates` is greater than 100, the `print` function inside the `if` block will run.

When the `if` condition evaluates to `False`, the indented code is skipped. If you want to evaluate other conditions, you can use the `elif` (short for 'else if') statement. You can include as many `elif` conditions as needed, as long as there is an initial `if`.

```
~ % cat conditionalStatement_1.py
#!/use/bin/python3

if numChoclates > 100:
    print("We got enough chocolate at home!")
elif numChoclates > 50:
    print("We have decent amount of chocolates home")
elif numChoclates > 30:
    print("There is some chocoalte at home")
```

If the value of `numChocolates` is greater than 100, the first condition is `True`, and its corresponding code block will run. All subsequent conditions will be skipped. If not, the script continues evaluating the next `elif` conditions.

If none of the `if` or `elif` statements evaluate to `True`, you can use an `else` statement to provide a catch-all block. The code under the `else` will only run if all preceding conditions are `False`.

```
~ % cat conditionalStatement_2.py
#!/use/bin/python3

if numChoclates > 100:
    print("We got enough chocolate at home!")
elif numChoclates > 50:
    print("We have decent amount of chocolates home")
elif numChoclates > 30:
    print("There is some chocoalte at home")
else:
    print("I eblieve we are running low on chocolates at home!")
```

Let us now define the variable `numChocolates` with a specific value and see how it affects the conditional logic. The variable must be set before the conditional block.

```
~ % cat conditionalStatement_3.py
#!/use/bin/python3

numChoclates = 231

if numChoclates > 100:
    print("We got enough chocolate at home!")
elif numChoclates > 50:
    print("We have decent amount of chocolates home")
elif numChoclates > 30:
    print("There is some chocoalte at home")
else:
    print("I eblieve we are running low on chocolates at home!")
```

Output:

```
~ % ./conditionalStatement_3.py
We got enough chocolate at home!
```


