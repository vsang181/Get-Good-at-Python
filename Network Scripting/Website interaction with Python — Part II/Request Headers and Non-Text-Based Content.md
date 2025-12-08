# Request Headers and Non-Text-Based Content

HTTP headers allow clients and servers to exchange additional metadata during an HTTP request or response. A header consists of a case-insensitive name, followed by a colon (`:`), and then the header value.

- A **request header** contains information about the request being sent—such as the browser type, accepted formats, authentication tokens, or the host being queried.
- A **response header** provides metadata about the server’s reply—such as the server type, caching policies, redirection information, cookies, or content type.

One of the most important headers for us to understand is the **Content-Type** header. This header tells the client what type of content is being delivered—for example, HTML, JSON, images, audio files, or binary data. The client will rely on this value when deciding how to interpret and display the server’s response.

To examine the content type (and other response headers), we can send an HTTP request to a server and print the full header set. The following script performs a simple GET request to www.securityshenanigans.com and outputs the server’s response headers:

```
~ % cat headers.py 
#!/usr/bin/python3

import requests

url = 'https://www.securityshenanigans.com/'
res = requests.get(url)
print(res.headers)
```

When executed, the server will respond with output similar to the following:

```
{'Server': 'openresty', 'Date': 'Mon, 08 Dec 2025 20:37:08 GMT', 'Content-Type': 'text/html', 'Transfer-Encoding': 'chunked', 'Connection': 'keep-alive', 'Content-Encoding': 'gzip', 'Cache-Control': 'max-age=0, no-store', 'Expires': 'Fri, 12 Sep 2025 01:13:56 GMT', 'Last-Modified': 'Thu, 19 Jun 2025 18:32:21 GMT', 'CF-Cache-Status': 'HIT', 'Age': '7586592', 'Set-Cookie': '__cf_bm=FIdneVYLuRjzpBsY_pM5wu40ekJXFTLLA1dYyF75gbw-1765226228-1.0.1.1-TDd5lBFKJdJeD2J8N0qLdIFhfrf2oplnWA7ob2n4RTEdmXxaVjcuct8iasHAp6TFjPGDc6molUPciDFzC3P6zv3JMby15hzr4NfMZ6TK6xI; path=/; expires=Mon, 08-Dec-25 21:07:08 GMT; domain=.zyro.com; HttpOnly', 'Vary': 'Accept-Encoding', 'CF-RAY': '9aaf0f1a4ce59848-LHR', 'alt-svc': 'h3=":443"; ma=86400', 'X-Hostinger-Datacenter': 'gcp-euw2', 'X-Hostinger-Node': 'gcp-euw2-builder-edge2', 'Content-Security-Policy': 'frame-ancestors zyro.com *.zyro.com *.builder-preview.com *.zyro.space *.hostinger.com *.hostinger.io *.hostinger.in *.hostinger.co.uk', 'Link': '<https://assets.zyrosite.com>; rel=preconnect; crossorigin, <https://userapp.zyrosite.com>; rel=preconnect; crossorigin, <https://fonts.googleapis.com>; rel=preconnect; crossorigin, <https://fonts.gstatic.com>; rel=preconnect; crossorigin, <https://cdn.zyrosite.com>; rel=preconnect; crossorigin', 'Strict-Transport-Security': 'max-age=63072000; includeSubDomains; preload;', 'X-Content-Type-Options': 'nosniff', 'X-Powered-By': 'HostingerWebsiteBuilder', 'platform': 'hostinger', 'X-XSS-Protection': '1; mode=block'}
```

In this response, the relevant portion for identifying content type is:

```
'Content-Type': 'text/html'
```

This tells us that the server is returning an HTML document encoded as text. Different types of resources—such as JSON (`application/json`), images (`image/png`, `image/jpeg`), video (`video/mp4`), or binary files (`application/octet-stream`)—will specify different content types accordingly.

Understanding these header values is important during reconnaissance and application testing, as they provide insight into how a server behaves and how data is structured, allowing us to correctly process or further exploit the information returned.
