# Building a Basic Server

We will start building our server by importing the `socket` module, initializing a socket, and defining a host and port:
```
~ % cat server.py 
#!/usr/bin/python3

import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
h = socket.gethostname()
p = 8080
```

Note that this code is almost identical to the beginning of our client-side code. We will now introduce a few more socket methods that our server will need to make use of.

The `socket.bind(address)` method binds, or assigns, a specific address and port to our program. In this case, we want to bind our server to the port we defined in the `port` variable

```
~ % cat server.py 
#!/usr/bin/python3

import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
h = socket.gethostname()
p = 8080

s.bind((host, port))
```

Like the `socket.connect` method, `socket.bind` expects a complete address as input in the format `(host, port)`. This is why there are double parentheses in the method call.

The `socket.listen(int)` method tells the server to listen for incoming connections and expects an integer.

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

The integer specified in socket.listen() represents the number of clients the server will allow to connect to itself simultaneously. Once the server is listening, it reports its status via the print function.

The socket.accept() method returns a pair of values (conn, address) where conn represents a new socket that will send and receive messages, and address represents the client address bound to the socket.

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

In the above listing, we start a `while True` loop that allows incoming connections via the newly created `conn, address` pair. Once a connection has been established, our server will report that the connection has occurred.

The `socket.send(bytes)` general socket method allows a client or server to send data to a socket. This data can then be received via the `socket.recv` method. The `bytes` argument provides the sequence of bytes that will be sent to the socket. Specifying these bytes correctly can affect how the method interacts with the receiving machine.

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

In the above listing, we use the new `conn` socket to send the text `"Connection Established"` to the client once it connects to the server.

We have now almost completed our server. The last functionality we will add is the ability to close the socket from the server side with `socket.close()`.

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

Notice how we close the `conn` socket and not the original server socket `s`, to allow our server to keep running and to accept further connections.

Let us summarise what we have learned. After creating a new socket, we use the `socket.bind()` method, which binds the program to a specified IP address and port. This allows the server to listen for incoming requests. To make sure the server is listening for these requests, we use the `socket.listen()` method. Once the client has requested to connect, we use the `socket.accept()` method to accept the connection and the `socket.send()` method to send a message back to the client. Finally, we invoke `socket.close()` (in this case, on the connection socket `conn`) to terminate the connection.
