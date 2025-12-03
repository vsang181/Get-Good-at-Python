# Error handling: `try` and `except` Clauses

As we build more advanced client programs, it becomes increasingly important to ensure that our scripts behave predictably, even when unexpected problems occur. For example, a server may fail to respond, the connection may time out, or the server may reject our request altogether. Without proper error handling, our Python script would simply crash, leaving the user without any meaningful information about what went wrong.

To avoid this, Python provides structured error handling through the use of `try` and `except` statements.

A simplified example of a `try`/`except` pair in pseudo-code looks like this:

```
try:
    do something
    break
except <exception type>:
    print an error statement
```

The logic works as follows:

- The `try` block contains code that Python will attempt to run.
- If all instructions inside the `try` block execute successfully, Python will skip the `except` block entirely and continue with the rest of the program.
- If an error (known as an exception) occurs at any point inside the `try` block, Python immediately stops executing that block and jumps to the matching `except` block.
- The code within the `except` block then runs, allowing us to handle the error gracefully.
- If the program encounters an exception for which no matching `except` block exists, execution stops completely, resulting in an unhandled exception.

Let us now implement proper error handling in our client program.

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

In this implementation, we specifically handle the `ConnectionRefusedError` exception. This error is raised when a server is not listening on the target port or is unable to accept a connection. Running the client while no server is active on port 808 confirms that our error-handling logic works:

```
~ % ./basic_client.py
The server is not accepting our connection request!
```

Notice that the final `print` statement never executes. This is because the `except` block prints the error message and exits the program immediately.

Although our error-handling logic currently prints a simple message and terminates the script, we could easily expand it to perform more complex actions—such as retrying the connection, attempting a failover server, or logging detailed diagnostic information.

In the upcoming exercise, you will use `try` and `except` blocks to implement reconnection logic that attempts to connect to a server multiple times before giving up.
