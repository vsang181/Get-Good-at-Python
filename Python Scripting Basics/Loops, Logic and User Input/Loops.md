# Loops

Looping is a fundamental concept in programming that allows us to repeat a block of code multiple times, either while a condition is true or over a defined sequence of elements. Python provides two primary types of loops:

1. `while` loops

2. `for` loops

## While Loops

A `while` loop will continue executing its code block as long as the specified condition evaluates to `True`. It is crucial to ensure the loop’s condition will eventually become `False`; otherwise, the loop will run indefinitely and the script may have to be terminated manually.

Let us consider a simple `while` loop example:
    
```
~ % cat whileLooop.py
#!/use/bin/python3

x = 0
while x < 10:
    print(x)
    x += 1
```

Output:

```
~ % ./whileLooop.py
0
1
2
3
4
5
6
7
8
9
```

Here, the loop continues as long as `x` is less than `10`. On each iteration, `x` is printed and then incremented by 1 using the shorthand operator `+=`. This is equivalent to writing `x = x + 1`.

> Note: Python relies on indentation to define blocks of code. The indented lines under while `x < 10`: belong to the loop. If they are not properly indented, Python will treat them as being outside of the loop and may raise a syntax error.

## While Loops with Lists

We can also iterate over a list using a `while` loop. Consider the following example:

```
~ % cat groceryList.py
#!/use/bin/python3

groceryList = ["Chicken", "Paprika", "Italianherbs", "Garlicpaste"]

groceryListCount = len(groceryList)

print("There are " + str(groceryListCount) + " items in teh grocery list.")

groceryIndex = 0
while groceryIdex < groceryListCount:
    print(groceryList[groceryIdex])
    groceryIdex += 1
```

Output:

```
~ % ./groceryList.py
["Chicken", "Paprika", "Italianherbs", "Garlicpaste"]
There are 4 items in the grocery list.
Chicken
Paprika
Italianherbs
Garlicpaste
```

In this example:

- We determine the number of items using `len()`.

- We then iterate over the list using a `while` loop and index-based access.

> In practice, you might skip the list count message or avoid printing the full list at the beginning. However, this is useful for illustrating the mechanics of `while` loops with lists.

## For Loops

A `for` loop in Python is used to iterate over a sequence such as a list, range, or dictionary. With a `for` loop, Python handles the counter automatically—there is no need to initialise or increment it manually as you do in a `while` loop.

Let us examine a basic example:

```
~ % cat forLoop.py
#!/use/bin/python3

for y in range(11):
    print(y)
```

Output:

```
~ % ./forLoop.py
0
1
2
3
4
5
6
7
8
9
10
```

This loop iterates through numbers from `0` to `10`, inclusive. The `range()` function returns a sequence of numbers starting at `0` by default and ending just before the stop value.

## Using Range with Start, Stop, and Step

The `range()` function can also accept three arguments:

```
range(start, stop, step)
```

- `start`: where the loop should begin

- `stop`: the value at which the loop will stop (not inclusive)

- `step`: how much to increment by each time

Example:

```
~ % cat forLoop_2.py
#!/use/bin/python3

for y in range(5,33,4):
    print(y)
```

Output:

```
~ % ./forLoop_2.py
5
9
13
17
21
25
29
```

Here, the loop starts at `5` and increases by `4` each time until just before `33`.

## Looping Through a Dictionary

We can also use a `for` loop to iterate through a dictionary’s contents. One common use is to loop through its keys and then access each associated value.

```
~ % cat forLoop_3.py
#!/use/bin/python3

person = {"Name":"Victor",
            "Age":"25",
            "University":"Queen's University Belfast",
            "Degree":"Masters"}

for key in person.keys():
      print(key + ": " + person[key])
```

Output:

```
~ % ./forLoop_3.py
Name: Victor
Age: 25
University: Queen's University Belfast
Degree: Masters
```

This technique:

- Loops through all the keys in the dictionary using .keys()``

- Prints each key followed by a colon and the corresponding value

## Summary

- `while` loops repeat as long as a condition is true.

- `for` loops repeat over sequences like lists, ranges, or dictionaries.

- Use `range(start, stop, step)` to control for loop iteration.

- Proper indentation and loop syntax are essential in Python.

- Looping through dictionaries allows dynamic access to structured data.
