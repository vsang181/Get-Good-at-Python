# Testing our Client and Server

Now that we have built both our client and server programs, let us verify whether they work correctly together. To do this, we will open two terminal windows: one to run the server and one to run the client. This separation allows us to observe how the programs interact in real time.

In Terminal One, start the server. You should see the following output:

```
~ % ./server.py
Server is listening for incoming connections
```

This confirms that the server is running and is ready to accept inbound connections.

Next, switch to Terminal Two and run the client program. The expected output is:

```
~ % ./basic_client.py
Connection Established
```

his shows that the client successfully connected to the server.

To further confirm the interaction, return to Terminal One, where the server is still running. You should now see additional output similar to:

```
~ % ./server.py
Server is listening for incoming connections
Connection Recieved from ('127.0.0.1', 48904)
```

Notice that in this example, the connection originates from port `48904`, which was automatically assigned to the client when it initiated the socket connection to our server on port 8080. You may observe a different port number when running your own programs; this is expected.

These automatically assigned ports are known as ephemeral ports. They are allocated temporarily by the operating system from a predefined range to ensure a free port is always available for outgoing connections. This mechanism allows multiple clients to connect simultaneously without conflicts, even if they are all connecting to the same server and port.
