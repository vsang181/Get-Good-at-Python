# Understanding the Transport Layer: Using the Python socket Module with HTTP

Imagine that we have identified a web server as our target and want to learn more about how it behaves. In this situation, we can write a Python script that sends HTTP requests directly to the server and analyses its responses. This technique is extremely useful for understanding how a web service communicates with clients, and it can also reveal whether the service is vulnerable to known exploits.

To perform this analysis, we will once again use the `socket` module to create a raw TCP connection to a web server running on port 80. Because we are working at the Transport Layer, our script must manually provide the HTTP request we want to send. In other words, we must encapsulate the Application Layer (HTTP) data inside the Transport Layer (TCP) connection ourselves.

We will begin our script by importing the `socket` module and defining the remote host and port we intend to communicate with.

```
~ % cat http-soc.py 
#!/usr/bin/python3

import socket

rm = "www.securityshenanigans.com/"
rp = 80
```

We name our script `http-soc.py`. It is important that we do not name the file `http.py`, because Python already includes a built-in module with that name, which would cause conflicts.

Next, we will store the exact HTTP request we want the server to receive. We will assign this request to a variable called `req`.

```
~ % cat http-soc.py 
#!/usr/bin/python3

import socket

rm = "www.securityshenanigans.com/"
rp = 80

req = "GET / HTTP/1.1\r\nHost: www.securityshenanigans.com\r\n\r\n"
```

Since we are constructing the HTTP request manually, we must include the precise syntax that HTTP expects, including the required newline characters (`\r\n`). Without the correct formatting, the server may ignore or reject our request.

Now let us initialise a socket and then connect to the remote server. Once connected, we will use the `socket.send()` method to transmit our HTTP request.

```
~ % cat http-soc.py 
#!/usr/bin/python3

import socket

rm = "www.securityshenanigans.com/"
rp = 80

req = "GET / HTTP/1.1\r\nHost: www.securityshenanigans.com\r\n\r\n"

cl = socket.socket(socket.AFINET, socket.SOCK_STREAM)
cl.connect((rm,rp))
cl.send(req.encode())
```

Finally, we want to capture and display the server’s response. We will retrieve the data using the `socket.recv()` method and then decode and print it.

```
~ % cat http-soc.py 
#!/usr/bin/python3

import socket

rm = "www.securityshenanigans.com/"
rp = 80

req = "GET / HTTP/1.1\r\nHost: www.securityshenanigans.com\r\n\r\n"

cl = socket.socket(socket.AFINET, socket.SOCK_STREAM)
cl.connect((rm,rp))
cl.send(req.encode())

resp = c;.recv(4096)
print(resp.decode())
```

It is important to note that the `send()` method requires a byte-like object, not a string. This is why we call `.encode()` on our request variable. Conversely, when we receive raw bytes from the server, we use `.decode()` to convert them back into a readable string.

The `recv()` method accepts a single argument, which specifies the maximum number of bytes to receive at one time. In this case, we are receiving up to 4096 bytes of data from the server.
