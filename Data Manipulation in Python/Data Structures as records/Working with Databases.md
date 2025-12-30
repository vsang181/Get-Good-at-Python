# Working with Databases

To store and retrieve structured data properly, we will now connect our Python program to a simple relational database. For this exercise, we will use **SQLite**, a lightweight file-based SQL database that is built into Python—so no installation is required.

We will create a small database to store composers and their compositions. Since composers can have many compositions, we will normalise our data into two tables:

1. **Composer** — one row per composer
2. **Compositions** — multiple rows per composer, one per composition

Let us begin building the database-management script.

## Initial Setup and Database Creation

We start by importing the required modules and checking whether the database file already exists.

```
1. from dataclasses import dataclass
2. import sqlite3
3. from os.path import exists
4. if not exists("music.db"):
5.     print("Creating database")
6. conn = sqlite3.connect("music.db")
```

- Line 1 imports `dataclass`, which we will use for structured records.
- Line 2 imports the `sqlite3` module.
- Line 3 allows us to check whether the database file already exists.
- Lines 4–5 print a message if the database needs to be created.
- Line 6 creates or opens the SQLite database file.

## Creating the Database Tables

SQLite tables must be created before we can store data. We use SQL commands with the `IF NOT EXISTS` clause to ensure that the script can run repeatedly without errors.

```
7. sq = 'CREATE TABLE IF NOT EXISTS Composer(Name TEXT NOT NULL, Nationality TEXT, BornYear INT, DiedYear INT, Exemplar TEXT);'
8. conn.execute(sq)

9. sq = 'CREATE TABLE IF NOT EXISTS Compositions(Composer TEXT NOT NULL, Composition TEXT NOT NULL);'
10. conn.execute(sq)

11. cursor = conn.cursor()
```

We now have:

- A main table storing composer details
- A second table storing compositions linked by composer name
- A cursor object ready for SQL operations

## Defining the Data Record Structure

We now create a dataclass mirroring our database record structure.

```
12. @dataclass
13. class Composer:
14.     Name: str
15.     Nationality: str
16.     BornYear: int
17.     DiedYear: int
18.     Exemplar: str
19.     Compositions: list
```

We also create a blank object to reuse when inserting records:

```
20. comp = Composer("", "", 0, 0, "", [])
```

## Main Program Loop and Adding a Composer

We now write our main loop, providing the user with options:

- Add a composer
- Insert a new composition
- List all stored music
- Quit

```
22. while True:
23.     action = input("(A)dd Composer, (I)nsert Composition, (L)ist Music, (Q)uit: ").upper()
24.     if action == 'Q':
25.         break
```

### Adding a Composer

```
27. if action == 'A':
28.     comp.Name = input("Name: ")
29.     comp.Nationality = input("Nationality: ")
30.     comp.BornYear = input("Year Born: ")
31.     comp.DiedYear = input("Year Died: ")
32.     comp.Compositions = []   # reset list
33.     while True:
34.         opus = input("Composition: ")
35.         if len(opus) == 0:
36.             break
37.         comp.Compositions.append(opus)
38.         ex = input("Is this the exemplar Y/N? ").upper()
39.         if ex == "Y":
40.             comp.Exemplar = opus
```

## Writing Data into SQLite

After gathering all data, we insert it into the database.

### Insert Composer Record

```
40. sq = f"INSERT INTO Composer (Name, Nationality, BornYear, DiedYear, Exemplar) VALUES ('{comp.Name}', '{comp.Nationality}', {comp.BornYear}, {comp.DiedYear}, '{comp.Exemplar}');"
46. cursor.execute(sq)
```

### Insert Compositions

```
47. for opus in comp.Compositions:
48.     sq = f"INSERT INTO Compositions (Composer, Composition) VALUES ('{comp.Name}', '{opus}');"
49.     cursor.execute(sq)
51. conn.commit()
```

This completes insertion of a composer and their works.

## Inserting Additional Compositions

```
52. if action == 'I':
53.     comp.Name = input("Name: ")
54.     sq = f"SELECT Name FROM Composer WHERE Name='{comp.Name}';"
55.     cursor.execute(sq)
56.     rows = cursor.fetchall()
57.     if len(rows) == 0:
58.         print("No such Composer")
59.     else:
60.         opus = input("Composition: ")
61.         sq = f"INSERT INTO Compositions (Composer, Composition) VALUES ('{comp.Name}', '{opus}');"
62.         cursor.execute(sq)
63.         conn.commit()
```

## Listing All Stored Music

```
65. if action == 'L':
66.     cursor.execute("SELECT * FROM Composer;")
67.     library = cursor.fetchall()
68.     for composer in library:
69.         print("Composer: " + composer[0])
70.         sq = f'SELECT Composition FROM Compositions WHERE Composer="{composer[0]}";'
71.         cursor.execute(sq)
72.         music = cursor.fetchall()
73.         for opus in music:
74.             print("  " + opus[0])
```

This displays:

Each composer

Their associated compositions

### Closing the Database

```
75. cursor.close()
76. conn.close()
```

### Example Run

```
~ % python3 music.py
Creating database
(A)dd Composer, (I)nsert Composition, (L)ist Music, (Q)uit: A
Name: Hildegard von Bingen
Nationality: German
Year Born: 1098
Year Died: 1179
Composition: O Euchari
Is this the exemplar Y/N? Y
Composition: Ordo Virtutum
Is this the exemplar Y/N? 
Composition: O Virtus Sapientiae
Is this the exemplar Y/N?
Composition: 
(A)dd Composer, (I)nsert Composition, (L)ist Music, (Q)uit: L
Composer: Hildegard von Bingen
  O Euchari
  Ordo Virtutum
  O Virtus Sapientiae
```

We now have a functioning database-backed application that:

- Uses **dataclasses** for clean, structured in-memory records
- Stores and retrieves data using **SQLite**
- Demonstrates practical CRUD operations (Create, Read, Update)
