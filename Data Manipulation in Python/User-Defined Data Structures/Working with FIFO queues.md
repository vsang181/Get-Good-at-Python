# Working with FIFO queues

A **First In**, **First Out** (**FIFO**) **queue** is a data structure in which the first item added is the first item removed. This behaviour is commonly used in scheduling systems, customer service desks, print queues, and networking buffers.

In Python, a simple FIFO queue can be implemented using a **list**, where:

- New entries are **appended** to the end of the list.
- Removals take place from the **beginning** of the list.

Below is a simple script that simulates a customer service queue, where customers arrive and are served at random intervals.

```
1. import random
2. queue = []
3. while True:
4.     adding = input("New customer: ")
5.     if adding == "quit":
6.         break
7.     if len(adding) != 0:
8.         queue.append(adding)
9.     if random.randrange(10) > 6:
10.        if len(queue) > 0:
11.            print("Now consulting with:", queue[0])
12.            queue.remove(queue[0])
13.     print("Queue length:", len(queue))
```

## Explanation of the Script

### Lines 1–2: Initial Setup

- We import the `random` module to simulate unpredictable service times.
- We initialise the queue as an empty list.

### Lines 3–8: Handling New Arrivals

- The loop continues until the user types `"quit"`.
- At line 4, the user may enter a customer namee.
- Pressing `Return` without typing anything simply adds no new customer.
- If a name is entered, line 8 appends it to the end of the queue.

### Lines 9–12: Randomised Service

- In a real-world scenario, customers are served at varying speeds.
- `random.randrange(10) > 6` introduces a ~30% chance of serving someone on any given loop iteration.
- If the queue is not empty:
  - Line 11 identifies the next customer to be served (the first in line).
  - Line 12 removes them from the queue.

### Line 13: Monitoring Queue Length

- After each cycle, we display the current number of people waiting.

## Example Output

```
~ % python3 fifo.py
New customer: Victor Sangwan
Queue length: 1
New customer: Willy Wonka
Queue length: 2
New customer: Umpa Lumpa
Now consulting with: Victor Sangwan
Queue length: 2
New customer: Lumpa Umpa
Queue length: 3
New customer: Sangwan Victor
Queue length: 4
New customer:
Now consulting with: Willy Wonka
Queue length: 4
New customer:
Queue length: 4
Now consulting with: Umpa Lumpa
Queue length: 3
New customer: quit
```

The queue grows and shrinks dynamically. Customers are always served in the exact order they arrived—demonstrating **true FIFO behaviour**.

## Note on Scalability

Although using a list is simple and perfectly adequate for learning purposes:

- Removing from the front of a Python list (`list.remove()` or `pop(0)`) is **O(n)** in time complexity.
- For high-performance or large-scale applications, the `collections.deque` structure is preferred, because it provides `O(1)` operations for both append and popleft.

However, for this Topic’s purposes, a list-based implementation is entirely appropriate.
