# Socket Methods

Most networking applications follow a client–server model, where a client initiates communication and a server listens for incoming requests. Our current project follows this same pattern: we are building a client that will reach out to a server, establish a connection, and receive a response. To achieve this, we must understand several fundamental socket methods that Python provides through its built-in `socket` module.

The `socket` module contains three main categories of methods:

1. **Client socket methods** — generally used by the connecting side
2. **Server socket methods** — used by the listening side
3. **General socket methods** — used by both clients and servers

Although these distinctions exist, it is important to note that certain methods can be used by either side depending on the needs of the program.

One useful general method is s`ocket.gethostname()`. This method returns the hostname of the machine on which the script is running. Throughout this module, we will rely on this method when testing our programs locally. When you later run your client against a remote system, you will simply replace the hostname with the server’s IP address.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808
```

In this example, we created a TCP socket using IPv4 (`AF_INET` and `SOCK_STREAM`), retrieved our local hostname, and specified port `808` as our connection target.

To initiate a connection to the server, we use the `socket.connect(address)` method. This method expects a single argument, which must be a tuple consisting of `(host, port)`.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808

soc.connect((host, port))
```

Notice the double parentheses in `soc.connect((host, port))`. This is intentional.
If we use only one pair of parentheses, Python would incorrectly interpret the host and port as separate arguments, causing an error. By wrapping them in an additional set of parentheses, we pass the required tuple as a single argument.

Once the connection is established, we can receive data from the server using the `socket.recv(bufsize)` method. This method accepts a buffer size that determines how many bytes can be read from the server at one time.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808

soc.connect((host, port))
msg = soc.recv(1024)

print(msg.decode('ascii'))
```

Here, the client connects to the server, then waits to receive up to 1024 bytes of data. The response is stored in the variable `msg`, decoded from ASCII, and printed to the console.

At this stage, your client is complete enough to establish a connection—assuming there is a server actively listening on the same machine at port 808. If you are following along, you will soon create the server in a later module.

Example output may resemble the following:

```
~ % ./basic_client.py 
Connection Established
```

This indicates that the client successfully connected and received a message from the server.

To gracefully terminate the connection, we use the `socket.close()` method. This ensures the socket is properly shut down, freeing system resources and closing the communication channel.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808

soc.connect((host, port))
msg = soc.recv(1024)
soc.close()

print(msg.decode('ascii'))
```

With this, we have a fully functional Python client. It:

1. Creates a TCP socket
2. Connects to a server on the specified host and port
3. Receives a message
4. Closes the connection
5. Outputs the server’s response to the terminal

This foundation prepares us to continue building more advanced networking tools, beginning with server-side code in the next section.
