# Combining File Operations in a Function

We have already covered how to work with files and how to define and use functions. Now, let us combine these two concepts to simplify file operations using a function. This will allow us to read the contents of a file into a variable, making it easier to work with that data within our script.

Consider the following example:

```
~ % cat fileManipulation.py
#!/usr/bin/python3

def storeFile(file):
    x = open(file, 'r')
    y = x.read()
    x.close()
    return y

# variable to store the filename
z = "file.txt"

y = storefile(z)
print(y)
```

This script does the following in a single function call:

1. Opens the specified file in read mode (`'r'`),

2. Reads its contents and stores them in a variable,

3. Closes the file, and

4. Returns the contents for further use in the script.

We then assign the filename to the variable `z` and pass it to the function `storeFile()`. The return value is stored in `y`, which we then print.

## Sample Output (assuming `file.txt` contains the line below):

```
~ % ./fileManipulation.py
What's cooking, Good looking?
```

This function allows us to work with the file’s contents through the variable `y` without making any direct modifications to the file itself. This reduces the risk of accidentally altering or corrupting the file—especially useful when dealing with sensitive data.

Another benefit of this function is that it ensures the file is closed as soon as it is no longer needed, which is a best practice in file handling.
