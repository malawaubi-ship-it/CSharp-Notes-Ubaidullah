# Module 15: Introduction to Generics

## 1. Learning outcomes

By the end of this lesson, you should be able to:
	-	Understand C# collections

Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 
Chapter 9, 20 & 21




## 2. Introduction to Generics
Generics in C# allow you to create classes, methods, and data structures that work with any data type while ensuring compile-time type safety. They prevent the need to write duplicate code and help reduce runtime errors. For instance, instead of writing separate versions of a function for integers, strings, etc., generics let you write one version that works with all data types.
Play Video
 
Example 1: Using a generic method to display any type
public class DisplayUtility
{
    public static void Show<T>(T value)
    {
        Console.WriteLine( $"Value: {value}");
    }
}
 
class MainProgram
{
    static void Main()
    {
        DisplayUtility.Show(123);
        DisplayUtility.Show("Hello Generics");
    }
}
Output:
Value: 123  
Value: Hello Generics
Example 2: Using generics to avoid boxing
List<int> numArray = new List<int> { 1, 2, 3 };
foreach (int n in numArray)
{
    Console.WriteLine( n); // No boxing/unboxing needed
}
Output:
1  
2  
3


## 3. Generic Methods
Generic Methods
Generic methods allow developers to write flexible and reusable code without compromising type safety. The type parameter (<T>) is defined in the method signature and replaced at compile time when the method is called.
Example 1: Swapping two variables using a generic method
public static void Swap<T>(ref T a, ref T b)
{
    T tempVal = a;
    a = b;
    b = tempVal;
}
 
class MainProgram
{
    static void Main()
    {
        int x = 5, y = 10;
        Swap(ref x, ref y);
        Console.WriteLine( $"x = {x}, y = {y}");
    }
}
Output:
x = 10, y = 5
Example 2: Comparing two values
public static bool AreEqual<T>(T a, T b)
{
    return a.Equals(b);
}
 
class MainProgram
{
    static void Main()
    {
        Console.WriteLine( AreEqual(5, 5));
        Console.WriteLine( AreEqual("apple", "banana"));
    }
}
Output:
True  
False
## 4. Generic Classes
Generic Classes
A generic class allows defining a blueprint for a class that can operate on any data type. This helps build reusable components like containers, wrappers, or repositories.
Example 1: Generic Box class
public class Box<T>
{
    public T Content { get; set; }
}
 
class MainProgram
{
    static void Main()
    {
        Box<int> intBox = new Box<int> { Content = 42 };
        Box<string> strBox = new Box<string> { Content = "Books" };
 
        Console.WriteLine( intBox.Content);
        Console.WriteLine( strBox.Content);
    }
}
Output:
42  
Books
Example 2: Generic Pair class
public class Pair<T1, T2>
{
    public T1 First { get; set; }
    public T2 Second { get; set; }
}
 
class MainProgram
{
    static void Main()
    {
        Pair<int, string> student = new Pair<int, string> { First = 101, Second = "Alice" };
        Console.WriteLine( $"ID: {student.First}, Name: {student.Second}");
    }
}
Output:
ID: 101, Name: Alice


## 5. Generic Interfaces
Generic Interfaces
Generic interfaces define a contract for operations that work on data of various types. Interfaces like IComparable<T> or IEnumerable<T> allow flexible, reusable implementations for comparison or iteration.
Example 1: Implementing IComparable<T>
public class Product : IComparable<Product>
{
    public string Name { get; set; }
 
    public int CompareTo(Product other)
    {
        return Name.CompareTo(other.Name);
    }
}
 
class MainProgram
{
    static void Main()
    {
        Product p1 = new Product { Name = "Apple" };
        Product p2 = new Product { Name = "Banana" };
 
        Console.WriteLine( p1.CompareTo(p2)); // Output depends on alphabetical order
    }
}
Output:
-1
Example 2: Custom collection implementing IEnumerable<T>
public class SimpleList<T> : IEnumerable<T>
{
    private List<T> _items = new List<T>();
 
    public void Add(T item) => _items.Add(item);
 
    public IEnumerator<T> GetEnumerator() => _items.GetEnumerator();
 
    IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();
}
 
class MainProgram
{
    static void Main()
    {
        var list = new SimpleList<int>();
        list.Add(1); list.Add(2); list.Add(3);
 
        foreach (var item in list)
            Console.WriteLine( item);
    }
}
Output:
1  
2  
3


## 6. Constraints on Generics
Constraints on Generics
Constraints provide control over the types that can be used as arguments for type parameters. They enable developers to use certain operations (e.g., object creation) that would otherwise be disallowed.
Example 1: Using new() constraint
public class Factory<T> where T : new()
{
    public T CreateInstance()
    {
        return new T();
    }
}
 
class Sample
{
    public string Text = "Created";
}
 
class MainProgram
{
    static void Main()
    {
        var factory = new Factory<Sample>();
        var instance = factory.CreateInstance();
        Console.WriteLine( instance.Text);
    }
}
Output:
Created
Example 2: Using class constraint
public class ReferenceHandler<T> where T : class
{
    public void PrintTypeName()
    {
        Console.WriteLine( typeof(T).Name);
    }
}
 
class MainProgram
{
    static void Main()
    {
        var handler = new ReferenceHandler<string>();
        handler.PrintTypeName();
    }
}
Output:
String


## 7. Case Study 1: Student Grade Management System
Case Study 1: Student Grade Management System
Problem Statement:
A university wants a system to manage student records and their corresponding grades. The system should:
	-	Store student data in a generic way.
	-	Use a dictionary to store student IDs and their grades.
	-	Calculate average grades and display student results.

Solution Approach:
	-	Create a generic Student<T> class to store student info (like ID and Name).
	-	Use a Dictionary<int, double> to map student IDs to their grades.
	-	Iterate over the dictionary and calculate the average

using System;
using System.Collections.Generic;
 
public class Student<T>
{
    public T ID { get; set; }
    public string Name { get; set; }
 
    public Student(T id, string name)
    {
        ID = id;
        Name = name;
    }
}
 
class MainProgram
{
    static void Main()
    {
        // Create a list of students
        List<Student<int>> students = new List<Student<int>>
        {
            new Student<int>(1, "Alice"),
            new Student<int>(2, "Bob"),
            new Student<int>(3, "Charlie")
        };
 
        // Store grades
        Dictionary<int, double> grades = new Dictionary<int, double>
        {
            { 1, 85.5 },
            { 2, 78.0 },
            { 3, 92.3 }
        };
 
        double total = 0;
        foreach (var student in students)
        {
            double grade = grades[student.ID];
            Console.WriteLine( $"{student.Name} (ID: {student.ID}) - Grade: {grade}");
            total += grade;
        }
 
        double avg = total / students.Count;
        Console.WriteLine( $"\nAverage Grade: {avg:F2}");
    }
}

Output:
Alice (ID: 1) - Grade: 85.5  
Bob (ID: 2) - Grade: 78  
Charlie (ID: 3) - Grade: 92.3
 
Average Grade: 85.27


## 8. Case Study 2: Task Scheduling System (Using Queue)
Case Study 2: Task Scheduling System (Using Queue<T>)
Problem Statement:
A software project management tool needs a feature to schedule and execute tasks in the order they are added (FIFO). Each task includes a name and an estimated time. The system must:
	-	Store tasks in order.
	-	Process each task in FIFO manner using Queue<T>.

Solution Approach:
	-	Create a generic TaskItem<T> class.
	-	Use Queue<TaskItem<string>> to manage task execution.
	-	Print and simulate execution.

using System;
using System.Collections.Generic;
 
public class TaskItem<T>
{
    public T Name { get; set; }
    public int TimeInMinutes { get; set; }
 
    public TaskItem(T name, int time)
    {
        Name = name;
        TimeInMinutes = time;
    }
}
 
class MainProgram
{
    static void Main()
    {
        Queue<TaskItem<string>> taskQueue = new Queue<TaskItem<string>>();
 
        // Add tasks
        taskQueue.Enqueue(new TaskItem<string>("Compile Code", 10));
        taskQueue.Enqueue(new TaskItem<string>("Run Tests", 20));
        taskQueue.Enqueue(new TaskItem<string>("Deploy Build", 15));
 
        Console.WriteLine( "Processing Tasks:\n");
 
        while (taskQueue.Count > 0)
        {
            var task = taskQueue.Dequeue();
            Console.WriteLine( $"Task: {task.Name}, Estimated Time: {task.TimeInMinutes} mins");
        }
    }
}

Output:
Processing Tasks:
 
Task: Compile Code, Estimated Time: 10 mins  
Task: Run Tests, Estimated Time: 20 mins  
Task: Deploy Build, Estimated Time: 15 mins


## 9. Case Study 3: Inventory Management System for a Retail Store
Case Study 3: Inventory Management System for a Retail Store
Problem Statement:
A retail store needs a system to manage its product inventory. Each product has a unique ID, name, and available quantity. The system should:
	-	Use a generic class to handle product information.
	-	Use a dictionary to store product IDs and their stock quantities.
	-	Allow updates to inventory (restocking or selling).
	-	Display product details and total stock available.

Solution Approach:
	-	Create a Product<T> class that stores the product ID, name, and price.
	-	Use Dictionary<int, int> to map product IDs to their current stock levels.
	-	Iterate through the inventory and display information.

using System;
using System.Collections.Generic;

public class Product<T>
{
    public T ProductID { get; set; }
    public string Name { get; set; }
    public double Price { get; set; }

    public Product(T id, string name, double price)
    {
        ProductID = id;
        Name = name;
        Price = price;
    }
}

class MainProgram
{
    static void Main()
    {
        List<Product<int>> products = new List<Product<int>>
        {
            new Product<int>(101, "Laptop", 899.99),
            new Product<int>(102, "Mouse", 25.50),
            new Product<int>(103, "Keyboard", 45.00)
        };

        Dictionary<int, int> stock = new Dictionary<int, int>
        {
            { 101, 15 },
            { 102, 50 },
            { 103, 30 }
        };

        int totalStock = 0;
        foreach (var item in products)
        {
            int quantity = stock[item.ProductID];
            Console.WriteLine( $"{item.Name} (ID: {item.ProductID}) - Stock: {quantity}, Price: R{item.Price:F2}");
            totalStock += quantity;
        }

        Console.WriteLine( $"\nTotal Items in Inventory: {totalStock}");
    }
}
Output:
Laptop (ID: 101) - Stock: 15, Price: R899.99  
Mouse (ID: 102) - Stock: 50, Price: R25.50  
Keyboard (ID: 103) - Stock: 30, Price: R45.00  

Total Items in Inventory: 95


## 10. Case Study 4: Library Book Loan Management System
Case Study 4: Library Book Loan Management System
Problem Statement:
A library wants to track the borrowing of books by students. Each student can borrow multiple books. The system should:
	-	Use a generic class to store student details.
	-	Use a dictionary to map student IDs to lists of books they've borrowed.
	-	Display each student's borrowed books.

Solution Approach:
	-	Use a generic Student<T> class to hold student details.
	-	Use a Dictionary<int, List<string>> to map student IDs to book titles.
	-	Display all borrowings per student.

using System;
using System.Collections.Generic;

public class Student<T>
{
    public T ID { get; set; }
    public string Name { get; set; }

    public Student(T id, string name)
    {
        ID = id;
        Name = name;
    }
}

class MainProgram
{
    static void Main()
    {
        List<Student<int>> students = new List<Student<int>>
        {
            new Student<int>(1001, "Palesa"),
            new Student<int>(1002, "Thabiso"),
            new Student<int>(1003, "Naledi")
        };

        Dictionary<int, List<string>> borrowedBooks = new Dictionary<int, List<string>>
        {
            { 1001, new List<string> { "C# Fundamentals", "LINQ in Action" } },
            { 1002, new List<string> { "Database Systems", "Operating Systems" } },
            { 1003, new List<string> { "Algorithms in C#", "Clean Code", "Design Patterns" } }
        };

        foreach (var student in students)
        {
            Console.WriteLine( $"{student.Name} (ID: {student.ID}) has borrowed:");

            foreach (var book in borrowedBooks[student.ID])
            {
                Console.WriteLine( $"  - {book}");
            }
            Console.WriteLine( );
        }
    }
}
Output:
Palesa (ID: 1001) has borrowed:
  - C# Fundamentals
  - LINQ in Action

Thabiso (ID: 1002) has borrowed:
  - Database Systems
  - Operating Systems

Naledi (ID: 1003) has borrowed:
  - Algorithms in C#
  - Clean Code
  - Design Patterns



## 11. References
Deitel, H.M. and Deitel, P.J., 2017. C# How to Program. 6th ed. Boston: Pearson Education.
Microsoft, 2024. Generics in C#. [online] Microsoft Learn. Available at: https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/ [Accessed 11 April 2025].
Albahari, J. and Albahari, B., 2021. C# 10 in a Nutshell: The Definitive Reference. 7th ed. Sebastopol: O’Reilly Media.
Microsoft, 2024. Collections in .NET. [online] Microsoft Learn. Available at: https://learn.microsoft.com/en-us/dotnet/standard/collections/ [Accessed 11 April 2025].
 
	-	2. Introduction to C# Collections
	-	3. List (Generic List)
	-	4. Dictionary
	-	5. Queue
	-	6. Stack
	-	7. HashSet
	-	14. Scenario Question: Inventory Management System
	-	15. References
