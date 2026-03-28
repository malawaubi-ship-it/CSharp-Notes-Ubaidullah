# Module 14: Collaborative Project

1. Learning outcomes

By the end of this lesson, you should be able to:
	•	Understand C# collections

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapter 9
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Collaborative Project

Write sample code on the following LINQ table. Each method must have its own well commented code.
 
3. Introduction to LINQ
Introduction to LINQ in C#
LINQ, which stands for Language Integrated Query, is a powerful feature in C# that allows developers to write expressive and readable queries directly within the language. Traditionally, querying data required using separate query languages such as SQL for databases or XPath for XML documents. LINQ changes this by integrating query syntax into C#, allowing for a uniform approach to querying various types of data sources, including collections in memory, databases, and XML files.
The key advantage of LINQ is its ability to bring consistency and type-safety to querying operations. Unlike traditional query approaches that use strings and lack compile-time checking, LINQ enables queries to be written using strongly-typed C# expressions. This allows developers to catch errors at compile-time, leverage IntelliSense support in IDEs like Visual Studio, and write less verbose and more readable code. LINQ queries can be written using either query syntax, which resembles SQL, or method syntax, which uses lambda expressions and method chaining.
LINQ works with any data source that implements the IEnumerable or IEnumerable<T> interfaces. The System.Linq namespace provides extension methods for these interfaces, enabling operations like filtering, sorting, and grouping directly on collections. LINQ is commonly used in C# with in-memory collections (LINQ to Objects), relational databases (LINQ to SQL or LINQ to Entities), and XML documents (LINQ to XML). Regardless of the data source, LINQ provides a consistent and elegant way to work with data in a type-safe and declarative manner.
Example 1: Filtering and Ordering Numbers Using Query Syntax

using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        List<int> numArray = new List<int> { 9, 2, 5, 1, 7, 4, 8 };

        var result = from n in numArray
                     where n > 4
                     orderby n
                     select n;

        foreach (var num in result)
        {
            Console.Write(num + " ");
        }
    }
}
 
Example 2: Using Method Syntax to Query a List of Strings

using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        List<string> fruits = new List<string> { "apple", "banana", "cherry", "apricot" };

        var result = fruits
            .Where(f => f.StartsWith("a"))
            .OrderBy(f => f);

        foreach (var fruit in result)
        {
            Console.WriteLine(/* Output */ fruit);
        }
    }
}
Output:
 

Play Video
3.1. Application of LINQ
LINQ (Language Integrated Query) is widely applied in real-world C# development to simplify data access, manipulation, and transformation across various data sources. Whether working with in-memory collections, databases, XML documents, or web services, LINQ offers a unified and declarative way to query and process data without switching to different syntaxes or technologies. Its ability to express complex queries concisely using native C# constructs makes LINQ both powerful and developer-friendly.
One of the most common applications of LINQ is in filtering and sorting data from collections. Instead of writing multiple loops and conditional statements, developers can express the intent of the operation clearly and compactly. LINQ also supports grouping, joining, projection (selecting specific parts of data), and aggregation operations, which are particularly useful in data analytics, reporting, and UI data-binding scenarios.
In enterprise applications, LINQ is extensively used with databases through LINQ to SQL or Entity Framework (LINQ to Entities), allowing developers to write database queries in C# and have them translated into SQL under the hood. This not only speeds up development but also improves maintainability and reduces errors. Similarly, LINQ to XML provides an elegant approach for navigating and querying XML structures, avoiding verbose DOM code.
By integrating seamlessly into the C# language and supporting a broad set of query operations, LINQ greatly enhances productivity, reduces code complexity, and improves readability across many software development contexts.

Example 1: Grouping Items Using LINQ
using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        List<string> names = new List<string> { "Alice", "Bob", "Charlie", "David", "Daniel", "Brian" };

        var grouped = from name in names
                      group name by name[0] into nameGroup
                      orderby nameGroup.Key
                      select nameGroup;

        foreach (var group in grouped)
        {
            Console.WriteLine(/* Output */ $"Names starting with '{group.Key}':");
            foreach (var name in group)
            {
                Console.WriteLine(/* Output */ $" - {name}");
            }
        }
    }
}
Explanation: This example groups names by their starting letter and displays the grouped results. It demonstrates how LINQ can replace more verbose dictionary-based grouping code.

Example 2: Using LINQ to Calculate Average of Filtered Values

using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        List<int> scores = new List<int> { 70, 85, 90, 60, 75, 95, 88 };

        double averageHighScores = scores
            .Where(score => score >= 80)
            .Average();

        Console.WriteLine(/* Output */ "Average of high scores (80+): " + averageHighScores);
    }
}
Explanation: This snippet filters out scores below 80 and calculates the average of the remaining ones using LINQ’s Where() and Average() methods.
3.2. The shared System.Linq namespace
The System.Linq namespace is a fundamental part of the .NET framework that enables Language Integrated Query (LINQ) functionality in C#. It introduces a set of extension methods for querying collections that implement the IEnumerable or IEnumerable<T> interfaces. This makes LINQ a first-class citizen in the C# language, allowing developers to write SQL-like queries directly in code, using familiar syntax and type safety.
Traditionally, querying data required external query languages such as SQL for databases or XPath for XML. These approaches involved string-based commands that lacked compile-time checking, IntelliSense support, and integration with the type system. The System.Linq namespace addresses this by allowing developers to write expressive and concise queries in C#, which are checked at compile-time and fully integrated with the language's features.
The real power of System.Linq lies in its standard query operators—such as Where(), Select(), OrderBy(), GroupBy(), Join(), and more—which simplify complex data manipulations. These methods are implemented as extension methods on IEnumerable<T>, allowing them to be used fluently with collections like arrays, lists, and even queryable data sources like LINQ to SQL or Entity Framework.

Example 1: Using Where() and Select() from System.Linq

using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        List<string> cities = new List<string> { "London", "Lisbon", "Berlin", "Los Angeles", "Madrid" };

        var lCities = cities
            .Where(city => city.StartsWith("L"))
            .Select(city => city.ToUpper());

        foreach (var city in lCities)
        {
            Console.WriteLine(/* Output */ city);
        }
    }
}
Explanation: This example uses Where() to filter cities that start with the letter "L", and Select() to convert the results to uppercase. These methods come from System.Linq and operate on IEnumerable<string>.

Example 2: Using GroupBy() to Organize Data

using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        var products = new List<string> { "Apple", "Avocado", "Banana", "Blueberry", "Cherry" };

        var groupedProducts = products.GroupBy(p => p[0]);

        foreach (var group in groupedProducts)
        {
            Console.WriteLine(/* Output */ $"Group {group.Key}:");
            foreach (var item in group)
            {
                Console.WriteLine(/* Output */ $" - {item}");
            }
        }
    }
}
Explanation: Here, GroupBy() is used to group product names by their first letter. This functionality is part of System.Linq, and it helps organize data with minimal code.
4. LINQ Standard Query operators
LINQ standard query operators are a set of extension methods provided by the System.Linq namespace that enable powerful querying capabilities directly on data collections in C#. These operators work primarily on sequences—objects that implement IEnumerable<T> or IQueryable<T>—and allow developers to perform common data operations such as filtering, projection, aggregation, sorting, joining, and more.
These operators allow developers to work with data in a high-level, declarative way, reducing the need for verbose loops or complex conditional logic. Since they are type-safe and integrated into the language, developers benefit from compile-time checking, IntelliSense support, and cleaner, more readable code.
There are two main syntaxes for using LINQ in C#: query syntax (which resembles SQL) and method syntax (which chains methods like Where(), Select(), etc.). Method syntax is often preferred for its flexibility and clarity, especially when chaining multiple operations.
Below are two practical examples to illustrate how standard query operators work:

Example 1: Filtering and Sorting with Where() and OrderBy()

using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        List<int> numArray = new List<int> { 12, 5, 8, 1, 19, 6, 3, 10 };

        var filteredAndSorted = numArray
            .Where(n => n > 5)
            .OrderBy(n => n);

        Console.WriteLine(/* Output */ "Numbers greater than 5, sorted:");
        foreach (var num in filteredAndSorted)
        {
            Console.Write(num + " ");
        }
    }
}
Explanation: In this example, Where() filters out numArray less than or equal to 5, and OrderBy() sorts the remaining numArray in ascending order.

Example 2: Aggregation with Sum() and Projection with Select()

using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        var prices = new List<double> { 19.99, 5.49, 15.89, 3.99 };

        var total = prices.Sum();
        var formattedPrices = prices.Select(p => $"${p:F2}");

        Console.WriteLine(/* Output */ "Formatted prices:");
        foreach (var price in formattedPrices)
        {
            Console.WriteLine(/* Output */ price);
        }

        Console.WriteLine(/* Output */ $"\nTotal: ${total:F2}");
    }
}
Explanation: This example uses Select() to project each price into a formatted string and Sum() to calculate the total of all prices. These operators streamline data transformation and aggregation.
4.1. The OrderBy() method.
The OrderBy() method is one of the fundamental LINQ standard query operators used to sort elements in a sequence in ascending order based on a specified key. This method is typically applied to collections that implement the IEnumerable<T> interface, such as lists or arrays.
The OrderBy() method takes a lambda expression that defines the sorting key. If no custom key is specified, it sorts based on the natural order of the data type. It returns a new sequence with the elements ordered, without modifying the original collection.
Below is a C# example that demonstrates how OrderBy() works with a list of integers:

using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        List<int> listOfNumbers = new List<int> { 6, 5, 4, 3, 7, 8, 9, 1, 2 };

        Console.WriteLine(/* Output */ "Before:");
        foreach (var item in listOfNumbers)
        {
            Console.Write(item + " ");
        }

        Console.WriteLine(/* Output */ );

        var sortedNumbers = listOfNumbers.OrderBy(num => num);

        Console.WriteLine(/* Output */ "After:");
        foreach (var item in sortedNumbers)
        {
            Console.Write(item + " ");
        }
    }
}
Output:

4.2. The Any() method.
The Any() method is a LINQ standard query operator that checks whether a sequence contains any elements. It returns a boolean value: true if the sequence has at least one element, and false if the sequence is empty. This method is particularly useful for validating collections before performing operations that require the presence of elements, helping avoid runtime exceptions such as NullReferenceException.
The Any() method can also be used with a predicate to determine whether any elements in the collection satisfy a specific condition. However, in its simplest form, it's used to check for the presence of any elements at all.
Here’s a simple example using Any() in C#:
using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    static void Main()
    {
        List<int> listOfNumbers = new List<int> { 6, 5, 4, 3, 7, 8, 9, 1, 2 };

        bool hasElements = listOfNumbers.Any();

        Console.WriteLine(/* Output */ "The list " + (hasElements ? "is not" : "is") + " empty.");
    }
}
Output:

Explanation:
In this example, Any() checks if listOfNumbers contains any items. Since it does, the output confirms the list is not empty. If the list had no elements, the output would be: "The list is empty."
4.3. Case Studies
Case Study 1: Filtering Students Based on Random Grades
Scenario: In this case study, we randomly generate a list of students with grades ranging from 0 to 100. We will use LINQ to filter students based on whether they passed (grade >= 50) or failed (grade < 50).
Example Code:
using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    class Student
    {
        public string Name { get; set; }
        public int Grade { get; set; }
    }

    static void Main()
    {
        Random rand = new Random();
        List<Student> students = new List<Student>
        {
            new Student { Name = "Alice", Grade = rand.Next(0, 101) },
            new Student { Name = "Bob", Grade = rand.Next(0, 101) },
            new Student { Name = "Charlie", Grade = rand.Next(0, 101) },
            new Student { Name = "David", Grade = rand.Next(0, 101) },
            new Student { Name = "Eva", Grade = rand.Next(0, 101) }
        };

        var passedStudents = students.Where(s => s.Grade >= 50).ToList();
        var failedStudents = students.Where(s => s.Grade < 50).ToList();

        Console.WriteLine(/* Output */ "Passed Students:");
        foreach (var student in passedStudents)
        {
            Console.WriteLine(/* Output */ $"{student.Name} - {student.Grade}");
        }

        Console.WriteLine(/* Output */ "\nFailed Students:");
        foreach (var student in failedStudents)
        {
            Console.WriteLine(/* Output */ $"{student.Name} - {student.Grade}");
        }
    }
}
Example Output (with random grades):
Passed Students:
Alice - 72
Charlie - 85
Eva - 61

Failed Students:
Bob - 35
David - 48
Explanation: In this case, the students' grades are randomly generated between 0 and 100. LINQ is used to filter and categorize students into "passed" and "failed" based on a passing grade of 50.

Case Study 2: Sorting Products by Random Price
Scenario: Here, we simulate an e-commerce application where we generate random product prices and sort them in ascending order using LINQ.
Example Code:
using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    class Product
    {
        public string Name { get; set; }
        public decimal Price { get; set; }
    }

    static void Main()
    {
        Random rand = new Random();
        List<Product> products = new List<Product>
        {
            new Product { Name = "Laptop", Price = (decimal)(rand.NextDouble() * (2000 - 500) + 500) }, 
            new Product { Name = "Smartphone", Price = (decimal)(rand.NextDouble() * (1000 - 100) + 100) },
            new Product { Name = "Headphones", Price = (decimal)(rand.NextDouble() * (300 - 20) + 20) },
            new Product { Name = "Tablet", Price = (decimal)(rand.NextDouble() * (600 - 150) + 150) },
            new Product { Name = "Smartwatch", Price = (decimal)(rand.NextDouble() * (500 - 50) + 50) }
        };

        var sortedProducts = products.OrderBy(p => p.Price).ToList();  // Ascending order

        Console.WriteLine(/* Output */ "Products Sorted by Price (Ascending):");
        foreach (var product in sortedProducts)
        {
            Console.WriteLine(/* Output */ $"{product.Name}: ${product.Price:F2}");
        }
    }
}
Example Output (with random prices):
Products Sorted by Price (Ascending):
Headphones: $98.42
Smartwatch: $143.73
Tablet: $389.52
Smartphone: $695.31
Laptop: $1421.47
Explanation: We generate random product prices within specified ranges. Then, LINQ's OrderBy() method is used to sort the products in ascending order based on their price.

Case Study 3: Grouping Customers by Region with Random Data
Scenario: For this case study, we simulate customers with random regions. We will then use LINQ to group customers by region.
Example Code:
using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    class Customer
    {
        public string Name { get; set; }
        public string Region { get; set; }
    }

    static void Main()
    {
        Random rand = new Random();
        List<string> regions = new List<string> { "North", "South", "East", "West" };

        List<Customer> customers = new List<Customer>
        {
            new Customer { Name = "John", Region = regions[rand.Next(regions.Count)] },
            new Customer { Name = "Sara", Region = regions[rand.Next(regions.Count)] },
            new Customer { Name = "Mike", Region = regions[rand.Next(regions.Count)] },
            new Customer { Name = "Anna", Region = regions[rand.Next(regions.Count)] },
            new Customer { Name = "David", Region = regions[rand.Next(regions.Count)] },
            new Customer { Name = "Linda", Region = regions[rand.Next(regions.Count)] }
        };

        var groupedCustomers = customers.GroupBy(c => c.Region).ToList();

        Console.WriteLine(/* Output */ "Customers Grouped by Region:");
        foreach (var group in groupedCustomers)
        {
            Console.WriteLine(/* Output */ $"Region: {group.Key}");
            foreach (var customer in group)
            {
                Console.WriteLine(/* Output */ $"- {customer.Name}");
            }
            Console.WriteLine(/* Output */ );
        }
    }
}
Example Output (with random regions):
Customers Grouped by Region:
Region: East
- Mike

Region: South
- Sara
- Linda

Region: West
- David

Region: North
- John
- Anna
Explanation: Here, we randomly assign a region to each customer from a predefined list (North, South, East, West). LINQ's GroupBy() method is then used to group the customers by their region.
4.4. WEEKLY ACTIVITY
Scenario Question:
Scenario: You are working for an e-commerce company that needs to analyze the sales data for the past month. The company wants to know the following:
	•	The total number of products sold in each category.
	•	The total sales revenue for each category.
	•	The most expensive product in each category.
The product sales data is stored in a list of Product objects with the following properties:
	•	ProductName (string) - the name of the product
	•	Category (string) - the category the product belongs to (e.g., "Electronics", "Clothing", etc.)
	•	Price (decimal) - the price of the product
	•	QuantitySold (int) - the number of units sold in the last month
Question: Write a LINQ query to solve this scenario and display the total number of products sold, total sales revenue, and the most expensive product in each category.
Solution:
C# Code:
using System;
using System.Collections.Generic;
using System.Linq;

class MainProgram
{
    class Product
    {
        public string ProductName { get; set; }
        public string Category { get; set; }
        public decimal Price { get; set; }
        public int QuantitySold { get; set; }
    }

    static void Main()
    {
        // Sample data
        List<Product> products = new List<Product>
        {
            new Product { ProductName = "Laptop", Category = "Electronics", Price = 899.99m, QuantitySold = 50 },
            new Product { ProductName = "Smartphone", Category = "Electronics", Price = 499.99m, QuantitySold = 120 },
            new Product { ProductName = "Headphones", Category = "Electronics", Price = 79.99m, QuantitySold = 200 },
            new Product { ProductName = "T-shirt", Category = "Clothing", Price = 19.99m, QuantitySold = 300 },
            new Product { ProductName = "Jeans", Category = "Clothing", Price = 39.99m, QuantitySold = 150 },
            new Product { ProductName = "Jacket", Category = "Clothing", Price = 59.99m, QuantitySold = 100 },
            new Product { ProductName = "Washing Machine", Category = "Appliances", Price = 499.99m, QuantitySold = 30 },
            new Product { ProductName = "Refrigerator", Category = "Appliances", Price = 799.99m, QuantitySold = 45 }
        };

        var categoryStats = from p in products
                            group p by p.Category into categoryGroup
                            select new
                            {
                                Category = categoryGroup.Key,
                                TotalProductsSold = categoryGroup.Sum(p => p.QuantitySold),
                                TotalRevenue = categoryGroup.Sum(p => p.Price * p.QuantitySold),
                                MostExpensiveProduct = categoryGroup.OrderByDescending(p => p.Price).First().ProductName
                            };

        // Display results
        foreach (var category in categoryStats)
        {
            Console.WriteLine(/* Output */ $"Category: {category.Category}");
            Console.WriteLine(/* Output */ $"Total Products Sold: {category.TotalProductsSold}");
            Console.WriteLine(/* Output */ $"Total Sales Revenue: ${category.TotalRevenue:F2}");
            Console.WriteLine(/* Output */ $"Most Expensive Product: {category.MostExpensiveProduct}");
            Console.WriteLine(/* Output */ );
        }
    }
}
Explanation:
	•	Data Structure: We have a Product class representing each product with properties for product name, category, price, and quantity sold.
	•	LINQ Query: The LINQ query uses the group by clause to group products by their category. For each group (i.e., category), we calculate:
	•	The total number of products sold using Sum(p => p.QuantitySold).
	•	The total revenue for that category using Sum(p => p.Price * p.QuantitySold).
	•	The most expensive product in the category using OrderByDescending(p => p.Price).First() to find the product with the highest price.
	•	Output: The results are displayed for each category, showing the total products sold, total sales revenue, and the most expensive product in the category.

Example Output:
Category: Electronics
Total Products Sold: 470
Total Sales Revenue: $179599.00
Most Expensive Product: Laptop

Category: Clothing
Total Products Sold: 550
Total Sales Revenue: $21945.00
Most Expensive Product: Jacket

Category: Appliances
Total Products Sold: 75
Total Sales Revenue: $9374.00
Most Expensive Product: Refrigerator


	•	2. Introduction to Generics
	•	3. Generic Methods
	•	4. Generic Classes
	•	5. Generic Interfaces
	•	6. Constraints on Generics
	•	11. References
