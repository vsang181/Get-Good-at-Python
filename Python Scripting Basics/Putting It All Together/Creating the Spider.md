# Creating the Spider

Now that we have our spider program idea in pseudocode and a flowchart, we will translate this plan to actual code. Instead of providing the entrie code base and explaining it, let us work through each step of programming this script as laid out in the flowchart. This way, we can confuct our scripting tests while writing the program, instead of havinga  final solution up front.

As we know we need to have the start of our program. let us name our script webSpider.py and add the sheband line.

```
~ % cat webSpider.py
#!/usr/bin/python3
```

According to our flowchar diiagram our first action is to take user inout of a webpage. The simplest way for us to do this is to add a varaiable for this value. Let us add a varaiable called URL and assign it to our exercise host address. For this demonstration, the addres will be 192.168.0.1.

```
~ % cat webSpider.py
#!/usr/bin/python3

URL = "http://127.0.0.1:5500/"
```

While the initial UROL set, we now need to store this ina URL list variable. We will call ours urlList. Instead of creating the urlList variable with the initial value in it, let us start with setting the varaiable with no values and add the URL varaiable in it.

```
~ % cat webSpider.py
#!/usr/bin/python3

URL = "http://127.0.0.1:5500/"
urlList = []

urlList.append(URL)
```

Instead of continuing forward, let us test our current code as written. The question is , "Are we properly adidng the value to the list varaible?" The easy way to test this is to print the urList varaiable before and after the appent() statement. Let us add this now.

```
~ % cat webSpider.py
#!/usr/bin/python3

URL = "http://127.0.0.1:5500/"
urlList = []

print(urlList)
urlList.append(URL)
print(urlList)
```

With the debugging print duncation added, let us execute the script to make sure urList varaiable is being handled appropiately.

```
~ % ./webSpider.py
[]
["http://127.0.0.1:5500/"]
```

With our test, we now know that the URL value has been added appropiately to the urList varaible. From here, we need to make a web request of that URL page and store it ina bvariable. As we covered before to fo this we must imporyt a module called `requests`. From there we can use that module to make the request. We will store the web request ina varaible called page. For the sake of cleaning up our code, let us remove those debugging print() funcations as well.

```
~ % cat webSpider.py
#!/usr/bin/python3

import requests

URL = "http://127.0.0.1:5500/"
urlList = []

urlList.append(URL)

page = requests.get(URL)
```

With the requests module imported in the page variable population, we can take another moment to debug our program. let us add a print statement for teh content of the webpage after the request to make sure we are pulling in what we expect.

```
~ % cat webSpider.py
#!/usr/bin/python3

import requests

URL = "http://127.0.0.1:5500/"
urlList = []

urlList.append(URL)

page = requests.get(URL)
print(page.text)
```

With the debugging statement in place, let us execute the script again.

```
~ % cat webSpider.py
<!-- index.html --> 
<html>
  <head>
    <title> My Website </title>
  </head>
  <body>
    <p> Hello World </p>
  </body>
</html>
```

great! this is what we expected. Now, let us remove the debugging print statement and move on to the next step.

The next step in oujr flowchart is to store the URL in a dictionary varaiable called isFollowed and assign in the value "yes". We will approach this the same way as the urlList varaiable and define the dictionary at the beginning of our script. From here, we can add the dictionary entry and its value after the page request. We will also add a debugging print statement after the netry to verify the dictionary is populated correctly.

```
~ % cat webSpider.py
#!/usr/bin/python3

import requests

URL = "http://127.0.0.1:5500/"
urlList = []
isFollowed = {}

urlList.append(URL)

page = requests.get(URL)
isFollowed[URL] = "yes"
print(isFollowed)
```

Let us execute the script to ensure it is working as expected.

```
{'http://127.0.0.1:5500/': 'yes'}
```

perfect! Now we will remove the print statement again and move on to the next step in our flowchart.

here, we need to parse the page for any links that have "http" in them. We will accomplish this by using a for loop with a split() method. The split() method will seperate the variable based on a newline character. instead of going back and forth, let us do this with debugging built-in to test if we can interatively read through each line in the page vrariable. To t=do this, we will declare a counter variable before the for loop and set the value to "0". Inside the loop, we will print the counter, the line in the page variable, then increment the counter variable. For now, we have not considered the fact the we need to search for the "http" string.

```
~ % cat webSpider.py
#!/usr/bin/python3

import requests

URL = "http://127.0.0.1:5500/"
urlList = []
isFollowed = {}

urlList.append(URL)

page = requests.get(URL)
isFollowed[URL] = "yes"

counter = 0
for line in page.text.split("\n"):
  print(counter)
  print(line)
  counter = counter + 1
```

With this let's execute our script.

```
~ % ./webSpider.py
1
<html>
2
  <head>
3
    <title> My Website </title>
4
  </head>
5
  <body>
6
    <p> Hello World </p>
.....
```

the goal of this step is to identify any link that has "http" in it. Let us remove the counter and print of each line and modify the script to check if "http" is in the line it iterates. We will print only these lines for this next step.

```
 % cat webSpider.py
#!/usr/bin/python3

import requests

URL = "http://127.0.0.1:5500/"
urlList = []
isFollowed = {}

urlList.append(URL)

page = requests.get(URL)
isFollowed[URL] = "yes"

for line in page.text.split("\n"):
  if "http" in line:
  print(line)
```

Let us execute teh script.

```
~ % ./webSpider.py

```
















