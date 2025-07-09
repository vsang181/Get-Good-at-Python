# Wiriting our First Python Script

We will begin our introduction to Python with a few simple examples, gradually progressing to more complex and practical scripts. While we cannot cover every detail here, Python's widespread popularity means there is a wealth of documentation and community support available should you encounter any issues.

Similar to Bash scripting, we can instruct the system to interpret a file as a Python script using a shebang line. This line specifies the absolute path to the Python interpreter and is placed at the top of the script file. A typical shebang for Python 3 might look like:

```
#!/usr/bin/python3
```

Once this line is added, the script can be saved, made executable using the `chmod` command, and run directly from the terminal using:

```
chmod +x randomscript.py
```

Alternatively, a Python script can be executed using the python3 command, which does not require a shebang line or executable permissions.

## Creating a Simple Python Script

Let us create a basic script that outputs a message to the terminal:

```
#!/usr/bin/python3
print("Hello World – isn't scripting fun?")
```

This script contains two lines:

- The first line (`#!/usr/bin/python3`) is the shebang, which tells the operating system to use the Python 3 interpreter located at `/usr/bin/python3`.

- The second line uses the `print()` function to display the message:

    `Hello World – isn't scripting fun?`

## Making the Script Executable

Before we can run the script directly, we need to set the appropriate permissions:

```
chmod +x randomscript.py
```

Once the script is executable, we can run it as follows:

```
~ % ./randomscript.py
Hello World – isn't scripting fun?
```

The output confirms that the script executed successfully and printed the expected message.

## Running Without Executable Permissions

Alternatively, we can run the script using the `python3` command, which does not require executable permissions or a shebang line:

```
~ % python3 randomscript.py
Hello World – isn't scripting fun?
```

Although the shebang line is not required when using this method, it is still considered good practice to include it, especially when sharing scripts or running them across different systems.
