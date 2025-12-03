# Using the `socket` module to create a basic port scanner

We are now going to build a simple port scanner using the `socket` and `time` libraries. Port scanning allows us to identify which ports are open on a target host. As penetration testers, this information helps us determine what services are running, what software versions might be in use, and even make educated guesses about the operating system.

We will begin our script by importing the required modules and using the `time.time()` method.

```
~ % cat scanner.py 
#!/usr/bin/python3

import socket
import time

startTime = time.time()
```

The `time.time()` method returns the current system time in seconds since the Unix epoch. By storing this value in the `startTime` variable at the beginning of our script, we can later calculate the total execution time of the port scan by subtracting this value from the time recorded at the end of the program.

Next, we will allow the user to specify the target host via the `input()` method. We then use `socket.gethostbyname()` to convert the provided hostname into an IPv4 address.

```
~ % cat scanner.py 
#!/usr/bin/python3

import socket
import time

startTime = time.time()

target = input('Please specify the host that you want to scan: ')
targetIP = socket.gethostbyname(target)
print('Initiating Scan for host: ', targetIP)
```

Alternatively, we could remove the `targetIP = socket.gethostbyname(target)` line and simply require the user to enter an IP address directly. When scanning external systems, you may wish to adjust this behaviour accordingly.

Next, we will use a `for` loop to determine which ports will be scanned. Instead of the standard `socket.connect()` method, we will make use of `socket.connect_ex()`. While both perform a connection attempt, `connect_ex()` returns an error code rather than raising an exception. A return value of `0` indicates that the connection was successful, meaning the port is open.

```
~ % cat scanner.py 
#!/usr/bin/python3

import socket
import time

startTime = time.time()

target = input('Please specify the host that you want to scan: ')
targetIP = socket.gethostbyname(target)
print('Initiating Scan for host: ', targetIP)

for i in range(1, 1000):
    scanner = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    conn = scanner.connect_ex((target_IP, i))
    if(conn == 0):
        print ('Port %d: OPEN'%(i))
    scanner.close()
```

In this loop, we scan ports 1 through 999. You can easily modify these values, expand the range, or enhance the script to accept port ranges via command-line arguments. We will leave such improvements as an optional extension.

Finally, we capture the time at the end of the scan and compute the total runtime.

```
endTime = time.time()
totalTime = endTime - startTime
print('Total Time: %s' % (totalTime))
```

Putting everything together, the completed script will look like this:

```
~ % cat scanner.py 
#!/usr/bin/python3

import socket
import time

startTime = time.time()

target = input('Please specify the host that you want to scan: ')
targetIP = socket.gethostbyname(target)
print('Initiating Scan for host: ', targetIP)

for i in range(1, 1000):
    scanner = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    conn = scanner.connect_ex((target_IP, i))
    if(conn == 0):
        print ('Port %d: OPEN'%(i))
    scanner.close()

entTime = time.time()
totalTime = entTime - startTime
print ('Total Time: %s' %(totalTime))
```

When executed, the script will prompt the user for a hostname and then perform the scan. The output may resemble the following:

```
~ % ./scanner.py
Please specify the host that you want to scan: localhost
Initiating Scan for host: 127.0.0.1
Port 22: OPEN
Port 80: OPEN
Port 8080: OPEN
Total Time 3.3222038555415246
```

In this example, `localhost` was used as the target. Because `socket.gethostbyname()` resolves hostnames into IPv4 addresses, `localhost` correctly resolves to the loopback address `127.0.0.1`.

The results show that three ports are open on the local machine. The scan took approximately 3.32 seconds to complete. You can further expand the script by looping through multiple hosts, creating nested loops, or by sending different packet types to collect more detailed fingerprinting information.
