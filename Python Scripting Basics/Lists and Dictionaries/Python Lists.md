# Python Lists

A list is a built-in Python data type that allows you to store multiple values in a single variable. These values are stored in an indexed order, meaning each element in the list has a numerical position starting from zero.

Python lists can contain values of different data types—including strings, numbers, and even other lists.

## Defining a List

A list is defined using square brackets `[]`, with individual items separated by commas:

```
~ % cat randomList.py
#!/usr/bin/python3

groceryList = ["chicken", "paprika", "italianherbs"]

print(type(groceryList))
```

Output:

```
~ % ./randomList.py
<class 'list'>
```

As expected, the output confirms that `groceryList` is a list.

## Accessing Items by Index

Each item in a list is associated with an index. For example:

- `"chicken"` has an index of `0`

- `"paprika"` has an index of `1`

- `"italianherbs"` has an index of `2`

If you know the value in the list but not its index, you can use the `.index()` method to find its position:

```
~ % cat randomList_2.py
#!/usr/bin/python3

groceryList = ["chicken", "paprika", "italianherbs"]

print(groceryList.index("italianherbs"))
```

Output:

```
~ % ./randomList_2.py
2
```

This confirms that `"italianherbs"` is located at index `2`.

> Note: The `.index()` method is also useful in string slicing, which we discussed earlier.

## Adding Items to a List

To add a new item to the end of a list, use the `.append()` method:

```
~ % cat randomList_3.py
#!/usr/bin/python3

groceryList = ["chicken", "paprika", "italianherbs"]

groceryList.append("garlic")

print(groceryList)
```

Output:

```
~ % ./randomList_3.py
['chicken', 'paprika', 'italianherbs', 'garlic']
```

As shown, the value `"garlic"` is appended to the end of the list.

## Removing Items from a List

To remove a specific item from a list, use the `.remove()` method:

```
~ % cat randomList_4.py
#!/usr/bin/python3

groceryList = ["chicken", "paprika", "italianherbs", "garlic"]

groceryList.remove("garlic")

print(groceryList)
```

Output:

```
~ % ./randomList_4.py
['chicken', 'paprika', 'italianherbs']
```

Here, `"garlic"` was successfully removed from the list.

## Getting the Length of a List

To find out how many items are in a list, use the built-in `len()` function:

```
~ % cat randomList_5.py
#!/usr/bin/python3

groceryList = ["chicken", "paprika", "italianherbs"]

print(len(groceryList))
```

Output: 

```
~ % ./randomList_5.py
3
```

This tells us that the list contains three items.


