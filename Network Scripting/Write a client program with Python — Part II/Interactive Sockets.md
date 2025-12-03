# Interactive Sockets

In many situations, we may want to establish a connection to a server and then continue communicating with it based on what the server sends back to us. Rather than connecting, receiving a single message, and closing the connection, we can maintain an interactive session. To achieve this behaviour, we can use Python’s `telnetlib` module, which provides an implementation of the Telnet protocol and includes built-in functionality for interactive communication.

Let us begin by reviewing our original client script and preparing it for modification.
```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808

soc.connect((host, port))
msg= client.recv(1024)
cleint.close()

print (msg.decode(`ascii`))
```

To introduce interactivity, we will import the `telnetlib` module and use its `interact()` method. This method enables a live, two-way communication loop between our client and the server. It continuously listens for incoming data and sends outgoing data until the connection closes.

We will begin by writing a wrapper function that will set up the Telnet object and initiate the interactive session.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

def interact(socket):
    t = telnetlib.telnet()
    t.sock = s
    t.interact()

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808

soc.connect((host, port))
msg= client.recv(1024)

print (msg.decode(`ascii`))
cleint.close()
```

A few details to notice:

- The name of our wrapper function is `interact`, but it is distinct from `telnetlib`’s `interact()` method. This is perfectly acceptable because each name exists in its own scope.
- Inside the function, we create a Telnet object, assign our socket to it, and then invoke the built-in `interact()` method.
- The Telnet `interact()` method internally uses a `while True` loop to continuously read from and write to the socket, allowing the client to remain active for as long as the server keeps the connection open.

Next, we will call our new function after establishing the connection and receiving the server’s initial message.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

def interact(socket):
    t = telnetlib.telnet()
    t.sock = s
    t.interact()

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808

soc.connect((host, port))
msg= client.recv(1024)

print (msg.decode(`ascii`))
interact(client)
cleint.close()
```

With these changes, our client is now capable of entering an interactive session after receiving the server’s initial response. This means:

1. **The connection must remain open** — If the server closes the connection immediately after sending data, the client will not be able to continue interacting.
2. **The server must accept and handle additional input** — An interactive client is only useful if the server is designed to respond to whatever the user sends next.

Since we have not yet implemented our own interactive server, you will test this behaviour using the remote VM provided in the next exercise.
