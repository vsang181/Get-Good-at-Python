# Handling Unknown Data Size

In the above demonstration, we assumed that the server was only going to send our script 1024 bytes of data. Sometimes, however, we may not be able to anticipate the exact size of the server's response. Let us execute our script against a server that sends us more than 1024 bytes and examine what happens.

We have adjusted our server so that it sends the "Connection Established" string followed by 2000 `"A"` characters. We will then execute our script and pass the results to `sed`, `tr`, and `wc` to count the exact number of `"A"` characters we receive from the server.

```
~ % ./basic_client.py | sed 's/[^A]//g' | tr -d '\n' | wc -c
    1002
```

Since the "Connection Established" string is 22 characters long, 1002 out of the 2000 `"A"` characters are sent to the client. This is because our implementation of the `socket.recv` method only allows 1024 bytes of data to be received by our client.

The socket module documentation suggests that the value used for each `socket.recv` call should be a small power of 2, such as 1024, 2048, or 4096. When we do not know how many bytes we will receive, we can process the response in a loop by using smaller chunks until all data has been received. In the following exercise, you will add a loop to the client program so that it can receive arbitrary chunks of data.
