# Doubling up on our lists

Sometimes we want a data structure that stores complex data objects while keeping them in a particular order. Although Python’s **sort()** function works well for simple lists, sorting becomes more challenging when list entries contain multiple fields.

A common solution is to use a **linked list**, where each element contains:

**1.** The **data**
**2.** A **pointer (index) to the next element**

In such a list, we maintain a pointer to the first element and traverse the list by following the chain of pointers. The final element contains a **null pointer** (we will use `0` to mark the end).

A visual example of a simple linked list:

<img width="800" height="330" alt="image" src="https://github.com/user-attachments/assets/11231912-7830-4ce9-8d17-66c1f8a31727" />

A useful variation is a **circular linked** list, where the last node points back to the first. In such designs, there is no strict “beginning” or “end”.

Below, we build a simple linked-list manager in Python using nested lists to simulate pointer-based structures.

## Script Structure

```
1. linky = [["FirstPointer", 0, "", ""]]
2. while True:
3.     action = input("(A)dd, (R)emove, (L)ist, (D)ump, (Q)uit: ").upper()
4.     if action == "Q":
5.         break
6.     if action in ("A", "R"):
7.         name = input("Enter name: ")
```

### Explanation

- Line **1**: Initialise the list with a **header node**
  - `"FirstPointer"` is a label
  - `0` is the pointer to the first real node
  - final two empty strings store extra fields (birth date and start date later)
- Lines **2–5**: User command loop
- Lines **6–7**: Prompt for a name when adding or removing an entry

## Dumping and Listing the Linked List

```
8.     if action == "D":
9.         print(linky)

10.    if action == "L":
11.        index = linky[0][1]
12.        while index > 0:
13.            print(linky[index][0])
14.            index = linky[index][1]
```

### Explanation

- `"D"` prints the **raw structure**, useful for debugging
- `"L"` traverses the list in order:
  - `index = linky[0][1]` gets the first entry
  - Continue printing names until pointer becomes `0`

## Adding an Entry

```
15.    if action == "A":
16.        bdate = input("Birth date as yymmdd: ")
17.        sdate = input("Start date as yymmdd: ")
18.        newx = len(linky)
19.        linky.append([name, 0, bdate, sdate])
20.        index = 0
21.        while True:
22.            nxt = linky[index][1]
23.            if nxt == 0:
24.                linky[index][1] = newx
25.                break
26.            if linky[nxt][0] > name:
27.                linky[index][1] = newx
28.                linky[newx][1] = nxt
29.                break
30.            index = nxt
```

### Explanation

- Lines **16–19**:
  - Capture the new record’s data
  - Determine the new index `newx`
  - Append the new node with a null pointer (`0`)
- Lines **20–30**: insert the entry in alphabetical order
  - If we reach the end (`nxt == 0`) → append
  - If the new name should come before the next node → insert before it
  - Otherwise move forward in the chain

## Removing an Entry

```
31.    if action == "R":
32.        index = 0
33.        while True:
34.            nxt = linky[index][1]
35.            if nxt == 0:
36.                print("Entry not found")
37.                break
38.            if name == linky[nxt][0]:
39.                linky[index][1] = linky[nxt][1]
40.                break
41.            index = nxt
```

### Explanation

- Starting from the header node
- If end-of-list reached → entry not found
- If next node matches the name → bypass it (logical deletion)
- Otherwise, continue traversing

> Note: To keep the code simple, deleted nodes remain as "garbage" in the list, but they are no longer linked.

## Full Corrected Code Listing

```
linky = [["FirstPointer", 0, "", ""]]

while True:
    action = input("(A)dd, (R)emove, (L)ist, (D)ump, (Q)uit: ").upper()
    if action == "Q":
        break

    if action in ("A", "R"):
        name = input("Enter name: ")

    if action == "D":
        print(linky)

    if action == "L":
        index = linky[0][1]
        while index > 0:
            print(linky[index][0])
            index = linky[index][1]

    if action == "A":
        bdate = input("Birth date as yymmdd: ")
        sdate = input("Start date as yymmdd: ")
        newx = len(linky)
        linky.append([name, 0, bdate, sdate])
        index = 0
        while True:
            nxt = linky[index][1]
            if nxt == 0:
                linky[index][1] = newx
                break
            if linky[nxt][0] > name:
                linky[index][1] = newx
                linky[newx][1] = nxt
                break
            index = nxt

    if action == "R":
        index = 0
        while True:
            nxt = linky[index][1]
            if nxt == 0:
                print("Entry not found")
                break
            if name == linky[nxt][0]:
                linky[index][1] = linky[nxt][1]
                break
            index = nxt
```

## Demonstration Run

```
(A)dd, (R)emove, (L)ist, (D)ump, (Q)uit: A
Enter name: Victor.S
Birth date as yymmdd: 990101
Start date as yymmdd: 241105

(A)dd, (R)emove, (L)ist, (D)ump, (Q)uit: A
Enter name: Willy.W
Birth date as yymmdd: 980202
Start date as yymmdd: 241022

(A)dd, (R)emove, (L)ist, (D)ump, (Q)uit: L
Willy.W
Victor.S

(A)dd, (R)emove, (L)ist, (D)ump, (Q)uit: R
Enter name: Willy.W

(A)dd, (R)emove, (L)ist, (D)ump, (Q)uit: L
Victor.S

(A)dd, (R)emove, (L)ist, (D)ump, (Q)uit: Q
```

The linked list correctly maintains alphabetical ordering and updates as entries are added or removed.

## Doubly Linked List Variant (Overview)

A doubly linked list includes two pointers in each node:

```
[ backward_pointer , forward_pointer , data... ]
```

Example initial node:

```
  linky = [["FirstPointer", 0, 0, "", ""]]
```

Insertion logic becomes:

```
linky[index][2] = newx        # current → new (forward)
linky[newx][1] = index        # new → current (backward)
linky[newx][2] = nxt          # new → next (forward)
linky[nxt][1] = newx          # next → new (backward)
```

This allows traversal in both directions.
