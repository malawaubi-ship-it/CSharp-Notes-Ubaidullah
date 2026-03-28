# Module 19: XML Processing in C#

## Learning Outcomes

By the end of this module you should be able to:
- Read and write XML documents using `XmlDocument`.
- Use `XmlReader` for efficient sequential XML reading.
- Query XML data using LINQ to XML (`XDocument`).

---

## What is XML?

**XML (Extensible Markup Language)** is a text-based format for representing structured data.
It is human-readable and widely used for configuration files, data interchange, and web services.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<library>
    <book id="1">
        <title>C# Data Structures and Algorithms</title>
        <author>Marcin Jamro</author>
        <year>2018</year>
    </book>
    <book id="2">
        <title>Clean Code</title>
        <author>Robert C. Martin</author>
        <year>2008</year>
    </book>
</library>
```

---

## XmlDocument (DOM Approach)

`XmlDocument` loads the entire XML into memory as a tree structure.
Good for small-to-medium files where you need to read, modify, or navigate freely.

```csharp
using System;
using System.Xml;

// Create an XML document programmatically
XmlDocument doc = new XmlDocument();
XmlElement root = doc.CreateElement("library");
doc.AppendChild(root);

XmlElement book = doc.CreateElement("book");
book.SetAttribute("id", "1");

XmlElement title = doc.CreateElement("title");
title.InnerText = "C# Data Structures and Algorithms";
XmlElement author = doc.CreateElement("author");
author.InnerText = "Marcin Jamro";

book.AppendChild(title);
book.AppendChild(author);
root.AppendChild(book);

// Save to file
doc.Save("library.xml");
Console.WriteLine("XML saved.");

// Load and read
XmlDocument loaded = new XmlDocument();
loaded.Load("library.xml");

XmlNodeList books = loaded.GetElementsByTagName("book");
foreach (XmlNode b in books)
{
    string id       = b.Attributes["id"].Value;
    string bookTitle = b["title"].InnerText;
    Console.WriteLine($"Book {id}: {bookTitle}");
}
```

---

## XmlReader (Streaming Approach)

`XmlReader` reads XML **sequentially** without loading the whole file into memory.
Use this for very large XML files where memory is a concern.

```csharp
using System;
using System.Xml;

// Read XML sequentially using XmlReader
using XmlReader reader = XmlReader.Create("library.xml");
while (reader.Read())
{
    if (reader.NodeType == XmlNodeType.Element && reader.Name == "title")
    {
        reader.Read(); // move to the text node inside <title>
        Console.WriteLine($"Title: {reader.Value}");
    }
}
```

---

## LINQ to XML (XDocument) — Recommended Approach

LINQ to XML provides the most elegant and expressive way to work with XML in modern C#.
It integrates naturally with LINQ queries.

```csharp
using System;
using System.Linq;
using System.Xml.Linq;

// Create XML using XDocument
XDocument xmlDoc = new XDocument(
    new XElement("library",
        new XElement("book",
            new XAttribute("id", "1"),
            new XElement("title", "C# Data Structures and Algorithms"),
            new XElement("author", "Marcin Jamro"),
            new XElement("year", "2018")
        ),
        new XElement("book",
            new XAttribute("id", "2"),
            new XElement("title", "Clean Code"),
            new XElement("author", "Robert C. Martin"),
            new XElement("year", "2008")
        )
    )
);

xmlDoc.Save("library2.xml");

// Load and query using LINQ
XDocument loaded = XDocument.Load("library2.xml");

// Get all book titles
var titles = loaded.Descendants("book")
                   .Select(b => b.Element("title").Value);

foreach (string t in titles)
    Console.WriteLine(t);

// Filter: books published after 2010
var recent = loaded.Descendants("book")
                   .Where(b => int.Parse(b.Element("year").Value) > 2010)
                   .Select(b => new
                   {
                       Title = b.Element("title").Value,
                       Year  = b.Element("year").Value
                   });

foreach (var book in recent)
    Console.WriteLine($"{book.Title} ({book.Year})");

// Add a new book element
loaded.Root.Add(
    new XElement("book",
        new XAttribute("id", "3"),
        new XElement("title", "The Pragmatic Programmer"),
        new XElement("author", "David Thomas"),
        new XElement("year", "2019")
    )
);
loaded.Save("library2.xml");
```

---

## Comparison of XML Approaches

| Approach | Memory Usage | Random Access | Best For |
|----------|-------------|---------------|----------|
| `XmlDocument` | High (full tree) | Yes | Small files, modifications |
| `XmlReader` | Low (streaming) | No | Large files, read-only |
| `XDocument` (LINQ to XML) | Medium | Yes | General use, querying |

---

## Summary

XML remains widely used in configuration, data exchange, and legacy systems.
C# provides three distinct APIs. For most tasks, **LINQ to XML (`XDocument`)** is the recommended choice
because it combines the flexibility of DOM access with the power of LINQ queries.

Reference: Microsoft Docs. "LINQ to XML Overview." docs.microsoft.com
