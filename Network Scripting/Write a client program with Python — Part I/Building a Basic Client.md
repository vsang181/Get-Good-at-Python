# Building a Basic Client

Python is one of the most widely used languages in penetration testing and network automation due to its simplicity and the vast ecosystem of powerful libraries. One area where Python excels is in network scripting, especially when working with sockets. Sockets allow programs to communicate across networks, whether locally on the same machine or across the internet.

A socket acts as an endpoint for network communication. When two programs communicate, one acts as a server (listener) while the other acts as a client (initiator). Both use sockets to exchange data. Python gives us access to low-level socket functionality through its built-in `socket` module, which exposes the standard socket API.

As we begin writing our client-side program, it is strongly recommended that you type out each example manually rather than copying and pasting. Typing the code reinforces understanding and helps build your muscle memory for commonly used syntax.

Let us begin creating a simple Python script that imports the socket library and initialises a socket object.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(<socket_family>, <socket_type>, <protocol>)
```

In the example above, we imported the `socket` module and assigned the return value of `socket.socket()` to a variable named `soc`. This method accepts three parameters: `socket_family`, `socket_type`, and `protocol`. Before we supply values to these parameters, let us briefly examine what each one represents.

## socket_family

This parameter determines which addressing scheme the socket will use. The most common options include:

• `AF_INET` — for IPv4 addressing
• `AF_INET6` — for IPv6 addressing
• `AF_UNIX` — for Unix Domain Sockets (UDS), which allow inter-process communication without involving the network stack

For our purposes, we will use `AF_INET`, as most common network communication still relies on IPv4.

## socket_type

This determines the communication style of the connection:

• `SOCK_STREAM` — for TCP, a reliable, connection-oriented protocol
• `SOCK_DGRAM` — for UDP, a faster, connectionless protocol

Since we want a stable communication channel between our client and server, we will use TCP (`SOCK_STREAM`).

## protocol

This typically specifies a protocol number. In most cases, setting it to `0` allows Python to automatically select the default protocol based on the given socket family and type. Because TCP is the default protocol for an IPv4 stream socket, `0` is appropriate here.

Now let us supply the correct values to create a TCP over IPv4 client socket:

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```

Notice that we have omitted the third parameter (protocol). Since the default value of `0` is appropriate here, Python will automatically use the standard TCP protocol for our socket.

At this stage, we have successfully created the foundation of our client program. As we progress, we will gradually build additional functionality by learning and applying core socket methods. By the end of this module, we will have a working client capable of establishing a connection with a server, sending and receiving data, and handling variable-length network responses.
