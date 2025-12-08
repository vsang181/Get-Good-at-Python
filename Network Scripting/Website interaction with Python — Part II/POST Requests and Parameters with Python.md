# POST Requests and Parameters with Python

The `requests` module also allows us to send data to a server through an HTTP **POST** request. Unlike a GET request—where data is appended directly to the URL—POST requests transmit data within the **request body**. This is the mechanism used by most websites when handling form submissions, such as login fields, search fields, or subscription forms.

POST requests are especially useful during web application testing, because they allow us to:

- Submit credentials
- Emulate browser-based forms
- Interact with APIs
- Test how a server validates and processes user-supplied data

Let us examine a simple script that performs a POST request and displays the server's response:

```
~ % cat web_client.py
#!/usr/bin/python3

import requests

url = "https://www.securityshenanigans.com/"

info = {'check-key': 'check-value'}
post = requests.post(url, data=info)
print(post.text)
```

In this listing:

- The variable `url` stores the destination address of the POST request.
- The dictionary `info` represents the data we want to send to the server. Each key–value pair functions like a form field.
- The `requests.post()` method transmits the data in the body of the request.
- The response returned by the server is stored in the `post` object, and we display it using `post.text`.

This simple pattern can be expanded to include more complex data structures, authentication tokens, cookies, or JSON payloads depending on the server’s expectations.

Although we have focused on POST requests, the `requests` module provides additional HTTP methods such as **PUT**, **DELETE**, **HEAD**, and **OPTIONS**, each corresponding to different forms of web application interaction. As you continue building your scripting skills, we encourage experimenting with these methods to better understand how web servers behave and how different types of requests influence their responses.
