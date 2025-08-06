# Creating a Python Socket Client

To get started with our Python network client script, we will first need to import the `socket` module.

```
~ % cat networkClient.py
#!/usr/bin/python3

import socket
```

Next, we need to create a socket object. In our example, we will name it `x`.

```
x = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```

The syntax might seem complex, so let us break it down:

- `socket()` is a function that takes two arguments: `AF_INET` and `SOCK_STREAM`.

- `AF_INET` specifies that we are using an IPv4 address.

- `SOCK_STREAM` specifies that we are using a TCP connection.

Now that we have set up the socket, we can connect to a remote server. For this demonstration, we will connect to the IP address `192.168.0.4` on port `1234`.

```
x.connect(("192.168.0.4", 1234))
```

> Note: The IP address and port are passed together as a single tuple to the connect() function.

After connecting, let us check if the server sends anything to the client. We can do this using the recv() function:

```
print(x.recv(1024))
```

The number `1024` specifies the buffer size (in bytes) for receiving data. It defines how much data we can read at once. While you can set it higher or lower, 1024 bytes is a reasonable default for simple cases.

Once we receive the data, we will close the socket connection using the `close()` function.

Let us review the complete script so far:

```
~ % cat networkClient.py
#!/usr/bin/python3

import socket

x = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
x.connect(("192.168.0.4", 1234))

print(x.recv(1024))
x.close()
```

Now, let us run the script and see the output:

```
~ % ./networkClient.py
b'What is cooking,\ngood looking?'
```

You may notice the output includes a `b` before the string. This indicates that the data is in binary format (also known as a byte string). Additionally, the string contains a `\n` (newline character) that is not displayed as a new line.

The server is sending encoded data. We can decode this data on the client side using the `decode()` function. Let us update our `print()` statement accordingly:

```
print(x.recv(1024).decode())
```

Now let us run the updated script:

```
~ % ./networkClient.py
What is cooking,
good looking?
```

That is better! The text is properly formatted, and the binary prefix is gone.

The server only sent a fixed message. Of course, real-world applications are often much more complex and involve back-and-forth communication where the client sends data as well.

>The service on port 1234 has now been updated to allow the client to send input. These examples are meant to be followed along with rather than run exactly as-is.

Let us run the original script again and see what the server now says:

```
~ % ./networkClient.py
How many chocolates do you want?
```

Now the server is requesting a number, which we can send using the `send()` function.

Here is our updated script to send a value:

```
~ % cat networkClient.py
#!/usr/bin/python3

import socket

x = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
x.connect(("192.168.0.4", 1234))

print(x.recv(1024).decode())
x.send("6".encode())
x.close()
```

We are sending the number 6, encoded as a string so the server can interpret it.

Let us run the script:

```
~ % ./networkClient.py
How many chocolates do you want?
```

The output is the same. That is because we never checked for new data the server might have sent after receiving our input.

Let us fix that by adding another `recv()` call:

```
~ % cat networkClient.py
#!/usr/bin/python3

import socket

x = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
x.connect(("192.168.0.4", 1234))

print(x.recv(1024).decode())
x.send("6".encode())
print(x.recv(1024).decode())

x.close()
```

Now let us run the script one last time:

```
~ % ./networkClient.py
How many chocolates do you want?
Here are your 6 chocolates.
```

Perfect! The server accepted our input and responded accordingly.
