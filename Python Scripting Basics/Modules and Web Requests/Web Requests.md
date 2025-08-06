Web Requests

There are many powerful modules available in Python. In this section, we will focus on the `requests` module, which is commonly used for making web requests.

## Importing the `requests` Module

Let us begin by importing the module. Create a file named `webRequest.py`:

```
~ % cat webRequest.py
#!/usr/bin/python3

import requests
```

The `requests` module includes several useful functions and properties, such as:

- `get`

- `status_code`

- `headers`

- `encoding`

- `text`

- `json`

To keep things simple for now, we will focus on three of them: `get`, `status_code`, and `text`.

## Making a Web Request

Let us modify our script to send a GET request to the following URL:

https://www.securityshenanigans.com/

We will store the response in a variable and display the status of the webpage.

```
~ % cat webRequest.py
#!/usr/bin/python3

import requests

x = requests.get('https://www.securityshenanigans.com/')
print(x.status_code)
```

Here, the result of `requests.get()` is stored in the variable `x`. This response object contains the status code and other information about the request.

## Executing the Script

When we run the script:
```
~ % ./webRequest.py
200
```

A `200` status code means that the webpage was successfully reached. This kind of response code is useful when checking if a website or web resource is accessible. Other status codes might indicate problems (e.g., `404` for not found, `403` for forbidden, or `500` for server error).

If a resource is blocked, unavailable, or the request fails, the response might include an error code or even halt program execution if not handled properly.

## Viewing the Webpage Content

Although the HTTP response code is useful, it is usually not the main goal. Let us add another line to display the actual content of the page using the `.text` property.

Update your script as follows:

```
~ % cat webRequest_1.py
#!/usr/bin/python3

import requests

x = requests.get('https://www.securityshenanigans.com/')
print(x.status_code)
print(x,text)
```

Now, execute the updated script:

```
~ % ./webRequest_1.py
200
<!DOCTYPE html><html lang="en"> <head>...
```

The full HTML source code of the webpage is printed to the terminal. The example output above is trimmed for clarity, but in practice, it will show the complete HTML content of the page.

This HTML content can now be manipulated, parsed, or filtered within your Python script using additional tools or techniques (e.g., with libraries like `BeautifulSoup` or `re`).
