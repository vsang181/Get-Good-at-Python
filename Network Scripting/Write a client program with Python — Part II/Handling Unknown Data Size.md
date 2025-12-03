# Handling Unknown Data Size

n the previous demonstration, we assumed that the server would send no more than 1024 bytes of data. This worked because our server’s response happened to fit within that limit. However, in real-world scenarios, we often cannot predict how much data a server will send. A response may be a few kilobytes—or it may be several megabytes. If our client assumes a fixed size and the server sends more than that amount, the excess data will be lost.

To illustrate this problem, let us adjust our server so that it sends the string `"Connection Established"` followed by 2000 `"A"` characters. We will then run our client script and pipe its output through `sed`, `tr`, and `wc` to count exactly how many `"A"` characters the client receives.

```
~ % ./basic_client.py | sed 's/[^A]//g' | tr -d '\n' | wc -c
    1002
```

The string `"Connection Established"` contains 22 characters.

Since our client receives a total of 1024 bytes (as defined by the `socket.recv(1024)` call), only 1002 of the 2000 `"A"` characters are actually captured.

This demonstrates a key limitation of our current approach:

- `socket.recv(bufsize)` reads up to the specified number of bytes.
- Any remaining data is left unread until another `recv()` call is made.

Because the server sent more than 1024 bytes, our client only collected the first chunk and discarded the rest.

## How to Handle Variable-Length Data

According to the socket module documentation, the buffer size for each `recv()` call should generally be a small power of two—common values include **1024**, **2048**, or **4096** bytes.

When we do not know how large the server’s response will be, the correct approach is to:

1. Read data in chunks.
2. Append each chunk to a growing buffer.
3. Continue reading until the server finishes sending data.

This requires a loop that continuously receives data until `recv()` returns an empty byte string, indicating that no more data is available.
