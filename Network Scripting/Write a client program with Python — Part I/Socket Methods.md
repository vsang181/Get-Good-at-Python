# Socket Methods

The most common type of socket applications are client–server applications, such as the one we are currently building. This involves a client making a request to the server, and the client then receives a response from the server.

The socket module comes with various methods to facilitate the different actions a client (or a server) will perform during such communication. There are three sets of socket methods that we need to be aware of: client socket methods, server socket methods, and general socket methods. Usually, though not always, a client will invoke client socket methods, a server will invoke server socket methods, and both programs can make use of the general socket methods.

The `socket.gethostname()` method returns the name of the current system. We will be using it in our scripts to test execution on our local machine. This means that if we want to run our scripts against an external server, we will need to specify the IP address of the remote target.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808
```

In the above listing, we specify our own local host with the `socket.gethostname()` method and then specify the port we want to connect on as an integer.

The `socket.connect(address)` method is used to initiate a connection with the server. The method requires that we specify a single host and port to connect to, which we defined in the `host` and `port` variables.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
host = socket.gethostname()
port = 808

soc.connect((host, port))
```

Notice the double parentheses within the `soc.connect((host, port))` syntax. The reason for this is because the socket module treats `(host, port)` as a single argument. If we include only one pair of parentheses, Python would interpret our syntax as attempting to provide two arguments to a method that accepts only one.

Now that we understand how to use the `socket.connect` method, there are some general socket methods that we need to become familiar with so our client can receive data and terminate properly.

The `socket.recv(bufsize)` method allows the client to receive a TCP message from the socket. The `bufsize` (buffer size) argument defines the maximum amount of data that the method can receive at any one time.
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

In the above listing, a client would connect to a server and then print out any data it receives from the server via the `socket.recv()` method.

We now have enough code to connect to a server.

> If you are following along, you will not yet have the server code to test your client. For now, simply ensure that the client code you have written is identical to the code above.

```
~ % ./basic_client.py 
Connection Established
```

In the above listing, we execute our client against a server running on our own localhost and receive a message from the server that the connection has been established.

The `socket.close()` method is straightforward, as it will simply close the socket. This can be invoked from either end and will terminate the connection between the client and the server.

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

We have now built a fully functioning client program in Python. Our script is designed to connect to a local server that is running on port 808. The `socket.connect()` method will establish the connection. If the connection is successful, the client will receive a message from the server using `socket.recv()`. The `socket.close()` method will close the client, and finally the `print` function will decode and display the message from the server.
