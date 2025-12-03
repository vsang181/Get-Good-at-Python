# Testing our Client and Server

Now that we have built both our client and server programs, let us verify that they work correctly together. To do this, we will open two terminal windows—one to run the server and one to run the client. This setup allows us to see both sides of the communication process as it happens.

In `Terminal One`, start the server. You should see the following output:

```
~ % ./server.py
Server is listening for incoming connections
```

This indicates that the server is running properly and is ready to accept inbound connections.

Next, switch to `Terminal Two` and run the client program. The expected output will look like:

```
~ % ./basic_client.py
Connection Established
```

This confirms that the client successfully connected to the server and received the message sent by the server.

To further validate the interaction, return to `Terminal One` where the server is still running. You should now see an additional message such as:

```
~ % ./server.py
Server is listening for incoming connections
Connection Recieved from ('127.0.0.1', 48904)
```

Notice that the connection originates from port `48904`. This port was automatically assigned to the client when it initiated the socket connection to the server’s listening port (`8080`). When you run your own programs, the number you see may differ—this is completely normal.

These automatically assigned ports are known as ephemeral ports. They are temporary ports chosen by the operating system from a predefined range to ensure an available and conflict-free port is always used for outgoing connections. This mechanism is what enables multiple clients to connect simultaneously, even when they are all connecting to the same server and the same destination port.

With this step completed, we have successfully tested our basic client and server setup.
