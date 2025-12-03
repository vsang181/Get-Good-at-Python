# Building a Basic Server

We will start building our server by importing the `socket` module, initialising a socket, and defining a host and port:

```
~ % cat server.py 
#!/usr/bin/python3

import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
h = socket.gethostname()
p = 8080
```

This initial code is almost identical to the beginning of our client-side script. The main difference is how we will use this socket. On the server side, we must bind the socket to a specific address and port, then **listen** for incoming connections.

The `socket.bind(address)` method binds, or assigns, a specific address and port to our program. In this case, we want to bind our server to the `host` and `port` we defined in the host and port variables.

```
~ % cat server.py 
#!/usr/bin/python3

import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
h = socket.gethostname()
p = 8080

s.bind((host, port))
```

Like the `socket.connect` method on the client, `socket.bind` expects a single argument that is a tuple in the format `(host, port)`. This is why we see double parentheses in the call `s.bind((host, port))`.

Next, we must instruct the server to listen for incoming connections. We do this using the `socket.listen(int)` method, which expects an integer representing the maximum number of queued connections.

```
~ % cat server.py 
#!/usr/bin/python3

import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
h = socket.gethostname()
p = 8080

s.bind((host, port))
s.listen(2)
s
print('Server is listening for incoming connections')
```

The integer `2` in `s.listen(2)` represents the maximum number of queued client connections that the server will allow at once. Once `listen` has been called, the server is actively waiting for connection requests. We use `print` to provide a status update.

To accept incoming connections, we use the `socket.accept()` method. This method blocks until a client attempts to connect and then returns a pair of values: `(conn, address)`.

- `conn` is a new socket object that will be used to send and receive data.
- `address` is the address of the client connected to the server.

```
~ % cat server.py 
#!/usr/bin/python3

import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
h = socket.gethostname()
p = 8080

s.bind((host, port))
s.listen(2)
s
print('Server is listening for incoming connections')

while true:
    conn, address = s.accept()
    print("Connection recieved from %s" % str(addr))
```

In the above listing, we start a `while True` loop to allow the server to accept connections indefinitely. Each time a client connects, the server:

1. Creates a new socket object `conn` for that connection.
2. Captures the client address in `address`.
3. Prints a message reporting the connection.

To send data back to the client, we use the general socket method `socket.send(bytes)`. This method takes a sequence of bytes and transmits them over the socket. The data can then be received by the client using its `socket.recv` method.

```
~ % cat server.py 
#!/usr/bin/python3

import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
h = socket.gethostname()
p = 8080

s.bind((host, port))
s.listen(2)
s
print('Server is listening for incoming connections')

while true:
    conn, address = s.accept()
    print("Connection recieved from %s" % str(addr))
    msg = 'Connection Established' + "\r\n"
    conn.send(msg.encode('ascii'))
```

In this version, once a connection is accepted, the server sends the text `"Connection Established"` (followed by a carriage return and newline) to the client. We use `encode("ascii")` to convert the string into a byte sequence suitable for transmission.

The final step is to close the connection socket after we have responded to the client. We do this using `socket.close()` on the `conn` object. Closing only the connection socket allows the main server socket `s` to continue listening for new clients.

```
~ % cat server.py 
#!/usr/bin/python3

import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
h = socket.gethostname()
p = 8080

s.bind((host, port))
s.listen(2)
s
print('Server is listening for incoming connections')

while true:
    conn, address = s.accept()
    print("Connection recieved from %s" % str(addr))
    msg = 'Connection Established' + "\r\n"
    conn.send(msg.encode('ascii'))
    conn.close()
```

Notice that we call `conn.close()` and not `s.close()`. The `conn` socket represents the individual client connection, while `s` is the main listening socket. If we closed `s`, the server would stop accepting new connections.

Let us summarise the key points:

1. After creating a socket, we use `socket.bind()` to attach it to a specific IP address and port.
2. We call `socket.listen()` so that the server can listen for incoming connection requests.
3. When a client attempts to connect, `socket.accept()` returns a new connection socket and the client’s address.
4. We use `socket.send()` on the connection socket to transmit data back to the client.
5. Finally, we call `socket.close()` on the connection socket (`conn`) to terminate that particular connection, while keeping the main server socket active.

With this, we have a fully functional basic server that can be tested using the client we previously built.
