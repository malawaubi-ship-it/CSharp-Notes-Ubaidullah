# Module 19: XML Processing in C#

## 1. Learning outcomes

By the end of this lesson, you should be able to:
	-	Understand C# XML processing

Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469




## 2. XML Processing in C#
XML Processing in C#
Explain XML Parser Architectures and APIs
XML (Extensible Markup Language) is a widely used standard for encoding documents in a format that is both human-readable and machine-readable. XML processing involves parsing XML documents, modifying them, and generating new XML documents. In C#, there are several ways to process XML data, each suitable for different use cases and performance needs.
## 1. XML Parser Architectures:
There are several different XML parser architectures used to process XML documents in C#. Each has its advantages, depending on the specific scenario, such as performance, memory usage, and the complexity of the XML structure.
	-	DOM (Document Object Model):
	-	The DOM parser loads the entire XML document into memory as a tree structure. This model allows for easy access to the entire document and modification of any element. The DOM model is best used when you need to manipulate or traverse the entire XML structure.
	-	Advantages: Easy to use, allows random access to elements, suitable for small to medium-sized XML documents.
	-	Disadvantages: Memory-intensive, can be slow for large documents.
In C#, the DOM model is implemented using the XmlDocument class.
	-	SAX (Simple API for XML):
	-	SAX is an event-driven, read-only parser. It reads the XML document sequentially from top to bottom and triggers events as it encounters elements, attributes, and other XML components. SAX does not load the entire XML into memory, making it more memory-efficient for processing large XML documents.
	-	Advantages: Memory-efficient, fast for large documents, suitable for streaming XML data.
	-	Disadvantages: Read-only, cannot be used to modify the XML document during parsing.
In C#, SAX-like functionality is provided by the XmlReader class.
	-	LINQ to XML (Language Integrated Query):
	-	LINQ to XML allows for querying and manipulating XML documents using LINQ syntax. It provides a more modern, functional way to work with XML, offering a higher-level API that makes it easier to read and modify XML data in a declarative manner.
	-	Advantages: Clean and readable code, flexible, suitable for modern .NET development.
	-	Disadvantages: Can be slower than the other approaches for large XML files.
In C#, LINQ to XML is provided through the XDocument and XElement classes.
## 2. XML Parsing APIs in C#:
	-	XmlDocument (DOM-based parsing): System.Xml.XmlDocument provides an object model for XML documents. It allows easy manipulation of XML content, adding or removing elements, and navigating the document.
	-	XmlReader (SAX-based parsing): System.Xml.XmlReader provides a forward-only parser to read XML data. It does not load the entire document into memory, making it ideal for large files.
	-	XDocument/XElement (LINQ to XML): System.Xml.Linq.XDocument and System.Xml.Linq.XElement offer a LINQ-friendly way to work with XML documents. They provide methods to query XML data, modify it, and create new XML documents.
## 3. Build XML Documents Using C#
Build XML Documents Using C#
C# provides multiple ways to build XML documents, depending on the required performance and memory constraints. Below are examples of building XML documents using different approaches: XmlDocument (DOM), XmlWriter (streaming), and XDocument (LINQ to XML).
Building XML Using XmlDocument (DOM Approach)
The XmlDocument class allows you to create XML documents in a tree structure, making it easy to traverse and modify.
Example:
using System;
using System.Xml;
 
class CreateXmlWithXmlDocument
{
    static void Main()
    {
        // Create a new XmlDocument instance
        XmlDocument doc = new XmlDocument();
 
        // Create the root element <Library>
        XmlElement root = doc.CreateElement("Library");
        doc.AppendChild(root);
 
        // Create the <Book> element
        XmlElement book = doc.CreateElement("Book");
        root.AppendChild(book);
 
        // Add an attribute to the <Book> element (ID="1")
        XmlAttribute bookId = doc.CreateAttribute("ID");
        bookId.Value = "1";
        book.SetAttributeNode(bookId);
 
        // Create child elements <Title> and <Author>
        XmlElement title = doc.CreateElement("Title");
        title.InnerText = "Bojang le Dintlha tsa Botshelo";  // Title in Setswana
        book.AppendChild(title);
 
        XmlElement author = doc.CreateElement("Author");
        author.InnerText = "Priscilla Mokoena";  // Tswana name
        book.AppendChild(author);
 
        // Save the XML document to a file
        doc.Save("Library.xml");
        Console.WriteLine( "XML file created successfully!");
    }
}
Expected Output (Library.xml):
<?xml version="1.0" encoding="utf-8"?>
<Library>
    <Book ID="1">
        <Title>Bojang le Dintlha tsa Botshelo</Title>
        <Author>Priscilla Mokoena</Author>
    </Book>
</Library>

Building XML Using XmlWriter (Streaming Approach)
The XmlWriter class provides a way to create XML documents in a forward-only, streaming manner. It’s efficient for large XML documents as it doesn't load the entire document into memory.
Example:
using System;
using System.Xml;
 
class CreateXmlWithXmlWriter
{
    static void Main()
    {
        // Create XmlWriterSettings to format the XML
        XmlWriterSettings settings = new XmlWriterSettings();
        settings.Indent = true;
 
        // Create an XmlWriter instance
        using (XmlWriter writer = XmlWriter.Create("LibraryWriter.xml", settings))
        {
            // Write the XML document
            writer.WriteStartDocument();
 
            // Write the root element <Library>
            writer.WriteStartElement("Library");
 
            // Write the <Book> element with ID attribute
            writer.WriteStartElement("Book");
            writer.WriteAttributeString("ID", "1");
 
            // Write <Title> and <Author> elements
            writer.WriteElementString("Title", "Izinkinga Zempilo");  // Zulu title
            writer.WriteElementString("Author", "Thuli Zondi");  // Zulu name
 
            // Close the <Book> element
            writer.WriteEndElement();
 
            // Close the <Library> element
            writer.WriteEndElement();
 
            // End the document
            writer.WriteEndDocument();
        }
 
        Console.WriteLine( "XML file created successfully using XmlWriter!");
    }
}
Expected Output (LibraryWriter.xml):
<?xml version="1.0" encoding="utf-8"?>
<Library>
  <Book ID="1">
    <Title>Izinkinga Zempilo</Title>
    <Author>Thuli Zondi</Author>
  </Book>
</Library>



## 4. Building XML Using XDocument (LINQ to XML)
Building XML Using XDocument (LINQ to XML)
LINQ to XML offers a more modern and declarative way to build and query XML documents. It allows for LINQ queries directly on XML, providing a more readable syntax.
Example:
using System;
using System.Xml.Linq;
 
class CreateXmlWithXDocument
{
    static void Main()
    {
        // Create a new XDocument with a root element
        XDocument doc = new XDocument(
            new XElement("Library",
                new XElement("Book", new XAttribute("ID", "1"),
                    new XElement("Title", "Uhlanga Lwempilo"),  // Zulu title
                    new XElement("Author", "Lerato Ndlovu")  // Zulu name
                )
            )
        );
 
        // Save the XML document to a file
        doc.Save("LibraryLinq.xml");
        Console.WriteLine( "XML file created successfully using LINQ to XML!");
    }
}
Expected Output (LibraryLinq.xml):
<?xml version="1.0" encoding="utf-8"?>
<Library>
  <Book ID="1">
    <Title>Uhlanga Lwempilo</Title>
    <Author>Lerato Ndlovu</Author>
  </Book>
</Library>

Conclusion
	-	DOM Parsing (XmlDocument) is best for applications that need to load and modify the entire XML structure in memory.
	-	SAX Parsing (XmlReader) is a memory-efficient way to read XML documents sequentially, suitable for large documents.
	-	LINQ to XML (XDocument, XElement) provides a modern, readable, and flexible approach for working with XML data.


## 5. Example 1: Building XML Using XmlDocument (DOM Approach)
Example 1: Building XML Using XmlDocument (DOM Approach)
The XmlDocument class provides a DOM-based approach to creating and manipulating XML documents. It loads the XML document into memory and allows easy access to the nodes.
Code Example:
using System;
using System.Xml;
 
class CreateXmlWithXmlDocument
{
    static void Main()
    {
        // Create a new XmlDocument instance
        XmlDocument doc = new XmlDocument();
 
        // Create the root element <Library>
        XmlElement root = doc.CreateElement("Library");
        doc.AppendChild(root);
 
        // Create a <Book> element
        XmlElement book = doc.CreateElement("Book");
        root.AppendChild(book);
 
        // Add an attribute to the <Book> element (ID="1")
        XmlAttribute bookId = doc.CreateAttribute("ID");
        bookId.Value = "1";
        book.SetAttributeNode(bookId);
 
        // Create child elements <Title> and <Author>
        XmlElement title = doc.CreateElement("Title");
        title.InnerText = "Bojang le Dintlha tsa Botshelo";  // Title in Setswana
        book.AppendChild(title);
 
        XmlElement author = doc.CreateElement("Author");
        author.InnerText = "Priscilla Mokoena";  // Tswana name
        book.AppendChild(author);
 
        // Save the XML document to a file
        doc.Save("Library.xml");
        Console.WriteLine( "XML file created successfully!");
    }
}
Expected Output (Library.xml):
<?xml version="1.0" encoding="utf-8"?>
<Library>
    <Book ID="1">
        <Title>Bojang le Dintlha tsa Botshelo</Title>
        <Author>Priscilla Mokoena</Author>
    </Book>
</Library>



## 6. Example 2: Building XML Using XmlWriter (Streaming Approach)
Example 2: Building XML Using XmlWriter (Streaming Approach)
The XmlWriter class provides a streaming approach to XML creation. It is efficient for generating large XML documents since it does not load the entire document into memory at once.
Code Example:
using System;
using System.Xml;
 
class CreateXmlWithXmlWriter
{
    static void Main()
    {
        // Create XmlWriterSettings to format the XML
        XmlWriterSettings settings = new XmlWriterSettings();
        settings.Indent = true;
 
        // Create an XmlWriter instance
        using (XmlWriter writer = XmlWriter.Create("LibraryWriter.xml", settings))
        {
            // Write the XML document
            writer.WriteStartDocument();
 
            // Write the root element <Library>
            writer.WriteStartElement("Library");
 
            // Write the <Book> element with ID attribute
            writer.WriteStartElement("Book");
            writer.WriteAttributeString("ID", "1");
 
            // Write <Title> and <Author> elements
            writer.WriteElementString("Title", "Izinkinga Zempilo");  // Zulu title
            writer.WriteElementString("Author", "Thuli Zondi");  // Zulu name
 
            // Close the <Book> element
            writer.WriteEndElement();
 
            // Close the <Library> element
            writer.WriteEndElement();
 
            // End the document
            writer.WriteEndDocument();
        }
 
        Console.WriteLine( "XML file created successfully using XmlWriter!");
    }
}
Expected Output (LibraryWriter.xml):
<?xml version="1.0" encoding="utf-8"?>
<Library>
  <Book ID="1">
    <Title>Izinkinga Zempilo</Title>
    <Author>Thuli Zondi</Author>
  </Book>
</Library>


## 7. Example 3: Building XML Using XDocument (LINQ to XML)
Example 3: Building XML Using XDocument (LINQ to XML)
The XDocument class allows you to create and manipulate XML documents using LINQ, which provides a more modern and readable way to handle XML data.
Code Example:
using System;
using System.Xml.Linq;
 
class CreateXmlWithXDocument
{
    static void Main()
    {
        // Create a new XDocument with a root element
        XDocument doc = new XDocument(
            new XElement("Library",
                new XElement("Book", new XAttribute("ID", "1"),
                    new XElement("Title", "Uhlanga Lwempilo"),  // Zulu title
                    new XElement("Author", "Lerato Ndlovu")  // Zulu name
                )
            )
        );
 
        // Save the XML document to a file
        doc.Save("LibraryLinq.xml");
        Console.WriteLine( "XML file created successfully using LINQ to XML!");
    }
}
Expected Output (LibraryLinq.xml):
<?xml version="1.0" encoding="utf-8"?>
<Library>
  <Book ID="1">
    <Title>Uhlanga Lwempilo</Title>
    <Author>Lerato Ndlovu</Author>
  </Book>
</Library>

Conclusion
	-	XmlDocument (DOM-based): Best for scenarios where you need to load, navigate, and modify the entire XML document in memory. It is ideal for smaller XML files.
	-	XmlWriter (Streaming): Suitable for scenarios where memory usage is a concern, and you need to generate large XML documents efficiently without loading everything into memory at once.
	-	XDocument (LINQ to XML): Provides a modern, clean syntax for working with XML documents, making it the best choice for most C# applications that require XML processing.
 


## 8. Scenarios
Scenario 1: DOM-Based XML Creation with XmlDocument
Scenario Question:
A local library wants to keep track of their books in an XML file. Each book must have a unique ID, a title in Setswana, and an author. Use the DOM-based XmlDocument approach to create the file.
Solution:
using System;
using System.Xml;

class LibraryXmlDom
{
    static void Main()
    {
        XmlDocument doc = new XmlDocument();

        XmlElement root = doc.CreateElement("Library");
        doc.AppendChild(root);

        XmlElement book = doc.CreateElement("Book");
        root.AppendChild(book);

        XmlAttribute id = doc.CreateAttribute("ID");
        id.Value = "101";
        book.Attributes.Append(id);

        XmlElement title = doc.CreateElement("Title");
        title.InnerText = "Bojang le Dintlha tsa Botshelo";  // Setswana
        book.AppendChild(title);

        XmlElement author = doc.CreateElement("Author");
        author.InnerText = "Priscilla Mokoena";  // Tswana name
        book.AppendChild(author);

        doc.Save("Library.xml");
        Console.WriteLine( "Library.xml created successfully.");
    }
}
Expected Output (Library.xml):
<?xml version="1.0" encoding="utf-8"?>
<Library>
  <Book ID="101">
    <Title>Bojang le Dintlha tsa Botshelo</Title>
    <Author>Priscilla Mokoena</Author>
  </Book>
</Library>

Scenario 2: Streaming XML with XmlWriter
Scenario Question:
An online bookstore is generating a live XML feed of new books. To reduce memory usage, they want to use a streaming approach. Create an XML file using XmlWriter that lists books with their ID, title (in Zulu), and author.
Solution:
using System;
using System.Xml;

class LibraryXmlWriter
{
    static void Main()
    {
        XmlWriterSettings settings = new XmlWriterSettings { Indent = true };

        using (XmlWriter writer = XmlWriter.Create("LiveBooks.xml", settings))
        {
            writer.WriteStartDocument();
            writer.WriteStartElement("Books");

            writer.WriteStartElement("Book");
            writer.WriteAttributeString("ID", "202");
            writer.WriteElementString("Title", "Izinkinga Zempilo");  // Zulu
            writer.WriteElementString("Author", "Thuli Zondi");
            writer.WriteEndElement();

            writer.WriteEndElement();
            writer.WriteEndDocument();
        }

        Console.WriteLine( "LiveBooks.xml created successfully using XmlWriter.");
    }
}
Expected Output (LiveBooks.xml):
<?xml version="1.0" encoding="utf-8"?>
<Books>
  <Book ID="202">
    <Title>Izinkinga Zempilo</Title>
    <Author>Thuli Zondi</Author>
  </Book>
</Books>

Scenario 3: LINQ to XML with XDocument
Scenario Question:
A digital archive stores multilingual books. Use LINQ to XML (XDocument) to create an XML file that lists a book in isiZulu with its title and author.
Solution:
using System;
using System.Xml.Linq;

class LibraryXDocument
{
    static void Main()
    {
        XDocument doc = new XDocument(
            new XElement("Archive",
                new XElement("Book", new XAttribute("ID", "303"),
                    new XElement("Title", "Uhlanga Lwempilo"),  // isiZulu
                    new XElement("Author", "Lerato Ndlovu")
                )
            )
        );

        doc.Save("DigitalArchive.xml");
        Console.WriteLine( "DigitalArchive.xml created using XDocument.");
    }
}
Expected Output (DigitalArchive.xml):
<?xml version="1.0" encoding="utf-8"?>
<Archive>
  <Book ID="303">
    <Title>Uhlanga Lwempilo</Title>
    <Author>Lerato Ndlovu</Author>
  </Book>
</Archive>

Summary Table
Approach
Class/Method Used
Best For
File Output Example
DOM
XmlDocument
Modifying or reading entire XML in memory
Library.xml
Streaming
XmlWriter
Large XML files or streaming generation
LiveBooks.xml
LINQ to XML
XDocument, XElement
Clean, modern querying and creation
DigitalArchive.xml


	-	2. Video Reference
	-	7. Scenario 1: E-commerce Product Catalog Update
	-	8. Scenario 2: Employee Data Query and Export to CSV
