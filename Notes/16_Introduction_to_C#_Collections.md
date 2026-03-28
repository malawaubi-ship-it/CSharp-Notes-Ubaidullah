# Module 16: Introduction to C# Collections

1. Learning outcomes

By the end of this lesson, you should be able to:
	•	Understand C# collections

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469
Chapter 9 & 21
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Introduction to C# Collections
Introduction to C# Collections
Explanation: C# collections are objects that hold multiple items of data. They are part of the .NET framework, providing various ways to store, access, and manage groups of related data. Collections are much more flexible and efficient than arrays. The most common collections are provided under two namespaces:
	•	System.Collections (non-generic collections like ArrayList, Hashtable).
	•	System.Collections.Generic (generic collections like List<T>, Dictionary<TKey, TValue>, Queue<T>, Stack<T>).
Generic collections offer type safety, which means you can specify the type of elements the collection will hold, making the code easier to maintain and reducing the possibility of runtime errors.
Play Video
 

3. List (Generic List)
List<T> (Generic List)
Explanation: A List<T> is a dynamic array that can store any data type. It automatically resizes as elements are added or removed. Lists provide indexed access to elements, allowing easy iteration and modification. It’s the most commonly used collection when you need to manage a collection of items with flexibility and speed.

Example 1: Adding Elements to a List
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        List<int> numArray = new List<int>();
        numArray.Add(10);
        numArray.Add(20);
        numArray.Add(30);
 
        foreach (var number in numArray)
        {
            Console.WriteLine(/* Output */ number);
        }
    }
}
Output:
10
20
30

Example 2: Inserting and Removing Elements in a List
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        List<string> fruits = new List<string> { "Apple", "Banana", "Orange" };
        fruits.Insert(1, "Mango");  // Insert "Mango" at index 1
        fruits.Remove("Banana");  // Remove "Banana"
 
        foreach (var fruit in fruits)
        {
            Console.WriteLine(/* Output */ fruit);
        }
    }
}
Output:
Apple
Mango
Orange
 
4. Dictionary
Dictionary<TKey, TValue>
Explanation: A Dictionary<TKey, TValue> is a collection that stores key-value pairs. It allows for fast lookups, retrieval, and management of data based on a unique key. The dictionary is useful when you need to quickly access data by a unique identifier (e.g., retrieving a student’s name using their student ID). It provides O(1) complexity for lookups.

Example 1: Using Dictionary to Store Key-Value Pairs
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        Dictionary<int, string> employees = new Dictionary<int, string>
        {
            { 101, "John" },
            { 102, "Mary" },
            { 103, "Peter" }
        };
 
        Console.WriteLine(/* Output */ "Employee with ID 102: " + employees[102]);
    }
}
Output:
Employee with ID 102: Mary

Example 2: Iterating Over a Dictionary
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        Dictionary<int, string> products = new Dictionary<int, string>
        {
            { 1, "Laptop" },
            { 2, "Smartphone" },
            { 3, "Tablet" }
        };
 
        foreach (var product in products)
        {
            Console.WriteLine(/* Output */ $"Product ID: {product.Key}, Product Name: {product.Value}");
        }
    }
}
Output:
Product ID: 1, Product Name: Laptop
Product ID: 2, Product Name: Smartphone
Product ID: 3, Product Name: Tablet

 
5. Queue
Queue<T>
Explanation: A Queue<T> is a collection that follows the First-In, First-Out (FIFO) principle. It is useful for managing tasks, like processing print jobs, where the first item added is the first one to be processed. It supports operations like enqueue (adding an element) and dequeue (removing an element).

Example 1: Enqueue and Dequeue Operations
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        Queue<string> tasks = new Queue<string>();
        tasks.Enqueue("Task1");
        tasks.Enqueue("Task2");
        tasks.Enqueue("Task3");
 
        Console.WriteLine(/* Output */ "Processing: " + tasks.Dequeue()); // Dequeues Task1
        Console.WriteLine(/* Output */ "Processing: " + tasks.Dequeue()); // Dequeues Task2
    }
}
Output:
Processing: Task1
Processing: Task2

Example 2: Iterating Through a Queue
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        Queue<int> numbersQueue = new Queue<int>();
        numbersQueue.Enqueue(5);
        numbersQueue.Enqueue(10);
        numbersQueue.Enqueue(15);
 
        Console.WriteLine(/* Output */ "Items in queue:");
        foreach (var number in numbersQueue)
        {
            Console.WriteLine(/* Output */ number);
        }
    }
}
Output:
Items in queue:
5
10
15
 
6. Stack
Stack<T>
Explanation: A Stack<T> is a collection that follows the Last-In, First-Out (LIFO) principle. The last element added to the stack is the first one to be removed. It’s often used in scenarios like undo operations, where the most recent action needs to be reversed first.

Example 1: Pushing and Popping Elements from a Stack
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        Stack<string> history = new Stack<string>();
        history.Push("Page 1");
        history.Push("Page 2");
        history.Push("Page 3");
 
        Console.WriteLine(/* Output */ "Back in history: " + history.Pop());  // Pops "Page 3"
        Console.WriteLine(/* Output */ "Back in history: " + history.Pop());  // Pops "Page 2"
    }
}
Output:
Back in history: Page 3
Back in history: Page 2

Example 2: Checking the Top Element Without Removing It
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        Stack<int> numberStack = new Stack<int>();
        numberStack.Push(1);
        numberStack.Push(2);
        numberStack.Push(3);
 
        Console.WriteLine(/* Output */ "Top element is: " + numberStack.Peek());  // Peek doesn't remove it
    }
}
Output:
Top element is: 3
 
7. HashSet
HashSet<T>
Explanation: A HashSet<T> is a collection that stores unique elements without maintaining any specific order. It is useful for scenarios where you need to check if an item exists in the collection without worrying about duplicates. The HashSet is optimized for fast lookups.

Example 1: Adding and Checking for Duplicates
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        HashSet<string> uniqueItems = new HashSet<string>();
        uniqueItems.Add("Apple");
        uniqueItems.Add("Banana");
        uniqueItems.Add("Apple");  // Duplicate, will not be added
 
        Console.WriteLine(/* Output */ "Total unique items: " + uniqueItems.Count);
    }
}
Output:
Total unique items: 2

Example 2: Performing Set Operations (Union)
using System;
using System.Collections.Generic;
 
class MainProgram
{
    static void Main()
    {
        HashSet<int> set1 = new HashSet<int> { 1, 2, 3 };
        HashSet<int> set2 = new HashSet<int> { 3, 4, 5 };
 
        set1.UnionWith(set2);  // Union operation
 
        Console.WriteLine(/* Output */ "Union of sets:");
        foreach (var item in set1)
        {
            Console.WriteLine(/* Output */ item);
        }
    }
}
Output:
Union of sets:
1
2
3
4
5
 
 
8. Case Study 1: Student Record Management System
Case Study 1: Student Record Management System
Problem:
You are tasked with creating a student record management system for a school, where each student has a unique student ID, name, and grade. The system should:
	•	Store student records (ID, name, and grade).
	•	Provide functionalities to:
	•	Add a new student.
	•	Remove a student by ID.
	•	Retrieve a student's details by their ID.
	•	Retrieve a list of students with grades above a certain threshold.
You must use the appropriate collections to achieve this functionality.

Solution:
To implement the student record management system, we will use a Dictionary<int, Tuple<string, double>>:
	•	The key will be the student ID (an int).
	•	The value will be a Tuple<string, double>, where:
	•	The first item is the student’s name (a string).
	•	The second item is the student’s grade (a double).
Code:
using System;
using System.Collections.Generic;
 
class StudentRecordSystem
{
    static void Main()
    {
        // Initialize the dictionary to store student records
        Dictionary<int, Tuple<string, double>> studentRecords = new Dictionary<int, Tuple<string, double>>();
 
        // Add students
        studentRecords.Add(101, new Tuple<string, double>("John", 85.5));
        studentRecords.Add(102, new Tuple<string, double>("Mary", 92.3));
        studentRecords.Add(103, new Tuple<string, double>("Alice", 78.4));
 
        // Retrieve a student by ID
        int searchId = 102;
        if (studentRecords.ContainsKey(searchId))
        {
            var student = studentRecords[searchId];
            Console.WriteLine(/* Output */ $"Student ID: {searchId}, Name: {student.Item1}, Grade: {student.Item2}");
        }
 
        // Remove a student by ID
        int removeId = 103;
        if (studentRecords.ContainsKey(removeId))
        {
            studentRecords.Remove(removeId);
            Console.WriteLine(/* Output */ $"Student with ID {removeId} has been removed.");
        }
 
        // Retrieve students with grades above 80
        Console.WriteLine(/* Output */ "Students with grade above 80:");
        foreach (var record in studentRecords)
        {
            if (record.Value.Item2 > 80)
            {
                Console.WriteLine(/* Output */ $"ID: {record.Key}, Name: {record.Value.Item1}, Grade: {record.Value.Item2}");
            }
        }
    }
}
Output:
Student ID: 102, Name: Mary, Grade: 92.3
Student with ID 103 has been removed.
Students with grade above 80:
ID: 101, Name: John, Grade: 85.5
ID: 102, Name: Mary, Grade: 92.3
 
9. Case Study 2: Student Grades Tracker
Case Study 2: Student Grades Tracker
Problem:
You want to store and retrieve a list of students with their test scores.
Solution:
Use a Dictionary<string, List<int>> to map student names to their list of scores.
Code:
using System;
using System.Collections.Generic;
 
class StudentGrades
{
    static void Main()
    {
        Dictionary<string, List<int>> studentGrades = new Dictionary<string, List<int>>();
 
        // Add student scores
        studentGrades["Alice"] = new List<int> { 85, 90, 78 };
        studentGrades["Bob"] = new List<int> { 70, 88, 95 };
 
        // Print average grades
        foreach (var student in studentGrades)
        {
            double average = (double)student.Value.Sum() / student.Value.Count;
            Console.WriteLine(/* Output */ $"{student.Key}'s average score: {average:F2}");
        }
    }
}
Sample Output:
Alice's average score: 84.33
Bob's average score: 84.33

 
10. Case Study 3: Online Shopping Cart
Case Study 3: Online Shopping Cart
Problem:
Build a shopping cart system where users can add items and view the total cost.
Solution:
Use a Dictionary<string, int> to store item quantities and a Dictionary<string, double> for item prices.
Code:
using System;
using System.Collections.Generic;
 
class ShoppingCart
{
    static void Main()
    {
        Dictionary<string, double> prices = new Dictionary<string, double>
        {
            { "Laptop", 999.99 },
            { "Mouse", 25.50 },
            { "Keyboard", 45.75 }
        };
 
        Dictionary<string, int> cart = new Dictionary<string, int>();
 
        // Add items to cart
        AddToCart(cart, "Laptop");
        AddToCart(cart, "Mouse");
        AddToCart(cart, "Mouse"); // Adding second mouse
 
        // Display cart and total
        double total = 0;
        Console.WriteLine(/* Output */ "Cart Summary:");
        foreach (var item in cart)
        {
            double subtotal = prices[item.Key] * item.Value;
            Console.WriteLine(/* Output */ $"{item.Key} x {item.Value} = ${subtotal:F2}");
            total += subtotal;
        }
 
        Console.WriteLine(/* Output */ $"Total: ${total:F2}");
    }
 
    static void AddToCart(Dictionary<string, int> cart, string item)
    {
        if (cart.ContainsKey(item))
            cart[item]++;
        else
            cart[item] = 1;
    }
}
Sample Output:
Cart Summary:
Laptop x 1 = $999.99
Mouse x 2 = $51.00
Total: $1050.99
  
11. Case Study 4: Call Center Queue
🧠 Case Study 4: Call Center Queue
Problem:
Handle a queue of customer support calls in the order they arrive.
Solution:
Use a Queue<string> to represent the call order.
Code:
using System;
using System.Collections.Generic;
 
class CallCenter
{
    static void Main()
    {
        Queue<string> callQueue = new Queue<string>();
 
        callQueue.Enqueue("Alice");
        callQueue.Enqueue("Bob");
        callQueue.Enqueue("Charlie");
 
        Console.WriteLine(/* Output */ $"Now serving: {callQueue.Dequeue()}");
 
        Console.WriteLine(/* Output */ "Pending calls:");
        foreach (var caller in callQueue)
        {
            Console.WriteLine(/* Output */ caller);
        }
    }
}
Sample Output:
Now serving: Alice
Pending calls:
Bob
Charlie
 
12. Case Study 5: Recently Opened Documents
Case Study 5: Recently Opened Documents
Problem:
Track the most recently opened files in a text editor (most recent first, no duplicates).
Solution:
Use a Stack<string> for ordering, and a HashSet<string> to prevent duplicates.
Code:
using System;
using System.Collections.Generic;
 
class RecentFiles
{
    static void Main()
    {
        Stack<string> recentFiles = new Stack<string>();
        HashSet<string> fileSet = new HashSet<string>();
 
        OpenFile(recentFiles, fileSet, "Doc1.txt");
        OpenFile(recentFiles, fileSet, "Doc2.txt");
        OpenFile(recentFiles, fileSet, "Doc1.txt"); // Reopens Doc1.txt
 
        Console.WriteLine(/* Output */ "Recently Opened Files:");
        foreach (var file in recentFiles)
        {
            Console.WriteLine(/* Output */ file);
        }
    }
 
    static void OpenFile(Stack<string> stack, HashSet<string> set, string fileName)
    {
        if (set.Contains(fileName))
        {
            var tempStack = new Stack<string>();
            while (stack.Peek() != fileName)
                tempStack.Push(stack.Pop());
            stack.Pop(); // Remove old instance
            while (tempStack.Count > 0)
                stack.Push(tempStack.Pop());
        }
 
        stack.Push(fileName);
        set.Add(fileName);
    }
}
Sample Output:
Recently Opened Files:
Doc1.txt
Doc2.txt
 
13. Case Study 5: Library Book Borrowing System
Case Study 5: Library Book Borrowing System
Problem:
Track which books are borrowed by which members.
Solution:
Use:
	•	Dictionary<int, string> for BookID → Title
	•	Dictionary<int, List<int>> for MemberID → List of borrowed BookIDs
Code:
using System;
using System.Collections.Generic;
 
class LibrarySystem
{
    static void Main()
    {
        Dictionary<int, string> books = new Dictionary<int, string>
        {
            { 1, "1984" },
            { 2, "To Kill a Mockingbird" },
            { 3, "The Hobbit" }
        };
 
        Dictionary<int, List<int>> memberLoans = new Dictionary<int, List<int>>();
 
        BorrowBook(memberLoans, 1001, 1); // 1984
        BorrowBook(memberLoans, 1001, 2); // Mockingbird
        BorrowBook(memberLoans, 1002, 3); // Hobbit
 
        ReturnBook(memberLoans, 1001, 1); // Return 1984
 
        Console.WriteLine(/* Output */ "Books borrowed by Member 1001:");
        foreach (int bookId in memberLoans[1001])
        {
            Console.WriteLine(/* Output */ books[bookId]);
        }
    }
 
    static void BorrowBook(Dictionary<int, List<int>> loans, int memberId, int bookId)
    {
        if (!loans.ContainsKey(memberId))
            loans[memberId] = new List<int>();
        loans[memberId].Add(bookId);
    }
 
    static void ReturnBook(Dictionary<int, List<int>> loans, int memberId, int bookId)
    {
        if (loans.ContainsKey(memberId))
            loans[memberId].Remove(bookId);
    }
}
Sample Output:
Books borrowed by Member 1001:
To Kill a Mockingbird
 
14. Scenario Question: Inventory Management System
Scenario Question: Inventory Management System
Problem:
You are developing an inventory management system for a small warehouse. The system needs to:
	•	Track products in the inventory, where each product has:
	•	Product ID (unique identifier)
	•	Product Name
	•	Quantity Available
	•	Price per unit
	•	Provide functionalities to:
	•	Add a new product.
	•	Update the quantity of a product (when stock is updated or items are sold).
	•	Retrieve the details of a product by its ID.
	•	Retrieve a list of products with low stock (e.g., stock less than 10 items).
	•	Calculate the total value of all products in the inventory (Quantity × Price).
You need to implement a system using C# collections that efficiently manages these tasks.

Solution:
For this scenario, we can use a Dictionary<int, Product>:
	•	Key: The Product ID (integer).
	•	Value: The Product object, which contains:
	•	ProductName (string)
	•	QuantityAvailable (integer)
	•	PricePerUnit (double)
We will also implement methods for the various functionalities.

Code:
using System;
using System.Collections.Generic;
 
class InventoryManagementSystem
{
    // Define the Product class
    class Product
    {
        public string ProductName { get; set; }
        public int QuantityAvailable { get; set; }
        public double PricePerUnit { get; set; }
 
        // Constructor
        public Product(string productName, int quantityAvailable, double pricePerUnit)
        {
            ProductName = productName;
            QuantityAvailable = quantityAvailable;
            PricePerUnit = pricePerUnit;
        }
 
        // Method to calculate the total value of the product's stock
        public double TotalValue()
        {
            return QuantityAvailable * PricePerUnit;
        }
    }
 
    static void Main()
    {
        // Initialize the dictionary to store products
        Dictionary<int, Product> inventory = new Dictionary<int, Product>();
 
        // Add new products to the inventory
        inventory.Add(101, new Product("Laptop", 20, 800.00));
        inventory.Add(102, new Product("Smartphone", 50, 500.00));
        inventory.Add(103, new Product("Tablet", 5, 300.00));
 
        // Update the quantity of a product
        UpdateProductQuantity(inventory, 102, 60);  // Add 10 more smartphones to stock
        UpdateProductQuantity(inventory, 103, 2);   // Add 2 more tablets to stock
 
        // Retrieve and display product details by product ID
        Console.WriteLine(/* Output */ "Product Details for ID 102:");
        PrintProductDetails(inventory, 102);
 
        // Display all products with low stock (less than 10 items)
        Console.WriteLine(/* Output */ "\nProducts with low stock (less than 10):");
        DisplayLowStockProducts(inventory, 10);
 
        // Calculate and display the total value of all products in the inventory
        double totalInventoryValue = CalculateTotalInventoryValue(inventory);
        Console.WriteLine(/* Output */ $"\nTotal Inventory Value: ${totalInventoryValue}");
    }
 
    // Method to update the quantity of a product
    static void UpdateProductQuantity(Dictionary<int, Product> inventory, int productId, int quantityChange)
    {
        if (inventory.ContainsKey(productId))
        {
            inventory[productId].QuantityAvailable += quantityChange;
            Console.WriteLine(/* Output */ $"Updated Product ID {productId}: New Quantity = {inventory[productId].QuantityAvailable}");
        }
        else
        {
            Console.WriteLine(/* Output */ "Product ID not found.");
        }
    }
 
    // Method to print product details by product ID
    static void PrintProductDetails(Dictionary<int, Product> inventory, int productId)
    {
        if (inventory.ContainsKey(productId))
        {
            var product = inventory[productId];
            Console.WriteLine(/* Output */ $"Product Name: {product.ProductName}, Quantity Available: {product.QuantityAvailable}, Price per Unit: ${product.PricePerUnit}");
        }
        else
        {
            Console.WriteLine(/* Output */ "Product not found.");
        }
    }
 
    // Method to display products with low stock (less than the threshold)
    static void DisplayLowStockProducts(Dictionary<int, Product> inventory, int threshold)
    {
        foreach (var product in inventory)
        {
            if (product.Value.QuantityAvailable < threshold)
            {
                Console.WriteLine(/* Output */ $"Product ID: {product.Key}, Name: {product.Value.ProductName}, Quantity: {product.Value.QuantityAvailable}");
            }
        }
    }
 
    // Method to calculate the total value of all products in the inventory
    static double CalculateTotalInventoryValue(Dictionary<int, Product> inventory)
    {
        double totalValue = 0;
        foreach (var product in inventory)
        {
            totalValue += product.Value.TotalValue();
        }
        return totalValue;
    }
}

Explanation:
	•	Product Class:
	•	Represents a product in the inventory, with properties for product name, quantity, and price.
	•	The TotalValue method calculates the total value of the product based on its price and available quantity.
	•	Dictionary for Inventory:
	•	The Dictionary<int, Product> holds the inventory where each product is identified by its unique Product ID.
	•	The key is the Product ID, and the value is the Product object.
	•	Adding Products:
	•	Products are added to the dictionary using the Add method, specifying the unique product ID and creating a new Product object.
	•	Updating Product Quantity:
	•	The UpdateProductQuantity method allows updating the quantity of an existing product by providing the Product ID and the change in quantity. It modifies the QuantityAvailable of the corresponding product.
	•	Retrieving Product Details:
	•	The PrintProductDetails method retrieves and prints the details (name, available quantity, price) of a product by its Product ID.
	•	Displaying Low Stock Products:
	•	The DisplayLowStockProducts method filters and displays products with a quantity below the specified threshold (in this case, 10).
	•	Calculating Total Inventory Value:
	•	The CalculateTotalInventoryValue method calculates the total value of all products in the inventory by summing the TotalValue of each product.

Output:
Updated Product ID 102: New Quantity = 60
Updated Product ID 103: New Quantity = 7
Product Details for ID 102:
Product Name: Smartphone, Quantity Available: 60, Price per Unit: $500
 
Products with low stock (less than 10):
Product ID: 103, Name: Tablet, Quantity: 7
 
Total Inventory Value: $57000

Key Concepts Demonstrated:
	•	Dictionary: Used to map product IDs to their respective Product objects.
	•	Product Class: Encapsulates the data and logic related to products.
	•	Inventory Operations: Includes adding products, updating quantities, retrieving details, filtering based on stock levels, and calculating total inventory value.
 
15. References
Deitel, H. and Deitel, P., 2017. C# for Programmers. 6th ed. Pearson Education, Inc.
Nakov, P., Petrov, P., and Ivanov, K., 2016. Beginning C# Programming. 1st ed. Apress.
Microsoft, 2021. C# Programming Guide. [online] Available at: https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/ [Accessed 11 April 2025].
Jones, M., 2018. Mastering C# Collections. Packt Publishing.


	•	2. Concurrency in C# - Multithreading and Parallelism
	•	3. Implementing Multithreading in C#
	•	9. Concept Overview
	•	10. Video
	•	11. Scenario 1: Concurrency in Processing Orders in an E-Commerce System
	•	12. References
