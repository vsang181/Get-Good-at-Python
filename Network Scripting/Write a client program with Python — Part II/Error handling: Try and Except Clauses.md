# Error Handling: Try and Except Clauses

Sometimes, our code may not work as desired because the server responds in a way that we do not expect or because it is not working properly. To make our program more robust, we can introduce error handling that will tell the client what to do if it encounters an error.

Python makes use of `try` and `except` statements to handle errors. Here is an example of what a `try` and `except` pair might look like in pseudo-code:

```
try:
    do something
    break
except <exception type>:
    print an error statement
```

A `try` statement attempts to execute any code within the `try` block. If the code within the `try` block executes successfully, the program will skip over the `except` block and continue its normal execution flow.

If, however, it does encounter an error (also known as an exception), execution flow will immediately jump to the corresponding `except` block with the matching exception type. Then, the code within the `except` block is executed to handle the exception. Once the `except` block finishes executing, the program will continue its execution flow.

Finally, if there is no corresponding exception type for the error encountered within the `try` block, the program will stop its execution because it does not know how to continue. This is called an unhandled exception.

Let us go ahead and add `try` and `except` statements to our Python client.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808

try:
    soc.connect((host, port))
    msg = soc.recv(1024)
    soc.close()
    print(msg.decode('ascii'))

except ConnectionRefusedError:
    print("The server is not accepting our connection request!")
    exit(1)

print("This sentence will only print if the except block was not executed.")
```

The above code checks for the specific exception called `ConnectionRefusedError`, which indicates that a server is unwilling or unable to accept the client’s connection. We can run our client code against a non-existent server to validate the `try`/`except` blocks.

```
~ % ./basic_client.py
The server is not accepting our connection request!
```

Notice how the last line of our program is not executed. This is because the `except` block prints a statement and then exits the program before the last line can run.

Here, we are only using the `except` block to print a statement and exit. However, we could create far more complex instructions, allowing our program to perform diagnostics, connect to another server, or take some other action. In the following exercise, you will use `try` and `except` statements to allow the program to reconnect to a server an arbitrary number of times.
