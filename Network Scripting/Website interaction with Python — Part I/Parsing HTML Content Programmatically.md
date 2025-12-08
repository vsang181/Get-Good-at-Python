# Parsing HTML Content Programmatically

When using `requests.content()` or `requests.text()` to retrieve a webpage, you will often receive a large amount of raw HTML data. While this is useful for inspection, it is rarely convenient when we only want to extract specific information.
This is where **web scraping** becomes valuable. Web scraping allows us to filter, narrow down, and extract only the important data from a webpage.

As penetration testers, this can save us a significant amount of time. Instead of manually searching through a webpage, we can write a script that retrieves the exact details we are interested in—whether links, comments, meta tags, banners, or hidden fields.

## Retrieving Webpage Content with urllib3

We will begin by using the `urllib3` module to send an HTTP request and obtain the raw HTML content of a webpage. While the `requests` library internally uses `urllib3`, here we import it directly so that we become familiar with alternative HTTP-handling syntax.

```
~ % cat parse.py 
#!/usr/bin/python3

import urllib3

http = urllib3.PoolManager()

url = 'https://www.securityshenanigans.com/'

res = http.request('GET', url)
print(res.data.decode('utf-8'))
```

In this script:

- `urllib3.PoolManager()` creates a connection manager to handle HTTP requests.
- The `url` variable stores the target we want to fetch.
- `http.request('GET', url)` retrieves the HTML from the website.
- `res.data.decode('utf-8')` converts the raw bytes into human-readable text.

Running the script prints the entire HTML response to the terminal. To avoid displaying the full output, we can pipe it into the `head` command:

```
~ % ./parse.py | head -n 20
<!DOCTYPE html><html lang="en"> <head><meta charset="utf-8">...
...
```

This confirms that our script successfully retrieves the webpage content.
However, the output is still raw HTML—unstructured and difficult to read.

## Introducing BeautifulSoup for HTML Parsing

To make the data more readable and to extract specific elements from the page, we will now introduce the **BeautifulSoup** library.

BeautifulSoup allows us to:

- Parse HTML into a structured, searchable format
- Extract specific tags, attributes, or text
- Cleanly format the webpage content for easier

Modify your script as follows:

```
~ % cat parse.py 
#!/usr/bin/python3

import urllib3

from urllib.request import urlopen
from bs4 import BeatifulSoup

url = 'https://www.megacorpone.com/'

page = url.read()
beaut = BeautifulSoup(page, features="html.parser")

print(beaut)
```

Key points:

- `urlopen()` retrieves the raw HTML data.
- `.read()` stores this data in memory.
- `BeautifulSoup()` parses the HTML into a structured format using the built-in HTML parser.
- Printing the `beaut` variable now displays formatted HTML output.

Example output:

```
~ % ./parse.py
<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta http-equiv="X-UA-Compatible" content="IE=edge"/>
<meta name="viewport" content="width=device-width, initial-scale=1"/>
<title>MegaCorp One - Nanotechnology Is the Future</title>
<link href="assets/css/bootstrap.css" rel="stylesheet"/>
<link href="assets/css/style.css" rel="stylesheet"/>
<link href="assets/css/font-awesome.min.css" rel="stylesheet"/>
...
...
```

While this output may look similar to the raw HTML, the key difference is that the content is now **parsed**, meaning BeautifulSoup can help us:

- Isolate specific tags,
- Extract text,
- Find links,
- Navigate through nested HTML structures,
- Clean up unnecessary formatting.

## Extracting Only Textual Content

BeautifulSoup’s `text` method allows us to extract only the human-readable text from the webpage, ignoring all the HTML tags.

For example:

```
print(beaut.text)
```

This will output only the visible text on the webpage—much easier to process, search, or analyse during reconnaissance.
