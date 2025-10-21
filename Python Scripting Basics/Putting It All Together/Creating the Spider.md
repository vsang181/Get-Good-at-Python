# Creating the Spider

Now that we have developed our spider program concept in pseudocode and represented it through a flowchart, the next step is to translate this plan into executable code. Rather than presenting the entire completed script and then explaining it, we shall proceed step by step, writing and testing each section in accordance with our flowchart. This approach allows us to verify the functionality of individual components as we progress, rather than debugging a large, finalised codebase at once.

To begin, we must establish the foundation of our program. We shall name the script webSpider.py and add the shebang line, which informs the operating system which interpreter to use when executing the file.

```
#!/usr/bin/python3
```

According to our flowchart, the first task is to obtain user input for a webpage. For simplicity, we shall assign this value directly to a variable named `URL`. For demonstration purposes, we will use the address `http://127.0.0.1:5500/` as our target.

```
URL = "http://127.0.0.1:5500/"
```

Next, we must store this URL in a list that will contain all discovered web addresses during the crawl. We shall call this list `urlList`. Initially, the list will be empty, and we will append our starting URL to it.

```
urlList = []
urlList.append(URL)
```

Before proceeding further, it is sensible to verify that the URL has indeed been appended to the list. We can achieve this by printing the list both before and after the append operation.

```
print(urlList)
urlList.append(URL)
print(urlList)
```

Upon execution, the output should confirm that the value was successfully added:

```
[]
["http://127.0.0.1:5500/"]
```

Once we have confirmed that the list behaves as expected, we can proceed to the next step: making an HTTP request to the specified URL. To perform web requests, we will use the `requests` module, which simplifies handling of HTTP operations in Python. We will import this module and assign the retrieved webpage to a variable named `page`.

```
import requests

URL = "http://127.0.0.1:5500/"
urlList = []

urlList.append(URL)

page = requests.get(URL)
```

To verify that the webpage content has been fetched correctly, we shall print the text of the page. This is an effective debugging step to ensure our request is functioning properly.

```
print(page.text)
```

When executed, the program should display the HTML content of the target page, confirming a successful connection.

```
<!-- index.html --> 
<html>
  <head>
    <title>My Website</title>
  </head>
  <body>
    <p>Hello World</p>
  </body>
</html>
```

Having validated this, we can remove the debugging print statement. Our next objective is to track which URLs have already been visited. To achieve this, we will use a dictionary called `isFollowed`, where each key will represent a URL and its corresponding value will indicate whether it has been processed. For instance, a URL marked as `"yes"` means it has already been followed.

```
isFollowed = {}
isFollowed[URL] = "yes"
print(isFollowed)
```

Execution of this section should produce:

```
{'http://127.0.0.1:5500/': 'yes'}
```

This confirms that the dictionary has been populated correctly. Now we shall move on to parsing the webpage for links.

To identify links, we will iterate through the lines of the page’s HTML using a `for` loop and the `split("\n")` method. Initially, we will print each line to understand the structure of the HTML and later refine the loop to search specifically for strings containing `"http"`.

```
counter = 0
for line in page.text.split("\n"):
    print(counter)
    print(line)
    counter += 1
```

This approach helps us examine each line of HTML code. After verifying the structure, we modify the loop to print only the lines containing hyperlinks:

```
for line in page.text.split("\n"):
    if "http" in line:
        print(line)
```

The output will display all HTML lines that include an HTTP reference. However, some of these links may point to external domains. Since our spider is designed to remain within a particular host, we shall further refine our condition to include only links that contain `127.0.0.1`.

```
for line in page.text.split("\n"):
    if "http" in line:
        if "127.0.0.1" in line:
            print(line)
```

Once we have filtered relevant links, the next challenge is to extract the URLs themselves from the surrounding HTML tags. We can achieve this through string slicing. Using the starting index of `"http"` and an appropriate end condition (such as `"">"` or `"\" "`), we can isolate the URL.

For example:

```
start = "http"
end = "\">"
for line in page.text.split("\n"):
    if "http" in line:
        if "127.0.0.1" in line:
            print(line[line.index(start):line.index(end)])
```

During execution, this may occasionally raise a `ValueError` if the expected end condition is not found. This occurs because not all links are terminated by the same characters. To resolve this, we include an additional check to determine which termination pattern (`"\">"` or `"\" "`) appears in the line before attempting to slice.

```
start = "http"
for line in page.text.split("\n"):
    if "http" in line:
        if "127.0.0.1" in line:
            if "\">" in line:
                end = "\">"
            else:
                end = "\" "
            print(line[line.index(start):line.index(end)])
```

This refined logic ensures we capture all valid links correctly. We can further enhance the extraction by checking for stray quotation marks and re-slicing where necessary.

After confirming that the extracted URLs are correctly displayed, we can store them in our `urlList` list—provided they do not already exist there. To manage this, we create a helper function named `checkUrlList()` that verifies whether a given URL is already present in the list.

```
def checkUrlList(URL):
    if URL in urlList:
        return True
    else:
        return False
```

Once validated, we integrate this function into our parsing loop. If a new link is discovered, it is appended to `urlList` and marked as `"no"` in the `isFollowed` dictionary, indicating it has not yet been visited.

Finally, to avoid revisiting links that have already been processed, we create another function called `isFollowedCheck()`. This function returns `True` if the link has been marked as `"yes"` and `False` otherwise.

```
def isFollowedCheck(URL):
    for entry in isFollowed.keys():
        if URL != entry:
            return False
        else:
            if isFollowed[URL] == "yes":
                return True
            else:
                return False
```

With these logical components in place, we can now assemble the complete spider. The program will loop through all URLs stored in `urlList`, requesting each page, parsing it for new links, and adding any new URLs it encounters. The process continues recursively until no unfollowed links remain.

At the end, the program prints the list of all unique links it discovered, each on a separate line. For readability, the output displays neatly formatted URLs representing every page and resource within the target host.

When executed, the script produces a structured list such as:

```
http://127.0.0.1/
http://127.0.0.1/css/main.css
http://127.0.0.1/index.html
http://127.0.0.1/gettingStarted.html
http://127.0.0.1/techniques.html
http://127.0.0.1/tutorials.html
http://127.0.0.1/shops.html
http://127.0.0.1/images/Crazy_Gaming_Table.jpg
http://127.0.0.1/images/Painter-Tux-Beret-Art-Artist-Brush-Blotch-Colour-161318.png
```

The spider takes a short while to complete as it recursively retrieves and processes each link. Once finished, it presents a comprehensive list of every internal hyperlink found within the specified host. This step-by-step build not only constructs a functional web spider but also provides valuable insight into how web crawlers systematically explore and catalogue websites using HTTP requests, link parsing, and iterative logic.
