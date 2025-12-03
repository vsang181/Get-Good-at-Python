# Working at the Application Layer: Making HTTP GET Requests with Python

Python allows us to communicate directly over HTTP without having to manually craft raw TCP packets. Instead of working at the Transport Layer with sockets, we can operate at the Application Layer by using the `requests` library, which greatly simplifies sending and receiving HTTP messages.

In this section, we will use the `requests` module to create a simple HTTP GET request and display the response.

Let us begin our script by importing the `requests` module and defining a target URL that we want to query.
```
~ % cat web_client.py 
#!/usr/bin/python3

import requests

url = "www.securityshenanigans.com"
```

Next, we will use our first `requests` method: `requests.get()`. This method sends an HTTP GET request to the URL provided and returns a response object. This response object can then be inspected, parsed, and formatted in various useful ways.

```
~ % cat web_client.py 
#!/usr/bin/python3

import requests

url = "www.securityshenanigans.com"

res = requests.get(url)
print(response.content.decode())
```

In the above listing, we access the raw bytes of the response using `res.content`. We then decode these bytes and print them so that we can view the page contents in plain text.

The basic script can be modified in many ways to extract specific information from a web server. For example, during the reconnaissance phase of a penetration test, we might only be interested in retrieving the **status** **code** of a particular page.

The `res.status_code` attribute allows us to extract the HTTP status code from the server’s response.

```
~ % cat web_client.py 
#!/usr/bin/python3

import requests

url = "www.securityshenanigans.com/doesnotexist.html"

res = requests.get(url)
print(response.status_code)
```

As a reminder, HTTP status codes fall into the following categories:

- 100–199: Informational responses
- 200–299: Successful responses
- 300–399: Redirects
- 400–499: Client errors
- 500–599: Server errors

Since the path `/doesnotexist.html` does not exist, the server will return a 404 – Not Found error, which falls under the Client Error category.

Next, let us modify the script so it prints only the response headers. This can be achieved using the `res.headers` attribute. Analysing headers can give us valuable information about the server’s configuration, technology stack, and behaviour.

```
~ % cat web_client.py 
#!/usr/bin/python3

import requests

url = "https://www.securityshenanigans.com/"

res = requests.get(url)
print(response.headers)
```

This version of the script sends a request to the homepage of the site and prints all header information returned by the server.

Finally, the `res.text` attribute allows us to print the response body in Unicode.

```
~ % cat web_client.py 
#!/usr/bin/python3

import requests

url = "https://www.securityshenanigans.com/"

res = requests.get(url)
print(response.text)
```

This script makes a request to the specified URL and prints the page content in a readable, text-based format.

Remember the following rule of thumb:

- Use `res.content` when the server returns **binary data** (e.g., an image, PDF, or file download).
- Use `res.text` when the server returns **textual data** (e.g., HTML, JSON, XML).

If you are unsure which to use, try both and compare the results.
