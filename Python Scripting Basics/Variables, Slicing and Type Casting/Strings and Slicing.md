# Strings and Slicing

Most people new to Python will already be familiar with strings from other programming languages. In Python, strings are data types used to store sequences of characters—such as letters, numbers, and symbols—and are typically defined by enclosing the value in quotation marks.

## Defining Strings

Let us review two examples of string variables:

```
myName = "Victor"
notMyName = "RANDOM@2025"
```

In the code above, we have created two string variables: `myName` and `notMyName`, each containing different values.

## What Is Slicing?

Strings in Python can be sliced, which means extracting a portion of the string by specifying start and end positions (called indices). This technique is commonly used to extract relevant parts of a string or a list, especially in tasks such as data cleaning, automation, or even web scraping.

For example, suppose we are writing a Python script to scrape a website for hyperlinks—a task commonly carried out by penetration testers when gathering information about a target. A typical HTML anchor tag might look like this:

```
<a href="https://www.securityshenanigans.com">My Website</a>
```

To extract only the URL portion (`https://www.securityshenanigans.com`), we can use string slicing.

> Note: Because the string contains double quotes (`"`), we will use single quotes (`'`) to define the entire string in Python to avoid syntax issues.

## Manual Slicing

Let us first extract the URL manually by identifying the start and end indices:

```
~ % cat slicing.py
#!/usr/bin/python3

x = '<a href="https://www.securityshenanigans.com">My Website</a>'
url = x[9:44]

print(url)
```

When we run the script:

```
~ % ./slicing.py
https://www.securityshenanigans.com
```

Explanation:

- Index 9 is where the URL starts (the `"h"` in `https`).

- Index 44 is where it ends (just after the `"m"` in `.com`).

By slicing from index `9` to `44` (note that the end index is exclusive), we retrieve the exact URL.

## Using `index()` for Dynamic Slicing

Manually counting indices is not practical in real-world scripts. Instead, we can locate the start and end dynamically using the `.index()` function, which returns the position of a substring within a string:

```
~ % cat slicing_2.py
#!/usr/bin/python3

x = '<a href="https://www.securityshenanigans.com">My Website</a>'
start = 'http'
end = '">'

print(x.index(start))  # Outputs: 9
print(x.index(end))    # Outputs: 44
```

Now that we know how to find these positions dynamically, we can use them directly in our slicing operation:

```
~ % cat slicing_3.py
#!/usr/bin/python3

x = '<a href="https://www.securityshenanigans.com">My Website</a>'
start = 'http'
end = '">'

url = x[x.index(start):x.index(end)]

print(url)
```

Running this script:

```
~ % ./slicing_3.py
https://www.securityshenanigans.com
```

## Final Notes

In the final example:

- `x.index(start)` dynamically finds the starting index of the URL.

- `x.index(end)` finds where the URL ends.

- `x[...]` slices the string accordingly.

The advantage of this method is that it works regardless of the length or structure of the anchor tag, as long as the patterns (`http` and `">`) remain consistent. This makes the script far more flexible and reliable for real-world use cases.





























