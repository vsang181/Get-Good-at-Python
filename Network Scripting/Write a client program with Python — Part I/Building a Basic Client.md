# Building a Basic Client

Although there are many programming languages that we can use to complete our tasks, Python is a very popular language that penetration testers use to create their network scripts. This is due to its ease of use and the large number of libraries available for it.

For programs and systems to communicate with each other on a network, they use sockets and the socket API to send messages back and forth. A socket is essentially an endpoint that allows network communication to flow between two programs running over a network. We can implement network sockets on several different channel types.

As we begin to write our scripts, we recommend that you follow along and type the syntax in your own Python files. Try not to copy and paste the code, because writing it yourself can help reinforce understanding and memory.

Let us use the following code to start creating a script that uses the socket module. We will import the socket library for our Python script and then call the `socket.socket` method.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(<socket_family>, <socket_type>, <protocol>)
```

Above, we see the `socket.socket` method assigned to the variable `soc`. The `socket.socket` method itself contains three (currently unset) variables: `socket_family`, `socket_type`, and `protocol`. Let us examine these variable placeholders.

The `socket_family` variable allows us to specify a protocol domain that will act as the transport mechanism. The most common, `AF_INET`, is used for IPv4 Internet addressing, and `AF_INET6` is used for IPv6 Internet addressing. `AF_UNIX` is the address family for Unix Domain Sockets (UDS). This socket family allows the operating system to pass data directly from process to process without going through the network stack.

The `socket_type` variable specifies the communication style between two endpoints. The socket type is usually either `SOCK_DGRAM` for the User Datagram Protocol (UDP) or `SOCK_STREAM` for the Transmission Control Protocol (TCP).

The `protocol` variable can be used to specify the protocol number. It is usually set to `0`, which is the default value that will be used if it is not specified.

To supply these variables with values, we will create a socket that communicates with an IPv4 address using TCP to transmit our communications.

```
~ % cat basic_client.py 
#!/usr/bin/python3

import socket

soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```

Notice that we have not specified a protocol, so it will default to the value of `0` as mentioned above.

We will continue to expand on this script as we create our client. Before we proceed, we need to understand some of the methods that are built into the socket module. We will slowly build up our client by applying each relevant method. At the end of this process, we will have a fully functional networking client that can handle errors and receive data of arbitrary length.





