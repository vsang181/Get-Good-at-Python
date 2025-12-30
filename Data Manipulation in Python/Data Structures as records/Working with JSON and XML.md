# Working with JSON and XML

In many real-world systems, data is exchanged using **XML** or **JSON** formats. Both are text-based and platform-independent, making them ideal for data storage, APIs, and configuration files. Python includes modules for reading and manipulating both formats, making it straightforward to integrate them into your scripts.

## Working with XML

XML uses tags to structure data in a tree format defined by the **Document Object Model (DOM)**. Every XML document begins with a root element, and each element can contain child elements, attributes, and text.

<img width="1278" height="349" alt="Screenshot 2025-12-30 at 01 26 10" src="https://github.com/user-attachments/assets/a37a3b1c-761c-4410-a048-a150a919ba08" />

Web pages are themselves XML-like structures. If you view a page’s source code, you will see a nested arrangement of tags such as:

```
<html>
  <head>
    <title>Example Page</title>
  </head>
  <body>
    ...
  </body>
</html>

```

We can apply the same structure to store structured data. For example, here is a simple XML file named **library.xml**, encoding composers and their works:

```
<Library>
  <Composer>
    <Name>Hildegard von Bingen</Name>
    <Nationality>German</Nationality>
    <BornYear>1098</BornYear>
    <DiedYear>1179</DiedYear>
    <Exemplar>O Euchari</Exemplar>
    <CompositionList>
      <Composition>O Euchari</Composition>
      <Composition>Ordo Virtutum</Composition>
      <Composition>O Virtus Sapientiae</Composition>
    </CompositionList>
  </Composer>

  <Composer>
    <Name>Jaufre Rudel</Name>
    <Nationality>Occitan</Nationality>
    <BornYear>1120</BornYear>
    <DiedYear>1147</DiedYear>
    <Exemplar></Exemplar>
    <CompositionList>
      <Composition>Quan lo Rossinhol</Composition>
      <Composition>Lanquan lo Temps Renovelha</Composition>
    </CompositionList>
  </Composer>
</Library>
```

### Parsing XML with ElementTree

Python’s built-in **xml.etree.ElementTree** module (usually abbreviated as `et`) provides an easy way to load and traverse XML data.

```
>>> import xml.etree.ElementTree as et

>>> tree = et.parse('library.xml')
>>> root = tree.getroot()

>>> print(len(root))
2
```

- `parse()` loads the XML file.
- `getroot()` gives us the root `<Library>` element.
- The root has two `<Composer>` child nodes, so its length is 2.

### Accessing XML Data

```
>>> print(root.tag)
Library

>>> print(root[0].tag)
Composer

>>> print(root[0][0].text)
Hildegard von Bingen
```

### Iterating Through the XML Structure

```
>>> for composer in root:
...     print(composer[0].text)
...
Hildegard von Bingen
Jaufre Rudel
```

This allows us to navigate the tree and retrieve any element’s value.

## Working with JSON

JSON (JavaScript Object Notation) is widely used in modern applications, especially web APIs and cloud services. JSON maps perfectly into Python dictionaries and lists, which makes it extremely convenient to work with.

Here is an equivalent JSON representation of our library:

```
{
  "Composers": [
    {
      "Name": "Hildegard von Bingen",
      "Nationality": "German",
      "BornYear": 1098,
      "DiedYear": 1179,
      "Exemplar": "O Euchari",
      "CompositionList": [
        {"Composition": "O Euchari"},
        {"Composition": "Ordo Virtutum"},
        {"Composition": "O Virtus Sapientiae"}
      ]
    },

    {
      "Name": "Jaufre Rudel",
      "Nationality": "Occitan",
      "BornYear": 1120,
      "DiedYear": 1147,
      "Exemplar": "",
      "CompositionList": [
        {"Composition": "Quan lo Rossinhol"},
        {"Composition": "Lanquan lo Temps Renovelha"}
      ]
    }
  ]
}
```

Assume this file is saved as **library.json**.

## Loading JSON into Python

```
>>> import json

>>> f = open("library.json", "r")
>>> library = json.load(f)

>>> type(library)
<class 'dict'>
```

JSON objects become Python dictionaries, and JSON arrays become Python lists.

## Accessing JSON Data

```
>>> for composer in library["Composers"]:
...     print(composer["Name"])
...
Hildegard von Bingen
Jaufre Rudel
```

From this point, you can work with JSON data exactly as you would with any Python dictionary.

## Summary

- **XML** is hierarchical and tag-based. ElementTree allows us to parse, navigate, and extract data from XML files using tree structures.
- **JSON** is lightweight, easier to read, and ideal for web data. Python’s `json` module converts JSON directly into dictionaries and lists for easy manipulation.

Both formats are essential tools for modern data interchange, and Python provides excellent support for working with them.
