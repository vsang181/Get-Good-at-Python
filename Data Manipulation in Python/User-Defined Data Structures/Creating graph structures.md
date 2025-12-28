# Creating graph structures

A **graph** is a data structure consisting of **nodes** (also called vertices) and the **edges** that connect them. Graphs are used extensively in mathematics and computer science to model complex real-world problems.

A classic example is the Travelling Salesman Problem (TSP)****:

> Given a set of cities and the distances between them, what is the shortest possible route that visits each city exactly once and returns to the starting point?

Modern navigation systems use graph-based algorithms to determine the shortest route between two points.

In Python, we typically represent a graph by creating a **node data structure** in which each node contains:

**1.** A **name** or identifier
**2.** A **list of connections** (edges) to other nodes
  - These can include just the neighbour names
  - Or they may include metadata, such as distances or weights

## Example: A Small Travelling Salesman Graph

The example graph (referred to in the text) consists of four cities connected by roads, with weights representing distances in kilometres. To model this graph in Python, we can use a list of nodes where each node is represented as:

```
[
  city_name,
  [
    (other_city, distance),
    (other_city, distance),
    ...
  ]
]
```

Each tuple stores a connected city and the distance to it.

Let us create the graph structure and append the node for **Baltimore**.

```
>>> nodes = []

>>> nodes.append([
...     "Baltimore",
...     [("WashingtonDC", 66),
...      ("Annapolis", 48),
...      ("Columbia", 29)]
... ])
```

Here:

- `"Baltimore"` is the node’s label
- The list following it contains three connections, each represented as a tuple of (`city_name`, `distance`)

This structure can be extended by appending additional city nodes in the same format.

We will leave the Travelling Salesman Problem here and continue with a more specialised hierarchical structure: the **tree**.
