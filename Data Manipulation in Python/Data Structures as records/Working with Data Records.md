# Working with Data Records

We have covered a broad range of data-handling techniques in this Topic, so we will conclude with a brief review of **data records**.

In business systems, a record is a structured set of related data fields—traditionally stored in relational databases using SQL, but increasingly also in modern NoSQL systems such as **MongoDB**, **CouchDB**, and cloud-native databases like **AWS DynamoDB**.

Business applications commonly operate by:

1. Reading a record from persistent storage
2. Processing or modifying it in memory
3. Writing it back to the database

Python naturally supports this workflow. While we can represent records using dictionaries or basic data types, a more structured and elegant approach is to use the **dataclasses** module introduced in Python 3.7.

A dataclass allows us to model a record in a way that mirrors a real database row—clean, readable, and self-documenting.

To illustrate, let us construct a simple data structure for managing a small database of original **Bardcore composers**.

Each record will store:

- The composer’s name
- Nationality
- Years of birth and death
- A representative (“exemplar”) composition
- A list of other known compositions
- Defining and Using a Data Record with dataclass
- We begin by defining the structure:

```
>>> from dataclasses import dataclass

>>> @dataclass
... class Composer:
...     Name: str
...     Nationality: str
...     YearBorn: int
...     YearDied: int
...     Exemplar: str
...     Compositions: list
...
```

Now let us create our first record:

```
>>> comp1 = Composer("Hildegard von Bingham", "German", 1098, 1179, "O Euchari", [])
>>> type(comp1)
<class '__main__.Composer'>
```

We can access fields using normal dot notation:

```
>>> print(comp1.Name, str(comp1.YearBorn) + '-' + str(comp1.YearDied))
Hildegard von Bingham 1098-1179
```

A dataclass behaves much like a structured object, but with the simplicity of a dictionary and automatic support for:

- Pretty-printing
- Comparison
- Default values (if desired)
- Type hints for readability and error checking

## Updating the Record

Dataclasses allow direct assignment to fields.

Suppose we decide to update Hildegard’s exemplar work and add additional compositions:

```
>>> comp1.Exemplar = "Ordo Virtutum"
>>> comp1.Compositions.append("O Euchari")
>>> comp1.Compositions.append("Ordo Virtutum")
>>> comp1.Compositions.append("O Virtus Sapientiae")
```

At this point, `comp1` represents a well-structured, easily accessible data record.

Working with such a record is no different from working with individual variables—except that the information is properly organised and far easier to maintain.
