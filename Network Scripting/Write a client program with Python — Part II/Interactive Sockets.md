# Interactive Sockets

Sometimes we may want to establish a connection with a server and then send it data based on the information it provides us. To do this, we can create an Interactive Socket with the `telnetlib` library. Let us begin with our original script and import `telnetlib`.

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

The `telnetlib` module allows for an implementation of the Telnet protocol. We will be modifying our script to make use of the `telnetlib.interact()` method, which will allow us to interact with the server dynamically. To implement this method, we will create a function that we will call after our client has connected to the server.

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

Notice that the function we have created is named `interact`. The name of the Telnet method is also `interact`! This is not essential—we could call our function anything we wish. However, it is a good reminder that we should always understand the scope of different code blocks so that we do not become confused.

The mechanism that allows this client to maintain interactivity with the server is handled entirely through Telnet’s own `interact` function. This function sets up a `while True` loop that continuously reads and writes data. Since `True` is always true, it continues to read and write data from and to the server until the connection is closed.

Next, we will call our new function after we connect to the server.

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

In the above listing, our client code is now capable of interacting dynamically with the server it connects to. Note that this functionality depends on two things:

1. The server must allow the connection to stay open. If it closes the connection, our client will not be able to send any further data.

2. The server must be configured to receive the data we send to it. Since we have not yet implemented our own server, you can try the above client code against the remote VM in the following exercise.
