# Building stacks of data

Stacks are a widely used data structure in computing, particularly for handling tasks such as function calls, parameter passing, expression evaluation, and backtracking. A stack follows the **Last In**, **First Out (LIFO)** principle, meaning the most recently added item is the first one to be removed.

In Python, lists naturally support stack behaviour through two key operations:

- **append()** → pushes an item onto the stack
- **pop()** → removes and returns the last item pushed

Let us demonstrate this with a simple example:

```
>>> stack = []

>>> stack.append(0x001F30)
>>> stack.append(0x002C5C)
>>> stack.append(0x001F38)

>>> print(hex(stack.pop()))
0x1f38

>>> print(hex(stack.pop()))
0x2c5c
```

Each call to **pop()** removes the most recently appended value, perfectly reflecting the LIFO behaviour of a stack.

Therefore, Python lists are inherently well-suited for implementing stacks without requiring any additional modules or special syntax.
