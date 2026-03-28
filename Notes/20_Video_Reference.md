# Module 20: Video Reference

1. Learning outcomes

By the end of this lesson, you should be able to:
	•	Understand C# XML processing

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 

   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Video Reference
Play Video

3. Case Study 1: Creating and Writing an XML Document
Case Study 1: Creating and Writing an XML Document
Problem:
A school system needs to generate an XML file that stores student information. The XML document must contain a root element called <School> with multiple <Student> elements, each having child elements like Name, Age, and Grade.
Solution:
We can use the XmlDocument class to create an XML file where student data is written under a root <School> element.
Code:
using System;
using System.Xml;
 
class CreateStudentXML
{
    static void Main()
    {
        // Create an instance of XmlDocument
        XmlDocument doc = new XmlDocument();
 
        // Create the root element <School>
        XmlElement schoolElement = doc.CreateElement("School");
        doc.AppendChild(schoolElement);
 
        // Create multiple <Student> elements
        for (int idx = 1; idx <= 3; idx++)
        {
            XmlElement studentElement = doc.CreateElement("Student");
            studentElement.SetAttribute("ID", i.ToString());
 
            // Add Name, Age, Grade elements to each <Student>
            XmlElement nameElement = doc.CreateElement("Name");
            nameElement.InnerText = $"Student {i}";
            studentElement.AppendChild(nameElement);
 
            XmlElement ageElement = doc.CreateElement("Age");
            ageElement.InnerText = (i + 10).ToString();
            studentElement.AppendChild(ageElement);
 
            XmlElement gradeElement = doc.CreateElement("Grade");
            gradeElement.InnerText = (i % 2 == 0) ? "A" : "B";
            studentElement.AppendChild(gradeElement);
 
            // Append the student to the root
            schoolElement.AppendChild(studentElement);
        }
 
        // Save the XML document to a file
        doc.Save("Students.xml");
        Console.WriteLine(/* Output */ "XML file created successfully.");
    }
}
Expected Output (Students.xml):
<?xml version="1.0" encoding="utf-8"?>
<School>
  <Student ID="1">
    <Name>Student 1</Name>
    <Age>11</Age>
    <Grade>B</Grade>
  </Student>
  <Student ID="2">
    <Name>Student 2</Name>
    <Age>12</Age>
    <Grade>A</Grade>
  </Student>
  <Student ID="3">
    <Name>Student 3</Name>
    <Age>13</Age>
    <Grade>B</Grade>
  </Student>
</School>
Explanation:
	•	The code creates an XML document with a <School> root element and multiple <Student> elements.
	•	Each <Student> has a Name, Age, and Grade element.
	•	The XML file is saved to disk.

 
4. Case Study 2: Reading and Modifying XML Document
Case Study 2: Reading and Modifying XML Document
Problem:
A library system needs to read an existing XML file that contains book data and modify the price of a book based on the BookID. After modification, the updated data should be saved back to the file.
Solution:
We use the XmlDocument class to read an XML file, update an element, and save the changes back to the file.
Code:
using System;
using System.Xml;
 
class ModifyBookPrice
{
    static void Main()
    {
        // Load the existing XML document
        XmlDocument doc = new XmlDocument();
        doc.Load("Books.xml");
 
        // Find the book with BookID="2"
        XmlNode bookNode = doc.SelectSingleNode("//Book[@BookID='2']");
 
        // Modify the Price of the selected book
        if (bookNode != null)
        {
            XmlNode priceNode = bookNode.SelectSingleNode("Price");
            if (priceNode != null)
            {
                priceNode.InnerText = "19.99"; // Update price
                Console.WriteLine(/* Output */ "Price updated successfully.");
            }
        }
 
        // Save the modified XML document
        doc.Save("Books_Updated.xml");
    }
}
Expected Output:
Price updated successfully.
Expected XML Output (Books_Updated.xml):
<?xml version="1.0" encoding="utf-8"?>
<Library>
  <Book BookID="1">
    <Title>C# Programming</Title>
    <Author>John Smith</Author>
    <Price>29.99</Price>
  </Book>
  <Book BookID="2">
    <Title>XML for Beginners</Title>
    <Author>Mary Jane</Author>
    <Price>19.99</Price> <!-- Price updated here -->
  </Book>
</Library>
Explanation:
	•	The program reads the XML document Books.xml.
	•	It finds the book with BookID="2", changes the price of that book, and saves the updated document to Books_Updated.xml.

 
5. Case Study 3: Writing XML with XDocument (LINQ to XML)
Case Study 3: Writing XML with XDocument (LINQ to XML)
Problem:
We need to create an XML document that stores contact information for a list of people. The XML file must have a root <Contacts> element, and each contact should have Name, Phone, and Email.
Solution:
We can use LINQ to XML with XDocument to easily generate the XML document in a concise way.
Code:
using System;
using System.Linq;
using System.Xml.Linq;
 
class CreateContactsXML
{
    static void Main()
    {
        // Create a list of contacts
        var contacts = new[]
        {
            new { Name = "Priscilla Tswana", Phone = "123-456-7890", Email = "priscilla@example.com" },
            new { Name = "Thabo Zulu", Phone = "987-654-3210", Email = "thabo@example.com" },
            new { Name = "Lerato Ndlovu", Phone = "555-666-7777", Email = "lerato@example.com" }
        };
 
        // Create the XML document
        XDocument doc = new XDocument(
            new XElement("Contacts",
                contacts.Select(contact =>
                    new XElement("Contact",
                        new XElement("Name", contact.Name),
                        new XElement("Phone", contact.Phone),
                        new XElement("Email", contact.Email)
                    )
                )
            )
        );
 
        // Save the XML document to a file
        doc.Save("Contacts.xml");
        Console.WriteLine(/* Output */ "Contacts XML file created successfully.");
    }
}
Expected Output (Contacts.xml):
<?xml version="1.0" encoding="utf-8"?>
<Contacts>
  <Contact>
    <Name>Priscilla Tswana</Name>
    <Phone>123-456-7890</Phone>
    <Email>priscilla@example.com</Email>
  </Contact>
  <Contact>
    <Name>Thabo Zulu</Name>
    <Phone>987-654-3210</Phone>
    <Email>thabo@example.com</Email>
  </Contact>
  <Contact>
    <Name>Lerato Ndlovu</Name>
    <Phone>555-666-7777</Phone>
    <Email>lerato@example.com</Email>
  </Contact>
</Contacts>
Explanation:
	•	The XDocument class is used to create an XML document by using LINQ syntax.
	•	The program generates an XML file with a <Contacts> root element and multiple <Contact> elements.

 
6. Case Study 4: Reading and Querying XML with LINQ to XML
Case Study 4: Reading and Querying XML with LINQ to XML
Problem:
A company wants to read an XML file containing employee data and query for all employees who belong to the "Sales" department.
Solution:
We use LINQ to XML to read the XML document, filter data based on a condition (employees in the "Sales" department), and display the results.
Code:
using System;
using System.Linq;
using System.Xml.Linq;
 
class QueryEmployeeDepartment
{
    static void Main()
    {
        // Load the XML document
        XDocument doc = XDocument.Load("Employees.xml");
 
        // Query for employees in the Sales department
        var salesEmployees = from employee in doc.Descendants("Employee")
                             where (string)employee.Element("Department") == "Sales"
                             select new
                             {
                                 Name = employee.Element("Name").Value,
                                 Department = employee.Element("Department").Value
                             };
 
        // Display the results
        Console.WriteLine(/* Output */ "Employees in Sales Department:");
        foreach (var employee in salesEmployees)
        {
            Console.WriteLine(/* Output */ $"Name: {employee.Name}, Department: {employee.Department}");
        }
    }
}
Expected Output:
Employees in Sales Department:
Name: John Doe, Department: Sales
Name: Mary Jane, Department: Sales
Expected XML Input (Employees.xml):
<?xml version="1.0" encoding="utf-8"?>
<Company>
  <Employee>
    <Name>John Doe</Name>
    <Department>Sales</Department>
  </Employee>
  <Employee>
    <Name>Mary Jane</Name>
    <Department>Sales</Department>
  </Employee>
  <Employee>
    <Name>Sam Smith</Name>
    <Department>HR</Department>
  </Employee>
</Company>
Explanation:
	•	The program reads the Employees.xml file using XDocument.
	•	It queries for all employees in the "Sales" department using LINQ syntax.
	•	The results are displayed on the console.
 
7. Scenario 1: E-commerce Product Catalog Update
Scenario 1: E-commerce Product Catalog Update
Problem:
An e-commerce platform needs to update its product catalog. The product information is stored in an XML file, and the company needs to add new products, update the price of some existing products, and remove outdated products. Your task is to implement a solution that can:
	•	Add new products to the catalog.
	•	Update the price of an existing product based on the ProductID.
	•	Remove a product based on the ProductID.
Solution:
We will use XmlDocument to modify the XML file. The solution includes three functionalities:
	•	Adding a new product.
	•	Updating an existing product’s price.
	•	Removing a product.
Code:
using System;
using System.Xml;
 
class ECommerceCatalog
{
    static void Main()
    {
        string filePath = "ProductCatalog.xml";
        XmlDocument doc = new XmlDocument();
        doc.Load(filePath);
 
        // 1. Add a new product
        AddNewProduct(doc, "P004", "Wireless Mouse", 29.99);
        
        // 2. Update the price of an existing product
        UpdateProductPrice(doc, "P002", 19.99);
        
        // 3. Remove a product
        RemoveProduct(doc, "P003");
 
        // Save the modified document
        doc.Save("UpdatedProductCatalog.xml");
        Console.WriteLine(/* Output */ "Catalog updated successfully.");
    }
 
    static void AddNewProduct(XmlDocument doc, string productId, string productName, double productPrice)
    {
        XmlElement productElement = doc.CreateElement("Product");
        productElement.SetAttribute("ProductID", productId);
 
        XmlElement nameElement = doc.CreateElement("ProductName");
        nameElement.InnerText = productName;
        productElement.AppendChild(nameElement);
 
        XmlElement priceElement = doc.CreateElement("Price");
        priceElement.InnerText = productPrice.ToString("F2");
        productElement.AppendChild(priceElement);
 
        doc.DocumentElement.AppendChild(productElement);
        Console.WriteLine(/* Output */ $"New product '{productName}' added.");
    }
 
    static void UpdateProductPrice(XmlDocument doc, string productId, double newPrice)
    {
        XmlNode productNode = doc.SelectSingleNode($"//Product[@ProductID='{productId}']");
        if (productNode != null)
        {
            XmlNode priceNode = productNode.SelectSingleNode("Price");
            priceNode.InnerText = newPrice.ToString("F2");
            Console.WriteLine(/* Output */ $"Price of product with ID '{productId}' updated.");
        }
        else
        {
            Console.WriteLine(/* Output */ $"Product with ID '{productId}' not found.");
        }
    }
 
    static void RemoveProduct(XmlDocument doc, string productId)
    {
        XmlNode productNode = doc.SelectSingleNode($"//Product[@ProductID='{productId}']");
        if (productNode != null)
        {
            doc.DocumentElement.RemoveChild(productNode);
            Console.WriteLine(/* Output */ $"Product with ID '{productId}' removed.");
        }
        else
        {
            Console.WriteLine(/* Output */ $"Product with ID '{productId}' not found.");
        }
    }
}
Expected Output:
New product 'Wireless Mouse' added.
Price of product with ID 'P002' updated.
Product with ID 'P003' removed.
Catalog updated successfully.
Expected XML Output (UpdatedProductCatalog.xml):
<?xml version="1.0" encoding="utf-8"?>
<ProductCatalog>
  <Product ProductID="P001">
    <ProductName>Wireless Keyboard</ProductName>
    <Price>49.99</Price>
  </Product>
  <Product ProductID="P002">
    <ProductName>Bluetooth Speaker</ProductName>
    <Price>19.99</Price> <!-- Price updated here -->
  </Product>
  <Product ProductID="P004">
    <ProductName>Wireless Mouse</ProductName>
    <Price>29.99</Price> <!-- New product added -->
  </Product>
</ProductCatalog>
 
8. Scenario 2: Employee Data Query and Export to CSV
Scenario 2: Employee Data Query and Export to CSV
Problem:
A company’s HR department has an XML file containing employee data. The HR team needs to:
	•	Retrieve all employees who have a specific department.
	•	Export the data of these employees (Name, Department, and Salary) to a CSV file.
You are tasked with implementing this solution using LINQ to XML in C#.
Solution:
We will use LINQ to XML to query the employees from the XML file based on their department. Then, we will export the relevant data to a CSV file.
Code:
using System;
using System.Linq;
using System.Xml.Linq;
using System.IO;
 
class EmployeeQueryAndExport
{
    static void Main()
    {
        string xmlFilePath = "Employees.xml";
        string csvFilePath = "SalesEmployees.csv";
 
        // Load the XML document
        XDocument doc = XDocument.Load(xmlFilePath);
 
        // Query all employees in the 'Sales' department
        var salesEmployees = from employee in doc.Descendants("Employee")
                             where (string)employee.Element("Department") == "Sales"
                             select new
                             {
                                 Name = employee.Element("Name").Value,
                                 Department = employee.Element("Department").Value,
                                 Salary = employee.Element("Salary").Value
                             };
 
        // Export the data to a CSV file
        ExportToCSV(salesEmployees, csvFilePath);
        Console.WriteLine(/* Output */ "Sales department employees exported to CSV.");
    }
 
    static void ExportToCSV(IEnumerable<dynamic> employees, string filePath)
    {
        using (StreamWriter writer = new StreamWriter(filePath))
        {
            // Write CSV header
            writer.WriteLine("Name,Department,Salary");
 
            // Write employee data
            foreach (var employee in employees)
            {
                writer.WriteLine($"{employee.Name},{employee.Department},{employee.Salary}");
            }
        }
    }
}
Expected Output:
Sales department employees exported to CSV.
Expected CSV Output (SalesEmployees.csv):
Name,Department,Salary
Khotso Mokoena,Sales,50000
Kea Lebona,Sales,55000
Expected XML Input (Employees.xml):
<?xml version="1.0" encoding="utf-8"?>
<Company>
  <Employee>
    <Name>Khotso Mokoena</Name>
    <Department>Sales</Department>
    <Salary>50000</Salary>
  </Employee>
  <Employee>
    <Name>Kea Lebona</Name>
    <Department>Sales</Department>
    <Salary>55000</Salary>
  </Employee>
  <Employee>
    <Name>Reabetswe Msimango</Name>
    <Department>HR</Department>
    <Salary>45000</Salary>
  </Employee>
</Company>

Conclusion:
These two scenarios demonstrate practical use cases for XML processing in C# using Sesotho names:
	•	Catalog Update: The first scenario updates an XML document (adding, updating, and removing elements).
	•	Data Query and Export: The second scenario queries an XML document for employees in a specific department and exports the relevant data to a CSV file.


