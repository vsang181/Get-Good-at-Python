# Python Dictionaries

In Python, a dictionary is a data structure that stores data in the form of key-value pairs. Dictionaries allow for fast, meaningful access to values based on their associated keys. They are defined using curly braces {}.

## Creating a Dictionary

You can create a dictionary by enclosing comma-separated key-value pairs inside curly brackets, like so:

```
randomDictionary = {
    "firstName": "Victor",
    "lastName": "S",
    "company": "Darktrace"
}
```

In the example above, the dictionary `randomDictionary` contains three key-value pairs.

## Adding a New Key-Value Pair

To add a new entry to a dictionary, simply reference the dictionary using the new key, and assign it a value:

```
~ % cat randonDictionary.py
#!/usr/bin/python3

randomDictionary = {
    "firstName": "Victor",
    "lastName": "S",
    "company": "Darktrace"
}

randomDictionary["age"] = "25"

print(randomDictionary)
```

Output:

```
~ % ./randonDictionary.py
{'firstName': 'Victor', 'lastName': 'S', 'company': 'Darktrace', 'age': '25'}
```

The new key `"age"` with the value `"25"` has been added to the dictionary.

## Accessing Values by Key

You can retrieve a value by referencing its key within square brackets:

```
~ % cat randonDictionary_2.py
#!/usr/bin/python3

randomDictionary = {
    "firstName": "Victor",
    "lastName": "S",
    "company": "Darktrace"
}

print(randomDictionary["firstName"])
```

Output:

```
~ % ./randonDictionary_2.py
Victor
```

Here, we accessed the value `"Victor"` by referencing the key `"firstName"`.

## Modifying an Existing Value

To update the value of an existing key, use the same syntax as when adding a new pair. If the key already exists, the value will simply be overwritten:

```
~ % cat randonDictionary_3.py
#!/usr/bin/python3

randomDictionary = {
    "firstName": "Victor",
    "lastName": "S",
    "company": "Darktrace"
}

randomDictionary["age"] = "25"

print(randomDictionary)

randomDictionary["company"] = "Unemployed"

print(randomDictionary)
```

Output:

```
~ % ./randonDictionary_3.py
{'firstName': 'Victor', 'lastName': 'S', 'company': 'Darktrace', 'age': '25'}
{'firstName': 'Victor', 'lastName': 'S', 'company': 'Unemployed', 'age': '25'}
```

As shown, the value for `"company"` has been updated from `"Darktrace"` to `"Unemployed"`.

## Retrieving Dictionary Keys

To get a list of all the keys in a dictionary, you can use the `.keys()` method:

```
~ % cat randonDictionary_4.py
#!/usr/bin/python3

randomDictionary = {
    "firstName": "Victor",
    "lastName": "S",
    "company": "Darktrace"
}

print(randomDictionary.keys())
```

Output:

```
~ % ./randonDictionary_4.py
dict_keys(['firstName', 'lastName', 'company'])
```

This returns a special view object containing all the dictionary’s keys. You can convert it to a list if needed by wrapping it with `list()`.
