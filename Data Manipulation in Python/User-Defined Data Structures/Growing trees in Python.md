# Growing trees in Python

A **tree** is a special type of graph consisting of **nodes** connected by **links** **(edges)** with two key constraints:

**1.** A tree begins at a **root node** and extends through levels of **parent** and **child** nodes.
**2.** Each node has **exactly one parent** (except the root, which has none) and **zero or more children**.
**3.** A tree contains **no cycles**—you cannot start at a node and loop back to it by following edges.

Trees are widely used in computing—for example, family trees, hierarchical file systems, Active Directory structures, and evolutionary biology models.

### Example Context: The Steiner Problem in Graphs

We will use a simplified model inspired by the **Steiner Problem in Graphs**, which asks:

> Given a set of nodes and pairwise distances, what is the minimal way to connect them?

As a biological analogy, amino acids can be represented as sequences of **three RNA nucleotides**, where each nucleotide can be **A**, **G**, **C**, or **U**. By extending this idea, one can use tree structures to estimate evolutionary paths by comparing such sequences.

We will not attempt to solve the Steiner problem algorithmically. Instead, we will:

- Build a **tree structure** in Python
- Store at each node:
  - A name
  - A six-character _nucleotide_ sequence (AGCU-based)
  - A link to its _parent_
  - A list of _children_
- Calculate the **total graph weight** (sum of distances between each node and its parent)
- Allow the user to **move nodes** within the tree and observe how the weight changes

Distance between two nodes will be defined as:

> The number of differing characters in the same index positions of their respective sequences.

We will use a **doubly-linked structure**: each node stores a pointer to its parent and a list of children.

Below is the initial model we will be working with:

<img width="1567" height="713" alt="image" src="https://github.com/user-attachments/assets/f848c457-ba7e-4e84-ac23-a632d63648c2" />

The node names and six-character sequences are stored in a **fixed-width text file**, where each line contains:

```
<16-character name><space><6-character sequence>
```

We will calculate distances dynamically rather than storing them.

## Loading the Tree Structure

```
1. graph = []
2. index = 0
3. f = open("graph.txt", "r")
4. for line in f:
5.     graph.append([line[0:16].strip(), line[17:23], 0, []])
6.     if index > 0:
7.         graph[0][3] += [index]
8.     index += 1
```

### Explanation

- **Lines 1–2**: Initialise an empty graph list and an index counter.
- **Line 3**: Open the input file.
- **Line 5**: Append a new node represented as a 4-element list:
  **1.** Node name (trimmed)
  **2.** Six-character nucleotide sequence
  **3.** Parent index (initially 0, meaning “root”)
  **4.** List of children (initially empty)
- **Lines 6–7**: Every node except the first is added as a child of the root.
- **Line 8**: Increment index for the next iteration.

After this loop completes, all nodes are loaded and connected as children of the root.

## Calculating the Tree Weight

```
9. while True:
10.     weight = 0
11.     for node in graph:
12.         distance = 0
13.         code1 = node[1]
14.         code2 = graph[node[2]][1]
15.         for i in range(6):
16.             if code1[i] != code2[i]:
17.                 distance += 1
18.         weight += distance
19.     print("Graph weight:", weight)
```

### How it works

- **Line 9**: Begin an infinite loop (we break later when the user exits).
- **Lines 10–11**: Reset the total weight and iterate through all nodes.
- **Lines 12–14**:
  - Extract the node’s sequence
  - Retrieve its parent’s sequence
- **Lines 15–17**: Compare positions 0–5 of both sequences; increment distance for mismatches.
- **Line 18**: Add the computed distance to the total graph weight.
- **Line 19**: Display the current weight.

> The root compares against itself, contributing zero distance, so no exclusion is needed.

## Moving Nodes Within the Tree

We now allow the user to reposition a node by assigning it a new parent.

```
20.     n1 = input("Node:        ")
21.     if len(n1) == 0:
22.         break
23.     n2 = input("New parent:  ")
24.     i1 = 0; i2 = 0
25.     for i in range(len(graph)):
26.         if graph[i][0] == n1:
27.             i1 = i
28.         if graph[i][0] == n2:
29.             i2 = i
30.     if (i1 == 0 or i1 == i2):
31.         print("Invalid node!")
```

### Explanation

- **Lines 20–23**: Request the node to move and its new parent.
- **Lines 24–29**: Search for their indices in the graph.
- **Line 30**: Validate the selection:
  - Cannot move the root
  - Cannot set a node as its own parent

## Applying the Move

```
32.     else:
33.         i3 = graph[i1][2]
34.         graph[i3][3].remove(i1)
35.         graph[i1][2] = i2
36.         graph[i2][3] += [i1]
37. f.close()
```

### Interpretation

- **Line 33**: Retrieve the current parent index of the node being moved.
- **Line 34**: Remove the node from its old parent’s list of children.
- **Line 35**: Assign its new parent.
- **Line 36**: Add it to the new parent’s list of children.
- The main loop then recalculates the weight with the updated structure.

## Full Script (Corrected Formatting)

```
graph = []
index = 0
f = open("graph.txt", "r")

for line in f:
    graph.append([line[0:16].strip(), line[17:23], 0, []])
    if index > 0:
        graph[0][3] += [index]
    index += 1

while True:
    weight = 0
    for node in graph:
        distance = 0
        code1 = node[1]
        code2 = graph[node[2]][1]
        for i in range(6):
            if code1[i] != code2[i]:
                distance += 1
        weight += distance
    print("Graph weight:", weight)

    n1 = input("Node:        ")
    if len(n1) == 0:
        break

    n2 = input("New parent:  ")
    i1 = 0; i2 = 0
    for i in range(len(graph)):
        if graph[i][0] == n1:
            i1 = i
        if graph[i][0] == n2:
            i2 = i

    if i1 == 0 or i1 == i2:
        print("Invalid node!")
    else:
        i3 = graph[i1][2]
        graph[i3][3].remove(i1)
        graph[i1][2] = i2
        graph[i2][3] += [i1]

f.close()
```

## Sample Run

```
~ % python3 graph.py
Graph weight: 14
Node:       Node1
New parent: Node2
Graph weight: 13
Node:       Node3
New parent: Node2
Graph weight: 11
Node:       Node4
New parent: Node1
Graph weight: 10
Node:
```

<img width="361" height="556" alt="image" src="https://github.com/user-attachments/assets/b7353f56-2bad-4ee6-ad1f-9973bbea20ee" />

As nodes are repositioned, the total weight decreases, reflecting more efficient structural relationships.

<br>

This script is a conceptual demonstration. It does not enforce full tree validity—for example:

- It does not prevent cycles
- It does not prevent disconnected subgraphs

But it effectively teaches:

- Tree representation using Python lists
- Linked structures (parent + children lists)
- Distance-based scoring
- Dynamic rearrangement of nodes
