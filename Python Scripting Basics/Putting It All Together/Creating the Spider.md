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
<link href="http://127.0.0.1/css/main.css" rel="stylesheet" type="text/css" />
    <li><a href="http://127.0.0.1/index.html" class="current">Home</a>
</li>

    <li><a href="http://127.0.0.1/gettingStarted.html">Getting Started</a>
</li>

    <li><a href="http://127.0.0.1/techniques.html">Techniques</a></li>
    <li><a href="http://127.0.0.1/tutorials.html">Painting Tutorials</a></li>
    <li><a href="http://127.0.0.1/shops.html">Miniature Manufacturers</a>

    <img class="imgRight" src="http://127.0.0.1/images/Crazy_Gaming_Table.jpg"
    alt="Crazy Tabletop Game Setup!" caption="This is way more than I have ever seen, but
    this is a wargamer's dream!" width="200px" height="150px">
    <!-- Image taken from:
    https://c2.staticflickr.com/4/3044/2775801876_f168dfcb66_b.jpg -->
</li>

    <li><a href="http://127.0.0.1/gettingStarted.html">Getting Started</a>
</li>

    <li><a href="http://127.0.0.1/techniques.html">Techniques</a></li>
    <li><a href="http://127.0.0.1/tutorials.html">Painting Tutorials</a></li>
    <li><a href="http://127.0.0.1/shops.html">Miniature Manufacturers</a>

    <img class="imgRight" src="http://127.0.0.1/images/Painter-Tux-Beret-Art-
    Artist-Brush-Blotch-Colour-161318.png" width="40px" height="37px" alt="Shhhh... It's a
    secret.">
    <!-- Image taken from:  http://maxpixel.freegreatpicture.com/Painter-Tux-Beret-Art-
    Artist-Brush-Blotch-Colour-161318 -->
```

IN THE OUTPUT, THERE ARE LINKS THAT DO NOT CONTAIN THE IP ADDRESS OF OUr host. Let us filter this further with a nested if statement.

```
for line in page.text.split("\n"):
  if "http" in line:
      if "127.0.0.1" in line:
          print(line)
```

Let us execute the script again to check if the output changes.

```
~ % ./webSpider.py
    <link href="http://127.0.0.1/css/main.css" rel="stylesheet" type="text/css" />
        <li><a href="http://127.0.0.1/index.html" class="current">Home</a>
</li>

        <li><a href="http://127.0.0.1/gettingStarted.html">Getting Started</a>
</li>

        <li><a href="http://127.0.0.1/techniques.html">Techniques</a></li>
        <li><a href="http://127.0.0.1/tutorials.html">Painting Tutorials</a></li>
        <li><a href="http://127.0.0.1/shops.html">Miniature Manufacturers</a>
</li>

    <img class="imgRight" src="http://127.0.0.1/images/Crazy_Gaming_Table.jpg"
    alt="Crazy Tabletop Game Setup!" caption="This is way more than I have ever seen, but
    this is a wargamer's dream!" width="200px" height="150px">
        <li><a href="http://127.0.0.1/gettingStarted.html">Getting Started</a>
</li>

        <li><a href="http://127.0.0.1/techniques.html">Techniques</a></li>
        <li><a href="http://127.0.0.1/tutorials.html">Painting Tutorials</a></li>
        <li><a href="http://127.0.0.1/shops.html">Miniature Manufacturers</a>
</li>

    <img class="imgRight" src="http://127.0.0.1/images/Painter-Tux-Beret-Art-
    Artist-Brush-Blotch-Colour-161318.png" width="40px" height="37px" alt="Shhhh... It's a
    secret.">
```

Instead of printing the line to the terminal, we need to filter out the links. We will do this with a start and end index to get the URL of each line and print that to the terminal. Let us do this the same way as covered in teh Strings and Slicing section of this Module.

```
start = "http"
end = "\">"
for line in page.text.split("\n"):
    if "http" in line:
        if "127.0.0.1" in line:
            print(;ine[line.index(start):line.index(end)])
```

Let us execute teh script and find out if we were able to parse the links correctly.

```
~ % ./webSpider.py
Traceback (most recent call last):
  File "/Users/victorsangwan/./webspider.py", line 20, in <module>
    print(;ine[line.index(start):line.index(end)])
ValueError: substring not found
```

The script failed to execute. The error message indicates that there is an issue with the substring, so our parsing did not work as intended. let us debug this issue to revioew what is going on. To start, let us print the index values for the start and the end conditions.

```
start = "http"
end = "\">"
for line in page.text.split("\n"):
    if "http" in line:
        if "127.0.0.1" in line:
            print(line)
            print(line.index(start))
            print(line.index(stop))
            #print(line[line.index(start):line.index(end)])
```

Let us execute the script again.

```
~ % ./webSpider.py
    <link href="http://127.0.0.1/css/main.css" rel="stylesheet" type="text/css" />
16
Traceback (most recent call last):
  File "/Users/victorsangwan/./webspider.py", line 22, in <module>
    print(line.index(end))
ValueError: substring not found
```

The script failed again. The line and the start index were printed on the terminal, which wouild indicate that the end index is the issue. let us reveiw the link lines again. To save time, only two lines will be shown in the following listing.

```
<link href="http://127.0.0.1/css/main.css" rel="stylesheet" type="text/css" />
    <li><a ref="http://127.0.0.1/css/main.css" class="current">Home</a>
</li>
```

In the example listing above, the URL links have a different ending condition, With this we can not create an index condition of "">" for all lines. instead, The first line shown above ends the URL link wiuth a "" " condition. Let us write up a short if/else statement to check for the potential ending condition and set the end varaible to the found condition.

```
start = "http"
for line in page.text.split(\n""):
    if "http" in line:
        if "127.0.0.1" in line:
            if "\">" in line:
                end = "\">"
            else:
                end = "\" "
            print(line)
            print(line.index(start))
            print(line.index(end))
            #print(line[line.index(start):line.index(end)])
```

let us execute the script again to analyse the different in output.

```
~ % ./webSpider.py
    <link href="http://127.0.0.1/css/main.css" rel="stylesheet" type="text/css" />
16
50
        <li><a ref="http://127.0.0.1/css/main.css" class="current">Home</a>
</li>
25
73
```

There is a lot of terminal output with the method we used to debug. Let us cut all the debugging statements and print the new URL values to find out the slicing is workibng as expected.

```
start = "http"
for line in page.text.split("\n"):
    if "http" in line:
        if "127.0.0.1" in lines:
            if "\">" in line:
                end = "\">"
            else:
                end = "\" "
            print(line[line.index(start):line.index(end)])
```

Let is execute the script to find the URL results.

```
~ % ./webSpider.py
http://127.0.0.1/css/main.css
http://127.0.0.1/index.html" class="current
http://127.0.0.1/gettingStarted.html
http://127.0.0.1/techniques.html
http://127.0.0.1/tutorials.html
http://127.0.0.1/shops.html
http://127.0.0.1/images/Crazy_Gaming_Table.jpg" alt="Crazy Tabletop Game Setup!" caption="This is way more than I have ever seen, but this is a wargamer's dream!" width="200px" height="150px
http://127.0.0.1/gettingStarted.html
http://127.0.0.1/techniques.html
http://127.0.0.1/tutorials.html
http://127.0.0.1/shops.html
http://127.0.0.1/images/Painter-Tux-Beret-Art-Artist-Brush-Blotch-Colour-161318.png" width="40px" height="37px" alt="Shhh... It's a secret.
```

So close! There are many URL lines that are correctly sliced, but there are a few lines that have extra HTML data in them. Let us set this to a varaibale and run an additional test on the varaible to determine if there are any quotes (") in the line. If tehre are, we can slice the line again with the end varaibale set to """.

```
start = "http"
for line in page.text.split("\n"):
    if "http" in line:
        if "127.0.0.1" in lines:
            if "\">" in line:
                end = "\">"
            else:
                end = "\" "
            slices = line[line.index(start):line.index(end)]
            if "\"" in sliced:
                end = "\""
                print(sliced[slices.index(start):line.index(end)])
            else:
                print(sliced)
```

If the sliced varaiable has quotes (") in it, it will be sliced an additional time with a new end condition for the index. Otherwise, the program will assume the line was fine and print the sliced varaible without modification.

```
~ % ./webSpider.py
http://127.0.0.1/css/main.css
http://127.0.0.1/index.html
http://127.0.0.1/gettingStarted.html
http://127.0.0.1/techniques.html
http://127.0.0.1/tutorials.html
http://127.0.0.1/shops.html
http://127.0.0.1/images/Crazy_Gaming_Table.jpg
http://127.0.0.1/gettingStarted.html
http://127.0.0.1/techniques.html
http://127.0.0.1/tutorials.html
http://127.0.0.1/shops.html
http://127.0.0.1/images/Painter-Tux-Beret-Art-Artist-Brush-Blotch-Colour-161318.png
```

The output of the parsing algorithm we set appears to be working now. Now that we have the expected output, we need to refer to the urlList and add the link if it is not in the list already. To do this, let us take a moment away from this section of the code and add a custom funcation at the top of our script called checkUrlList. This fucnation will take a parameter and loop through the urlList list varaible to check if it exists or not. It wil then return true or False based on the search result.

```
def checkUrlList(URL):
    if URL in urlList:
        return true
    else:
        return false
```

As we have been doing, let us add debig print funcations to test the funcation. Let us do this after our first URL is added to the urlList list. We will add one print statement that should result in a "True" return and another that should result in a "False" return.

```
urlList.append(URL)
print(checkUrlList(URL))
print(checkUrlList("http://127.0.0.1/"))
```

Let us execute the script and find out what each debugging statement returns.

```
~ % ./webSpider.py
True
False
```

Now that we validated the checkUrlList funcation, let us incorporate it in the http parsing section. If the link is found in the urlList, it will be ignored. If it is not on the list, it will be added.

We can remove all the debugging print() functions from the code as well. Instead of the print funcations, let us set the sliced value to a different variable called parsedURL. For the sake of brevity, we will also add the debugging print statement outside of the loop to analyse if the sliced URLs were added to the urlList variable.

```
start = "http"
for line in page.text.split("\n"):
    if "http" in line:
        if "127.0.0.1" in lines:
            if "\">" in line:
                end = "\">"
            else:
                end = "\" "
            slices = line[line.index(start):line.index(end)]
            if "\"" in sliced:
                end = "\""
                print(sliced[slices.index(start):line.index(end)])
            else:
                print(sliced)
```











