# Working with Files

Reading from and writing to files is an important function for data ingestion and for saving information that persists after the script finishes running. To open a file, we use the `open()` function and assign it to a variable. We must specify both the file name and the mode in which to open it.

The available modes are:

- Read: `"r"` – Opens the file for reading (default mode).

- Write: `"w"` – Opens the file for writing. This will overwrite the file if it already exists.

- Append: `"a"` – Opens the file for appending. Data is added to the end of the file if it exists.

- Read and Write: `"r+"` – Opens the file for both reading and writing.

If we want to work with binary files, we append a `b` to the mode (e.g., `"rb"` for reading binary, `"wb"` for writing binary). For now, we will focus on working with text files.

## Reading a File

To open a file in read mode and store it in a variable:

```
x = open("data.txt", "r")
```

Once the file is opened, we can read its contents using the `read()` method:

```
y = x.read()
```

This stores the entire contents of the file into the variable y as a single string. However, reading the entire file at once might not be efficient—especially with large files such as logs. To read a file line by line, we can use a loop along with readline() or simply iterate over the file object:

```
x = open("data.txt", "r")

for y in x:
    print(y)
```

Each iteration stores the current line in the variable `y`, which we can then process.

## Writing to a File

To write data to a file, we open it in either write (`"w"`) or append (`"a"`) mode. Using `"w"` will overwrite the file if it already exists, while `"a"` will preserve the existing content and add new data to the end.

```
z = "Hello there would you like to visit my chocolate factory?"

x = open ("data.txt", "a")

x.write(z)
```

## Closing a File

After we are done reading or writing, it is good practice to close the file using the close() method:

```
x.close()
```

While not always strictly necessary in small scripts, closing files helps free up system resources and ensures that other programs or scripts can access the file if needed. It is a best practice to always close any files you open.

