Skip to main content
Print book
Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:31 AM
Table of contents
	•	1. Learning outcomes
	•	2. Data structures
	•	3. Case Study 1
	•	4. Case Study 2
	•	5. Case Study 3
1. Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd.

    
Not signed in? Click here and then refresh this page.
2. Data structures
1. Introduction to Data Structures
Data structures are ways of organizing and storing data to perform operations efficiently. They are fundamental in programming and play a crucial role in solving complex computational problems.
Types of Data Structures
	•	Linear Data Structures – Data elements are arranged in a sequential manner.
	•	Arrays
	•	Linked Lists
	•	Stacks
	•	Queues
	•	Non-Linear Data Structures – Data elements are arranged in a hierarchical manner.
	•	Trees
	•	Graphs
2. Arrays
	•	A collection of elements stored in contiguous memory locations.
	•	Elements are accessed using an index.
	•	Advantages: Fast access using an index.
	•	Disadvantages: Fixed size, inserting/removing elements is expensive.
Example in C#:
int[] numArray = new int[5] {1, 2, 3, 4, 5};
Console.WriteLine(/* Output */ numArray[2]); // Output: 3
3. Linked Lists
	•	A sequence of nodes where each node contains data and a reference to the next node.
	•	Advantages: Dynamic size, efficient insertions/deletions.
	•	Disadvantages: More memory usage due to pointers.
Example in C#:
csharp
CopyEdit
public class Node {
    public int Data;
    public Node Next;
    public Node(int data) {
        Data = data;
        Next = null;
    }
}
4. Stacks
	•	A LIFO (Last In, First Out) data structure.
	•	Supports Push (insert) and Pop (remove) operations.
Example in C#:
csharp
CopyEdit
Stack<int> stack = new Stack<int>();
stack.Push(10);
stack.Push(20);
Console.WriteLine(/* Output */ stack.Pop()); // Output: 20
5. Queues
	•	A FIFO (First In, First Out) data structure.
	•	Supports Enqueue (insert) and Dequeue (remove) operations.
Example in C#:
Queue<int> queue = new Queue<int>();
queue.Enqueue(1);
queue.Enqueue(2);
Console.WriteLine(/* Output */ queue.Dequeue()); // Output: 1

Activities with Solutions
Activity 1: Implement a Stack Using an Array
Task: Implement a stack in C# using an array with methods for Push, Pop, and Peek.
Solution:

public class StackArray {
    private int[] stack;
    private int top;
    private int maxSize;
 
    public StackArray(int size) {
        maxSize = size;
        stack = new int[maxSize];
        top = -1;
    }
 
    public void Push(int value) {
        if (top == maxSize - 1) {
            Console.WriteLine(/* Output */ "Stack Overflow");
            return;
        }
        stack[++top] = value;
    }
 
    public int Pop() {
        if (top == -1) {
            Console.WriteLine(/* Output */ "Stack Underflow");
            return -1;
        }
        return stack[top--];
    }
 
    public int Peek() {
        if (top == -1) {
            Console.WriteLine(/* Output */ "Stack is empty");
            return -1;
        }
        return stack[top];
    }
}

Activity 2: Implement a Queue Using a Linked List
Task: Implement a queue in C# using a linked list with methods for Enqueue and Dequeue.
Solution:
public class Node {
    public int Data;
    public Node Next;
    public Node(int data) {
        Data = data;
        Next = null;
    }
}
 
public class QueueLinkedList {
    private Node front;
    private Node rear;
 
    public QueueLinkedList() {
        front = rear = null;
    }
 
    public void Enqueue(int data) {
        Node newNode = new Node(data);
        if (rear == null) {
            front = rear = newNode;
            return;
        }
        rear.Next = newNode;
        rear = newNode;
    }
 
    public int Dequeue() {
        if (front == null) {
            Console.WriteLine(/* Output */ "Queue is empty");
            return -1;
        }
        int value = front.Data;
        front = front.Next;
        if (front == null) rear = null;
        return value;
    }
}
 
 
3. Case Study 1
Case Study 1: Employee Management System (Using Linked List)
Problem Statement:
A company needs a system to manage its employees. The system should allow adding new employees, removing employees by ID, and displaying all employees.
Solution:
We will use a linked list to store employee records dynamically.
C# Implementation:

using System;

public class Employee {
    public int ID;
    public string Name;
    public Employee Next;

    public Employee(int id, string name) {
        ID = id;
        Name = name;
        Next = null;
    }
}

public class EmployeeList {
    private Employee head;

    public void AddEmployee(int id, string name) {
        Employee newEmployee = new Employee(id, name);
        if (head == null) {
            head = newEmployee;
        } else {
            Employee tempVal = head;
            while (tempVal.Next != null) {
                tempVal = tempVal.Next;
            }
            tempVal.Next = newEmployee;
        }
        Console.WriteLine(/* Output */ $"Employee {name} added.");
    }

    public void RemoveEmployee(int id) {
        if (head == null) {
            Console.WriteLine(/* Output */ "Employee list is empty.");
            return;
        }
        if (head.ID == id) {
            head = head.Next;
            Console.WriteLine(/* Output */ $"Employee ID {id} removed.");
            return;
        }
        Employee tempVal = head;
        while (tempVal.Next != null && tempVal.Next.ID != id) {
            tempVal = tempVal.Next;
        }
        if (tempVal.Next == null) {
            Console.WriteLine(/* Output */ "Employee not found.");
        } else {
            tempVal.Next = tempVal.Next.Next;
            Console.WriteLine(/* Output */ $"Employee ID {id} removed.");
        }
    }

    public void DisplayEmployees() {
        if (head == null) {
            Console.WriteLine(/* Output */ "No employees found.");
            return;
        }
        Employee tempVal = head;
        while (tempVal != null) {
            Console.WriteLine(/* Output */ $"ID: {tempVal.ID}, Name: {tempVal.Name}");
            tempVal = tempVal.Next;
        }
    }
}

// Test the system
class MainProgram {
    static void Main() {
        EmployeeList empList = new EmployeeList();
        empList.AddEmployee(101, "Alice");
        empList.AddEmployee(102, "Bob");
        empList.DisplayEmployees();
        empList.RemoveEmployee(101);
        empList.DisplayEmployees();
    }
}
Output:
Employee Alice added.
Employee Bob added.
ID: 101, Name: Alice
ID: 102, Name: Bob
Employee ID 101 removed.
ID: 102, Name: Bob


4. Case Study 2
Case Study 2: Browser Back & Forward Navigation (Using Stack)
Problem Statement:
A web browser needs a mechanism to navigate back and forward through the pages a user visits. Implement a navigation system using stacks.
Solution:
Two stacks are used:
	•	backStack for storing visited pages.
	•	forwardStack for tracking forward navigation.
C# Implementation:
using System;
using System.Collections.Generic;

public class BrowserHistory {
    private Stack<string> backStack = new Stack<string>();
    private Stack<string> forwardStack = new Stack<string>();
    private string currentPage = "Home";

    public void Visit(string page) {
        backStack.Push(currentPage);
        currentPage = page;
        forwardStack.Clear();
        Console.WriteLine(/* Output */ $"Visited: {currentPage}");
    }

    public void Back() {
        if (backStack.Count > 0) {
            forwardStack.Push(currentPage);
            currentPage = backStack.Pop();
            Console.WriteLine(/* Output */ $"Back to: {currentPage}");
        } else {
            Console.WriteLine(/* Output */ "No back history available.");
        }
    }

    public void Forward() {
        if (forwardStack.Count > 0) {
            backStack.Push(currentPage);
            currentPage = forwardStack.Pop();
            Console.WriteLine(/* Output */ $"Forward to: {currentPage}");
        } else {
            Console.WriteLine(/* Output */ "No forward history available.");
        }
    }

    public void ShowCurrentPage() {
        Console.WriteLine(/* Output */ $"Current Page: {currentPage}");
    }
}

// Test Browser Navigation
class MainProgram {
    static void Main() {
        BrowserHistory browser = new BrowserHistory();
        browser.Visit("Page1");
        browser.Visit("Page2");
        browser.Back();
        browser.Forward();
        browser.Visit("Page3");
        browser.Back();
    }
}
Output:

Visited: Page1
Visited: Page2
Back to: Page1
Forward to: Page2
Visited: Page3
Back to: Page2


 
5. Case Study 3
Case Study 3: Task Scheduler (Using Queue)
Problem Statement:
A system needs to process background tasks in a First-In, First-Out (FIFO) manner. Implement a task scheduler using a queue.
Solution:
	•	Use a queue to store tasks.
	•	Process tasks in the order they arrive.
C# Implementation:

using System;
using System.Collections.Generic;

public class TaskScheduler {
    private Queue<string> taskQueue = new Queue<string>();

    public void AddTask(string task) {
        taskQueue.Enqueue(task);
        Console.WriteLine(/* Output */ $"Task added: {task}");
    }

    public void ProcessTask() {
        if (taskQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Processing: {taskQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No tasks to process.");
        }
    }

    public void ShowTasks() {
        if (taskQueue.Count == 0) {
            Console.WriteLine(/* Output */ "No pending tasks.");
            return;
        }
        Console.WriteLine(/* Output */ "Pending tasks:");
        foreach (var task in taskQueue) {
            Console.WriteLine(/* Output */ task);
        }
    }
}

// Test Task Scheduler
class MainProgram {
    static void Main() {
        TaskScheduler scheduler = new TaskScheduler();
        scheduler.AddTask("Email Report");
        scheduler.AddTask("Database Backup");
        scheduler.ShowTasks();
        scheduler.ProcessTask();
        scheduler.ShowTasks();
    }
}
Output:

Task added: Email Report
Task added: Database Backup
Pending tasks:
Email Report
Database Backup
Processing: Email Report
Pending tasks:
Database Backup

Summary of Case Studies
Case Study
Data Structure Used
Key Feature
Employee Management System
Linked List
Dynamic memory allocation for employee records
Browser Navigation
Stack
LIFO-based back and forward navigation
Task Scheduler
Queue
FIFO-based task processing

These case studies cover real-world scenarios where linked lists, stacks, and queues are used effectively. Let me know if you need further modifications or additional examples! 🚀

















Skip to main content
Print book
2.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
2.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:31 AM
Table of contents
	•	1. Learning outcomes
	•	2. Case Study: Task Scheduler Using Queue
	•	3. Data Structures and Input/Output in C#
	•	4. Lists in C#
	•	4.1. Input and Output in C#
	•	4.2. ArrayList in C#
	•	4.3. Generic List in C#
	•	4.4. Linked List
	•	4.5. Circular-linked List
	•	4.6. Case Study 1
	•	4.7. Case Study 2
	•	4.8. Case Study 3
	•	4.9. Case Study 4
	•	5. Activity
1. Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd.

    
Not signed in? Click here and then refresh this page.
2. Case Study: Task Scheduler Using Queue
Understanding the Problem
Imagine you are developing a task scheduling system for a company. The system needs to handle background tasks, such as sending emails, backing up databases, and generating reports. However, these tasks must be executed in the order they were received—First-In, First-Out (FIFO).
This is a common problem in computing where jobs are queued up and processed in sequence. A real-world example of this would be a printer queue: when multiple users send documents to a shared printer, the printer processes the documents in the order they were submitted.
Solution: Using a Queue
A queue is the ideal data structure for this scenario. A queue follows the FIFO (First-In, First-Out) principle, meaning that the first task added will be the first one to be processed.
Queues provide two main operations:
	•	Enqueue – Adds a task to the queue.
	•	Dequeue – Removes and processes the first task in the queue.
Example: Task Scheduler Using Queue
Let’s implement a simple task scheduler using a queue in C#.

using System;
using System.Collections.Generic;
 
public class TaskScheduler {
    private Queue<string> taskQueue = new Queue<string>();
 
    public void AddTask(string task) {
        taskQueue.Enqueue(task);
        Console.WriteLine(/* Output */ $"Task added: {task}");
    }
 
    public void ProcessTask() {
        if (taskQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Processing: {taskQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No tasks to process.");
        }
    }
 
    public void ShowTasks() {
        if (taskQueue.Count == 0) {
            Console.WriteLine(/* Output */ "No pending tasks.");
            return;
        }
        Console.WriteLine(/* Output */ "Pending tasks:");
        foreach (var task in taskQueue) {
            Console.WriteLine(/* Output */ task);
        }
    }
}
 
// Test Program
class MainProgram {
    static void Main() {
        TaskScheduler scheduler = new TaskScheduler();
        scheduler.AddTask("Email Report");
        scheduler.AddTask("Database Backup");
        scheduler.ShowTasks();
        scheduler.ProcessTask();
        scheduler.ShowTasks();
    }
}
Output
Task added: Email Report  
Task added: Database Backup  
Pending tasks:  
Email Report  
Database Backup  
Processing: Email Report  
Pending tasks:  
Database Backup  
In this example, we use a Queue<string> to store tasks. The program allows adding tasks to the queue, processing them one by one, and displaying the remaining tasks.

3. Data Structures and Input/Output in C#
C# provides a variety of data structures that allow us to store, manage, and manipulate data efficiently. Understanding these structures is crucial for developing robust applications. In this lesson, we will explore different types of lists in C#, understand how to perform input and output operations, and learn how to implement a task scheduler using a queue.
By the end of this lesson, you will be able to: ✔ Understand different types of lists and their usage. ✔ Use queues to implement a simple task scheduler. ✔ Perform input and output operations in C#. ✔ Work with ArrayLists, Generic Lists, Sorted Lists, Linked Lists, and Circular Linked Lists. ✔ Complete two hands-on activities to reinforce learning.

4. Lists in C#
A list is a data structure that stores a collection of elements. Unlike arrays, which have a fixed size, lists can dynamically grow and shrink. Lists allow easy insertion, deletion, and searching of elements, making them more flexible than arrays.
C# provides different types of lists, including ArrayList, Generic List, Sorted List, Linked List, and Circular Linked List. Each type has its own advantages and use cases. Let’s explore them one by one.

4.1. Input and Output in C#
Understanding Input and Output
Input and Output (I/O) operations allow a program to interact with users. Input refers to data received from the user, while output refers to data displayed to the user. C# provides the Console.ReadLine() method to read input and Console.WriteLine(/* Output */ ) to display output.
Example: Basic Input and Output
Console.Write("Enter your name: ");
string name = Console.ReadLine();
Console.WriteLine(/* Output */ "Hello, " + name);
Output
Enter your name: John  
Hello, John  

 
4.2. ArrayList in C#
An ArrayList is a non-generic collection that can store different types of data. Unlike arrays, ArrayList can dynamically grow and shrink. However, because it stores objects, type safety is not enforced.
Example: Using ArrayList
using System;
using System.Collections;
 
class MainProgram {
    static void Main() {
        ArrayList arrList = new ArrayList();
        arrList.Add(10);
        arrList.Add("Hello");
        arrList.Add(3.14);
        
        foreach (var item in arrList) {
            Console.WriteLine(/* Output */ item);
        }
    }
}
Output
10  
Hello  
3.14  

 
4.3. Generic List in C#
A Generic List (List<T>) is a strongly typed collection that provides better performance and type safety compared to ArrayList.
Example: Using Generic List

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        List<int> numArray = new List<int> { 10, 20, 30 };
        numArray.Add(40);
 
        foreach (int num in numArray) {
            Console.WriteLine(/* Output */ num);
        }
    }
}
Output
10  
20  
30  
40  

 
4.4. Linked List
Introduction:
A Linked List is a linear data structure where each element (called a node) is connected to the next one. Unlike arrays, linked lists do not require contiguous memory, making them efficient for dynamic memory allocation. In C#, linked lists are commonly implemented using the LinkedList<T> class, which is part of the System.Collections.Generic namespace.
Structure of a Linked List:
	•	Node: Each node contains two parts:
	•	Data: The actual data stored in the node.
	•	Next: A reference (or pointer) to the next node in the list.
	•	Head: The first node of the list.
	•	Tail: The last node of the list (which typically points to null).
Types of Linked Lists:
	•	Singly Linked List: Each node has a reference to the next node. The last node points to null.
	•	Doubly Linked List: Each node contains two references: one to the next node and another to the previous node.
	•	Circular Linked List: The last node points back to the head node, forming a circular structure.
Basic Operations:
	•	Insertion:
	•	At the beginning: Add a new node as the head.
	•	At the end: Traverse to the last node and append the new node.
	•	At a given position: Traverse the list and insert the node at the required position.
	•	Deletion:
	•	From the beginning: Remove the head node.
	•	From the end: Traverse to the second-to-last node and set its next reference to null.
	•	From a given position: Traverse the list, update the references to bypass the node to be deleted.
	•	Traversal: Starting from the head node, visit each node until null is reached (for singly linked lists) or the desired condition is met.
	•	Search: Traverse the list to find a node with specific data.
C# Implementation (Singly Linked List Example):

using System;

public class Node {
    public int Data;
    public Node Next;

    public Node(int data) {
        Data = data;
        Next = null;
    }
}

public class LinkedList {
    public Node Head;

    // Insert a node at the beginning
    public void InsertAtBeginning(int data) {
        Node newNode = new Node(data);
        newNode.Next = Head;
        Head = newNode;
    }

    // Print the list
    public void PrintList() {
        Node current = Head;
        while (current != null) {
            Console.Write(current.Data + " ");
            current = current.Next;
        }
        Console.WriteLine(/* Output */ );
    }

    // Delete a node with a specific value
    public void Delete(int value) {
        if (Head == null) return;

        if (Head.Data == value) {
            Head = Head.Next; // Remove head
            return;
        }

        Node current = Head;
        while (current.Next != null && current.Next.Data != value) {
            current = current.Next;
        }

        if (current.Next != null) {
            current.Next = current.Next.Next; // Remove node
        }
    }
}

class MainProgram {
    static void Main() {
        LinkedList list = new LinkedList();
        list.InsertAtBeginning(10);
        list.InsertAtBeginning(20);
        list.InsertAtBeginning(30);

        Console.WriteLine(/* Output */ "List: ");
        list.PrintList();

        list.Delete(20);
        Console.WriteLine(/* Output */ "After Deleting 20: ");
        list.PrintList();
    }
}
Expected Output:
List:
30 20 10
After Deleting 20:
30 10

4.5. Circular-linked List
Introduction:
A Circular Linked List is a variation of the linked list where the last node points back to the first node, creating a loop. This makes it a circular structure. Circular linked lists can be either singly or doubly linked.
Key Characteristics:
	•	The last node’s Next points to the first node.
	•	There is no null node in a circular linked list; the list is circular, meaning you can traverse it endlessly.
	•	Circular Singly Linked List: Each node has a reference to the next node, and the last node points to the head node.
	•	Circular Doubly Linked List: Each node has two references: one to the next node and another to the previous node. Both the head and tail nodes point to each other, completing the loop.
Advantages:
	•	Circular linked lists are especially useful for implementing applications like round-robin scheduling, playing a playlist of songs, or managing a circular buffer.
	•	Can be useful in situations where the list is frequently traversed and you want to avoid rechecking the starting point after reaching the end.
Basic Operations in Circular Linked List:
	•	Insertion at the beginning, end, or specific position: Similar to regular linked lists, but ensuring that the last node’s Next points to the first node.
	•	Traversal: To avoid infinite loops, traversal should stop when we reach the starting node again.
	•	Deletion: Remove a node, ensuring the circular structure is maintained by adjusting the Next pointer of the previous node.
C# Implementation (Circular Singly Linked List Example):

using System;

public class Node {
    public int Data;
    public Node Next;

    public Node(int data) {
        Data = data;
        Next = null;
    }
}

public class CircularLinkedList {
    private Node head;

    // Insert a node at the end of the list (circular)
    public void InsertAtEnd(int data) {
        Node newNode = new Node(data);
        
        if (head == null) {
            head = newNode;
            newNode.Next = head; // Point to itself
        } else {
            Node tempVal = head;
            while (tempVal.Next != head) { // Traverse until we reach the last node
                tempVal = tempVal.Next;
            }
            tempVal.Next = newNode;
            newNode.Next = head; // Make the list circular again
        }
    }

    // Print the circular list
    public void PrintList() {
        if (head == null) {
            Console.WriteLine(/* Output */ "List is empty.");
            return;
        }

        Node current = head;
        do {
            Console.Write(current.Data + " ");
            current = current.Next;
        } while (current != head); // Stop when we loop back to the head
        Console.WriteLine(/* Output */ );
    }

    // Delete a node with a specific value
    public void Delete(int value) {
        if (head == null) return;

        if (head.Data == value) {
            // If there's only one node
            if (head.Next == head) {
                head = null;
            } else {
                Node tempVal = head;
                while (tempVal.Next != head) { // Traverse to the last node
                    tempVal = tempVal.Next;
                }
                head = head.Next; // Move head to the next node
                tempVal.Next = head; // Adjust the last node to point to the new head
            }
            return;
        }

        Node current = head;
        while (current.Next != head && current.Next.Data != value) {
            current = current.Next;
        }

        if (current.Next != head) {
            current.Next = current.Next.Next; // Remove the node
        }
    }
}

class MainProgram {
    static void Main() {
        CircularLinkedList list = new CircularLinkedList();
        list.InsertAtEnd(10);
        list.InsertAtEnd(20);
        list.InsertAtEnd(30);

        Console.WriteLine(/* Output */ "Circular List: ");
        list.PrintList();

        list.Delete(20);
        Console.WriteLine(/* Output */ "After Deleting 20: ");
        list.PrintList();
    }
}
Expected Output:
Circular List:
10 20 30
After Deleting 20:
10 30

Comparison of Linked List and Circular Linked List:
Feature
Linked List
Circular Linked List
End of List
The last node points to null.
The last node points to the head.
Traversal
Stops when null is encountered.
Loops infinitely, requires careful stopping.
Use Cases
Good for dynamically changing data.
Ideal for round-robin scheduling, circular buffers, etc.
Memory Management
No circular references, easy to delete.
More complex due to circular references.
Conclusion:
	•	A Linked List is a basic dynamic data structure ideal for applications that need efficient insertions and deletions.
	•	A Circular Linked List is a variation where the last node points back to the first node, making it suitable for scenarios where the data needs to be processed in a cyclic manner.
Both structures provide efficient ways of handling dynamic data with flexible memory usage, depending on the specific problem requirements.
 
4.6. Case Study 1
Problem:
You need to develop a simple task management application where tasks can have mixed data types (e.g., string for task description, integer for priority, and DateTime for deadlines). For this, an ArrayList is suitable because it can hold elements of any data type, allowing you to store these varied properties for each task.
Solution:
We will use an ArrayList to store tasks, where each task is a combination of task description (string), priority (int), and deadline (DateTime). We'll implement functionality to add new tasks, display tasks, and remove a task.
Code Solution:
using System;
using System.Collections;
 
public class Task {
    public string Description { get; set; }
    public int Priority { get; set; }
    public DateTime Deadline { get; set; }
 
    public Task(string description, int priority, DateTime deadline) {
        Description = description;
        Priority = priority;
        Deadline = deadline;
    }
}
 
class MainProgram {
    static void Main() {
        ArrayList taskList = new ArrayList();
        
        // Adding tasks with mixed data types
        taskList.Add(new Task("Send Email", 1, DateTime.Now.AddHours(2)));
        taskList.Add(new Task("Backup Database", 2, DateTime.Now.AddDays(1)));
        taskList.Add(new Task("Generate Report", 3, DateTime.Now.AddHours(5)));
        
        // Displaying tasks
        foreach (Task task in taskList) {
            Console.WriteLine(/* Output */ $"Task: {task.Description}, Priority: {task.Priority}, Deadline: {task.Deadline}");
        }
 
        // Removing a task
        taskList.RemoveAt(1); // Remove second task
        Console.WriteLine(/* Output */ "\nAfter removing second task:\n");
        
        // Displaying tasks after removal
        foreach (Task task in taskList) {
            Console.WriteLine(/* Output */ $"Task: {task.Description}, Priority: {task.Priority}, Deadline: {task.Deadline}");
        }
    }
}
Expected Output:

Task: Send Email, Priority: 1, Deadline: [DateTime]
Task: Backup Database, Priority: 2, Deadline: [DateTime]
Task: Generate Report, Priority: 3, Deadline: [DateTime]
 
After removing second task:
 
Task: Send Email, Priority: 1, Deadline: [DateTime]
Task: Generate Report, Priority: 3, Deadline: [DateTime]

 
4.7. Case Study 2
Problem:
You are tasked with developing a simple grade management system for a class. You need to store students' grades, which will be integers. A Generic List<int> is suitable as it ensures type safety and provides flexible manipulation of the grade data.
Solution:
We'll use a Generic List<int> to store the student grades and implement functions to add, remove, and display grades.
Code Solution:

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        // Creating a generic list to store student grades
        List<int> grades = new List<int> { 85, 92, 76, 88, 95 };
 
        // Adding a new grade
        grades.Add(89);
 
        // Removing a grade
        grades.Remove(76);
 
        // Displaying all grades
        Console.WriteLine(/* Output */ "Student Grades:");
        foreach (int grade in grades) {
            Console.WriteLine(/* Output */ grade);
        }
 
        // Calculating average grade
        double average = CalculateAverage(grades);
        Console.WriteLine(/* Output */ $"\nAverage Grade: {average:F2}");
    }
 
    static double CalculateAverage(List<int> grades) {
        double sum = 0;
        foreach (int grade in grades) {
            sum += grade;
        }
        return sum / grades.Count;
    }
}
Expected Output:

Student Grades:
85
92
88
95
89
 
Average Grade: 89.80

 
4.8. Case Study 3
Problem:
You need to develop a music player application where users can dynamically add or remove songs from the playlist. A Linked List is ideal because it allows efficient insertion and removal of songs from the beginning, middle, or end of the list.
Solution:
We'll use a LinkedList<string> to represent the playlist. We will implement methods to add new songs, remove songs, and display the entire playlist.
Code Solution:

using System;
using System.Collections.Generic;
 
public class Playlist {
    private LinkedList<string> songs = new LinkedList<string>();
 
    // Add a song to the playlist
    public void AddSong(string song) {
        songs.AddLast(song);
        Console.WriteLine(/* Output */ $"Song added: {song}");
    }
 
    // Remove a song from the playlist
    public void RemoveSong(string song) {
        if (songs.Contains(song)) {
            songs.Remove(song);
            Console.WriteLine(/* Output */ $"Song removed: {song}");
        } else {
            Console.WriteLine(/* Output */ "Song not found in the playlist.");
        }
    }
 
    // Display all songs in the playlist
    public void ShowPlaylist() {
        Console.WriteLine(/* Output */ "\nCurrent Playlist:");
        foreach (var song in songs) {
            Console.WriteLine(/* Output */ song);
        }
    }
}
 
class MainProgram {
    static void Main() {
        Playlist playlist = new Playlist();
        
        // Adding songs to the playlist
        playlist.AddSong("Song A");
        playlist.AddSong("Song B");
        playlist.AddSong("Song C");
        
        // Displaying the playlist
        playlist.ShowPlaylist();
        
        // Removing a song
        playlist.RemoveSong("Song B");
        
        // Displaying the playlist after removal
        playlist.ShowPlaylist();
    }
}
Expected Output:

Song added: Song A
Song added: Song B
Song added: Song C
 
Current Playlist:
Song A
Song B
Song C
 
Song removed: Song B
 
Current Playlist:
Song A
Song C

 
4.9. Case Study 4
Problem:
You are designing a game where players can navigate through different levels, and the navigation should loop back to the first level after reaching the last one. A Circular Linked Listis ideal to model this behavior.
Solution:
We'll create a Circular Linked List where each node represents a level in the game. The last node will point back to the first node, creating a circular structure for navigation.
Code Solution:

using System;
 
public class Level {
    public string LevelName { get; set; }
    public Level NextLevel { get; set; }
 
    public Level(string levelName) {
        LevelName = levelName;
    }
}
 
public class CircularLinkedList {
    private Level head;
 
    public void AddLevel(string levelName) {
        Level newLevel = new Level(levelName);
        if (head == null) {
            head = newLevel;
            head.NextLevel = head; // Point to itself, circular link
        } else {
            Level tempVal = head;
            while (tempVal.NextLevel != head) {
                tempVal = tempVal.NextLevel;
            }
            tempVal.NextLevel = newLevel;
            newLevel.NextLevel = head; // Complete the circular link
        }
    }
 
    public void ShowLevels() {
        if (head == null) {
            Console.WriteLine(/* Output */ "No levels in the game.");
            return;
        }
 
        Level current = head;
        do {
            Console.WriteLine(/* Output */ current.LevelName);
            current = current.NextLevel;
        } while (current != head); // Stop when we loop back to the first level
    }
}
 
class MainProgram {
    static void Main() {
        CircularLinkedList gameLevels = new CircularLinkedList();
        
        // Adding levels to the game
        gameLevels.AddLevel("Level 1");
        gameLevels.AddLevel("Level 2");
        gameLevels.AddLevel("Level 3");
        
        // Displaying all levels in a circular fashion
        gameLevels.ShowLevels();
    }
}
Expected Output:

Level 1
Level 2
Level 3

These case studies demonstrate how to apply different data structures in real-world scenarios using C#:
	•	ArrayList for heterogeneous task data.
	•	Generic List for managing student grades.
	•	Linked List for dynamic playlist management.
	•	Circular Linked List for looping through game levels.
Each solution provides an efficient way to handle the problem using the most appropriate data structure.
 
 
5. Activity
Activity 1: Implement a Stack for Undo Feature
Task:
Create a C# program that simulates an Undo feature using a Stack. The user should be able to add actions, undo the last action, and view all actions.
using System;
using System.Collections.Generic;
 
class UndoSystem {
    private Stack<string> actions = new Stack<string>();
 
    public void AddAction(string action) {
        actions.Push(action);
        Console.WriteLine(/* Output */ $"Action added: {action}");
    }
 
    public void UndoAction() {
        if (actions.Count > 0) {
            Console.WriteLine(/* Output */ $"Undoing: {actions.Pop()}");
        } else {
            Console.WriteLine(/* Output */ "No actions to undo.");
        }
    }
 
    public void ShowActions() {
        Console.WriteLine(/* Output */ "Actions:");
        foreach (var action in actions) {
            Console.WriteLine(/* Output */ action);
        }
    }
}
 
// Test Program
class MainProgram {
    static void Main() {
        UndoSystem undoSystem = new UndoSystem();
        undoSystem.AddAction("Opened File");
        undoSystem.AddAction("Edited Text");
        undoSystem.ShowActions();
        undoSystem.UndoAction();
        undoSystem.ShowActions();
    }
}
 
Skip to main content
Print book
3.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
3.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:33 AM
Table of contents
	•	1. Learning outcomes
	•	2. Introduction
	•	3. Using Stack in C#:
	•	4. Advantages of Using Stacks:
	•	5. Disadvantages of Using Stacks:
	•	6. Case Study 1
	•	7. Case Study 2
	•	8. Case Study 3
	•	9. Conclusion
	•	10. Activity
1. Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd.

   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Introduction
A Stack is a linear data structure that follows the Last-In, First-Out (LIFO) principle. In a stack, the last element added (pushed) is the first one to be removed (popped). You can think of it like a stack of plates in a cafeteria where the last plate placed on the top is the first one you take off.

Stack Operations:
	•	Push: Adds an element to the top of the stack.
	•	Pop: Removes and returns the top element from the stack.
	•	Peek: Returns the top element without removing it from the stack.
	•	IsEmpty: Checks whether the stack is empty or not.
	•	Clear: Clears all elements in the stack.
Stacks are typically used in scenarios where you need to reverse the order of elements or maintain the execution order, such as undo/redo operations, expression evaluation, etc.
Real-World Examples of Stacks:
	•	Undo/Redo Mechanism in Text Editors: Each action is pushed onto the stack. When an undo operation is requested, the last action is popped.
	•	Function Call Stack in Programming: The call stack stores information about the active subroutines or functions in a program. When a function is called, its context is pushed onto the stack. When it finishes execution, the context is popped off.
	•	Expression Evaluation (Postfix/Infix): Stacks are commonly used to evaluate expressions in different notations (infix, postfix).

Play Video
3. Using Stack in C#:
C# provides a built-in Stack<T> class in the System.Collections.Generic namespace that allows easy manipulation of stack elements. This class is a generic type, meaning it can hold elements of any type.
Basic Stack Operations in C#:
1.     Creating a Stack: You can create a stack by simply using the Stack<T> class.

Stack<int> stack = new Stack<int>();
2.     Push Operation: The Push method adds an element to the top of the stack.

stack.Push(10);
stack.Push(20);
stack.Push(30);
3.     Pop Operation: The Pop method removes and returns the top element from the stack.

int topElement = stack.Pop();
Console.WriteLine(/* Output */ topElement); // Output: 30
4.     Peek Operation: The Peek method returns the top element without removing it from the stack.

int topElement = stack.Peek();
Console.WriteLine(/* Output */ topElement); // Output: 20
5.     IsEmpty Operation: The IsEmpty property checks if the stack is empty.

bool isEmpty = stack.Count == 0;
Console.WriteLine(/* Output */ isEmpty); // Output: False
6.     Clear Operation: The Clear method removes all elements from the stack.

stack.Clear();
Console.WriteLine(/* Output */ stack.Count); // Output: 0

Example Code: Basic Stack Operations in C#

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        // Create a stack of integers
        Stack<int> stack = new Stack<int>();
 
        // Push elements onto the stack
        stack.Push(10);
        stack.Push(20);
        stack.Push(30);
 
        // Peek the top element
        Console.WriteLine(/* Output */ "Top element: " + stack.Peek()); // Output: 30
 
        // Pop the top element
        Console.WriteLine(/* Output */ "Popped element: " + stack.Pop()); // Output: 30
 
        // Check if the stack is empty
        Console.WriteLine(/* Output */ "Is the stack empty? " + (stack.Count == 0 ? "Yes" : "No")); // Output: No
 
        // Pop remaining elements
        stack.Pop();
        stack.Pop();
 
        // After popping all elements, check if the stack is empty
        Console.WriteLine(/* Output */ "Is the stack empty now? " + (stack.Count == 0 ? "Yes" : "No")); // Output: Yes
    }
}
Output:

Top element: 30
Popped element: 30
Is the stack empty? No
Is the stack empty now? Yes

Advanced Use Cases of Stacks:
1. Undo/Redo Functionality:
Stacks are often used to implement undo and redo functionality. Each user action is pushed onto the stack. If the user presses "Undo," the most recent action is popped from the stack.

using System;
using System.Collections.Generic;
 
class UndoRedoSystem {
    private Stack<string> undoStack = new Stack<string>();
    private Stack<string> redoStack = new Stack<string>();
 
    public void PerformAction(string action) {
        undoStack.Push(action);
        Console.WriteLine(/* Output */ $"Action performed: {action}");
        redoStack.Clear(); // Clear redo stack after a new action
    }
 
    public void Undo() {
        if (undoStack.Count > 0) {
            string lastAction = undoStack.Pop();
            redoStack.Push(lastAction);
            Console.WriteLine(/* Output */ $"Undo: {lastAction}");
        } else {
            Console.WriteLine(/* Output */ "Nothing to undo.");
        }
    }
 
    public void Redo() {
        if (redoStack.Count > 0) {
            string lastUndoneAction = redoStack.Pop();
            undoStack.Push(lastUndoneAction);
            Console.WriteLine(/* Output */ $"Redo: {lastUndoneAction}");
        } else {
            Console.WriteLine(/* Output */ "Nothing to redo.");
        }
    }
}
 
class MainProgram {
    static void Main() {
        UndoRedoSystem system = new UndoRedoSystem();
        
        system.PerformAction("Action 1");
        system.PerformAction("Action 2");
        
        system.Undo();  // Undo Action 2
        system.Redo();  // Redo Action 2
    }
}
Expected Output:

Action performed: Action 1
Action performed: Action 2
Undo: Action 2
Redo: Action 2
2. Balanced Parentheses (Expression Validation):
Stacks can be used to check if parentheses in an expression are balanced. A balanced expression means that every opening parenthesis has a corresponding closing parenthesis.

using System;
using System.Collections.Generic;
 
class MainProgram {
    static bool IsBalanced(string expression) {
        Stack<char> stack = new Stack<char>();
 
        foreach (char ch in expression) {
            if (ch == '(') {
                stack.Push(ch); // Push opening parentheses onto stack
            } else if (ch == ')') {
                if (stack.Count == 0 || stack.Pop() != '(') {
                    return false; // Unmatched closing parentheses
                }
            }
        }
        return stack.Count == 0; // Stack should be empty if balanced
    }
 
    static void Main() {
        string expression = "(a + b) * (c + d)";
        Console.WriteLine(/* Output */ $"Is the expression '{expression}' balanced? {IsBalanced(expression)}");
    }
}
Expected Output:
Is the expression '(a + b) * (c + d)' balanced? True

4. Advantages of Using Stacks:
	•	LIFO Access: Allows processing of elements in reverse order.
	•	Memory Efficiency: Stack elements are managed using memory that is dynamically allocated.
	•	Simple Operations: Stack operations are very simple to implement and are typically constant-time operations (O(1)).
	•	Reversing Data: Stacks can be used to reverse data efficiently, such as in string reversal or expression evaluation.
 
5. Disadvantages of Using Stacks:
	•	Limited Access: You can only access the top element of the stack at a given time. This is restrictive compared to other data structures like arrays or lists, where you can access any element.
	•	Fixed Size (if implemented with an array): If a stack is implemented using an array, the size may be fixed, and you'd need to resize the array when it exceeds capacity.
 
6. Case Study 1
Problem:
You are developing a simple text editor and need to implement an Undo/Redo functionality. Each time the user types something, the editor should push the action onto a stack. The user should be able to undo and redo actions. The stack will help you manage the history of text changes.
Solution:
To implement this feature, we need two stacks:
	•	Undo Stack to store actions that can be undone.
	•	Redo Stack to store undone actions that can be redone.
When the user types, the action is pushed onto the undo stack. If the user clicks "Undo", the most recent action is popped from the undo stack and pushed onto the redo stack. If the user clicks "Redo", the action is popped from the redo stack and pushed back onto the undo stack.

using System;
using System.Collections.Generic;
 
class TextEditor {
    private Stack<string> undoStack = new Stack<string>();
    private Stack<string> redoStack = new Stack<string>();
 
    public void PerformAction(string action) {
        undoStack.Push(action);
        Console.WriteLine(/* Output */ $"Action performed: {action}");
        redoStack.Clear(); // Clear redo stack after new action
    }
 
    public void Undo() {
        if (undoStack.Count > 0) {
            string lastAction = undoStack.Pop();
            redoStack.Push(lastAction);
            Console.WriteLine(/* Output */ $"Undo: {lastAction}");
        } else {
            Console.WriteLine(/* Output */ "Nothing to undo.");
        }
    }
 
    public void Redo() {
        if (redoStack.Count > 0) {
            string lastUndoneAction = redoStack.Pop();
            undoStack.Push(lastUndoneAction);
            Console.WriteLine(/* Output */ $"Redo: {lastUndoneAction}");
        } else {
            Console.WriteLine(/* Output */ "Nothing to redo.");
        }
    }
}
 
class MainProgram {
    static void Main() {
        TextEditor editor = new TextEditor();
 
        // Perform actions
        editor.PerformAction("Typed 'Hello'");
        editor.PerformAction("Typed 'World'");
        editor.PerformAction("Typed '!'");
 
        // Undo actions
        editor.Undo(); // Undo '!'
        editor.Undo(); // Undo 'World'
 
        // Redo actions
        editor.Redo(); // Redo 'World'
        editor.Redo(); // Redo '!'
    }
}
Expected Output:

Action performed: Typed 'Hello'
Action performed: Typed 'World'
Action performed: Typed '!'
Undo: Typed '!'
Undo: Typed 'World'
Redo: Typed 'World'
Redo: Typed '!'

 
7. Case Study 2
Problem:
You are tasked with validating mathematical expressions to check if the parentheses are balanced. The expression might contain parentheses like (), {}, and []. You need to ensure that every opening parenthesis has a corresponding closing parenthesis in the correct order.
Solution:
The stack data structure can help efficiently solve this problem. As we encounter an opening parenthesis, we push it onto the stack. When we encounter a closing parenthesis, we pop the stack and check if the top element matches the corresponding opening parenthesis. If it does, the parentheses are balanced for that pair. If not, the expression is unbalanced.

using System;
using System.Collections.Generic;
 
class ParenthesesValidator {
    public bool IsBalanced(string expression) {
        Stack<char> stack = new Stack<char>();
 
        foreach (char ch in expression) {
            if (ch == '(' || ch == '{' || ch == '[') {
                stack.Push(ch); // Push opening parentheses onto stack
            } else if (ch == ')' || ch == '}' || ch == ']') {
                if (stack.Count == 0) {
                    return false; // No matching opening parenthesis
                }
                char top = stack.Pop();
                if (!Matches(top, ch)) {
                    return false; // Mismatched parentheses
                }
            }
        }
        return stack.Count == 0; // Stack should be empty if balanced
    }
 
    private bool Matches(char open, char close) {
        return (open == '(' && close == ')') || 
               (open == '{' && close == '}') || 
               (open == '[' && close == ']');
    }
}
 
class MainProgram {
    static void Main() {
        ParenthesesValidator validator = new ParenthesesValidator();
 
        string expression1 = "(a + b) * (c + d)";
        string expression2 = "{[a + b] * (c + d}";
        string expression3 = "[(a + b) * {c + d}]";
 
        Console.WriteLine(/* Output */ $"Is the expression '{expression1}' balanced? {validator.IsBalanced(expression1)}");
        Console.WriteLine(/* Output */ $"Is the expression '{expression2}' balanced? {validator.IsBalanced(expression2)}");
        Console.WriteLine(/* Output */ $"Is the expression '{expression3}' balanced? {validator.IsBalanced(expression3)}");
    }
}
Expected Output:

Is the expression '(a + b) * (c + d)' balanced? True
Is the expression '{[a + b] * (c + d}' balanced? False
Is the expression '[(a + b) * {c + d}]' balanced? True

 
8. Case Study 3
Problem:
You are developing a simple browser navigation system where a user can visit multiple web pages. The user should be able to navigate back to the previous pages using a back button. Implementing this feature using a Stack will allow efficient tracking of the visited pages and navigation backward.
Solution:
We can use a stack to keep track of the history of visited pages. Every time a new page is visited, the page URL is pushed onto the stack. When the back button is clicked, the most recent page URL is popped from the stack and displayed.

using System;
using System.Collections.Generic;
 
class BrowserHistory {
    private Stack<string> historyStack = new Stack<string>();
    private string currentPage;
 
    public void VisitPage(string url) {
        if (currentPage != null) {
            historyStack.Push(currentPage); // Push current page to history stack before visiting a new page
        }
        currentPage = url;
        Console.WriteLine(/* Output */ $"Visited: {url}");
    }
 
    public void GoBack() {
        if (historyStack.Count > 0) {
            currentPage = historyStack.Pop(); // Pop the most recent page
            Console.WriteLine(/* Output */ $"Back to: {currentPage}");
        } else {
            Console.WriteLine(/* Output */ "No pages in history.");
        }
    }
}
 
class MainProgram {
    static void Main() {
        BrowserHistory browser = new BrowserHistory();
 
        // Simulate visiting pages
        browser.VisitPage("www.google.com");
        browser.VisitPage("www.facebook.com");
        browser.VisitPage("www.github.com");
 
        // Simulate going back
        browser.GoBack(); // Go back to www.facebook.com
        browser.GoBack(); // Go back to www.google.com
        browser.GoBack(); // No pages in history
    }
}
Expected Output:

Visited: www.google.com
Visited: www.facebook.com
Visited: www.github.com
Back to: www.facebook.com
Back to: www.google.com
No pages in history.

Summary:
	•	Undo/Redo Functionality: A text editor's undo/redo feature can be efficiently implemented using two stacks: one for undo actions and another for redo actions.
	•	Balanced Parentheses Check: Stacks help efficiently validate whether a string has balanced parentheses by matching opening and closing parentheses as they are encountered.
	•	Browser History Navigation: The stack is used to store visited pages, and the user can navigate back by popping pages from the stack.
Each of these case studies illustrates a practical use of stacks in solving real-world problems, showcasing their versatility and importance in various applications.
 
9. Conclusion
Stacks are an essential data structure in programming, with many real-world applications such as undo/redo functionality, expression evaluation, and maintaining function calls in the program. In C#, you can use the built-in Stack<T> class to efficiently manage stack operations. Understanding stacks and their use cases will help in solving problems that involve managing ordered data in a LIFO manner.
10. Activity
Create a stack in C# that will mimic the browser forward and backward functionality. Each tab will be represented by a string.












Skip to main content
Print book
4.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
4.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:33 AM
Table of contents
	•	1. Learning outcomes
	•	2. Introduction to Queues
	•	3. Implementing Queues in C#
	•	4. Types of Queues in C#
	•	5. Practical Use Cases of Queues
	•	6. Case study 1
	•	7. Case study 2
	•	8. Case Study 3
	•	9. Activity
1. Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
 
Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd.

   
Not signed in? Click here and then refresh this page.
2. Introduction to Queues
Introduction to Queues
A queue is a linear data structure that follows the First-In, First-Out (FIFO) principle. This means that the first element added to the queue will be the first one to be removed. Queues are widely used in programming for managing tasks that must be processed in order.

Real-World Examples of Queues
	•	Print Queue: Documents sent to a printer are printed in the order they were received.
	•	Call Center Queue: Calls are answered in the order they were received.
	•	Task Scheduling: Background tasks like sending emails or processing orders are executed in the order they were added.
	•	CPU Scheduling: The operating system manages processes in a queue.

3. Implementing Queues in C#
C# provides built-in support for queues through the Queue<T> class in the System.Collections.Generic namespace.
Basic Queue Operations
Operation
Description
Enqueue(item)
Adds an element to the end of the queue
Dequeue()
Removes and returns the element at the front of the queue
Peek()
Returns the front element without removing it
Count
Returns the number of elements in the queue
Contains(item)
Checks if an element exists in the queue
Clear()
Removes all elements from the queue

2. Implementing a Queue in C#
Example: Basic Queue Operations

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        Queue<string> queue = new Queue<string>();
 
        // Enqueue - Adding elements
        queue.Enqueue("Alice");
        queue.Enqueue("Bob");
        queue.Enqueue("Charlie");
 
        Console.WriteLine(/* Output */ "Queue after Enqueue operations:");
        foreach (var person in queue)
            Console.WriteLine(/* Output */ person);
 
        // Peek - Check first element
        Console.WriteLine(/* Output */ "\nFront of the queue: " + queue.Peek());
 
        // Dequeue - Removing elements
        Console.WriteLine(/* Output */ "\nProcessing: " + queue.Dequeue());
        Console.WriteLine(/* Output */ "Processing: " + queue.Dequeue());
 
        Console.WriteLine(/* Output */ "\nQueue after Dequeue operations:");
        foreach (var person in queue)
            Console.WriteLine(/* Output */ person);
    }
}
Output:

Queue after Enqueue operations:
Alice
Bob
Charlie
 
Front of the queue: Alice
 
Processing: Alice
Processing: Bob
 
Queue after Dequeue operations:
Charlie

 
4. Types of Queues in C#
C# supports different types of queues, depending on the use case:
3.1 Standard Queue (FIFO)
The Queue<T> class implements a simple FIFO queue where elements are added to the back and removed from the front.

Queue<int> queue = new Queue<int>();
queue.Enqueue(1);
queue.Enqueue(2);
queue.Enqueue(3);
Console.WriteLine(/* Output */ queue.Dequeue()); // Output: 1

3.2 Priority Queue
A priority queue processes elements based on their priority instead of their arrival order. The PriorityQueue<TElement, TPriority> class in .NET 6+ provides a built-in way to create priority queues.
Example: Task Scheduler with Priority Queue

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        PriorityQueue<string, int> taskQueue = new PriorityQueue<string, int>();
 
        taskQueue.Enqueue("Low Priority Task", 3);
        taskQueue.Enqueue("High Priority Task", 1);
        taskQueue.Enqueue("Medium Priority Task", 2);
 
        Console.WriteLine(/* Output */ "Processing tasks in priority order:");
        while (taskQueue.Count > 0) {
            Console.WriteLine(/* Output */ taskQueue.Dequeue());
        }
    }
}
Output:

Processing tasks in priority order:
High Priority Task
Medium Priority Task
Low Priority Task
Explanation: Tasks with lower priority numArray are processed first.

3.3 Double-Ended Queue (Deque)
A deque (double-ended queue) allows insertion and deletion at both ends. It can be implemented using LinkedList<T>.
Example: Deque using LinkedList

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        LinkedList<int> deque = new LinkedList<int>();
 
        // Adding elements at both ends
        deque.AddLast(1);
        deque.AddLast(2);
        deque.AddFirst(0);
 
        // Removing elements from both ends
        deque.RemoveLast();
        deque.RemoveFirst();
 
        Console.WriteLine(/* Output */ "Deque after operations:");
        foreach (var item in deque)
            Console.WriteLine(/* Output */ item);
    }
}
Output:
Deque after operations:
1

 
5. Practical Use Cases of Queues
Task Scheduler Using Queue
Problem: Background tasks (e.g., email notifications, database backups) must be executed in the order they were added.
Solution: Use a Queue<string> to manage tasks.

using System;
using System.Collections.Generic;
 
class TaskScheduler {
    private Queue<string> taskQueue = new Queue<string>();
 
    public void AddTask(string task) {
        taskQueue.Enqueue(task);
        Console.WriteLine(/* Output */ $"Task added: {task}");
    }
 
    public void ProcessTask() {
        if (taskQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Processing: {taskQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No tasks to process.");
        }
    }
 
    public void ShowTasks() {
        Console.WriteLine(/* Output */ "Pending tasks:");
        foreach (var task in taskQueue)
            Console.WriteLine(/* Output */ task);
    }
}
 
class MainProgram {
    static void Main() {
        TaskScheduler scheduler = new TaskScheduler();
        scheduler.AddTask("Send Email");
        scheduler.AddTask("Backup Database");
        scheduler.ShowTasks();
        scheduler.ProcessTask();
        scheduler.ShowTasks();
    }
}
Output:
Task added: Send Email
Task added: Backup Database
Pending tasks:
Send Email
Backup Database
Processing: Send Email
Pending tasks:
Backup Database

Call Center Queue System
A call center assigns customer calls to agents in the order they are received.

using System;
using System.Collections.Generic;
 
class CallCenter {
    private Queue<string> callQueue = new Queue<string>();
 
    public void ReceiveCall(string caller) {
        callQueue.Enqueue(caller);
        Console.WriteLine(/* Output */ $"Call received from: {caller}");
    }
 
    public void AnswerCall() {
        if (callQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Answering call from: {callQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No calls in queue.");
        }
    }
}
 
class MainProgram {
    static void Main() {
        CallCenter center = new CallCenter();
        center.ReceiveCall("Customer 1");
        center.ReceiveCall("Customer 2");
        center.AnswerCall();
        center.AnswerCall();
    }
}
Output:
Call received from: Customer 1
Call received from: Customer 2
Answering call from: Customer 1
Answering call from: Customer 2

Summary
Feature
Description
FIFO Principle
Queues process elements in First-In, First-Out order.
Queue<T>
The standard C# queue class for managing ordered data.
PriorityQueue<TElement, TPriority>
Elements are processed based on priority.
Deque (Double-Ended Queue)
Supports insertion and deletion from both ends.
Real-World Applications
Used in task scheduling, call centers, printer queues, and messaging systems.

Conclusion
Queues are fundamental data structures widely used in real-world applications. C# provides multiple ways to implement queues, including Queue<T>, PriorityQueue<T>, and LinkedList<T> for deques. Understanding queues helps in building efficient systems for processing tasks in sequence 
6. Case study 1
Problem Statement
A telecom company needs a Customer Service Call Queue system where customer calls are answered in the order they were received. The system should:
	•	Allow new customer calls to be added to the queue.
	•	Process calls in a First-In, First-Out (FIFO) manner.
	•	Display the current queue of waiting calls.

Solution
We can implement this system using a Queue<string> in C#.
Implementation:

using System;
using System.Collections.Generic;
 
class CallCenter {
    private Queue<string> callQueue = new Queue<string>();
 
    // Method to add a call to the queue
    public void ReceiveCall(string caller) {
        callQueue.Enqueue(caller);
        Console.WriteLine(/* Output */ $"Call received from: {caller}");
    }
 
    // Method to answer and remove a call from the queue
    public void AnswerCall() {
        if (callQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Answering call from: {callQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No calls in the queue.");
        }
    }
 
    // Display all pending calls
    public void ShowQueue() {
        if (callQueue.Count == 0) {
            Console.WriteLine(/* Output */ "No pending calls.");
        } else {
            Console.WriteLine(/* Output */ "Pending Calls:");
            foreach (var caller in callQueue) {
                Console.WriteLine(/* Output */ caller);
            }
        }
    }
}
 
// Test the Call Center System
class MainProgram {
    static void Main() {
        CallCenter center = new CallCenter();
        center.ReceiveCall("Customer 1");
        center.ReceiveCall("Customer 2");
        center.ReceiveCall("Customer 3");
 
        center.ShowQueue();
 
        center.AnswerCall();
        center.ShowQueue();
    }
}
Output:
Call received from: Customer 1
Call received from: Customer 2
Call received from: Customer 3
 
Pending Calls:
Customer 1
Customer 2
Customer 3
 
Answering call from: Customer 1
 
Pending Calls:
Customer 2
Customer 3
✅ Queue ensures that customers are served in order!

 
7. Case study 2
Problem Statement
A university computer lab has multiple students sending print requests to a shared network printer. The printer must:
	•	Accept multiple print jobs.
	•	Process the print jobs in order of submission.
	•	Display the current print queue.

Solution
A Queue<string> is ideal for handling print jobs.
Implementation:

using System;
using System.Collections.Generic;
 
class PrintQueue {
    private Queue<string> jobQueue = new Queue<string>();
 
    // Method to add a print job
    public void AddPrintJob(string document) {
        jobQueue.Enqueue(document);
        Console.WriteLine(/* Output */ $"Print job added: {document}");
    }
 
    // Method to process the next print job
    public void ProcessPrintJob() {
        if (jobQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Printing: {jobQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No print jobs in the queue.");
        }
    }
 
    // Show all pending print jobs
    public void ShowQueue() {
        if (jobQueue.Count == 0) {
            Console.WriteLine(/* Output */ "No pending print jobs.");
        } else {
            Console.WriteLine(/* Output */ "Pending Print Jobs:");
            foreach (var job in jobQueue) {
                Console.WriteLine(/* Output */ job);
            }
        }
    }
}
 
// Test the Print Queue System
class MainProgram {
    static void Main() {
        PrintQueue printer = new PrintQueue();
        printer.AddPrintJob("Assignment.pdf");
        printer.AddPrintJob("Research_Paper.docx");
        printer.AddPrintJob("Presentation.pptx");
 
        printer.ShowQueue();
 
        printer.ProcessPrintJob();
        printer.ShowQueue();
    }
}
Output:
Print job added: Assignment.pdf
Print job added: Research_Paper.docx
Print job added: Presentation.pptx
 
Pending Print Jobs:
Assignment.pdf
Research_Paper.docx
Presentation.pptx
 
Printing: Assignment.pdf
 
Pending Print Jobs:
Research_Paper.docx
Presentation.pptx
✅ The queue ensures print jobs are processed in the order they were added!

 
8. Case Study 3
Problem Statement
A fast-food restaurant processes orders from customers. The system should:
	•	Accept new orders and add them to a queue.
	•	Process orders in the order they were placed.
	•	Display the list of pending orders.

Solution
A Queue<string> is perfect for tracking orders.
Implementation:
using System;
using System.Collections.Generic;
 
class RestaurantOrderQueue {
    private Queue<string> orderQueue = new Queue<string>();
 
    // Method to add an order
    public void PlaceOrder(string order) {
        orderQueue.Enqueue(order);
        Console.WriteLine(/* Output */ $"Order placed: {order}");
    }
 
    // Method to serve an order
    public void ServeOrder() {
        if (orderQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Serving order: {orderQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No orders in the queue.");
        }
    }
 
    // Show all pending orders
    public void ShowPendingOrders() {
        if (orderQueue.Count == 0) {
            Console.WriteLine(/* Output */ "No pending orders.");
        } else {
            Console.WriteLine(/* Output */ "Pending Orders:");
            foreach (var order in orderQueue) {
                Console.WriteLine(/* Output */ order);
            }
        }
    }
}
 
// Test the Restaurant Order Queue System
class MainProgram {
    static void Main() {
        RestaurantOrderQueue restaurant = new RestaurantOrderQueue();
        restaurant.PlaceOrder("Burger");
        restaurant.PlaceOrder("Pizza");
        restaurant.PlaceOrder("Pasta");
 
        restaurant.ShowPendingOrders();
 
        restaurant.ServeOrder();
        restaurant.ShowPendingOrders();
    }
}
Output:
Order placed: Burger
Order placed: Pizza
Order placed: Pasta
 
Pending Orders:
Burger
Pizza
Pasta
 
Serving order: Burger
 
Pending Orders:
Pizza
Pasta
✅ Orders are served in the same sequence they were placed!

Summary of Case Studies
Case Study
Description
Queue Used
Customer Service Call Queue
Manages customer support calls in FIFO order
Queue<string>
Print Job Queue
Ensures print jobs are processed in order of submission
Queue<string>
Restaurant Order Queue
Tracks and processes restaurant orders in order of arrival
Queue<string>
 
 
9. Activity
Create a queue in C# that will schedule customers in a pharmacy. Customers will enqueue and get a ticket. Their ticket number will then be called when it’s their turn to use the counter.


























Skip to main content
Print book
5.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
5.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:34 AM
Description
 
 
Table of contents
	•	1. Lesson Outcomes
	•	2. Priority Queue
	•	3. Priority Queues
	•	4. Using the Built-in PriorityQueue in C#
	•	5. Scenario 1: Customer Support Ticket System
	•	6. Scenario 2: Airline Check-in System
	•	7. Activity
1. Lesson Outcomes
 
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms
	•	Implement data structures in C#.
	•	Demonstrate how strings are structured and processed.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision.


Prescribed Reading
 
Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd.
Jamro, M., (2018). Stacks and Queues, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p108-p113
 

  
Not signed in? Click here and then refresh this page.
2. Priority Queue
Introduction
A Priority Queue is a special type of queue where elements are dequeued based on their priority rather than their order of arrival. Unlike a standard queue that follows the First-In, First-Out (FIFO) principle, a priority queue processes higher-priority elements first, regardless of when they were added.
In C#, a Priority Queue can be implemented using:
	•	The PriorityQueue<TElement, TPriority> class (introduced in .NET 6).
	•	A SortedList<TPriority, Queue<TElement>>.
	•	A Binary Heap (Min-Heap / Max-Heap).

Why Use a Priority Queue?
A Priority Queue is useful when tasks or elements must be processed based on priority rather than order. Some real-world use cases include:
	•	Operating System Task Scheduling: High-priority processes execute before lower-priority ones.
	•	Dijkstra’s Algorithm: Used in shortest path calculations.
	•	Hospital Emergency Room Management: Critical patients are treated first.
	•	Networking: Packet scheduling where important data packets are transmitted first.


3. Priority Queues
Priority queues[1] can be seen as an extension of regular queues, where there are sub queues within a main queue. Each sub queue is assigned a priority. As elements are enqueued, they are assigned to the sub queue with their priority. When elements are dequeued, elements are dequeued from the sub queue with the highest priority. When this sub queue is empty, then the algorithm will dequeue elements from the sub queue with the next highest priority, and so on.
 
Priority queues are implemented in C# and the source code[2] and documentation[3] can be viewed on the Microsoft website.
 
It is worth noting that C# implementations of priority queues vary to the traditional theoretical implementation. Priority queues in C# are not guaranteed to output elements within the same priority in the same order.
 

[1] GeeksforGeeks (2023b) What is Priority Queue   Introduction to Priority Queue. https://www.geeksforgeeks.org/priority-queue-set-1-introduction/.
[2] Reference source (2024). https://referencesource.microsoft.com/#WindowsBase/Base/MS/Internal/PriorityQueue.cs,f9df8c3c0cbdff22.
[3] Dotnet-Bot (2024) PriorityQueue Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.priorityqueue-2?view=net-8.0.
4. Using the Built-in PriorityQueue in C#
The PriorityQueue<TElement, TPriority> class (introduced in .NET 6) provides a simple way to implement a priority queue.
Example: Task Management System

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        PriorityQueue<string, int> taskQueue = new PriorityQueue<string, int>();
 
        // Adding tasks with different priorities (lower number = higher priority)
        taskQueue.Enqueue("Low Priority Task", 3);
        taskQueue.Enqueue("Medium Priority Task", 2);
        taskQueue.Enqueue("High Priority Task", 1);
 
        // Processing tasks based on priority
        Console.WriteLine(/* Output */ "Processing tasks based on priority:");
        while (taskQueue.Count > 0) {
            Console.WriteLine(/* Output */ taskQueue.Dequeue());
        }
    }
}
Output:
Processing tasks based on priority:
High Priority Task
Medium Priority Task
Low Priority Task
✅ Lower priority values are dequeued first (since smaller numArray have higher priority).

2. Implementing a Priority Queue Using SortedList<TPriority, Queue<TElement>>
If using .NET versions before .NET 6, we can implement a priority queue using SortedList.
Example: Hospital Emergency Room Queue

using System;
using System.Collections.Generic;
 
class PriorityQueue<T> {
    private SortedList<int, Queue<T>> queue = new SortedList<int, Queue<T>>();
 
    public void Enqueue(T item, int priority) {
        if (!queue.ContainsKey(priority)) {
            queue[priority] = new Queue<T>();
        }
        queue[priority].Enqueue(item);
    }
 
    public T Dequeue() {
        if (queue.Count == 0) throw new InvalidOperationException("Queue is empty");
 
        int highestPriority = queue.Keys[0];
        T item = queue[highestPriority].Dequeue();
 
        if (queue[highestPriority].Count == 0) {
            queue.Remove(highestPriority);
        }
        return item;
    }
 
    public bool IsEmpty() {
        return queue.Count == 0;
    }
}
 
class MainProgram {
    static void Main() {
        PriorityQueue<string> erQueue = new PriorityQueue<string>();
 
        erQueue.Enqueue("Patient with mild symptoms", 3);
        erQueue.Enqueue("Patient with broken arm", 2);
        erQueue.Enqueue("Patient with heart attack", 1);
 
        Console.WriteLine(/* Output */ "Processing patients:");
        while (!erQueue.IsEmpty()) {
            Console.WriteLine(/* Output */ erQueue.Dequeue());
        }
    }
}
Output:
Processing patients:
Patient with heart attack
Patient with broken arm
Patient with mild symptoms
✅ The most critical patients (lower priority number) are treated first.

3. Implementing a Priority Queue Using a Min-Heap
A Heap is a more efficient way to implement a priority queue. It provides:
	•	O(log n) time complexity for insertion and removal.
	•	Efficient memory usage compared to SortedList.
Min-Heap Implementation of Priority Queue

using System;
using System.Collections.Generic;
 
class MinHeapPriorityQueue<T> where T : IComparable<T> {
    private List<T> heap = new List<T>();
 
    private void Swap(int idx, int jdx) {
        T tempVal = heap[idx];
        heap[idx] = heap[jdx];
        heap[jdx] = tempVal;
    }
 
    public void Enqueue(T item) {
        heap.Add(item);
        int idx = heap.Count - 1;
 
        // Heapify up
        while (idx > 0) {
            int parent = (i - 1) / 2;
            if (heap[idx].CompareTo(heap[parent]) >= 0) break;
            Swap(i, parent);
            i = parent;
        }
    }
 
    public T Dequeue() {
        if (heap.Count == 0) throw new InvalidOperationException("Queue is empty");
 
        T root = heap[0];
        heap[0] = heap[^1]; // Move last element to root
        heap.RemoveAt(heap.Count - 1);
 
        // Heapify down
        int idx = 0;
        while (true) {
            int left = 2 * i + 1, right = 2 * i + 2, smallest = i;
 
            if (left < heap.Count && heap[left].CompareTo(heap[smallest]) < 0) smallest = left;
            if (right < heap.Count && heap[right].CompareTo(heap[smallest]) < 0) smallest = right;
 
            if (smallest == i) break;
            Swap(i, smallest);
            i = smallest;
        }
 
        return root;
    }
 
    public bool IsEmpty() => heap.Count == 0;
}
 
class MainProgram {
    static void Main() {
        MinHeapPriorityQueue<int> pq = new MinHeapPriorityQueue<int>();
 
        pq.Enqueue(5);
        pq.Enqueue(2);
        pq.Enqueue(8);
        pq.Enqueue(1);
 
        Console.WriteLine(/* Output */ "Dequeuing elements in priority order:");
        while (!pq.IsEmpty()) {
            Console.WriteLine(/* Output */ pq.Dequeue());
        }
    }
}
Output:
Dequeuing elements in priority order:
1
2
5
8
✅ A Min-Heap ensures the smallest element is always dequeued first.

Comparison of Implementations
Implementation
Best Use Case
Time Complexity
PriorityQueue<TElement, TPriority> (Built-in)
Simple tasks with priority-based ordering
O(log n) for enqueue/dequeue
SortedList<TPriority, Queue<TElement>>
Small datasets where sorting is manageable
O(log n) for enqueue, O(1) for dequeue
Min-Heap
Large datasets requiring efficiency
O(log n) for both enqueue and dequeue

Conclusion
	•	Priority Queues process elements based on importance rather than order.
	•	C# provides a built-in PriorityQueue<TElement, TPriority> class for easy implementation.
	•	SortedList-based and Heap-based approaches are useful for versions before .NET 6.
	•	Heaps are the most efficient for priority queue implementation.
 
5. Scenario 1: Customer Support Ticket System
Problem Statement:
A company receives customer support requests and needs to prioritize them based on urgency.
	•	High Priority (1): Critical issues (e.g., system outage).
	•	Medium Priority (2): Important issues (e.g., slow performance).
	•	Low Priority (3): General inquiries (e.g., account questions). The system should process tickets based on priority, ensuring critical issues are handled first.

Solution: Using PriorityQueue<TElement, TPriority> in C#
using System;
using System.Collections.Generic;
 
class SupportTicketSystem {
    private PriorityQueue<string, int> ticketQueue = new PriorityQueue<string, int>();
 
    public void SubmitTicket(string issue, int priority) {
        ticketQueue.Enqueue(issue, priority);
        Console.WriteLine(/* Output */ $"Ticket added: {issue} (Priority: {priority})");
    }
 
    public void ProcessTicket() {
        if (ticketQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Processing: {ticketQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No tickets to process.");
        }
    }
}
 
// Test Program
class MainProgram {
    static void Main() {
        SupportTicketSystem supportSystem = new SupportTicketSystem();
 
        supportSystem.SubmitTicket("System outage", 1);
        supportSystem.SubmitTicket("Slow performance", 2);
        supportSystem.SubmitTicket("Account inquiry", 3);
 
        Console.WriteLine(/* Output */ "\nProcessing tickets:");
        while (true) {
            supportSystem.ProcessTicket();
            if (supportSystem.ticketQueue.Count == 0) break;
        }
    }
}
Output:
Ticket added: System outage (Priority: 1)
Ticket added: Slow performance (Priority: 2)
Ticket added: Account inquiry (Priority: 3)
 
Processing tickets:
Processing: System outage
Processing: Slow performance
Processing: Account inquiry
✅ Critical issues are handled first, ensuring better customer service.

 
6. Scenario 2: Airline Check-in System
Problem Statement:
An airline check-in system prioritizes boarding based on passenger status:
	•	Priority (1): First-Class & VIP members
	•	Priority (2): Business-Class passengers
	•	Priority (3): Economy-Class passengers The system should board passengers in priority order.

Solution: Implementing a Custom Priority Queue Using SortedList
using System;
using System.Collections.Generic;
 
class AirlineCheckIn {
    private SortedList<int, Queue<string>> checkInQueue = new SortedList<int, Queue<string>>();
 
    public void CheckInPassenger(string passengerName, int priority) {
        if (!checkInQueue.ContainsKey(priority)) {
            checkInQueue[priority] = new Queue<string>();
        }
        checkInQueue[priority].Enqueue(passengerName);
        Console.WriteLine(/* Output */ $"Passenger Checked In: {passengerName} (Priority: {priority})");
    }
 
    public void BoardPassenger() {
        if (checkInQueue.Count == 0) {
            Console.WriteLine(/* Output */ "No passengers to board.");
            return;
        }
 
        int highestPriority = checkInQueue.Keys[0];
        string passenger = checkInQueue[highestPriority].Dequeue();
        Console.WriteLine(/* Output */ $"Boarding Passenger: {passenger}");
 
        if (checkInQueue[highestPriority].Count == 0) {
            checkInQueue.Remove(highestPriority);
        }
    }
}
 
// Test Program
class MainProgram {
    static void Main() {
        AirlineCheckIn airlineCheckIn = new AirlineCheckIn();
 
        airlineCheckIn.CheckInPassenger("John (VIP)", 1);
        airlineCheckIn.CheckInPassenger("Alice (Business)", 2);
        airlineCheckIn.CheckInPassenger("Bob (Economy)", 3);
 
        Console.WriteLine(/* Output */ "\nBoarding Passengers:");
        while (true) {
            airlineCheckIn.BoardPassenger();
            if (airlineCheckIn.checkInQueue.Count == 0) break;
        }
    }
}
Output:

Passenger Checked In: John (VIP) (Priority: 1)
Passenger Checked In: Alice (Business) (Priority: 2)
Passenger Checked In: Bob (Economy) (Priority: 3)
 
Boarding Passengers:
Boarding Passenger: John (VIP)
Boarding Passenger: Alice (Business)
Boarding Passenger: Bob (Economy)
✅ Passengers board based on their priority, ensuring a smooth check-in process.
 
 
7. Activity
Develop a priority queue to manage patients in the emergency department of a hospital. Patients are assigned a priority from 0 (highest) to 4 (lowest). The queue should ensure that the patients with the highest priority are seen first.












































Skip to main content
Print book
6.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
6.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:34 AM
Table of contents
	•	1. Learning outcomes
	•	2. Activity
	•	3. Practice Activities
1. Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd
   
Not signed in? Click here and then refresh this page.
2. Activity
	•	Describe the difference between a queue and a stack.
	•	Describe the difference between a queue and a priority queue.
	•	Describe the difference between a list and an array list. Which one is better and why?
3. Practice Activities
Case Study 1: Hospital Emergency Room Patient Management
Problem Statement:
In a hospital emergency room, patients are treated based on the severity of their condition. The priority levels are:
	•	Critical (Priority 1) – Life-threatening cases
	•	Serious (Priority 2) – Requires immediate medical attention
	•	Stable (Priority 3) – Can wait for treatment
The hospital must process patients in order of priority, ensuring that critical patients receive attention first.

Solution: Implementing a Priority Queue for Patient Management

using System;
using System.Collections.Generic;

class HospitalQueue {
    private PriorityQueue<string, int> patientQueue = new PriorityQueue<string, int>();

    public void AddPatient(string name, int priority) {
        patientQueue.Enqueue(name, priority);
        Console.WriteLine(/* Output */ $"Patient Added: {name} (Priority: {priority})");
    }

    public void TreatPatient() {
        if (patientQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Treating Patient: {patientQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No patients to treat.");
        }
    }
}

// Test Program
class MainProgram {
    static void Main() {
        HospitalQueue hospital = new HospitalQueue();

        hospital.AddPatient("John (Critical)", 1);
        hospital.AddPatient("Alice (Stable)", 3);
        hospital.AddPatient("Bob (Serious)", 2);

        Console.WriteLine(/* Output */ "\nTreating Patients:");
        while (true) {
            hospital.TreatPatient();
            if (hospital.patientQueue.Count == 0) break;
        }
    }
}
Output:
Patient Added: John (Critical) (Priority: 1)
Patient Added: Alice (Stable) (Priority: 3)
Patient Added: Bob (Serious) (Priority: 2)

Treating Patients:
Treating Patient: John (Critical)
Treating Patient: Bob (Serious)
Treating Patient: Alice (Stable)
✅ Critical patients are treated first, ensuring efficient medical care.

Case Study 2: Job Scheduling in an Operating System
Problem Statement:
An operating system schedules processes based on priority:
	•	Priority 1: System processes
	•	Priority 2: User applications
	•	Priority 3: Background tasks
The OS must process higher-priority jobs first.

Solution: Using a Custom Priority Queue
using System;
using System.Collections.Generic;

class JobScheduler {
    private SortedList<int, Queue<string>> jobQueue = new SortedList<int, Queue<string>>();

    public void AddJob(string jobName, int priority) {
        if (!jobQueue.ContainsKey(priority)) {
            jobQueue[priority] = new Queue<string>();
        }
        jobQueue[priority].Enqueue(jobName);
        Console.WriteLine(/* Output */ $"Job Added: {jobName} (Priority: {priority})");
    }

    public void ExecuteJob() {
        if (jobQueue.Count == 0) {
            Console.WriteLine(/* Output */ "No jobs to execute.");
            return;
        }

        int highestPriority = jobQueue.Keys[0];
        string job = jobQueue[highestPriority].Dequeue();
        Console.WriteLine(/* Output */ $"Executing Job: {job}");

        if (jobQueue[highestPriority].Count == 0) {
            jobQueue.Remove(highestPriority);
        }
    }
}

// Test Program
class MainProgram {
    static void Main() {
        JobScheduler scheduler = new JobScheduler();

        scheduler.AddJob("System Update", 1);
        scheduler.AddJob("User App Execution", 2);
        scheduler.AddJob("Background Sync", 3);

        Console.WriteLine(/* Output */ "\nExecuting Jobs:");
        while (true) {
            scheduler.ExecuteJob();
            if (scheduler.jobQueue.Count == 0) break;
        }
    }
}
Output:
Job Added: System Update (Priority: 1)
Job Added: User App Execution (Priority: 2)
Job Added: Background Sync (Priority: 3)

Executing Jobs:
Executing Job: System Update
Executing Job: User App Execution
Executing Job: Background Sync
✅ System-critical jobs run before background tasks.

Case Study 3: Parcel Delivery System
Problem Statement:
A courier company prioritizes deliveries based on urgency:
	•	Priority 1: Express deliveries
	•	Priority 2: Standard deliveries
	•	Priority 3: Economy deliveries
The system must ensure express parcels are delivered first.

Solution: Implementing Priority Queue for Delivery
using System;
using System.Collections.Generic;

class ParcelDelivery {
    private PriorityQueue<string, int> deliveryQueue = new PriorityQueue<string, int>();

    public void AddParcel(string parcel, int priority) {
        deliveryQueue.Enqueue(parcel, priority);
        Console.WriteLine(/* Output */ $"Parcel Added: {parcel} (Priority: {priority})");
    }

    public void DeliverParcel() {
        if (deliveryQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Delivering: {deliveryQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No parcels to deliver.");
        }
    }
}

// Test Program
class MainProgram {
    static void Main() {
        ParcelDelivery deliverySystem = new ParcelDelivery();

        deliverySystem.AddParcel("Express Parcel A", 1);
        deliverySystem.AddParcel("Standard Parcel B", 2);
        deliverySystem.AddParcel("Economy Parcel C", 3);

        Console.WriteLine(/* Output */ "\nDelivering Parcels:");
        while (true) {
            deliverySystem.DeliverParcel();
            if (deliverySystem.deliveryQueue.Count == 0) break;
        }
    }
}
Output:

Parcel Added: Express Parcel A (Priority: 1)
Parcel Added: Standard Parcel B (Priority: 2)
Parcel Added: Economy Parcel C (Priority: 3)

Delivering Parcels:
Delivering: Express Parcel A
Delivering: Standard Parcel B
Delivering: Economy Parcel C
✅ Urgent parcels are delivered first, ensuring timely service.

Case Study 4: Stock Market Order Processing
Problem Statement:
A stock exchange processes buy/sell orders based on priority:
	•	Priority 1: Market Orders (executed immediately)
	•	Priority 2: Limit Orders (executed at a set price)
	•	Priority 3: Stop Orders (triggered later)
The system ensures real-time order execution.

Solution: Stock Order Processing with Priority Queue

using System;
using System.Collections.Generic;

class StockOrderSystem {
    private PriorityQueue<string, int> orderQueue = new PriorityQueue<string, int>();

    public void PlaceOrder(string order, int priority) {
        orderQueue.Enqueue(order, priority);
        Console.WriteLine(/* Output */ $"Order Placed: {order} (Priority: {priority})");
    }

    public void ProcessOrder() {
        if (orderQueue.Count > 0) {
            Console.WriteLine(/* Output */ $"Processing Order: {orderQueue.Dequeue()}");
        } else {
            Console.WriteLine(/* Output */ "No orders to process.");
        }
    }
}

// Test Program
class MainProgram {
    static void Main() {
        StockOrderSystem stockSystem = new StockOrderSystem();

        stockSystem.PlaceOrder("Market Order: Buy 100 Shares", 1);
        stockSystem.PlaceOrder("Limit Order: Buy at $50", 2);
        stockSystem.PlaceOrder("Stop Order: Sell if Price Falls", 3);

        Console.WriteLine(/* Output */ "\nProcessing Orders:");
        while (true) {
            stockSystem.ProcessOrder();
            if (stockSystem.orderQueue.Count == 0) break;
        }
    }
}
Output:

Order Placed: Market Order: Buy 100 Shares (Priority: 1)
Order Placed: Limit Order: Buy at $50 (Priority: 2)
Order Placed: Stop Order: Sell if Price Falls (Priority: 3)

Processing Orders:
Processing Order: Market Order: Buy 100 Shares
Processing Order: Limit Order: Buy at $50
Processing Order: Stop Order: Sell if Price Falls
✅ Market orders are executed first for real-time trading.

Conclusion
These four case studies demonstrate how Priority Queues improve efficiency in different real-world applications.



















Skip to main content
Print book
7.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
7.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:35 AM
Table of contents
	•	1. Learning outcomes
	•	2. Case Study
	•	3. Hashing
	•	3.1. Hash Tables
	•	3.2. Dictionaries
	•	3.3. Sorted Dictionaries
	•	3.4. Hash Sets
	•	3.5. Sorted Sets
1. Learning outcomes
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). Dictionaries and Sets, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p115-p143
  
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Case Study
Clothing One Ltd is a department shop that sells many different products. They need to have a system that stores information about the different products they sell. This system must be able to retrieve information quickly, as it is used by the point-of-sale computers to retrieve price information, when customers checkout. The company uses hashing for this. Each product is assigned a unique identification number, that can be represented using a barcode. When a user scans the barcode, the computer reads in the unique identifier number, and queries this in the data system. The computer then returns the relevant product information.
3. Hashing
The idea behind hashing is that an input value is used to obtain some output value. The input  value is know as a key. The output value is known as a value. Together, they are commonly called a key-value pair. A hashing algorithm is then used to map the key to its corresponding value. These values are present in a structure known as buckets. The key doesn’t map to the value itself, rather it maps to a bucket, in which the value is stored. This allows users to retrieve elements from the data structure like they do in arrays, except with hashing, a key is used instead of an index.
 
The image below shows keys being mapped to values, present in buckets, with a hash function.
Ideally, each bucket will only have one key pointing to it, however, implementing such a system is often complex. Realistically, buckets will have multiple keys pointing to them. Such an event is known as a hash collision. When this occurs, values are stored in arrays, lists or binary trees (or another suitable data structure) within the bucket. A separate search must then be done to retrieve the value corresponding to the key. A key will only ever point to one bucket.
 
Hashing functions can be complicated, or as simple as a modulus operation. Here is a visualisation of hashing done using modulus[1].
 
As values are retrieved using a key, hashing offers a best and worst case retrieval, insertion and deletion time of O(1). However, in a worst case scenario, when extreme hash collisions takes place, and all elements are present in a single bucket, hashing will offer a worst case retrieval, insertion and deletion of O(n).
 

[1] Open Hashing visualization (2024). https://www.cs.usfca.edu/~galles/visualization/OpenHash.html.
3.1. Hash Tables
Hashing algorithms can be complicated to implement. Fortunately, C# includes a few data structures based on hashing. HashTable is a non-generic data structure, which means values can be any type. The documentation[1] and implementation[2] can be found on the Microsoft website.
 

[1] Dotnet-Bot (2024) Hashtable Class (System.Collections). https://learn.microsoft.com/en-us/dotnet/api/system.collections.hashtable?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#mscorlib/system/collections/hashtable.cs,10fefb6e0ae510dd.
3.2. Dictionaries
Dictionaries are another hash implementation offered by C#. It is a generic alternative to HashTable, and it is recommended to use this over HashTable. The documentation[1] and implementation[2] can be found on the Microsoft website.
 

[1] Dotnet-Bot (2024) Dictionary Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#mscorlib/system/collections/generic/dictionary.cs,d3599058f8d79be0.
3.3. Sorted Dictionaries
SortedDictionary is a class that, to the user, acts like a dictionary, and keeps its keys always sorted. The documentation[1] and implementation[2] can be viewed on the Microsoft website. While having keys always sorted can be advantageous in certain scenarios, sorted dictionaries have the disadvantage of slow performance, having a retrieval, insertion and deletion time of O(logn).
 

[1] Dotnet-Bot (2024) SortedDictionary Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.sorteddictionary-2?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#System/compmod/system/collections/generic/sorteddictionary.cs,ba6f0c7de63e2c74.
3.4. Hash Sets
A set is a data structure that stores a single type (generic) of data. Unlike HashTable and Dictionary, a set only requires a single value, not a key-value pair. Each element in a sett must be unique. It is useful for performing mathematical operations such as unions, intersections, subtractions, etc. The documentation[1] and implementation[2] for HashSets can be viewed on the Microsoft website.
 

[1] Dotnet-Bot (2024) HashSet Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#System.Core/System/Collections/Generic/HashSet.cs,50c894a3f7ad7bd0.
3.5. Sorted Sets
Much like with SortDictionary, HashSets have a sorted equivalent, SortedSet. This performs similarly to HashSet, except that the elements are always sorted. The documentation[1] and C# implementation[2] can be viewed on the Microsoft website.
 

[1] Dotnet-Bot (2024) SortedSet Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.sortedset-1?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#System/compmod/system/collections/generic/sortedset.cs,bae1c41b842726a2.
































Skip to main content
Print book
8.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
8.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:35 AM
Table of contents
	•	1. Learning outcomes
	•	2. Case Study
	•	3. Binary Trees
	•	4. Tree Traversal
	•	4.1. Pre-order
	•	4.2. Post-order
	•	4.3. In-order
	•	5. Binary Search Trees
	•	6. AVL Trees
	•	7. Red-Black Trees
	•	8. Binary Heaps
	•	8.1. Min-Heap
	•	8.2. Max-Heap
1. Learning outcomes
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). Variants of Trees, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p145-p200
  
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Case Study
In a word processing application, users often require an efficient and accurate spell checker to detect and correct spelling errors in their documents. Binary trees can be utilized to implement a dictionary data structure for storing valid words, enabling fast and accurate spell checking functionality.
3. Binary Trees
So far, we have looked at unitary data structures, such as linked-lists, which is made up of nodes that are linked together, where each node will have at most 2 connections: forwards and backwards. There are data structures that allow for nodes to more than 2 connections. One such example is a tree structure.
 
In a tree structure, a node is connected to one or more child nodes. The node at the beginning of the tree, with no parent node is called the root. The nodes at the end of the tree, with no children nodes are called leaves. Nodes that share a parent are known as siblings. We will only look at a type of tree called a binary tree in this module, where every node can have at most 2 child nodes.
 
In the image below, node 1 is the root, whilst nodes 5, 6 and 3 are leaves. Note how the structure branches out from the root.

4. Tree Traversal
When iterating through a unitary structure, such as a linked-list, we just proceed in either a forward or backward direction, as there is only one path. However, with binary trees, the structure is more complicated, thus, there are multiple paths to choose when iterating.
 
There are 3 ways for traversing a binary tree: pre-order, post-order and in-order.
4.1. Pre-order
In pre-order traversal, the root is visited first, followed by the left child node. The next left child node is visited until there is no left child node (a recursive operation), in which case, the right child node is visited, and we reverse up the tree[1].
 
The image below shows you pre-order traversal. The numArray represent the order in which the nodes are visited.  
 

[1] GeeksforGeeks (2023a) Preorder traversal of binary tree. https://www.geeksforgeeks.org/preorder-traversal-of-binary-tree/.
4.2. Post-order
In post-order traversal, the left child is visited first (recursively), followed by the right child, and then the root is visited last.[1]
 
The image below shows you post-order traversal. The numArray represent the order in which the nodes are visited.
 
 

[1] GeeksforGeeks (2023a) Postorder traversal of binary tree. https://www.geeksforgeeks.org/postorder-traversal-of-binary-tree/.
4.3. In-order
In in-order traversal, we visit the left child node first (recursively), then visit its parent, then visit the right child node.[1]
 
The image below shows you in-order traversal. The numArray represent the order in which the nodes are visited.
 

[1] GeeksforGeeks (2023a) Inorder traversal of binary tree. https://www.geeksforgeeks.org/inorder-traversal-of-binary-tree/.
5. Binary Search Trees
Regular binary trees do not specify any relationship between the values of nodes. When searching for an element, in the worst case, we must traverse the entire tree, leading to a time complexity of O(n).
 
We can specify rules in a binary tree:
	•	The value of a node’s left child must be smaller than it.
	•	The value of a node’s right child must be larger than it. 
 
The rules above must hold true for every node. When these rules are implemented, the tree becomes sorted, and such a tree is called a binary search tree.
 
This is advantageous because this allows us to perform a binary search. When searching for an element in a binary search tree, we compare the value with that of the node, and one of 3 outcomes will be produced:
	•	The values are equal: in which case, the element has been found.
	•	The value is less than the node: in which case we search the left node.
	•	The value is greater than the node: in which case we search the right node. 
 
This search is done recursively. If a left or right node doesn’t exist (or is null), it means we have reached the end of the tree and the element does not exist.
 
Let us look at the diagram below:

 
Suppose we are searching for 20:
	•	We compare 20 with the first node: 20 < 45, so we proceed to the left child.
	•	We compare 20 with the node: 20 > 15, so we proceed to the right child.
	•	We compare 20 with the node: 20 == 20. The element has been found. 
Suppose we are searching for 51:
	•	We compare 51 with the first node: 51 > 45, so we proceed to the right node.
	•	We compare 51 with the node: 51 < 79, so we proceed to the left node.
	•	We compare 51 to the node: 51 < 55, so we proceed to the left node.
	•	We compare 51 to the node: 51 > 50, so we proceed to the right node.
	•	The node is null (it does not exist). We have reached the end of the tree. Therefore, 51 does not exist. 
From the tree above, we see that at every subtree, half of the subtree gets discarded after a comparison is made, which does not need to be searched. This gives binary search a O(logn) lookup time. You can find a useful visualisation on the University of San Francisco website[1].
 

[1] Binary Search Tree Visualization (2024). https://www.cs.usfca.edu/~galles/visualization/BST.html.
6. AVL Trees
One of the issues with binary search trees is that its structure depends on when elements are added and removed. A tree created with the insertion of [1,2,3] will look different than a tree with the insertion of [2,1,3], even though they have the same elements. An extreme problem occurs when each node only has a left node or each node only has a right node. This refers to the balance of a tree.
 
The following image shows an unbalanced tree where each node only has a right child node.  
When this occurs, we cannot benefit from binary search, since the structure becomes unitary. The lookup time will become O(n).
 
To solve this, we need an algorithm that balances trees for us, or trees that will balance themselves. Such a tree is called an AVL tree[1], named after its inventors, Adelson-Velsky and Landis.
 
In AVL trees, the height (distance from leaf to root) between leave nodes is allowed to differ by at most 1 level. If the tree breaks this rule, rotations to subtrees are made until the tree is in compliance with this rule. AVL trees are a special type of binary search tree, so it must comply with binary search tree rules as well. The University of San Francisco has a useful visualisation[2].
 

[1] GeeksforGeeks (2023a) AVL Tree Data Structure. https://www.geeksforgeeks.org/introduction-to-avl-tree/.
[2] AVL Tree Visualzation (2024). https://www.cs.usfca.edu/~galles/visualization/AVLtree.html.
7. Red-Black Trees
Red-black trees[1] are another special type of binary search tree that is self-balanced. Each node is assigned a colour, either red or black. It follows the following rules:
	•	Nodes with values cannot be leave nodes (leaf nodes must be null)
	•	Both children of red nodes must be black
	•	Every path from the root to any leaf must have the same number of black nodes. 
 
The self-balancing feature allows Red-Black trees to maintain the same time complexity as AVL trees. In practice, however, AVL trees perform faster in retrieval operations as they are stricter about balancing. Red-black trees perform better in insertion and deletion as these are less complicated than in AVL trees.
 
The University of San Franciso has a useful visualisation[2].
 

[1] GeeksforGeeks (2023b) Introduction to Red Black Tree. https://www.geeksforgeeks.org/introduction-to-red-black-tree/.
[2] Red/Black tree visualization (2024). https://www.cs.usfca.edu/~galles/visualization/RedBlack.html.
8. Binary Heaps
Heaps are a type of binary tree (note, not binary search tree) that maintains a relationship between the child and parent node. There are two types of binary heaps: min-heap and max-heap.
8.1. Min-Heap
In a min-heap, parent nodes are smaller than their child nodes. The root node contains the minimum value.

8.2. Max-Heap
In a max-heap, parent nodes are larger than their child nodes. The root node contains the maximum value.





















Skip to main content
Print book
9.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
9.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:36 AM
Table of contents
	•	1. Learning outcomes
	•	2. Relevance Connection
	•	3. Sorting
	•	3.1. Selection Sort
	•	3.2. Insertion Sort
1. Learning outcomes
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). Arrays and Lists, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p48-p60
  
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Relevance Connection
Find 5 examples of when sorting data structures is required.
3. Sorting
Sorting is a method of arranging a list or array in a specific order, either ascending or descending. There are many different types of sorting algorithms, that work in different ways, which gives characteristics that may be beneficial or even negative in certain circumstances.
 
Time complexity is an important description of algorithms that describes the amount of time taken by an algorithm, by focusing on the number of operations required, that is independent of computer hardware. Sorting algorithms are often compared to each other using their time complexity.
 
Space complexity describes the amount of space required by an algorithm. The space complexity, in particular, mentioned here describes auxiliary space, i.e. additional space required by the sorting algorithm, excluding the array itself. This is an important descriptor when a sorting algorithm is required for a space constrain environment.
 
Sorting stability describes how a sorting algorithm will treat elements that are equal in value. A stable algorithm will maintain the order of equal items, relative to each other. An unstable algorithm is not guaranteed to maintain the order of equal items relative to each other.
3.1. Selection Sort
Selection Sort has been known long before the invention of modern computers and cannot be attributed to a single inventor. However, computer scientists have developed many variants over time. Heapsort is a popular example invented by JWJ Williams in 1964[1]. In the same paper, he also proposed the heap data structure, which we looked at last week.
 
In Selection Sort, the array can be categorised into 2 parts: sorted and unsorted. In each iteration, the smallest element (for ascending order) or largest element (for descending order) in the unsorted part is found and this element is then swapped with the leftmost unsorted element in the array.
 
The algorithm has a best-case, average-case and worst-case time complexity of .
 
Sorting can be done in-place, therefore the worst-case space complexity is .
 
Selection sort is not stable.
 
Virginia Tech has a useful visualisation tool for Selection Sort[2].
 

[1] Williams, J. (1964) 'Algorithm 232 : HEAPSORT,' Communications of the ACM, 7, pp. 347–348. https://ci.nii.ac.jp/naid/10010193304.
[2] Selection sort visualization (2024). https://opendsa-server.cs.vt.edu/embed/selectionsortAV.
3.2. Insertion Sort
Insertion sort predates modern computers and been in use in non-computer scenarios for a long time. However, many optimisations have been made by computer scientists. A popular example is a variant of Insertion Sort, called Shell Sort, developed by Donald Shell in 1959[1].
 
In Insertion Sort, the array can be categorised into 2 parts: sorted and unsorted. In each iteration, the algorithm will find a suitable position of an element, relative to elements already in the sorted section of the array.
 
Its best-case time complexity is . This occurs when the list is already sorted.
 
Its average and worst-case time complexity is . The worst-case scenario occurs when the array is in reverse order.
 
Sorting can be done in-place iteratively, therefore, Insertion Sort has a worst-case space complexity of .
 
Insertion Sort is also stable.
 
Virginia Tech has a useful visualisation tool for Insertion Sort[2].
 

[1] Shell, D.L. (1959) 'A high-speed sorting procedure,' Communications of the ACM, 2(7), pp. 30–32. https://doi.org/10.1145/368370.368387.
[2] Insertion sort visualization (2024). https://opendsa-server.cs.vt.edu/OpenDSA/AV/Sorting/insertionsortAV.html.



Skip to main content
Print book
10.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
10.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:36 AM
Table of contents
	•	1. Learning outcomes
	•	2. Relevance Connection
	•	3. Bubble Sort
	•	4. Quicksort
1. Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). Arrays and Lists, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p48-p60
  
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Relevance Connection
We will continue investigating sorting, We have looked at 2 types of sorting, research at least 3 more types of sorting.
3. Bubble Sort
The sorting algorithm was published in 1956 by Edward Harry Friend[1]. Due to its inefficiency, it is not in common use in real world scenarios, however, as it is a very simple algorithm, it is used in educational contexts.
 
In the algorithm, a “bubble” consists of 2 adjacent elements. If the elements in the bubble are in the incorrect order relative to each other, they are swapped. If they are in the correct order, their order is maintained. The bubble then steps 1 element forward and the algorithm is repeated. The algorithm will stop when the iteration counter reaches  However, an improvement can be made to the algorithm to stop when no swaps are made in an iteration, as this implies that the array is sorted.
 
Its best-case time complexity is . This occurs when the list is already sorted.
Its average and worst-case time complexity is . The worst-case scenario occurs when the array is in reverse order.
 
As Bubble Sort is an in-place iterative sorting algorithm, its worst-case space complexity is 
.
Another advantage of the algorithm is that it is stable.
 
Virginia Tech has a useful visualisation tool for Bubble Sort[2].
 

[1] Friend, E.H. (1956) 'Sorting on electronic computer systems,' Journal of the ACM, 3(3), pp. 134–168. https://doi.org/10.1145/320831.320833.
[2] Bubble Sort Visualization (2024). https://opendsa-server.cs.vt.edu/embed/bubblesortAV.
4. Quicksort
This sorting algorithm was published in 1961 by Tony Hoare[1], and is in common use today as it is efficient.
It follows the divide and conquer paradigm. A pivot element is selected in the array. Elements are then partitioned into two subarrays depending on whether they are greater than or less than the pivot. The subarrays are then sorted recursively.
 
It’s best and average case time complexity is . The best-case scenario occurs when the subarrays are equal in length in each recursive call (when the pivots are the median value).
its worst -case time complexity is This occurs when a subarray is size  in length in each recursive call (when the pivots are either the smallest or largest value).
 
An advantage to this type of sorting is that is can be done in place. It has a worst-case space complexity of , due to stack space requirement of the recursive calls made by the algorithm.
 
A disadvantage of Quicksort is that it is not stable.
 
Virginia Tech has a useful visualisation tool for Quicksort[2].
 

[1] Hoare, C. a. R. (1961) 'Algorithm 64: Quicksort,' Communications of the ACM, 4(7), p. 321. https://doi.org/10.1145/366622.366644.
[2] Quicksort Visualization (2024). https://opendsa-server.cs.vt.edu/embed/quicksortAV.



















Skip to main content
Print book
11.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
11.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:37 AM
Table of contents
	•	1. Learning outcomes
	•	2. Exploring Graphs
	•	3. Search Algorithms
1. Learning outcomes

By the end of this topic you should be able to:
learn graphs concepts, its application, adjacency list and matrix, node, edge and graph implementation, depth-first search and breadth-first search, application of Kruskal's and Prim's algorithms, as well as colouring and shortest path.
 

Prescribed Reading
Jamro, M., 2018. C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd. 
Page 202 – 257.  
Time Allocation:
2 Hours
 
2. Exploring Graphs

Adjacency list: An adjacency list represents a graph as an array of linked lists. The index of the array represents a vertex and each element in its linked list represents the other vertices that form an edge with the vertex.
Depth-first search (DFS) is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking. Extra memory, usually a stack, is needed to keep track of the nodes discovered so far along a specified branch which helps in backtracking of the graph.
Breadth-first search (BFS) is an algorithm for searching a tree data structure for a node that satisfies a given property. It starts at the tree root and explores all nodes at the present depth prior to moving on to the nodes at the next depth level. Extra memory, usually a queue, is needed to keep track of the child nodes that were encountered but not yet explored.
3. Search Algorithms

Search Algorithms: There are many types of search algorithms including Kruskal and Prim
Kruskal's algorithm is a minimum spanning tree algorithm that takes a graph as input and finds the subset of the edges of that graph which
	•	 form a tree that includes every vertex
	•	has the minimum sum of weights among all the trees that can be formed from the graph
Prim’s algorithm always starts with a single node, and it moves through several adjacent nodes, to explore all of the connected edges along the way. The idea behind Prim’s algorithm is simple, a spanning tree means all vertices must be connected. So, the two disjoint subsets of vertices must be connected to make a Spanning Tree.
Skip to main content
Print book
12.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
12.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:38 AM
Table of contents
	•	1. Learning outcomes
	•	2. Stack
	•	3. Queue
1. Learning outcomes

By the end of this topic you should be able to:c
you will learn about classification of data structures. Also, the diversity of some real-world applications in relation to arrays, lists, stacks, queues, dictionaries, sets, trees, heaps and graphs will be treated.
 

Prescribed Reading
Jamro, M., 2018. C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd. 
Page 258 – 269. 
Time Allocation:
2 Hours
 
2. Stack

 
Stack is a special type of collection that stores elements in LIFO style (Last In First Out). C# includes the generic Stack<T> and non-generic Stack collection classes. It is recommended to use the generic Stack<T> collection.
 
Stack is useful to store temporary data in LIFO style, and you might want to delete an element after retrieving its value.
 
Stack<T> Characteristics
Stack<T> is Last In First Out collection.
It comes under System.Collection.Generic namespace.
Stack<T> can contain elements of the specified type. It provides compile-time type checking and doesn't perform boxing-unboxing because it is generic.
Elements can be added using the Push() method. Cannot use collection-initializer syntax.
Elements can be retrieved using the Pop() and the Peek() methods. It does not support an indexer.
3. Queue

Queue represents a first-in, first out (FIFO) collection of object. It is used when you need a first-in, first-out access of items. When you add an item in the list, it is called enqueue, and when you remove an item, it is called dequeue . This class comes under System.Collections namespace and implements ICollection, IEnumerable, and ICloneable interfaces.
 Characteristics of Queue Class:
Enqueue adds an element to the end of the Queue.
Dequeue removes the oldest element from the start of the Queue.
Peek returns the oldest element that is at the start of the Queue but does not remove it from the Queue.
The capacity of a Queue is the number of elements the Queue can hold.
As elements are added to a Queue, the capacity is automatically increased as required by reallocating the internal array.
Queue accepts null as a valid value for reference types and allows duplicate elements.

















Skip to main content
Print book
13.1. Notes
Site:
Eduvos LMS
Course:
Data Structures and Algorithms in C#
Book:
13.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:38 AM
Table of contents
	•	1. Learning outcomes
	•	2. Collaborative Project / Case Study / Relevance Connection:
	•	3. Creating String Object
1. Learning outcomes

By the end of this topic you should be able to:
you will explore strings, strings operations, operations for manipulating strings, strings concatenation, switching to uppercase and lowercase letters, searching for a string within another string, extracting a portion of a string, splitting the string by a separator, replacing a substring, and regular expressions.
 

Prescribed Reading
Introduction to Programming with C# / Java Books » Chapter 13. Strings and Text Processing (introprogramming.info).
Time Allocation:
4 Hours
 
2. Collaborative Project / Case Study / Relevance Connection:

A string is an object of type String whose value is text. Internally, the text is stored as a sequential read-only collection of Char objects. There's no null-terminating character at the end of a C# string; therefore a C# string can contain any number of embedded null characters ('\0'). The Length property of a string represents the number of Char objects it contains, not the number of Unicode characters. To access the individual Unicode code points in a string, use the StringInfo object.
In C#, string is an object of System.String class that represent sequence of characters. We can perform many operations on strings such as concatenation, comparision, getting substring, search, trim, replacement etc. 
3. Creating String Object

Creating a String Object
You can create string object using one of the following methods −
	•	By assigning a string literal to a String variable
	•	By using a String class constructor
	•	By using the string concatenation operator (+)
	•	By retrieving a property or calling a method that returns a string
	•	By calling a formatting method to convert a value or an object to its string representation
Skip to main content
Print book
3.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
3.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:50 AM
Table of contents
	•	Learning outcomes
	•	1.3 Our First C# Program
	•	1.3.1 How Does Our First C# Program Work?
	•	1.3.2 Keywords
	•	1.4 Datatypes and Operators
	•	1.4.1 Datatypes
	•	1.4.1.1 Integer Types
	•	1.4.1.2 Real Floating-Point Types
	•	1.4.1.3 Boolean Type
	•	1.4.1.4 Character Type
	•	1.4.1.5 String Type
	•	1.4.1.6 Object Type
	•	1.4.2 Operators
	•	1.4.2.1 Arithmetic Operators
	•	1.4.2.2 Assignment Operators
	•	1.4.2.3 Comparison Operators
	•	1.4.2.4 Logical Operators
	•	1.4.2.5 Bitwise Operators
	•	1.4.2.6 Type Conversion
Learning outcomes
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 1, 2 & 3
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
1.3 Our First C# Program
Before we continue with an in-depth description of the C# language and the .NET platform, let’s take a look at a simple example, illustrating how a program written in C# looks like:
 
Code Example
class HelloCSharp 
{ 
static void Main(string[] args) 
{ 
System.Console.WriteLine(/* Output */ "Hello C#!");
 } 
 
 
The only thing this program does is to print the message "Hello, C#!" on the default output. It is still early to execute it, which is why we will only take a look at its structure. Later we will describe in full how to compile and run a given program from the command prompt as well as from a development environment. 
1.3.1 How Does Our First C# Program Work?
Our first program consists of three logical parts:
	•	Definition of a class HelloCSharp;
	•	Definition of a method Main();
	•	Contents of the method Main().
Defining a Class 
On the first line of our program we define a class called HelloCSharp. The simplest definition of a class consists of the keyword class, followed by its name. In our case the name of the class is HelloCSharp. The content of the class is located in a block of program lines, surrounded by curly brackets: {}. 
Defining the Main() Method 
On the third line we define a method with the name Main(), which is the starting point for our program. Every program written in C# starts from a Main() method with the following title (signature):
static void Main(string[] args) 
The method must be declared as shown above, it must be static and void, it must have a name Main and as a list of parameters it must have only one parameter of type array of string. In our example the parameter is called args but that is not mandatory. This parameter is not used in most cases so it can be omitted (it is optional). In that case the entry point of the program can be simplified and will look like this:
static void Main() 
If any of the aforementioned requirements is not met, the program will compile but it will not start because the starting point is not defined correctly. 
Contents of the Main() Method 
The content of every method is found after its signature, surrounded by opening and closing curly brackets. On the next line of our sample program we use the system object System.Console and its method WriteLine() to print a message on the default output (the console), in this case "Hello, C#!". 
In the Main() method we can write a random sequence of expressions and they will be executed in the order we assigned to them.
1.3.2 Keywords
C# uses the following keywords to build its programming constructs: 
abstract
as
base
bool
break
byte
case
catch
char
checked
class
const
continue
decimal
default
delegate
do
double
else
enum
event
explicit
extern
false
finally
fixed
float
for
foreach
goto
if
implicit
in
int
interface
internal
is
lock
long
namespace
new
null
object
operator
out
override
params
private
protected
public
readonly
ref
return
sbyte
sealed
short
sizeof
stackalloc
static
string
struct
switch
this
throw
true
try
typeof
uint
ulong
unchecked
unsafe
ushort
using
virtual
void
volatile
while
 
 
Since the creation of the first version of the C# language, not all keywords are in use. Some of them were added in later versions. The main program elements in C# (which are defined and used with the help of keywords) are classes, methods, operators, expressions, conditional statements, loops, data types, exceptions and few others. In the next few chapters of this book, we will review in details all these programming constructs along with the use of the most of the keywords from the table above
1.4 Datatypes and Operators
In this section we will discuss the various datatypes and operators in C#.  We will familiarize what they are and how to work with them. First we will consider the data types – integer types, real types with floating-point, Boolean, character, string, and object type. We will continue with the variables, with their characteristics, how to declare them, how they are assigned a value and what a variable initialization is.  Finally, we will get acquainted with the operators in C# and the actions they can perform when used with the different data types.
1.4.1 Datatypes
Data types are sets (ranges) of values that have similar characteristics. For instance byte type specifies the set of integers in the range of [0 … 255]. Data types are characterized by Name (for example, int), Size (how much memory they use)- for example, 4 bytes, and Default value (for example 0). 
Basic data types in C# are distributed into the following types:
-       Integer types – sbyte, byte, short, ushort, int, uint, long, ulong;
-       Real floating-point types – float, double;
-       Real type with decimal precision – decimal;
-       Boolean type – bool;
-       Character type – char;
-       String – string;
-       Object type – object. 
These data types are called primitive (built-in types), because they are embedded in C# language at the lowest level. We now discuss each of the primitive datatypes.
1.4.1.1 Integer Types
Integer types represent integer numArray and are sbyte, byte, short, ushort, int, uint, long and ulong. Let’s examine them one by one. 
 
The sbyte type is an 8-bit signed integer. This means that the number of possible values for it is 28, i.e. 256 values altogether, and they can be both, positive and negative. The minimum value that can be stored in sbyte is SByte.MinValue = -128 (-27), and the maximum value is SByte.MaxValue = 127 (27-1). The default value is the number 0. 
 
The byte type is an 8-bit unsigned integer type. It also has 256 different integer values (28) that can only be nonnegative. Its default value is the number 0. The minimal taken value is Byte.MinValue = 0, and the maximum is Byte.MaxValue = 255 (28-1). 
 
The short type is a 16-bit signed integer. Its minimal value is Int16.MinValue = -32768 (-215), and the maximum is Int16.MaxValue = 32767 (215-1). The default value for short type is the number 0. 
 
The ushort type is 16-bit unsigned integer. The minimum value that it can store is UInt16.MinValue = 0, and the minimum value is – UInt16.MaxValue = 65535 (216-1). Its default value is the number 0. 
 
The next integer type that we will consider is int. It is a 32-bit signed integer. As we can notice, the growth of bits increases the possible values that a type can store. The default value for int is 0. Its minimal value is Int32.MinValue = -2,147,483,648 (-231), and its maximum value is Int32.MaxValue = 2,147,483,647 (231-1).
 
The int type is the most often used type in programming. Usually programmers use int when they work with integers because this type is natural for the 32-bit microprocessor and is sufficiently "big" for most of the calculations performed in everyday life. 
 
The uint type is 32-bit unsigned integer type. Its default value is the number 0u or 0U (the two are equivalent). The 'u' letter indicates that the number is of type uint (otherwise it is understood as int). The minimum value that it can take is UInt32.MinValue = 0, and the maximum value is UInt32.MaxValue = 4,294,967,295 (232-1).
The long type is a 64-bit signed type with a default value of 0l or 0L (the two are equivalent but it is preferable to use 'L' because the letter 'l' is easily mistaken for the digit one '1'). The 'L' letter indicates that the number is of type long (otherwise it is understood int). The minimal value that can be stored in the long type is Int64.MinValue = -9,223,372,036,854,775,808 (-263) and its maximum value is Int64.MaxValue = 9,223,372,036,854, 775,807 (263-1). 
 
The biggest integer type is the ulong type. It is a 64-bit unsigned type, which has as a default value – the number 0u, or 0U (the two are equivalent). The suffix 'u' indicates that the number is of type ulong (otherwise it is understood as long). The minimum value that can be recorded in the ulong type is UInt64.MinValue = 0 and the maximum is UInt64.MaxValue = 18,446,744,073,709,551,615 (264-1).
 
Integer Types – Example 
 
Consider an example in which we declare several variables of the integer types we know, we initialize them and print their values to the console:
Code Example
// Declare some variables 
byte centuries = 20; 
ushort years = 2000; 
uint days = 730480; 
ulong hours = 17531520; 
// Print the result on the console 
Console.WriteLine(/* Output */ centuries + " centuries are " + years + 
" years, or " + days + " days, or " + hours + " hours."); 
 
// Console output: 
// 20 centuries are 2000 years, or 730480 days, or 17531520 
// hours. 
ulong maxIntValue = UInt64.MaxValue; 
Console.WriteLine(/* Output */ maxIntValue); // 18446744073709551615 
 
1.4.1.2 Real Floating-Point Types
Real types in C# are the real numArray we know from mathematics. They are represented by a floating-point according to the standard IEEE 754 and are float and double. Let’s consider in details these two data types and understand what their similarities and differences are. 
Real Type Float 
The first type we will consider is the 32-bit real floating-point type float. It is also known as a single precision real number. Its default value is 0.0f or 0.0F (both are equivalent). The character 'f' when put at the end explicitly indicates that the number is of type float (because by default all real numArray are considered double). More about this special suffix we can read bellow in the "Real Literals" section. The considered type has accuracy up to seven decimal places (the others are lost). For instance, if the number 0.123456789 is stored as type float it will be rounded to 0.1234568. The range of values, which can be included in a float type (rounded with accuracy of 7 significant decimal digits), range from ±1.5 × 10-45 to ±3.4 × 1038. 
 
Special Values of the Real Types 
The real data types have also several special values that are not real numArray but are mathematical abstractions: 
- Negative infinity -∞ (Single.NegativeInfinity). It is obtained when for instance we are dividing -1.0f by 0.0f. 
- Positive infinity +∞ (Single.PositiveInfinity). It is obtained when for instance we are dividing 1.0f by 0.0f. 
- Uncertainty (Single.NaN) – means that an invalid operation is performed on real numArray. It is obtained when for example we divide 0.0f by 0.0f, as well as when calculating square root of a negative number. 
 
Real Type Double 
The second real floating-point type in the C# language is the double type. It is also called double precision real number and is a 64-bit type with a default value of 0.0d and 0.0D (the suffix 'd' is not mandatory because by default all real numArray in C# are of type double). This type has precision of 15 to 16 decimal digits. The range of values, which can be recorded in double (rounded with precision of 15-16 significant decimal digits), is from ±5.0 × 10-324 to ±1.7 × 10308. 
 
The smallest real value of type double is the constant Double.MinValue = -1.79769e+308 and the largest is Double.MaxValue = 1.79769e+308. The closest to 0 positive number of type double is Double.Epsilon = 4.94066e-324. As with the type float the variables of type double can take the special values: Double.PositiveInfinity (+∞), Double.NegativeInfinity (-∞) and Double.NaN (invalid number). 
Real Floating-Point Types – Example 
Here is an example in which we declare variables of real number types, assign values to them and print them: 
Code Example
float floatPI = 3.14f; 
Console.WriteLine(/* Output */ floatPI); // 3.14 
double doublePI = 3.14; 
Console.WriteLine(/* Output */ doublePI); // 3.14 
double nan = Double.NaN; 
Console.WriteLine(/* Output */ nan); // NaN 
double infinity = Double.PositiveInfinity; 
Console.WriteLine(/* Output */ infinity); // Infinity 
 
1.4.1.3 Boolean Type
Boolean type is declared with the keyword bool. It has two possible values: true and false. Its default value is false. It is used most often to store the calculation result of logical expressions.
Code Example
// Declare some variables 
 
int a = 1; 
int b = 2; 
// Which one is greater? 
bool greaterAB = (a > b); 
// Is 'a' equal to 1? 
bool equalA1 = (a == 1); 
// Print the results on the console 
if (greaterAB) 
{ 
Console.WriteLine(/* Output */ "A > B"); 
} 
else 
{ 
Console.WriteLine(/* Output */ "A <= B"); 
} 
Console.WriteLine(/* Output */ "greaterAB = " + greaterAB); 
Console.WriteLine(/* Output */ "equalA1 = " + equalA1); 
// Console output: 
// A <= B 
// greaterAB = False 
// equalA1 = True  

 
In the example above, we declare two variables of type int, compare them and assign the result to the bool variable greaterAB. Similarly, we do the same for the variable equalA1. If the variable greaterAB is true, then A > B is printed on the console, otherwise A <= B is printed.
1.4.1.4 Character Type
Character type is a single character (16-bit number of a Unicode table character). It is declared in C# with the keyword char. The Unicode table is a technological standard that represents any character (letter, punctuation, etc.) from all human languages as writing systems (all languages and alphabets) with an integer or a sequence of integersThe smallest possible value of a char variable is 0, and the largest one is 65535. The values of type char are letters or other characters, and are enclosed in apostrophes. 
 
Character Type – Example 
Consider an example in which we declare one variable of type char, initialize it with value 'a', then 'b', then 'A' and print the Unicode values of these letters to the console:
Code Example
// Declare a variable 
char ch = 'a'; 
// Print the results on the console 
Console.WriteLine(/* Output */  
"The code of '" + ch + "' is: " + (int)ch); 
ch = 'b'; 
Console.WriteLine(/* Output */  
"The code of '" + ch + "' is: " + (int)ch); 
ch = 'A'; 
Console.WriteLine(/* Output */  
"The code of '" + ch + "' is: " + (int)ch); 
// Console output: 
// The code of 'a' is: 97 
// The code of 'b' is: 98 
// The code of 'A' is: 65
 

1.4.1.5 String Type
Strings are sequences of characters. In C# they are declared by the keyword string. Their default value is null. Strings are enclosed in quotation marks. Various text-processing operations can be performed using strings: concatenation (joining one string with another), splitting by a given separator, searching, replacement of characters and others. 
 
Strings – Example 
Consider an example in which we declare several variables of type string, initialize them and print their values on the console: 
Code Example
// Declare some variables 
string firstName = "John"; 
string lastName = "Smith"; 
string fullName = firstName + " " + lastName; 
// Print the results on the console 
Console.WriteLine(/* Output */ "Hello, " + firstName + "!"); 
Console.WriteLine(/* Output */ "Your full name is " + fullName + "."); 
// Console output: 
// Hello, John! 
// Your full name is John Smith.  
 

1.4.1.6 Object Type
Object type is a special type, which is the parent of all other types in the .NET Framework. Declared with the keyword object, it can take values from any other type. It is a reference type, i.e. an index (address) of a memory area which stores the actual value. 
 
Using Objects – Example 
Consider an example in which we declare several variables of type object, initialize them and print their values on the console:
 
Code Example
int i = 5; 
int? ni = i; 
Console.WriteLine(/* Output */ ni); // 5 
// i = ni; // this will fail to compile 
Console.WriteLine(/* Output */ ni.HasValue); // True 
i = ni.Value; 
Console.WriteLine(/* Output */ idx); // 5 
ni = null; 
Console.WriteLine(/* Output */ ni.HasValue); // False 
//i = ni.Value; // System.InvalidOperationException 
i = ni.GetValueOrDefault(); 
Console.WriteLine(/* Output */ idx); // 0 
 
As you can see from the example, we can store the value of any other type in an object type variable. This makes the object type a universal data container.
1.4.2 Operators
Every programming language uses operators, through which we can perform different actions on the data.
Operators in C# can be separated in several different categories: 
- Arithmetic operators – they are used to perform simple mathematical operations.
-Assignment operators – allow assigning values to variables.
- Comparison operators – allow comparison of two literals and/or variables.
- Logical operators – operators that work with Boolean data types and Boolean expressions.
- Binary operators – used to perform operations on the binary representation of numerical data.
- Type conversion operators – allow conversion of data from one type to another. 
Below is a list of the operators, separated into categories: 
Category 
Operators 
arithmetic
-, +, *, /, %, ++, -- 
logical
&&, ||, !, ^ 
binary
&, |, ^, ~, <<, >> 
comparison
==,!=, >, <, >=, <= 
assignment
=, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>= 
string concatenation
+ 
type conversion
(type), as, is, typeof, sizeof 
other
., new, (), [], ?:, ?? 
 
Some operators have precedence (priority) over others. For example, in math multiplication has precedence over addition. The operators with a higher precedence are calculated before those with lower. The operator () is used to change the precedence and like in math, it is calculated first.
 
The following table illustrates the precedence of the operators in C#:
Priority 
Operators 
Highest priority
 
(, ) 

++, -- (as postfix), new, (type), typeof, sizeof 

++, -- (as prefix), +, - (unary), !, ~ 

*, /, % 

+ (string concatenation) 

+, - 

<<, >> 

<, >, <=, >=, is, as 

==, != 

&, ^, | 

&& 

|| 

?:, ?? 

=, *=, /=, %=, +=, -=, <<=, >>=, &=, ^=, |= 
 
The operators located upper in the table have higher precedence than those below them, and respectively they have an advantage in the calculation of an expression. To change the precedence of an operator we can use brackets. When we write expressions that are more complex or have many operators, it is recommended to use brackets to avoid difficulties in reading and understanding the code.
1.4.2.1 Arithmetic Operators
The arithmetic operators in C# +, -, * are the same like the ones in math. They perform addition, subtraction and multiplication on numerical values and the result is also a numerical value. The division operator / has different effect on integer and real numArray. When we divide an integer by an integer (like int, long and sbyte) the returned value is an integer (no rounding, the fractional part is cut). Such division is called an integer division. Example of integer division: 7 / 3 = 2. 
 
Integer division by 0 is not allowed and causes a runtime exception DivideByZeroException. The remainder of integer division of integers can be obtained by the operator %. For example, 7 % 3 = 1, and –10 % 2 = 0. When dividing two real numArray or two numArray, one of which is real (e.g. float, double, etc.), a real division is done (not integer), and the result is a real number with a whole and a fractional part. For example: 5.0 / 2 = 2.5. In the division of real numArray it is allowed to divide by 0.0 and respectively the result is +∞ (Infinity), -∞ (-Infinity) or NaN (invalid value).  Here are some examples of arithmetic operators and their effect:
 
Code Example
int squarePerimeter = 17; 
double squareSide = squarePerimeter / 4.0; 
double squareArea = squareSide * squareSide; 
Console.WriteLine(/* Output */ squareSide); // 4.25 
Console.WriteLine(/* Output */ squareArea); // 18.0625
 
int a = 5; 
int b = 4; 
Console.WriteLine(/* Output */ a + b); // 9 
Console.WriteLine(/* Output */ a + (b++)); // 9 
Console.WriteLine(/* Output */ a + b); // 10 
Console.WriteLine(/* Output */ a + (++b)); // 11 
Console.WriteLine(/* Output */ a + b); // 11 
Console.WriteLine(/* Output */ 14 / a); // 2 
Console.WriteLine(/* Output */ 14 % a); // 4 
int one = 1; 
int zero = 0; 
 
// Console.WriteLine(/* Output */ one / zero); // DivideByZeroException 
double dMinusOne = -1.0; 
double dZero = 0.0; 
Console.WriteLine(/* Output */ dMinusOne / zero); // -Infinity 
Console.WriteLine(/* Output */ one / dZero); // Infinity 
1.4.2.2 Assignment Operators
The operator for assigning value to a variable is "=" (the character for mathematical equation). The syntax used for assigning value is as it follows:
operand1 = literal, expression or operand2; 
Here is an example to show the usage of the assignment operator: 
int x = 6;
string helloString = "Hello string.";
int y = x;
 In the example we assign value 6 to the variable x. On the second line we assign a text literal to the variable helloString, and on the third line we copy the value of the variable x to the variable y. The assignment operator can be used in cascade (more than once in the same expression). In this case assignments are carried out consecutively from right to left. Here’s an example:
int x, y, z;
x = y = z = 25; 
 On the first line in the example we initialize three variables and on the second line we assign them the value 25. 
The assignment operator in C# is "=", while the comparison operator is "==". The exchange of the two operators is a common error when we are writing code. Be careful not to confuse the comparison operator and the assignment operator as they look very similar. 
1.4.2.3 Comparison Operators
Comparison operators in C# are used to compare two or more operands. C# supports the following comparison operators: 
- greater than (>) 
- less than (<) 
- greater than or equal to (>=) 
- less than or equal to (<=) 
- equality (==) 
- difference (!=) 
 
All comparison operators in C# are binary (take two operands) and the returned result is a Boolean value (true or false). Comparison operators have lower priority than arithmetical operators but higher than the assignment operators. The following example demonstrates the usage of comparison operators in C#:
Code Example
int x = 10, y = 5; 
Console.WriteLine(/* Output */ "x > y : " + (x > y)); // True 
Console.WriteLine(/* Output */ "x < y : " + (x < y)); // False 
Console.WriteLine(/* Output */ "x >= y : " + (x >= y)); // True 
Console.WriteLine(/* Output */ "x <= y : " + (x <= y)); // False 
Console.WriteLine(/* Output */ "x == y : " + (x == y)); // False 
Console.WriteLine(/* Output */ "x != y : " + (x != y)); // True 
 
 
In the example, first we create two variables x and y and we assign them the values 10 and 5. On the next line we print on the console using the method Console.WriteLine(/* Output */ …) the result from comparing the two variables x and y using the operator >. The returned value is true because x has a greater value than y. Similarly, in the next rows the results from the other 5 comparison operators, used to compare the variables x and y, are printed.
1.4.2.4 Logical Operators
Logical (Boolean) operators take Boolean values and return a Boolean result (true or false). The basic Boolean operators are "AND" (&&), "OR" (||), "exclusive OR" (^) and logical negation (!). 
 
The following table contains the logical operators in C# and the operations that they perform:
x 
y 
!x 
x && y 
x || y 
x ^ y 
true 
true 
false 
true 
true 
false 
true 
false 
false 
false 
true 
true 
false 
true 
true 
false 
true 
true 
false 
false 
true 
false 
false 
false 
Source: Nakov et al (2013)
 
The table and the following example show that the logical "AND" (&&) returns true only when both variables contain truth. Logical "OR" (||) returns true when at least one of the operands is true. The logical negation operator (!) changes the value of the argument. For example, if the operand has a value true and a negation operator is applied, the new value will be false. The negation operator is a unary operator and it is placed before the argument. Exclusive "OR" (^) returns true if only one of the two operands has the value true. If the two operands have different values, exclusive "OR" will return the result true, if they have the same values it will return false. The following example illustrates the usage of the logical operators and their actions:
Code Example
bool a = true; 
bool b = false; 
Console.WriteLine(/* Output */ a && b); // False 
Console.WriteLine(/* Output */ a || b); // True 
Console.WriteLine(/* Output */ !b); // True 
Console.WriteLine(/* Output */ b || true); // True 
Console.WriteLine(/* Output */ (5 > 7) ^ (a == b)); // False 

1.4.2.5 Bitwise Operators
A bitwise operator is an operator that acts on the binary representation of numeric types. In computers all the data and particularly numerical data is represented as a series of ones and zeros. The binary numeral system is used for this purpose. For example, number 55 in the binary numeral system is represented as 00110111. 
 
Binary representation of data is convenient because zero and one in electronics can be implemented by Boolean circuits, in which zero is represented as "no electricity" or for example with a voltage of -5V and the one is presented as "have electricity" or say with voltage +5V.
 
Bitwise operators are very similar to the logical ones. In fact, we can imagine that the logical and bitwise operators perform the same thing but using different data types. Logical operators work with the values true and false (Boolean values), while bitwise operators work with numerical values and are applied bitwise over their binary representation, i.e., they work with the bits of the number (the digits 0 and 1 of which it consists). Just like the logical operators in C#, there are bitwise operators "AND" (&), bitwise "OR" (|), bitwise negation (~) and excluding "OR" (^). The bitwise operators' performance on binary digits 0 and 1 is shown in the following table:
 
x 
y 
~x 
x & y 
x | y 
x ^ y 
1 
1 
0 
1 
1 
0 
1 
0 
0 
0 
1 
1 
0 
1 
1 
0 
1 
1 
0 
0 
1 
0 
0 
0 
Source: Nakov et al (2013)
 
As we see bitwise and logical operators are very much alike. The difference in the writing of "AND" and "OR" is that the logical operators are written with double ampersand (&&) and double vertical bar (||), and the bitwise – with a single ampersand or vertical bar (& and |). Bitwise and logical operators for exclusive "OR" are the same "^". For logical negation we use "!", while for bitwise negation (inversion) the "~" operator is used. 
In programming there are two bitwise operators that have no analogue in logical operators. These are the bit shift left (<<) and bit shift right (>>). Used on numerical values, they move all the bits of the value to the left or right. The bits that fall outside the number are lost and replaced with 0. 
 
The bit shifting operators are used in the following way: on the left side of the operator we place the variable (operand) with which we want to use the operator, on the right side we put a numerical value, indicating how many bits we want to offset. For example, 3 << 2 means that we want to move the bits of the number three, twice to the left. The number 3 presented in bits looks like this: "0000 0011". When you move twice left, the binary value will look like this: "0000 1100", and this sequence of bits is the number 12. If we look at the example we can see that actually we have multiplied the number by 4. Bit shifting itself can be represented as multiplication (bitwise shifting left) or division (bitwise shifting right) by a power of 2. This occurrence is due to the nature of the binary numeral system. Example of moving to the right is 6 >> 2, which means to move the binary number "0000 0110" with two positions to the right. This means that we will lose two right-most digits and feed them with zeros on the left. The end result will be "0000 0001" which is 1.
 
Here is an example of using bitwise operators. The binary representation of the numArray and the results of the bitwise operators are shown in the comments (green text):
 
Code Example
byte a = 3; // 0000 0011 = 3 
byte b = 5; // 0000 0101 = 5 
Console.WriteLine(/* Output */ a | b); // 0000 0111 = 7 
Console.WriteLine(/* Output */ a & b); // 0000 0001 = 1 
Console.WriteLine(/* Output */ a ^ b); // 0000 0110 = 6 
Console.WriteLine(/* Output */ ~a & b); // 0000 0100 = 4 
Console.WriteLine(/* Output */ a << 1); // 0000 0110 = 6 
Console.WriteLine(/* Output */ a << 2); // 0000 1100 = 12 
Console.WriteLine(/* Output */ a >> 1); // 0000 0001 = 1 
 
In the example we first create and initialize the values of two variables a and b. Then we print on the console the results of some bitwise operations on the two variables. The first operation that we apply is "OR". The example shows that for all positions where there was 1 in the binary representation of the variables a and b, there is also 1 in the result. The second operation is "AND". The result of the operation contains 1 only in the right-most bit, because the only place where a and b have 1 at the same time is their right-most bit. Exclusive "OR" returns ones only in positions where a and b have different values in their binary bits. Finally, the logical negation and bitwise shifting: left and right, are illustrated.
1.4.2.6 Type Conversion
Generally, operators work over arguments with the same data type. However, C# has a wide variety of data types from which we can choose the most appropriate for a particular purpose. To perform an operation on variables of two different data types we need to convert both to the same data type. Type conversion (typecasting) can be explicit and implicit. 
 
All expressions in C# have a type. This type can derive from the expression structure and the types, variables and literals used in it. It is possible to write an expression which type is inappropriate for the current context. In some cases this will lead to a compilation error, but in other cases the context can get a type that is similar or related to the type of the expression. In this case the program performs a hidden type conversion.
 
Specific conversion from type S to type T allows the expression of type S to be treated as an expression of type T during the execution of the program. In some cases this will require a validation of the transformation. In C# not all types can be converted to all other types, but only to some of them. For convenience, we shall group some of the possible transformations in C# according to their type into three categories: 
- implicit conversion; 
- explicit conversion; 
- conversion to or from string; 
 
A.        Implicit Type Conversion
Implicit (hidden) type conversion is possible only when there is no risk of data loss during the conversion, i.e. when converting from a lower range type to a larger range (e.g. from int to long). To make an implicit conversion it is not necessary to use any operator and therefore such transformation is called implicit. The implicit conversion is done automatically by the compiler when you assign a value with lower range to a variable with larger range or if the expression has several types with different ranges. In such case the conversion is executed into the type with the highest range. Here is an example of implicit type conversion:
 
Code Example
int myInt = 5; 
Console.WriteLine(/* Output */ myInt); // 5 
long myLong = myInt; 
Console.WriteLine(/* Output */ myLong); // 5 
Console.WriteLine(/* Output */ myLong + myInt); // 10 
 
In the example we create a variable myInt of type int and assign it the value 5. After that we create a variable myLong of type long and assign it the value contained in myInt. The value stored in myLong is automatically converted from type int to type long. Finally, we output the result from adding the two variables. Because the variables are from different types they are automatically converted to the type with the greater range, i.e. to type long and the result that is printed on the console is long again. Indeed, the given parameter to the method Console.WriteLine(/* Output */ ) is of type long, but inside the method it will be converted again, this time to type string, so it can be printed on the console. This transformation is performed by the method Long.ToString().
 
B.        Explicit Type Conversion
Explicit type conversion is used whenever there is a possibility of data loss. When converting floating point type to integer type there is always a loss of data coming from the elimination of the fractional part and an explicit conversion is obligatory (e.g. double to long). To make such a conversion it is necessary to use the operator for data conversion (type). There may also be data loss when converting a type with a wider range to type with a narrower one (double to float or long to int). The following example illustrates the use of explicit type conversion and data loss that may occur in some cases:
 
Code Example
double myDouble = 5.1d; 
Console.WriteLine(/* Output */ myDouble); // 5.1 
 
long myLong = (long)myDouble; 
Console.WriteLine(/* Output */ myLong); // 5 
 
myDouble = 5e9d; // 5 * 10^9 
Console.WriteLine(/* Output */ myDouble); // 5000000000 
 
int myInt = (int)myDouble; 
Console.WriteLine(/* Output */ myInt); // -2147483648 
Console.WriteLine(/* Output */ int.MinValue); // -2147483648 
 
 
In the first line of the example we assign a value 5.1 to the variable myDouble. After we convert (explicitly) to type long using the operator (long) and print on the console the variable myLong we see that the variable has lost its fractional part, because long is an integer. Then we assign to the real double precision variable myDouble the value 5 billion. Finally, we convert myDouble to int by the operator (int) and print variable myInt. The result is the same like when we print int.MinValue because myDouble contains a value bigger than the range of int.
 
It is not always possible to predict what the value of a variable will be after its scope overflows! Therefore, use sufficiently large types and be careful when switching to a "smaller" type. 
 
C.        Conversion to String
If it is necessary we can convert any type of data, including the value null, to string. The conversion of strings is done automatically whenever you use the concatenation operator (+) and one of the arguments is not of type string. In this case the argument is converted to a string and the operator returns a new string representing the concatenation of the two strings.  Another way to convert different objects to type string is to call the method ToString() of the variable or the value. It is valid for all data types in .NET Framework. Even calling 3.ToString() is fully valid in C# and the result will return the string "3". Let’s take a look on several examples for converting different data types to string:
Code Example
int a = 5; 
int b = 7; 
 
string sum = "Sum = " + (a + b); 
Console.WriteLine(/* Output */ sum); 
 
String incorrect = "Sum = " + a + b; 
Console.WriteLine(/* Output */ incorrect); 
 
Console.WriteLine(/* Output */  
"Perimeter = " + 2 * (a + b) + ". Area = " + (a * b) + "."); 
 
 
From the results it is obvious, that concatenating a number to a character string returns in result the string followed by the text representation of the number. Note that the "+" for concatenating strings can cause unpleasant effects on the addition of numArray, because it has equal priority with the operator "+" for mathematical addition. Unless the priorities of the operations are changed by placing the brackets, they will always be executed from left to right.


























Skip to main content
Print book
4.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
4.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:50 AM
Table of contents
	•	Learning outcomes
	•	1.5 Variables
	•	1.5.1 Naming Variables - Rules
	•	1.5.2 Naming Variables - Recommendations
	•	1.5.3 Declaring Variables
	•	1.5.4 Assigning a Value to Variables
	•	1.5.5 Initialization of Variables
	•	1.6 Conclusion
Learning outcomes
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 1, 2 & 3
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
1.5 Variables
A variable is a container of information, which can change its value during the cause of program execution. It is a named area of memory, which stores a value from a particular data type, and that area of memory is accessible in the program by its name. It provides means for storing information, retrieving the stored information, and modifying the stored information. In C# programming, you will use variables to store and process information all the time. 
Variables are characterized by name (identifier), for example age; type (of the information preserved in them), for example int; value (stored information), for example 25.
1.5.1 Naming Variables - Rules
When we want the compiler to allocate a memory area for some information which is used in our program we must provide a name for it. It works like an identifier and allows referring to the relevant memory area.
The name of the variable can be any of our choice but must follow certain rules defined in the C# language specification:
- Variable names can contain the letters a-z, A-Z, the digits 0-9 as well as the character '_'.
- Variable names cannot start with a digit.
- Variable names cannot coincide with a keyword of the C# language. For example, base, char, default, int, object, this, null and many others cannot be used as variable names. 
A list of the C# keywords can be found in the section "Keywords" in chapter "Introduction to Programming". If we want to name a variable like a keyword, we can add a prefix to the name – "@". For example, @char and @null are valid variable names while char and null are invalid. Some examples of proper names are name, first_Name, name1. Improper names (will lead to compilation error):  example 1 (digit), if (keyword), 1name (starts with a digit).
1.5.2 Naming Variables - Recommendations
We will provide some recommendations how to name your variables, since not all names, allowed by the compiler, are appropriate for the variables. 
- The names should be descriptive and explain what the variable is used for. For example, an appropriate name for a variable storing a person’s name is personName and inappropriate name is a37.
- Only Latin characters should be used. Although Cyrillic is allowed by the compiler, it is not a good practice to use it in variable names or in the rest of the identifiers within the program.
- In C# it is generally accepted that variable names should start with a small letter and include small letters, every new word, however, starts with a capital letter. For instance, the name firstName is correct and better to use than firstname or first_name. Usage of the character _ in the variable names is considered a bad naming style.
- Variable names should be neither too long nor too short – they just need to clarify the purpose of the variable within its context.
- Uppercase and lowercase letters should be used carefully as C# distinguishes them. For instance, age and Age are different variables. 
Here are some examples of well-named variables:
- firstName 
- age 
- startIndex 
- lastNegativeNumberIndex 
And here are some examples for poorly named variables (although the names are correct from the C# compiler’s perspective):
- _firstName (starts with _)
- last_name (contains _)
- AGE (is written with capital letters)
- Start_Index (starts with capital letter and contains _)
- lastNegativeNumber_Index (contains _)
- a37 (the name is not descriptive and does not clearly provide the purpose of the variable)
- fullName23, fullName24, etc. (it is not appropriate for a variable name to contain digits unless this improves the clarity of the variable used; if you need to have multiple variables with similar names ending in a different number, storing the same or similar type of data, it may be more appropriate to create a single collection or array variable and name it fullNamesList, for example).
1.5.3 Declaring Variables
When you declare a variable, you perform the following steps:
- specify its type (such as int);
- specify its name (identifier, such as age);
- optionally specify initial value (such as 25) but this is not obligatory.
The syntax for declaring variables in C# is as follows:
<data type> <identifier> [= <initialization>]; 
Here is an example of declaring variables:
Code Example
string name;
int age;
1.5.4 Assigning a Value to Variables
Assigning a value to a variable is the act of providing a value that must be stored in the variable. This operation is performed by the assignment operator "=". On the left side of the operator we put the variable name and on the right side – its new value. 
Here is an example of assigning values to variables:
Code Example
name = "John Smith";
age = 25;
1.5.5 Initialization of Variables
The word initialization in programming means specifying an initial value. When setting value to variables at the time of their declaration we actually initialize them. 
 
Each data type in C# has a default value (default initialization) which is used when there is no explicitly set value for a given variable. Let’s summarize how to declare variables, initialize them and assign values to them with the following example:
Code Example
// Declare and initialize some variables 
byte centuries = 20; 
ushort years = 2000; 
decimal decimalPI = 3.141592653589793238m; 
bool isEmpty = true; 
char ch = 'a'; 
string firstName = "John"; 
ch = (char)5; 
char secondChar; 
// Here we use an already initialized variable and reassign it 
secondChar = ch; 
 
1.6 Conclusion
In this week, we discussed the principles, characteristics and features in using Visual Studio IDE. In addition, we critically evaluated the Visual Studio environment. Further, our first C# program was demonstrated and explained. C# datatypes and operators were discussed. Lastly, we discussed variables and their declaration in C#.






Skip to main content
Print book
5.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
5.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:51 AM
Table of contents
	•	Learning outcomes
	•	2.1 Introduction
	•	2.2 Control Statements
	•	2.2.1 Selection Statements
	•	2.2.2 Iteration Statements
	•	2.2.3 Jump Statement
	•	Case study
Learning outcomes
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 5 & 6
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2.1 Introduction
In this week we will discuss control structures in C# and give corresponding examples to demonstrate how they work. We will also discuss various relational operators in C# also give the corresponding examples to demonstrate them.

2.2 Control Statements
Control statements give additional means to control the processing within the applications being developed. This section explores the syntax and function of the the three major control statement C# offers. These statement are categorise as: 
	•	Selection Statement
	•	Iteration Statements
	•	Jump statement.
2.2.1 Selection Statements
The selection statements consist of the if, else, switch-case branching. The if and if-else are conditional control statements. Because of them the program can behave differently based on a defined condition checked during the execution of the statement. 
 
2.2.1.1       “if” Statements
The main format of the conditional statements if is as follows:
Code Example
if (Boolean expression) 
{ 
Body of the conditional statement; 
} 
 
 
 
It includes: if-clause, Boolean expression and body of the conditional statement. The Boolean expression can be a Boolean variable or Boolean logical expression. The body of the statement is the part locked between the curly brackets: {}. It may consist of one or more operations (statements). When there are several operations, we have a complex block operator, i.e. series of commands that follow one after the other, enclosed in curly brackets. 
 
The expression in the brackets which follows the keyword if must return the Boolean value true or false. If the expression is calculated to the value true, then the body of a conditional statement is executed. If the result is false, then the operators in the body will be skipped. Let’s take a look at an example of using a conditional statement if:
Code Example
static void Main() 
{ 
Console.WriteLine(/* Output */ "Enter two numArray."); 
Console.Write("Enter first number: "); 
int firstNumber = int.Parse(Console.ReadLine()); 
Console.Write("Enter second number: "); 
int secondNumber = int.Parse(Console.ReadLine()); 
int biggerNumber = firstNumber; 
if (secondNumber > firstNumber) 
{ 
biggerNumber = secondNumber; 
} 
Console.WriteLine(/* Output */ "The bigger number is: {0}", biggerNumber); 
} 
 
 
If we start the example and enter the numArray 4 and 5 we will get the following result:
Output
Enter two numArray. 
Enter first number: 4 
Enter second number: 5 
The bigger number is: 5 
 
2.2.1.2                  “if-else” Statements
In C#, as in most of the programming languages there is a conditional statement with else clause: the if-else statement. Its format is the following:
Code Example
if (Boolean expression) 
{ 
Body of the conditional statement; 
} 
else 
{ 
Body of the else statement; 
} 
 
 
The format of the if-else structure consists of the reserved word if, Boolean expression, body of a conditional statement, reserved word else and else-body statement. The body of else-structure may consist of one or more operators, enclosed in curly brackets, same as the body of a conditional statement.
 
This statement works as follows: the expression in the brackets (a Boolean expression) is calculated. The calculation result must be Boolean – true or false. Depending on the result there are two possible outcomes. If the Boolean expression is calculated to true, the body of the conditional statement is executed and the else-statement is omitted and its operators do not execute. Otherwise, if the Boolean expression is calculated to false, the else-body is executed, the main body of the conditional statement is omitted and the operators in it are not executed. Let’s take a look at the next example and illustrate how the if-else statement works:
Code Example
static void Main() 
{ 
int x = 2; 
if (x > 3) 
{ 
Console.WriteLine(/* Output */ "x is greater than 3"); 
} 
else 
{ 
Console.WriteLine(/* Output */ "x is not greater than 3"); 
} 
} 
 
 
 
The program code can be interpreted as follows: if x>3, the result at the end is: "x is greater than 3", otherwise (else) the result is: "x is not greater than 3". In this case, since x=2, after the calculation of the Boolean expression the operator of the else structure will be executed. The result of the example is:
Output
x is not greater than 3 
 
 
2.2.1.3                 Nested “if” Statements
Sometimes the programming logic in a program or an application needs to be represented by multiple if-structures contained in each other. We call them nested if or nested if-else structures.  We call nesting the placement of an if or if-else structure in the body of another if or else structure. In such situations every else clause corresponds to the closest previous if clause. This is how we understand which else clause relates to which if clause.
 
It’s not a good practice to exceed three nested levels, i.e. we should not nest more than three conditional statements into one another. If for some reason we need to nest more than three structures, we should export a part of the code in a separate method. Here is an example of using nested if structures:
Code Example
int first = 5; 
int second = 3; 
if (first == second) 
{ 
Console.WriteLine(/* Output */ "These two numArray are equal."); 
} 
else 
{ 
if (first > second) 
{ 
Console.WriteLine(/* Output */ "The first number is greater."); 
} 
else 
{ 
Console.WriteLine(/* Output */ "The second number is greater."); 
} 
} 
 
 
In the example above we have two numArray and compare them in two steps: first we compare whether they are equal and if not, we compare again, to determine which one is the greater. Here is the result of the execution of the code above:
Output
The first number is greater. 
 
 
2.2.1.4       Conditional Statements “switch-case”
In the following section we will cover the conditional statement switch. It is used for choosing among a list of possibilities. The structure switch-case chooses which part of the programming code to execute based on the calculated value of a certain expression (most often of integer type). The format of the structure for choosing an option is as follows:
 
Code Example
switch (integer_selector) 
{ 
case integer_value_1: 
statements; 
break; 
case integer_value_2: 
statements; 
break; 
// … 
default: 
statements; 
break; 
} 
 
The selector is an expression returning a resulting value that can be compared, like a number or string. The switch operator compares the result of the selector to every value listed in the case labels in the body of the switch structure. If a match is found in a case label, the corresponding structure is executed (simple or complex). If no match is found, the default statement is executed (when such exists). The value of the selector must be calculated before comparing it to the values inside the switch structure. The labels should not have repeating values, they must be unique. 
 
As it can be seen from the definition above, every case ends with the operator break, which ends the body of the switch structure. The C# compiler requires the word break at the end of each case-section containing code. If no code is found after a case-statement, the break can be omitted and the execution passes to the next case-statement and continues until it finds a break operator. After the default structure break is obligatory.  It is not necessary for the default clause to be last, but it’s recommended to put it at the end, and not in the middle of the switch structure.
 
The switch statement is a clear way to implement selection among many options (namely, a choice among a few alternative ways for executing the code). It requires a selector, which is calculated to a certain value. The selector type could be an integer number, char, string or enum. If we want to use for example an array or a float as a selector, it will not work. For non-integer data types, we should use a series of if statements. 
 
Using multiple labels is appropriate, when we want to execute the same structure in more than one case. Let’s look at the following example:
Code Example
int number = 6; 
switch (number) 
{ 
case 1: 
case 4: 
case 6: 
case 8: 
case 10: 
Console.WriteLine(/* Output */ "The number is not prime!"); break; 
case 2: 
case 3: 
case 5: 
case 7: 
Console.WriteLine(/* Output */ "The number is prime!"); break; 
default: 
Console.WriteLine(/* Output */ "Unknown number!"); break; 
} 
 
 
 
In the above example, we implement multiple labels by using case statements without break after them. In this case, first the integer value of the selector is calculated – that is 6, and then this value is compared to every integer value in the case statements. When a match is found, the code block after it is executed. If no match is found, the default block is executed. The result of the example above is as follows:
 
Output
The number is not prime! 
 
2.2.2 Iteration Statements
Iteration statement also called loop is a basic programming construct that allows repeated execution of a fragment of source code. Depending on the type of the loop, the code in it is repeated a fixed number of times or repeats until a given condition is true (exists).  Loops that never end are called infinite loops. Using an infinite loop is rarely needed except in cases where somewhere in the body of the loop a break operator is used to terminate its execution prematurely. This is categorised into do, for, for-each, and while loops.
  
2.2.2.1       Do-While Loops
The do-while loop is similar to the while loop, but it checks the condition after each execution of its loop body. This type of loops is called loops with condition at the end (post-test loop). A do-while loop looks like this:
Code Example
do 
{ 
executable code; 
} while (condition); 
 
  
By design do-while loops are executed according to the following scheme:
 
 
 
 
 
   Figure 3- do- while loops
Source: Nakov et al (2013)
 
Initially the loop body is executed. Then its condition is checked. If it is true, the loop’s body is repeated, otherwise the loop ends. This logic is repeated until the condition of the loop is broken. The body of the loop is executed at least once. If the loop’s condition is constantly true, the loop never ends.  The below is the example of a do while loop. In this example we will calculate the factorial of a given number n. 
 
 
Code Example
Console.Write("n = "); 
int n = int.Parse(Console.ReadLine()); 
decimal factorial = 1; 
do 
{ 
factorial *= n; 
n--; 
} while (n > 0); 
Console.WriteLine(/* Output */ "n! = " + factorial);  
 
 
 At the beginning we start with a result of 1 and multiply consecutively the result at each iteration by n, and reduce n by one unit, until n reaches 0. This gives us the product n*(n-1)*…*1. Finally, we print the result on the console. This algorithm always performs at least one multiplication and that’s why it will not work properly when n ≤ 0. 
 
Here is the result of the above example’s execution for n=7:
Output
n = 7
n! = 5040
 
 
2.2.2.2       For Loops
For-loops are a slightly more complicated than while and do-while loops but on the other hand they can solve more complicated tasks with less code. Here is the scheme describing for-loops:

 
 Figure 4- For loops
 
Source: Nakov et al (2013)
 
Let us look at how the program code of a for-loop looks like:
Code Example
for (initialization; condition; update) 
{ 
loop's body; 
} 
 
 
It consists of an initialization part for the counter (in the pattern int idx = 0), a Boolean condition (idx < 10), an expression for updating the counter (idx++, it might be i-- or for instance, i = i + 3) and body of the loop. 
The counter of the loop distinguishes it from other types of loops. Most often the counter changes from a given initial value to a final one in ascending order, for example from 1 to 100. The number of iterations of a given for-loop is usually known before its execution starts. A for-loop can have one or several loop variables that move in ascending or descending order or with a step. It is possible one loop variable to increase and the other – to decrease. It is even possible to make a loop from 2 to 1024 in steps of multiplication by 2, since the update of the loop variables can contain not only addition, but any other arithmetic (as well as other) operations.
 
Here is a complete example of a for-loop:
 
Code Example
for (int i = 0; idx <= 10; idx++) 
{ 
Console.Write(i + " "); 
} 
 
 
The result of its execution is the following:
Output
0 1 2 3 4 5 6 7 8 9 10 
 
The nested loops are programming constructs consisting of several loops located into each other. The innermost loop is executed more times, and the outermost – less times. Let’s see how two nested loops look like:
Code Example
for (initialization, verification, update) 
{ 
for (initialization, verification, update) 
{ 
executable code 
} 
… 
} 
 
 
After initialization of the first for loop, the execution of its body will start, which contains the second (nested) loop. Its variable will be initialized, its condition will be checked and the code within its body will be executed, then the variable will be updated and execution will continue until the condition returns false. After that the second iteration of the first for loop will continue, its variable will be updated and the whole second loop will be performed once again. The inner loop will be fully executed as many times as the body of the outer loop. Example: 
Code Example
int n = int.Parse(Console.ReadLine()); 
for (int row = 1; row <= n; row++) 
{ 
for (int col = 1; col <= row; col++) 
{ 
Console.Write(col + " "); 
} 
Console.WriteLine(/* Output */ ); 
}     
 
 
If we execute it, we will make sure that it works correctly. Here is how the result for n=7 looks like:
 
Output
1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5 
1 2 3 4 5 6 
1 2 3 4 5 6 7 
 
 
2.2.2.3       For Each Loops
The foreach loop (extended for-loop) is new for the C/C++/C# family of languages, but is well known for the VB and PHP programmers. This programming construct serves to iterate over all elements of an array, list or other collection of elements (IEnumerable). It passes through all the elements of the specified collection even if the collection is not indexed. Here is how a foreach loop looks like:
Code Example
foreach (type variable in collection) 
{ 
statements; 
} 
 
 
As we see, it is significantly simpler than the standard for-loop and therefore is very often preferred by developers because it saves writing when you need to go through all the elements of a given collection. Here is an example that shows how we can use foreach:
Code Example
int[] numArray = { 2, 3, 5, 7, 11, 13, 17, 19 }; 
foreach (int i in numArray) 
{ 
Console.Write(" " + i); 
} 
Console.WriteLine(/* Output */ ); 
string[] towns = { "London", "Paris", "Milan", "New York" }; 
foreach (string town in towns) 
{ 
Console.Write(" " + town); 
} 
 
 
In the example we create an array of numArray, which are after that went through with a foreach loop, and its elements are printed on the console. Then an array of city names (strings) is created and in the same way it is went through and its elements are printed on the console. The result of the example is:
 
Output
2 3 5 7 11 13 17 19 
London Paris Milan New York 
 
 
2.2.2.4       While Loops
One of the simplest and most commonly used loops is while.
 
Code Example
while (condition) 
{ 
loop body; 
} 
 
In the code above example, condition is any expression that returns a Boolean result – true or false. It determines how long the loop body will be repeated and is called the loop condition. In this example the loop body is the programming code executed at each iteration of the loop, i.e. whenever the input condition is true. The behaviour of while loops can be represented by the following scheme:
 

  
Figure 5- While Loop
 
Source: Nakov et al (2013)
 In the while loop, first of all the Boolean expression is calculated and if it is true the sequence of operations in the body of the loop is executed. Then again the input condition is checked and if it is true again the body of the loop is executed. All this is repeated again and again until at some point the conditional expression returns value false. At this point the loop stops and the program continues to the next line, immediately after the body of the loop. 
 
The body of the while loop may not be executed even once if in the beginning the condition of the cycle returns false. If the condition of the cycle is never broken the loop will be executed indefinitely. Let’s consider a very simple example of using the while loop. The purpose of the loop is to print on the console the numArray in the range from 0 to 9 in ascending order:
Code Example
// Initialize the counter 
int counter = 0; 
// Execute the loop body while the loop condition holds 
while (counter <= 9) 
{ 
// Print the counter value 
Console.WriteLine(/* Output */ "Number : " + counter); 
// Increment the counter 
counter++; 
} 
 
 
When executing the sample code we obtain the following result:
 
Output
Number : 0 
Number : 1 
Number : 2 
Number : 3 
Number : 4 
Number : 5 
Number : 6 
Number : 7 
Number : 8 
Number : 9 
 
2.2.3 Jump Statement
The Jump statements helps to transfer control during the cause of program execution. There are four Jump statements in C# such as Goto, Break, Continue, and Return.
 
2.2.3.1       Goto Statement
The goto statement can be used to jump to a specific segment of code. Goto can also be used for jumping to switch cases and default labels inside switch blocks. The overuse of goto could make the code difficult to read and maintain if you have many goto jumps within your code.
Code Example
1.   label1:  
2.         ;     
3.         //...     
4.         if (x == 0)  
5.             goto label1;  
6.         //...     
 
 
2.2.3.2       Break Statement
The break statement, used within for, while, and do-while blocks, causes processing to exit the innermost loop immediately. When a break statement is used, the code jumps to the next line following the loop block, see example below.
Code Example
1.   while (true)  
2.   {  
3.       //...     
4.       if (x == 0)  
5.           break;  
6.       //...     
7.   }  
8.   Console.WriteLine(/* Output */ "break");
 
2.2.3.3       Continue Statement
The continue statement (shown in example below) is used to jump to the end of the loop immediately and process the next iteration of the loop.
 
Code Example
1.   int x = 0;  
2.   while (true)  
3.   {  
4.       //...     
5.       if (x == 0)  
6.       {  
7.           x = 5;  
8.           continue;  
9.       }  
10.      //...     
11.    
12.      if (x == 5)  
13.             Console.WriteLine(/* Output */ "continue");  
14.      //...     
15.  }  
 
2.2.3.4       Return Statement
The return statement is used to prematurely return from a method. The return statement can return empty or with a value on the stack, depending upon the return value definition in the method, see example below. Void methods do not require a return value. For other functions, you need to return an appropriate value of the type you declared in the method signature
 
Code Example
1.   void MyFunc1() {  
2.       // ...     
3.       if (x == 1) return;  
4.       // ...     
5.   }  
6.   int MyFunc2() {  
7.       // ...     
8.       if (x == 2) return 1919;  
9.       // ...     
10.  }  
 
Case study
Case Study 1: E-Commerce Order Processing System
Scenario: You are tasked with developing a simple order processing system for an e-commerce platform. The system needs to apply different discounts based on certain conditions, check the stock availability, and ensure that the payment process is completed successfully.
Control Structures Used:
	•	If-Else Statements
	•	Switch Statement
	•	While Loop
	•	For Loop
Solution:

using System;

public class OrderProcessor
{
    public double ProcessOrder(int productId, int quantity, bool isPaymentSuccessful)
    {
        // Check if the product exists and quantity is available
        if (productId < 1 || quantity < 1)
        {
            Console.WriteLine(/* Output */ "Invalid product or quantity.");
            return 0;
        }

        double price = GetProductPrice(productId);
        double totalPrice = price * quantity;

        // Apply discount based on order quantity
        if (quantity > 10)
        {
            totalPrice *= 0.9; // 10% discount for orders with more than 10 items
        }
        else if (quantity >= 5)
        {
            totalPrice *= 0.95; // 5% discount for orders with 5-10 items
        }

        // Check stock availability
        int stock = GetProductStock(productId);
        if (quantity > stock)
        {
            Console.WriteLine(/* Output */ "Not enough stock available.");
            return 0;
        }

        // Check if payment was successful
        if (!isPaymentSuccessful)
        {
            Console.WriteLine(/* Output */ "Payment failed.");
            return 0;
        }

        return totalPrice;
    }

    private double GetProductPrice(int productId)
    {
        // Assume a product price based on its ID
        return 100.0; // Just for the example
    }

    private int GetProductStock(int productId)
    {
        // Assume stock availability based on product ID
        return 20; // Just for the example
    }
}

public class MainProgram
{
    public static void Main()
    {
        OrderProcessor processor = new OrderProcessor();
        
        // Case 1: Valid order with discount
        double price1 = processor.ProcessOrder(1, 6, true);
        Console.WriteLine(/* Output */ $"Total price: {price1:C}");

        // Case 2: Invalid order (out of stock)
        double price2 = processor.ProcessOrder(1, 25, true);
        Console.WriteLine(/* Output */ $"Total price: {price2:C}");

        // Case 3: Payment failure
        double price3 = processor.ProcessOrder(1, 6, false);
        Console.WriteLine(/* Output */ $"Total price: {price3:C}");
    }
}
Explanation:
	•	If-Else Statements are used to check the quantity of items, whether a discount should apply, and if the payment was successful.
	•	Switch Statement could be used in place of multiple if-else branches to select actions based on specific product IDs (if applicable).
	•	While Loop could be used for checking a condition until it's met, such as checking if a customer's payment method is valid.
	•	For Loop could be employed to iterate over a list of products for bulk processing, like applying discounts across multiple products.

Case Study 2: Student Grade Classification
Scenario: You are developing a student grading system where you need to categorize students into different grade categories based on their exam scores. The system should print out appropriate messages for students who pass or fail, and those who are eligible for special honors.
Control Structures Used:
	•	If-Else Statements
	•	Switch Statement
	•	For Loop
Solution:

using System;

public class GradeProcessor
{
    public string GetGrade(int score)
    {
        // Determine grade based on score
        if (score >= 90)
            return "A";
        else if (score >= 80)
            return "B";
        else if (score >= 70)
            return "C";
        else if (score >= 60)
            return "D";
        else
            return "F";
    }

    public string GetHonorStatus(int score)
    {
        // Special honor status
        if (score >= 85)
            return "Eligible for Honors";
        else
            return "Not eligible for Honors";
    }

    public void ProcessGrades(int[] studentScores)
    {
        foreach (var score in studentScores)
        {
            string grade = GetGrade(score);
            string honorStatus = GetHonorStatus(score);
            Console.WriteLine(/* Output */ $"Score: {score}, Grade: {grade}, Status: {honorStatus}");
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        GradeProcessor processor = new GradeProcessor();

        int[] studentScores = { 95, 88, 72, 65, 55, 100 };

        processor.ProcessGrades(studentScores);
    }
}
Explanation:
	•	If-Else Statements determine the grade based on the student's score and check whether the student is eligible for honors.
	•	Switch Statement could be used if you want to create multiple specific conditions (e.g., student classes, subjects) to categorize students based on their grades.
	•	For Loop is used to iterate through the array of student scores and apply the logic of categorizing each student's performance.










Skip to main content
Print book
7.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
7.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:51 AM
Table of contents
	•	Learning outcomes
	•	3.1 Introduction
	•	3.1.1 What is an Exception
	•	3.1.2 Why an exception occurs?
	•	3.1.3 Advantages of Exception Handling
	•	3.1.4 Difference between Error and Exception
	•	3.1.5 Types of Exception
	•	3.2 Catching and Handling Exceptions
	•	Case Study
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 8 & 13
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
3.1 Introduction
When we write a program, we describe step-by-step what the computer must do and in most of the cases we rely that the program will execute normally. Indeed, most of the time, programs are following this normal pattern, but there are some exceptions. Let’s say we want to read a file and display its contents on the screen. Let’s assume the file is located on a remote server and during the process of reading it, the connection goes down. The file then will be only partially loaded. The program will not be able to execute normally and show file’s contents on the screen. In this case, we have an exception from the normal (and correct) program execution and this exception must be reported to the user and/or the administrator.

Play Video
3.1.1 What is an Exception
An Exception is an unwanted event that interrupts the normal flow of the program. When an exception occurs program execution gets terminated.  In such cases we get a system generated message which may not be meaningful. The good thing about exceptions is that they can be handled in C#.  By handling the exceptions we can provide a meaningful message to the user about the issue rather than a system generated message, which may not be understandable to a user.
3.1.2 Why an exception occurs?
There can be several reasons that can cause a program to throw exception. For example:
	•	Opening a non-existing file in your program,
	•	Network connection problem,
	•	bad input data provided by user, etc.
3.1.3 Advantages of Exception Handling
	•	Exception handling ensures that the flow of the program doesn’t break when an exception occurs.
	•	For example, if a program has bunch of statements and an exception occurs mid-way after executing certain statements then the statements after the exception will not execute and the program will terminate abruptly.
	•	By handling we make sure that all the statements execute and the flow of program doesn’t break
3.1.4 Difference between Error and Exception
	•	Errors: indicate that something severe enough has gone wrong, the application should crash rather than try to handle the error.
	•	Exceptions: are events that occurs in the code.
	•	A programmer can handle such conditions and take necessary corrective actions.
3.1.5 Types of Exception
C# statements can execute in either checked or unchecked context. In a checked context, arithmetic overflow raises an exception. In an unchecked context, arithmetic overflow is ignored and the result is truncated by discarding any high-order bits that don't fit in the destination type. 
3.1.5.1       Checked Exception
The checked keyword is used to explicitly enable overflow checking for integral-type arithmetic operations and conversions. By default, an expression that contains only constant values causes a compiler error if the expression produces a value that is outside the range of the destination type. If the expression contains one or more non-constant values, the compiler does not detect the overflow. Evaluating the expression assigned to i2 in the following example does not cause a compiler error.
Code Example
// The following example causes compiler error CS0220 because 2147483647
// is the maximum value for integers.
//int i1 = 2147483647 + 10;
 
// The following example, which includes variable ten, does not cause
// a compiler error.
int ten = 10;
int i2 = 2147483647 + ten;
 
// By default, the overflow in the previous statement also does
// not cause a run-time exception. The following line displays
// -2,147,483,639 as the sum of 2,147,483,647 and 10.
Console.WriteLine(/* Output */ i2);
 
 
 By default, these non-constant expressions are not checked for overflow at run time either, and they do not raise overflow exceptions. The above example displays -2,147,483,639 as the sum of two positive integers.
Overflow checking can be enabled by compiler options, environment configuration, or use of the checked keyword. The example below demonstrate how to use a checked expression or a checked block to detect the overflow that is produced by the previous sum at run time. The example raise an overflow exception.
 
Code Example
// If the previous sum is attempted in a checked environment, an
// OverflowException error is raised.
 
// Checked expression.
Console.WriteLine(/* Output */ checked(2147483647 + ten));
 
// Checked block.
checked
{
    int i3 = 2147483647 + ten;
    Console.WriteLine(/* Output */ i3);
}
 
 
 
The program below is an example of a C# checked exception. This program throws an exception and stops program execution.
Code Example
	•	1. using System;  
	•	2. namespace CSharpProgram  
	•	3. {  
	•	4.     class Program  
	•	5.     {  
	•	6.         static void Main(string[] args)   
	•	7.         {  
	•	8.             checked  
	•	9.             {  
                int val = int.MaxValue;  
               Console.WriteLine(/* Output */ val + 2);  
           }  
        }  
    }  
}  
 
 
 
 
The output is given below:
 
Code Example
Unhandled Exception: System.OverflowException: Arithmetic operation resulted in an overflow.
 
 
 
3.1.5.2       Unchecked Exception
The unchecked keyword is used to suppress overflow-checking for integral-type arithmetic operations and conversions. In an unchecked context, if an expression produces a value that is outside the range of the destination type, the overflow is not flagged. For example, because the calculation in the following example is performed in an unchecked block or expression, the fact that the result is too large for an integer is ignored, and int1 is assigned the value -2,147,483,639.
 
Code Example
unchecked
{
    int1 = 2147483647 + 10;
}
int1 = unchecked(ConstantMax + 10);
 
 
If the unchecked environment is removed, a compilation error occurs. The overflow can be detected at compile time because all the terms of the expression are constants. Expressions that contain non-constant terms are unchecked by default at compile time and run time. Because checking for overflow takes time, the use of unchecked code in situations where there is no danger of overflow might improve performance. However, if overflow is a possibility, a checked environment should be used. Below is an example of unchecked exception.
Code Example
	•	1. using System;  
	•	2. namespace CSharpProgram  
	•	3. {  
	•	4.     class Program  
	•	5.     {  
	•	6.         static void Main(string[] args)   
	•	7.         {  
	•	8.             unchecked  
	•	9.             {  
                int val = int.MaxValue;  
                Console.WriteLine(/* Output */ val + 2);  
            }  
        }  
    }  
}  
 
 
Output
Code Example
-2147483647
3.2 Catching and Handling Exceptions
Exception handling is a mechanism, which allows exceptions to be thrown and caught. This mechanism is provided internally by the CLR (Common Language Runtime). Parts of the exception handling infrastructure are the language constructs in C# for throwing and catching exceptions. CLR takes care to propagate each exception to the code that can handle it. A general syntax of handling an exception is illustrated below.
try
{
          // Any number of statements;
          // some might cause an exception
}
catch(XxxException anExceptionInstance)
{
           // Do something about it
}

// Statements here execute whether there was an exception or not

An example of how an exception can be handles is as follows:

using System;
class MilesPerGallon
{
          static void Main()
           {
                  int milesDriven;
                  int gallonsOfGas;
                  int mpg;
                  try
                           {
                                  Write("Enter miles driven ");
                                   milesDriven = Convert.ToInt32(ReadLine());
                                   Write("Enter gallons of gas purchased ");
                                   gallonsOfGas = Convert.ToInt32(ReadLine());
                                   mpg = milesDriven / gallonsOfGas;
                             }
                     catch(Exception e)
                            {
                                   mpg = 0;
                                   WriteLine(e.message);
                             }
                         WriteLine("You got {0} miles per gallon", mpg);
                 }
}


Case Study
Case Study 1: Handling Invalid User Input in a Login System
Scenario: In a login system, the user is prompted to enter their username and password. If the username or password is empty, an exception should be thrown. Additionally, if the entered username does not match the stored username, a LoginException should be raised.
Exception Handling Used:
	•	try-catch block to handle input validation and login errors.
	•	throw to explicitly raise exceptions.
	•	custom exception class to handle specific login-related errors.
Solution:

using System;

public class LoginException : Exception
{
    public LoginException(string message) : base(message) { }
}

public class UserLoginSystem
{
    private string storedUsername = "admin";
    private string storedPassword = "password123";

    public void Login(string username, string password)
    {
        try
        {
            ValidateCredentials(username, password);
            Console.WriteLine(/* Output */ "Login successful.");
        }
        catch (LoginException ex)
        {
            Console.WriteLine(/* Output */ $"Login failed: {ex.Message}");
        }
    }

    private void ValidateCredentials(string username, string password)
    {
        if (string.IsNullOrEmpty(username) || string.IsNullOrEmpty(password))
        {
            throw new LoginException("Username and password cannot be empty.");
        }

        if (username != storedUsername)
        {
            throw new LoginException("Invalid username.");
        }

        if (password != storedPassword)
        {
            throw new LoginException("Incorrect password.");
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        UserLoginSystem loginSystem = new UserLoginSystem();

        // Case 1: Successful login
        loginSystem.Login("admin", "password123");

        // Case 2: Empty username
        loginSystem.Login("", "password123");

        // Case 3: Invalid username
        loginSystem.Login("user", "password123");

        // Case 4: Incorrect password
        loginSystem.Login("admin", "wrongpassword");
    }
}
Explanation:
	•	try-catch block: The try block contains the code that may throw exceptions. If an exception is thrown, the catch block handles it. In this case, the exception is a LoginExceptionthat catches specific errors like invalid credentials or empty input.
	•	throw keyword: Used to explicitly raise a LoginException when the conditions are met, such as an empty username or incorrect credentials.
	•	Custom LoginException class: A custom exception to handle login-specific errors with a descriptive message.


















Skip to main content
Print book
8.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
8.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:52 AM
Table of contents
	•	Learning outcomes
	•	3.3 Exceptions Handling Classes
	•	3.4 Exceptions Handling Methods
	•	3.4.1 Try …Catch Block
	•	3.4.2 Nested Try …Catch Block
	•	3.4.3 Try…Finally Block
	•	3.4.4 Throw Keyword
	•	3.5 Conclusion
	•	Case Study
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 8 & 13
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
3.3 Exceptions Handling Classes
When you have to throw an exception, you can often use an existing exception type in the .NET Framework instead of implementing a custom exception. You should use a standard exception type under these two conditions:
	•	You are throwing an exception that is caused by a usage error (that is, by an error in program logic made by the developer who is calling your method). Typically, you would throw an exception such as ArgumentException, ArgumentNullException, InvalidOperationException, or NotSupportedException. The string you supply to the exception object's constructor when instantiating the exception object should describe the error so that the developer can fix it.
	•	You are handling an error that can be communicated to the caller with an existing .NET Framework exception. You should throw the most derived exception possible. For example, if a method requires an argument to be a valid member of an enumeration type, you should throw an InvalidEnumArgumentException (the most derived class) rather than an ArgumentException.
The following table lists popular exception class and the conditions and meaning under which you would throw them.
Exception
Condition
NullPointerException
When you try to use a reference that points to null
ArithmeticException
When bad data is provided by user, for example, when you try to divide a number by zero this exception occurs because dividing a number by zero is undefined.
ArrayIndexOutOfBoundsException
When you try to access the elements of an array out of its bounds, for example array size is 5 (which means it has five elements) and you are trying to access the 10th element.
SQLException,
This class is created whenever the . NET Framework Data Provider for SQL Server encounters an error generated from the server. (Client side errors are thrown as standard common language runtime exceptions.) SqlException always contains at least one instance of SqlError.
ClassNotFoundException
ClassNotFoundException is an exception that occurs when you try to load a class at run time using Class. forName() or loadClass() methods and mentioned classes are not found in the classpath. 
IOException,
IOException is the base class for exceptions thrown while accessing information using streams, files and directories. The Base Class Library includes the following types, each of which is a derived class of IOException : DirectoryNotFoundException. EndOfStreamException. FileNotFoundException.
NullReferenceException
Handles errors generated from referencing a null object.
DivideByZeroException
Handles errors generated from dividing a dividend with zero.
ArrayTypeMismatchException
Handles errors generated when type is mismatched with the array type.

Play Video
3.4 Exceptions Handling Methods
An exception is a problem that arises during the execution of a program. A C# exception is a response to an exceptional circumstance that arises while a program is running, such as an attempt to divide by zero. Exceptions provide a way to transfer control from one part of a program to another. C# exception handling is built upon four keywords: try, catch, finally, and throw.
3.4.1 Try …Catch Block

 
A try block identifies a block of code for which particular exceptions is activated. The try block contains set of statements where an exception can occur. It is always followed by a catch block, which handles the exception that occurs in associated try block. A try block must be followed by catch blocks or finally block or both.
 
Syntax
Code Example
try
{
     //statements that may cause an exception
}
catch (exception(type) e(object))‏
{
     //error handling code
}
 
 
 
 
Consider the following example, where we create an array of three integers:
Code Example
int[] myNumbers = {1, 2, 3}
Console.WriteLine(/* Output */ myNumber[10]); // error!
 
 
 
The error message will be something like this:
Error
System.IndexOutOfRangeException: 'Index was outside the bounds of the array.'
 
 
If an error occurs, we can use try...catch to catch the error and execute some code to handle it. In the following example, we use the variable inside the catch block (e) together with the built-in Message property, which outputs a message that describes the exception:
Code Example
 
try
{
  int[] myNumbers = {1, 2, 3};
  Console.WriteLine(/* Output */ myNumbers[10]);
}
catch (Exception e)
{
  Console.WriteLine(/* Output */ e.Message);
}
 
 
 
The output will be:
 
Output
Index was outside the bounds of the array.
 
 
However, you can customise the message to fit your choice using the following example.
Code Example
try
{
  int[] myNumbers = {1, 2, 3};
  Console.WriteLine(/* Output */ myNumbers[10]);
}
catch (Exception e)
{
  Console.WriteLine(/* Output */ "Something went wrong.");
}
 
 
 
The output will be:
 
Output
Something went wrong.
 
 
3.4.2 Nested Try …Catch Block
When a try catch block is present in another try block then it is called the nested try catch block.  Each time a try block does not have a catch handler for a particular exception, then the catch blocks of parent try block are inspected for that exception, if match is found that that catch block executes.
Syntax
Code Example
// outer try block
try
{
 
   // inner try block
   try
     {
       // code...
     }
 
   // inner catch block
   catch
     {
       // code...
     }
}
 
// outer catch block
catch
  {
    // code...
  }
 
 
 
Consider the following example: In this program, DivideByZeroException is generated within the inner try block that is caught by a catch block associated with the inner try block and continue the flow of the program. When IndexOutOfRangeException generates within the inner try block which is not caught by the inner catch block then inner try block transfer this exception to the outer try block. After that, the catch block associated with the outer try block caught the exception which causes the program to terminate. Here for 17/0 and 24/0 inner try-catch block is executing but for number 25 outer try-catch block is executing.
 
Code Example
// C# program to illustrate how outer 
// try block will handle the exception 
// which is not handled by the inner 
// try catch block 
using System; 
 
class GFG { 
    
    // Main Method 
    static void Main() 
    { 
 
        // Here, number is greater 
        // than divisor. 
        int[] number = {8, 17, 24, 5, 25}; 
        int[] divisor = {2, 0, 0, 5}; 
 
        // Outer try block 
        
        // Here IndexOutOfRangeException occurs 
        // due to which program may terminates 
        try { 
            
            for (int j = 0; j < number.Length; jdx++) { 
 
                // Inner try block 
                
                // Here DivideByZeroException caught 
                // and allow the program to continue 
                // its execution 
 
                try { 
                    
                    Console.WriteLine(/* Output */ "Number: " + number[jdx] + 
                                    "\nDivisor: " + divisor[jdx] + 
                                    "\nQuotient: " + number[jdx] / divisor[jdx]); 
                } 
                
                // Catch block for inner try block 
                catch (DivideByZeroException) { 
                    
                    Console.WriteLine(/* Output */ "Inner Try Catch Block"); 
                } 
            } 
        } 
 
        // Catch block for outer try block 
        catch (IndexOutOfRangeException) { 
            
            Console.WriteLine(/* Output */ "Outer Try Catch Block"); 
            
        } 
    } 
}
 
 
 
The output is given below:
 
Output
Number: 8
Divisor: 2
Quotient: 4
Inner Try Catch Block
Inner Try Catch Block
Number: 5
Divisor: 5
Quotient: 1
Outer Try Catch Block
 
3.4.3 Try…Finally Block
A finally block contains all the crucial statements that must be executed whether exception occurs or not. The statements present in this block will always execute regardless of whether exception occurs in try block or not such as closing a connection, stream etc
Syntax
Code Example
// outer try block
try
{
 
   // inner try block
   try
     {
       // code...
     }
 
   // inner catch block
   catch
     {
       // code...
     }
}
 
// outer catch block
catch
  {
    // code...
  }
 
 
 
Consider the following example: 
Code Example
try
{
  int[] myNumbers = {1, 2, 3};
  Console.WriteLine(/* Output */ myNumbers[10]);
}
catch (Exception e)
{
  Console.WriteLine(/* Output */ "Something went wrong.");
}
finally
{
  Console.WriteLine(/* Output */ "The 'try catch' is finished.");
}
 
 
 
The output will be:
 
Code Example
     Something went wrong.  The 'try catch' is finished
 
 
3.4.4 Throw Keyword
The throw keyword is used to throw an exception explicitly. If we see syntax wise than throw is followed by an instance of Exception class and throws is followed by exception class names. The throw statement allows you to create a custom error. The throw statement is used together with an exception class like ArithmeticException, FileNotFoundException, IndexOutOfRangeException, TimeOutException, etc.
Syntax
Code Example
throw new exception_class("error message");
 
 
Example
 
Code Example
static void checkAge(int age)
{
  if (age < 18)
  {
    throw new ArithmeticException("Access denied - You must be at least 18 years old.");
  }
  else
  {
    Console.WriteLine(/* Output */ "Access granted - You are old enough!");
  }
}
 
static void Main(string[] args)
{
  checkAge(15);
}
 
 
 
 
The error message displayed in the program will be:
 
Error Message
System.ArithmeticException: 'Access denied - You must be at least 18 years old.'
 
 
If age was 20, you would not get an exception. For example if 
Code Example
checkAge(20);
 
 
The output will be:
 
Output
Access granted - You are old enough!
 
3.5 Conclusion
During this week, we discussed exception handling in C#. The two types of exception handling were discussed with the associate examples. We also discussed the exception handling classes followed by exception handling methods and the corresponding examples to demonstrate how they work. Finally, we have prepared exercises to strengthen our knowledge of the material in this unit.
Case Study
Case Study 2: File Handling with Exception Handling
Scenario: A file processing application attempts to read a file. If the file doesn't exist or there are any issues while reading the file, an exception should be caught, and the user should be informed about the error. Additionally, the system should ensure that the file is properly closed, even if an error occurs.
Exception Handling Used:
	•	try-catch-finally block to manage resources and handle exceptions gracefully.
	•	FileNotFoundException and IOException for specific errors related to file operations.
Solution:

using System;
using System.IO;

public class FileProcessor
{
    public void ReadFile(string filePath)
    {
        try
        {
            // Try to open and read the file
            string content = File.ReadAllText(filePath);
            Console.WriteLine(/* Output */ "File content:");
            Console.WriteLine(/* Output */ content);
        }
        catch (FileNotFoundException ex)
        {
            // Catch file not found errors
            Console.WriteLine(/* Output */ $"Error: File not found. {ex.Message}");
        }
        catch (IOException ex)
        {
            // Catch general IO exceptions
            Console.WriteLine(/* Output */ $"Error: Issue reading the file. {ex.Message}");
        }
        finally
        {
            // Cleanup or resource release can go here
            Console.WriteLine(/* Output */ "File operation completed.");
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        FileProcessor fileProcessor = new FileProcessor();

        // Case 1: File exists and can be read
        fileProcessor.ReadFile("existingFile.txt");

        // Case 2: File does not exist
        fileProcessor.ReadFile("nonExistentFile.txt");

        // Case 3: File exists but there is an issue reading it (e.g., permission error)
        fileProcessor.ReadFile("protectedFile.txt");
    }
}
Explanation:
	•	try-catch block: The try block attempts to execute the file reading operation. If an exception occurs, the corresponding catch block handles it. In this case, specific exceptions like FileNotFoundException and IOException are caught to handle different types of file errors.
	•	finally block: Ensures that any necessary cleanup is performed, such as closing resources or logging, regardless of whether an exception was thrown or not. Here, it prints a completion message.
	•	Specific exceptions: FileNotFoundException and IOException are used to catch errors specific to file-related operations.

Case Study 3: Division by Zero Handling
Scenario: In a calculator application, the user can perform division operations. If the user attempts to divide by zero, an exception should be thrown and handled appropriately to prevent the program from crashing.
Exception Handling Used:
	•	try-catch block to catch a DivideByZeroException.
	•	throw to raise an exception explicitly when dividing by zero.
Solution:

using System;

public class Calculator
{
    public double Divide(double numerator, double denominator)
    {
        try
        {
            // Check if the denominator is zero
            if (denominator == 0)
            {
                throw new DivideByZeroException("Cannot divide by zero.");
            }

            double result = numerator / denominator;
            return result;
        }
        catch (DivideByZeroException ex)
        {
            Console.WriteLine(/* Output */ $"Error: {ex.Message}");
            return double.NaN;  // Return Not-a-Number to indicate an error in division
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        Calculator calculator = new Calculator();

        // Case 1: Valid division
        Console.WriteLine(/* Output */ "Result: " + calculator.Divide(10, 2));

        // Case 2: Division by zero
        Console.WriteLine(/* Output */ "Result: " + calculator.Divide(10, 0));

        // Case 3: Valid division
        Console.WriteLine(/* Output */ "Result: " + calculator.Divide(25, 5));
    }
}
Explanation:
	•	try-catch block: Used to catch and handle the DivideByZeroException. When the denominator is zero, an exception is thrown, and the catch block handles it by displaying an error message.
	•	throw keyword: Used to explicitly throw a DivideByZeroException when the denominator is zero.
	•	Handling DivideByZeroException: When dividing by zero, the exception is caught, and the program doesn't crash. Instead, a user-friendly message is displayed, and the method returns NaN (Not-a-Number) to indicate an invalid result.
























Skip to main content
Print book
9.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
9.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:52 AM
Table of contents
	•	Learning outcomes
	•	4.1 Introduction
	•	4.1.1 Some key Concept
	•	4.1.2 Class
	•	4.1.3 Object
	•	4.1.4 Constructors
	•	4.1.5 Method
	•	Case Study
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire Object Oriented Skills in C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 4, 10, 12
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
4.1 Introduction
In this week we will familiarize ourselves with some key concept and the principles of object-oriented programming: inheritance, interface implementation, abstraction of data and behaviour, encapsulation of data and class implementation and polymorphism. We will familiarize ourselves with UML and its role in object-oriented modeling. We will briefly discuss design patterns and illustrate some of those that are widely used in practice. Finally, we have prepared exercises to strengthen our knowledge of the material in this week.
4.1.1 Some key Concept
There are two key concepts of Object Oriented Programming namely classes and object.
4.1.2 Class
Classes are a description (model) of real objects and events referred to as entities. An example would be a class called "Student". A class in C# is a blueprint which includes all your data.  A class contain fields (variables) and methods to describe the behavior of an object. Classes possess characteristics – in programming they are referred to as properties. An example would be a set of grades.  Classes also expose behavior known in programming as methods. An example would be sitting an exam.  Methods and properties can be visible only within the scope of the class, which declared them and their descendants (private / protected), or visible to all other classes (public).  To create a class, use the class keyword: 
Syntax 
Code Example
class ClassName {
2      member variables // class body
3        methods
4  }
 
Example: Create a class named "Car" with a variable color:
 
Code Example
class Car
{
  string color = "red";
}
 
 
When a variable is declared directly in a class, it is often referred to as a field (or attribute).
4.1.3 Object
Object in C# can be view in the following light:
	•	A major element in a class which has attributes (state) and behavior (action-what an object can do). 
	•	It is an instance of a class which can access your data.
	•	The building blocks of an OOP.
	•	A program that uses OO technology is a collection of objects
	•	Objects are instances of classes. For example, John is a Student and Peter is also a Student.
 
For instance: See a person as an object, a person has attributes such as eye, colour, age, height and so on. A person has behaviours such as walking, talking breathing, and so on. OOP is a programming technique in which programs are written on the basis of object
 
To create an object of Car, specify the class name, followed by the object name, and use the keyword new:
Create an object called "myObj" and use it to print the value of color:
 
 
Code Example
class Car 
{
  string color = "red";
 
  static void Main(string[] args)
  {
    Car myObj = new Car();
    Console.WriteLine(/* Output */ myObj.color);
  }
}
 
 
4.1.4 Constructors
A constructor is a special method that is used to initialize objects. The advantage of a constructor, is that it is called when an object of a class is created. It can be used to set initial values for fields. For example 
 
Code Example
// Create a Car class
class Car
{
  public string model;  // Create a field
 
  // Create a class constructor for the Car class
  public Car()
  {
    model = "Mustang"; // Set the initial value for model
  }
 
  static void Main(string[] args)
  {
    Car Ford = new Car();  // Create an object of the Car Class (this will call the constructor)
    Console.WriteLine(/* Output */ Ford.model);  // Print the value of model
  }
}
 
// Outputs "Mustang"
 
 
 
 Constructors can also take parameters, which is used to initialize fields.
 
The following example adds a string modelName, colour, and year  parameter to the constructor. Inside the constructor we set model to modelName (model=modelName), colour (colour = modelColour), year (year=modelYear). When we call the constructor, we pass a parameter to the constructor ("Red”, “1969”, “Mustang "), which will set the value of model to "Red 1969 Mustang ":
Code Example
class Car
{
  public string model;
  public string colour;
  public int year;
 
  // Create a class constructor with multiple parameters
  public Car(string modelName, string modelColour, int modelYear)
  {
    model = modelName;
    colour = modelColour;
    year = modelYear;
  }
 
  static void Main(string[] args)
  {
    Car Ford = new Car("Mustang", "Red", 1969);
    Console.WriteLine(/* Output */ Ford.colour + " " + Ford.year + " " + Ford.model);
  }
}
 
// Outputs Red 1969 Mustang
 
 
 
4.1.5 Method
A method is a block of code which only runs when it is called. You can pass data, known as parameters, into a method. Methods are used to perform certain actions, and they are also known as functions. We use method to reuse code: define the code once, and use it many times.
 
A method is defined with the name of the method, followed by parentheses (). C# provides some pre-defined methods, which you already are familiar with, such as Main(), but you can also create your own methods to perform certain actions. A method can be   created inside the Program class
 
Code Example
 
class MainProgram
{
  static void MyMethod() 
  {
    // code to be executed
  }
}
 
 
Let us explain the example method above.
	•	MyMethod() is the name of the method
	•	static means that the method belongs to the Program class and not an object of the Program class. You will learn more about objects and how to access methods through objects later in this tutorial.
	•	void means that this method does not have a return value. 
 
To call (execute) a method, write the method's name followed by two parentheses () and a semicolon; In the following example, MyMethod() is used to print a text (the action), when it is called:
Example
Inside Main(), call the myMethod() method:
Code Example
 
static void MyMethod() 
{
  Console.WriteLine(/* Output */ "I just got executed!");
}
 
static void Main(string[] args)
{
  MyMethod();
}
 
// Outputs "I just got executed!"
 
 
 
Information can be passed to methods as parameter. Parameters act as variables inside the method. They are specified after the method name, inside the parentheses. You can add as many parameters as you want, just separate them with a comma. The following example has a method that takes a string called fname as parameter. When the method is called, we pass along a first name, which is used inside the method to print the full name:
Code Example
static void MyMethod(string fname) 
{
  Console.WriteLine(/* Output */ fname + " Refsnes");
}
 
static void Main(string[] args)
{
  MyMethod("Liam");
  MyMethod("Jenny");
  MyMethod("Anja");
}
 
// Liam Refsnes
// Jenny Refsnes
// Anja Refsnes
 
 
 
 
 
 
 
 
You can have as many parameters as you like, example:
 
Code Example
static void MyMethod(string fname, int age) 
{
  Console.WriteLine(/* Output */ fname + " is " + age);
}
 
static void Main(string[] args)
{
  MyMethod("Liam", 5);
  MyMethod("Jenny", 8);
  MyMethod("Anja", 31);
}
 
// Liam is 5
// Jenny is 8
// Anja is 31
 
 
 
The void keyword, used in the examples above, indicates that the method should not return a value. If you want the method to return a value, you can use a primitive data type (such as int or double) instead of void, and use the return keyword inside the method. For example
 
Code Example
static int MyMethod(int x) 
{
  return 5 + x;
}
static void Main(string[] args)
{
  Console.WriteLine(/* Output */ MyMethod(3));
}
// Outputs 8 (5 + 3)
 
 
 
Multiple methods can have the same name with different parameters, this is called method overloading.
Code Example
int MyMethod(int x)
float MyMethod(float x)
double MyMethod(double x, double y)
 
 
 
Observe the methods above have the same name MyMethod() but with different parameters. 
 
For example: 
 
Code Example
static int PlusMethodInt(int x, int y)
{
  return x + y;
}
 
static double PlusMethodDouble(double x, double y)
{
  return x + y;
}
 
static void Main(string[] args)
{
  int myNum1 = PlusMethodInt(8, 5);
  double myNum2 = PlusMethodDouble(4.3, 6.26);
  Console.WriteLine(/* Output */ "Int: " + myNum1);
  Console.WriteLine(/* Output */ "Double: " + myNum2);
}
 
 
If derived class defines same method as defined in its base class, it is known as method overriding in C#. It is used to achieve runtime polymorphism. It enables you to provide specific implementation of the method which is already provided by its base class.To perform method overriding in C#, you need to use virtual keyword with base class method and override keyword with derived class method. Let's see a simple example of method overriding in C#. In this example, we are overriding the eat() method by the help of override keyword.
 
Example of Method Overriding in C#
Code Example
using System;  
public class Animal{  
    public virtual void eat(){  
        Console.WriteLine(/* Output */ "Eating...");  
    }  
}  
public class Dog: Animal  
{  
    public override void eat()  
    {  
        Console.WriteLine(/* Output */ "Eating bread...");  
    }  
}  
public class TestOverriding  
{  
    public static void Main()  
    {  
        Dog d = new Dog();  
        d.eat();  
    }  
}  
 
 
Output
Eating bread...
 
 
Case Study
Case Study 1: Object-Oriented Design for a Library Management System
Scenario:
You are tasked with building a simple library management system in C#. In this system, each book has properties such as title, author, ISBN, and publication year. Additionally, you need to manage the library's collection of books, which will be done by creating an Library class. The system should also allow you to borrow and return books, updating their availability.
Solution:

using System;
using System.Collections.Generic;

public class Book
{
    // Properties of the Book class
    public string Title { get; set; }
    public string Author { get; set; }
    public string ISBN { get; set; }
    public int PublicationYear { get; set; }
    public bool IsAvailable { get; set; }

    // Constructor to initialize a book with title, author, ISBN, and publication year
    public Book(string title, string author, string isbn, int publicationYear)
    {
        Title = title;
        Author = author;
        ISBN = isbn;
        PublicationYear = publicationYear;
        IsAvailable = true;  // A new book is available by default
    }

    // Method to display book details
    public void DisplayDetails()
    {
        Console.WriteLine(/* Output */ $"Title: {Title}");
        Console.WriteLine(/* Output */ $"Author: {Author}");
        Console.WriteLine(/* Output */ $"ISBN: {ISBN}");
        Console.WriteLine(/* Output */ $"Published Year: {PublicationYear}");
        Console.WriteLine(/* Output */ $"Availability: {(IsAvailable ? "Available" : "Not Available")}");
    }
}

public class Library
{
    // A list of books in the library
    private List<Book> books = new List<Book>();

    // Method to add a new book to the library
    public void AddBook(Book book)
    {
        books.Add(book);
        Console.WriteLine(/* Output */ $"Book '{book.Title}' added to the library.");
    }

    // Method to borrow a book
    public void BorrowBook(string isbn)
    {
        Book book = books.Find(b => b.ISBN == isbn);
        if (book != null && book.IsAvailable)
        {
            book.IsAvailable = false;
            Console.WriteLine(/* Output */ $"You borrowed '{book.Title}'.");
        }
        else
        {
            Console.WriteLine(/* Output */ "Sorry, the book is either unavailable or doesn't exist.");
        }
    }

    // Method to return a book
    public void ReturnBook(string isbn)
    {
        Book book = books.Find(b => b.ISBN == isbn);
        if (book != null && !book.IsAvailable)
        {
            book.IsAvailable = true;
            Console.WriteLine(/* Output */ $"You returned '{book.Title}'.");
        }
        else
        {
            Console.WriteLine(/* Output */ "Sorry, this book wasn't borrowed or doesn't exist.");
        }
    }

    // Method to display all books in the library
    public void DisplayBooks()
    {
        foreach (var book in books)
        {
            book.DisplayDetails();
            Console.WriteLine(/* Output */ );
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        // Create a library instance
        Library library = new Library();

        // Create books
        Book book1 = new Book("The Catcher in the Rye", "J.D. Salinger", "123-456-789", 1951);
        Book book2 = new Book("To Kill a Mockingbird", "Harper Lee", "987-654-321", 1960);
        Book book3 = new Book("1984", "George Orwell", "111-222-333", 1949);

        // Add books to the library
        library.AddBook(book1);
        library.AddBook(book2);
        library.AddBook(book3);

        // Display all books in the library
        library.DisplayBooks();

        // Borrow a book
        library.BorrowBook("123-456-789");

        // Try to borrow the same book again
        library.BorrowBook("123-456-789");

        // Return the book
        library.ReturnBook("123-456-789");

        // Display books again to show updated status
        library.DisplayBooks();
    }
}
Explanation:
1. Book Class:
	•	Properties: The Book class contains properties such as Title, Author, ISBN, PublicationYear, and IsAvailable. These define the essential attributes of a book.
	•	Constructor: The constructor initializes the book's properties. When a book is created, it is set to be available by default (IsAvailable = true).
	•	Methods:
	•	DisplayDetails: Prints the book's details, including the availability status.
	•	Other methods could include methods like UpdateAvailability or similar (although not needed for this basic example).
2. Library Class:
	•	Properties: The Library class holds a list of Book objects, representing the collection of books in the library.
	•	Methods:
	•	AddBook: Adds a new book to the library's collection.
	•	BorrowBook: Checks if a book with a given ISBN is available and marks it as unavailable if it is borrowed.
	•	ReturnBook: Marks a borrowed book as available again.
	•	DisplayBooks: Displays all the books in the library along with their details.
3. Program Class:
	•	Main Program: In the Main method, we instantiate the Library class and create several Book objects. These books are added to the library, and we demonstrate borrowing and returning books by calling the relevant methods.


Skip to main content
Print book
10.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
10.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:53 AM
Table of contents
	•	Learning outcomes
	•	4.2 Fundamental Principles of OOP
	•	4.2.1 Inheritance
	•	4.2.2 Abstraction
	•	4.2.2.1 Abstract Class
	•	4.2.2.2 Interface
	•	4.2.2.3 Types of Abstraction
	•	4.2.3 Encapsulation
	•	4.2.4 Polymorphism
	•	Case Study
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire Object Oriented Skills in C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 4, 10, 12
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
4.2 Fundamental Principles of OOP
In order for a programming language to be object-oriented, it has to enable working with classes and objects as well as the implementation and use of the fundamental object-oriented principles and concepts: inheritance, abstraction, encapsulation and polymorphism.
4.2.1 Inheritance
Inheritance is a fundamental principle of object-oriented programming. It allows a class to "inherit" (behavior or characteristics) of another, more general class. When a class includes a property of another class it is known as inheritance. It is a process of object reusability.
For example, a child includes the properties of its parents. Another example is that a lion belongs to the biological family of cats (Felidae). All cats that have four paws, are predators and hunt their prey. This functionality can be coded once in the Felidae class and all its predators can reuse it – Tiger, Puma, Bobcat, etc. Inheritance is described as is-kind-of relationship, e.g. Tiger is kind of animal.
 
Code Example
public class ParentClass {  
    public ParentClass() {  
        Console.WriteLine(/* Output */ "Parent Constructor.");  
    }  
    public void print() {  
        Console.WriteLine(/* Output */ "I'm a Parent Class.");  
    }  
}  
 
 
 
The ChildClass can inherit the properties of the ParentClass.
 
Code Example
public class ChildClass: ParentClass {  
    public ChildClass() {  
        Console.WriteLine(/* Output */ "Child Constructor.");  
    }  
    public static void Main() {  
        ChildClass child = new ChildClass();  
        child.print();  
    }  
}  
 
 
 
Output
Parent Constructor.
Child Constructor.
I'm a Parent Class.
 
 
When one class inherits another class which is further inherited by another class, it is known as multi-level inheritance in C#. Inheritance is transitive so the last derived class acquires all the members of all its base classes. Let's see the example of multi-level inheritance in C#.
Code Example
using System;  
   public class Animal  
    {  
       public void eat() { Console.WriteLine(/* Output */ "Eating..."); }  
   }  
   public class Dog: Animal  
   {  
       public void bark() { Console.WriteLine(/* Output */ "Barking..."); }  
   }  
   public class BabyDog : Dog  
   {  
       public void weep() { Console.WriteLine(/* Output */ "Weeping..."); }  
   }  
   class TestInheritance2{  
       public static void Main(string[] args)  
        {  
            BabyDog d1 = new BabyDog();  
            d1.eat();  
            d1.bark();  
            d1.weep();  
        }  
    }  
 
 
 
 
 Output:
 
Code Example
Eating...
Barking...
Weeping...
 
 
Types of Inheritance
	•	Single Inheritance: refers to a child and parent class relationship where a class extends to another class.
	•	Multilevel inheritance: refers to a child and parent class relationship where a class extends the child class.
	•	Hierarchical inheritance: refers to a child and parent class relationship where more than one classes extends the same class.
	•	Multiple Inheritance: refers to the concept of one class extending more than one classes, which means a child class has two parent classes.
	•	Hybrid inheritance: Combination of more than one types of inheritance in a single program.
4.2.2 Abstraction
Abstraction is more about hiding the implementation details.  In C# abstraction is achieved through abstract classes and interfaces. Interfaces allows you to abstract the implementation completely while abstract classes allow partial abstraction as well. Therefore, Abstraction can be achieved by two ways: Abstract class or Interface. Abstract class and interface both can have abstract methods which are necessary for abstraction.

4.2.2.1 Abstract Class
In C#, abstract class is a class which is declared abstract. It can have abstract and non-abstract methods. It cannot be instantiated. Its implementation must be provided by derived classes. Here, derived class is forced to provide the implementation of all the abstract methods. Let's see an example of abstract class in C# which has one abstract method draw(). Its implementation is provided by derived classes: Rectangle and Circle. Both classes have different implementation.
Code Example
using System;  
public abstract class Shape  
{  
    public abstract void draw();  
}  
public class Rectangle : Shape  
{  
    public override void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing rectangle...");  
    }  
}  
public class Circle : Shape  
{  
    public override void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing circle...");  
    }  
}  
public class TestAbstract  
{  
    public static void Main()  
    {  
        Shape s;  
        s = new Rectangle();  
        s.draw();  
        s = new Circle();  
        s.draw();  
    }  
}  
 
 
 
Output:
Output
drawing ractangle...
drawing circle... 
 
 
4.2.2.2 Interface
Interface in C# is a blueprint of a class. It is like abstract class because all the methods which are declared inside the interface are abstract methods. It cannot have method body and cannot be instantiated. It is used to achieve multiple inheritance which can't be achieved by class. It is used to achieve fully abstraction because it cannot have method body. Its implementation must be provided by class or struct. The class or struct which implements the interface, must provide the implementation of all the methods declared inside the interface. Let's see the example of interface in C# which has draw() method. Its implementation is provided by two classes: Rectangle and Circle.
Code Example
 using System;  
public interface Drawable  
{  
    void draw();  
}  
public class Rectangle : Drawable  
{  
    public void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing rectangle...");  
    }  
}  
public class Circle : Drawable  
{  
    public void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing circle...");  
    }  
}  
public class TestInterface  
{  
    public static void Main()  
    {  
        Drawable d;  
        d = new Rectangle();  
        d.draw();  
        d = new Circle();  
        d.draw();  
    }  
}  
 
 
 
 
Output
drawing ractangle...
drawing circle...
 
4.2.2.3 Types of Abstraction
There are two major types of abstraction:
	•	Data abstraction
	•	Data abstraction is the way to create complex data types and exposing only meaningful operations to interact with the data type, whereas hiding all the implementation details from outside works.
	•	The benefit of this approach involves capability of improving the implementation over time e.g. solving performance issues. The idea is that such changes are not supposed to have any impact on client code since they involve no difference in the abstract behaviour.
	•	Control abstraction
	•	A software is essentially a collection of numerous statements written in any programming language. Most of the times, statement are similar and repeated over places multiple times.
	•	Control abstraction is the process of identifying all such statements and expose them as a unit of work. We normally use this feature when we create a function to perform any work.
4.2.3 Encapsulation
Encapsulation is one of the main concepts in OOP. It is also called "information hiding". Encapsulation is the concept of wrapping data into a single unit. It collects data members and member functions into a single unit called class. The purpose of encapsulation is to prevent alteration of data from outside. This data can only be accessed by getter functions of the class. A fully encapsulated class has getter and setter functions that are used to read and write data. This class does not allow data access directly.
 
Let say in real life, a Secretary using a Laptop only knows about its screen, keyboard and mouse. Everything else is hidden internally under the cover. She does not know about the inner workings of Laptop, because she doesn’t need to, and if she does, she might make a mess. Therefore parts of the properties and methods remain hidden to her. The person writing the class has to decide what should be hidden and what not. When we program, we must define as private every method or field which other classes should not be able to access.
 
Here, we are creating an example in which we have a class that encapsulates properties and provides getter and setter functions.
Code Example
namespace AccessSpecifiers  
{  
    class Student  
    {  
        // Creating setter and getter for each property  
        public string ID { get; set; }  
        public string Name { get; set; }  
        public string Email { get; set; }  
    }  
}  
 
 
 
 
Code Example
using System;  
namespace AccessSpecifiers  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Student student = new Student();  
            // Setting values to the properties  
            student.ID = "101";  
            student.Name = "Gugu Ruan";  
            student.Email = "MyEamil@pearson.com";  
            // getting values  
            Console.WriteLine(/* Output */ "ID = "+student.ID);  
            Console.WriteLine(/* Output */ "Name = "+student.Name);  
            Console.WriteLine(/* Output */ "Email = "+student.Email);  
        }  
    }  
}  
 
 
 
 
Output: 
Output
ID = 101
Name = Gugu Ruan
Email = myemail@pearson.com 
 
4.2.4 Polymorphism
The term "Polymorphism" is the combination of "poly" + "morphs" which means many forms. It is a greek word. There are two types of polymorphism in C#: compile time polymorphism and runtime polymorphism. Compile time polymorphism is achieved by method overloading and operator overloading in C#. It is also known as static binding or early binding. Runtime polymorphism in achieved by method overriding which is also known as dynamic binding or late binding.
 
Let's see a simple example of runtime polymorphism in C#
Code Example
 using System;  
public class Animal{  
    public virtual void eat(){  
        Console.WriteLine(/* Output */ "eating...");  
    }  
}  
public class Dog: Animal  
{  
    public override void eat()  
    {  
        Console.WriteLine(/* Output */ "eating bread...");  
    }  
      
}  
public class TestPolymorphism  
{  
    public static void Main()  
    {  
        Animal a= new Dog();  
        a.eat();  
    }  
}  
 
 
 
 
Output: 
Output
eating bread...
 
 
Another example of runtime polymorphism in C# where we are having two derived classes is shown below.
 
Code Example
 using System;  
public class Shape{  
    public virtual void draw(){  
        Console.WriteLine(/* Output */ "drawing...");  
    }  
}  
public class Rectangle: Shape  
{  
    public override void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing rectangle...");  
    }  
      
}  
public class Circle : Shape  
{  
    public override void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing circle...");  
    }  
  
}  
 
 
 
 
Code Example
public class TestPolymorphism  
{  
    public static void Main()  
    {  
        Shape s;  
        s = new Shape();  
        s.draw();  
        s = new Rectangle();  
        s.draw();  
        s = new Circle();  
        s.draw();  
  
    }  
}  
 
 
 
 
 Output:
Output
drawing...
drawing rectangle...
drawing circle...
 
 
Compile time polymorphism is achieved by method overloading. Let's see a simple example of Compile time polymorphism in C#. Let’s say you have a function that prints multiplication of numArray, then our overloaded methods will have the same name but different number of arguments: 
 
Code Example
using System;
public class Demo {
   public static int mulDisplay(int one, int two) {
      return one * two;
   }
 
   public static int mulDisplay(int one, int two, int three) {
      return one * two * three;
   }
 
   public static int mulDisplay(int one, int two, int three, int four) {
      return one * two * three * four;
   }
}
 
public class Program {
   public static void Main() {
      Console.WriteLine(/* Output */ "Multiplication of two numArray: "+Demo.mulDisplay(10, 15));
      Console.WriteLine(/* Output */ "Multiplication of three numArray: "+Demo.mulDisplay(8, 13, 20));
      Console.WriteLine(/* Output */ "Multiplication of four numArray: "+Demo.mulDisplay(3, 7, 10, 7));
   }
}
 
 
 
Output:
Output
Multiplication of two numArray: 150
Multiplication of three numArray: 2080
Multiplication of four numArray: 1470
 
Case Study
Case Study 2: Object-Oriented Design for an E-commerce System
Scenario:
In an e-commerce system, products are sold in a store. Each product has properties like name, price, and stock quantity. The system needs to manage products, including adding them to a cart and updating the stock when products are purchased.
Solution:

using System;
using System.Collections.Generic;

public class Product
{
    // Properties of the Product class
    public string Name { get; set; }
    public decimal Price { get; set; }
    public int StockQuantity { get; set; }

    // Constructor to initialize the product with name, price, and stock
    public Product(string name, decimal price, int stockQuantity)
    {
        Name = name;
        Price = price;
        StockQuantity = stockQuantity;
    }

    // Method to display product details
    public void DisplayDetails()
    {
        Console.WriteLine(/* Output */ $"Product: {Name}");
        Console.WriteLine(/* Output */ $"Price: {Price:C}");
        Console.WriteLine(/* Output */ $"Stock: {StockQuantity}");
    }

    // Method to reduce stock when a product is bought
    public bool Purchase(int quantity)
    {
        if (quantity <= StockQuantity)
        {
            StockQuantity -= quantity;
            Console.WriteLine(/* Output */ $"Purchased {quantity} {Name}(s).");
            return true;
        }
        else
        {
            Console.WriteLine(/* Output */ "Insufficient stock.");
            return false;
        }
    }
}

public class Cart
{
    private List<Product> products = new List<Product>();
    
    // Method to add a product to the cart
    public void AddToCart(Product product, int quantity)
    {
        if (product.Purchase(quantity))
        {
            products.Add(product);
            Console.WriteLine(/* Output */ $"{quantity} of {product.Name} added to cart.");
        }
    }

    // Method to display cart contents
    public void DisplayCart()
    {
        Console.WriteLine(/* Output */ "\nCart Contents:");
        foreach (var product in products)
        {
            product.DisplayDetails();
            Console.WriteLine(/* Output */ );
        }
    }

    // Method to calculate total price of items in the cart
    public decimal CalculateTotal()
    {
        decimal total = 0;
        foreach (var product in products)
        {
            total += product.Price;
        }
        return total;
    }
}

public class MainProgram
{
    public static void Main()
    {
        // Create products
        Product product1 = new Product("Laptop", 899.99m, 10);
        Product product2 = new Product("Headphones", 99.99m, 50);

        // Display product details
        product1.DisplayDetails();
        product2.DisplayDetails();

        // Create a shopping cart
        Cart cart = new Cart();

        // Add products to the cart
        cart.AddToCart(product1, 2);  // Adding 2 laptops to the cart
        cart.AddToCart(product2, 5);  // Adding 5 headphones to the cart

        // Display cart contents
        cart.DisplayCart();

        // Calculate and display total price
        Console.WriteLine(/* Output */ $"Total Price: {cart.CalculateTotal():C}");
    }
}
Explanation:
1. Product Class:
	•	Properties: The Product class has properties such as Name, Price, and StockQuantity to represent product details.
	•	Constructor: The constructor initializes the product's name, price, and stock quantity.
	•	Methods:
	•	DisplayDetails: Prints the details of the product, including its price and stock.
	•	Purchase: Reduces the stock when a product is bought and returns true if successful, false if there is insufficient stock.
2. Cart Class:
	•	Properties: The Cart class manages a list of products added to the shopping cart.
	•	Methods:
	•	AddToCart: Adds a product to the cart and updates the stock using the Purchase method from the Product class.
	•	DisplayCart: Displays the products in the cart.
	•	CalculateTotal: Calculates the total price of the products in the cart.
3. Program Class:
	•	Main Program: In the Main method, we create Product objects, display their details, add products to the cart, and display the cart's contents along with the total price.

Key Concepts:
	•	Classes & Objects: In both case studies, we use classes to define blueprints for creating objects that represent real-world entities (e.g., Book, Product).
	•	Properties & Methods: Properties define the attributes of an object, while methods define behaviors or actions an object can perform (e.g., DisplayDetails, Purchase).
	•	Encapsulation: The internal details of the objects (e.g., how stock is updated) are hidden inside the class, and the objects provide methods to interact with them. This ensures that the user does not need to know how the internal logic works.























Skip to main content
Print book
11.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
11.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:54 AM
Table of contents
	•	Learning outcomes
	•	4.3 Class Diagram
	•	4.3.1 Generalization
	•	4.3.2 Associations
	•	4.3.3 Aggregation
	•	4.3.4 Composition
	•	4.4 Conclusion
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire Object Oriented Skills in C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 4, 10, 12
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
4.3 Class Diagram
A Class Diagram is one of several types of diagrams defined in UML. UML (Unified Modeling Language) is a notation for visualizing different processes and objects related to software development. Let’s discuss class diagrams.
What is UML Class Diagram? 
It is commonly accepted to draw class diagrams as rectangles with name, attributes (member variables) and operations (methods). The connections between them are denoted with various types of arrows. 
Briefly, we will explain two pieces of UML terminology, so we can understand the examples more easily. The first one is generalization. Generalization is a term signifying the inheritance of a class or the implementation of an interface. 
The other term is association. An association, would be, e.g. "The Lion has paws", where Paw is another class. Association is has-a relationship. This is what a sample class diagram looks like:
 
 Figure 6- Association
The class is represented as a rectangle, divided in 3 boxes one under another. The name of the class is at the top. Next, there are the attributes (UML term) of the class (in .NET they are called member variables and properties). At the very bottom are the operations (UML term) or methods (in .NET jargon). The plus/minus signs indicate whether an attribute / operation is visible (+ means public) or not visible (- means private). Protected members are marked with #.
4.3.1 Generalization
Generalization is the process of taking out common properties and functionalities from two or more classes and combining them together into another class which acts as the parent class of those classes or what we may say the generalized class of those specialized classes.  All the subclasses are a type of superclass.  So we can say that subclass “is-A” superclass. Therefore Generalization is termed as “is-A relationship”

 Figure 7 -Generalization
 Below is a class diagram that visually illustrates generalization (Felidae inherited by Lion inherited by AfricanLion): 
 
 Figure 8 – Class Diagram
In this example, the arrows indicate generalization (inheritance).
4.3.2 Associations
Association is relation between two separate classes which establishes through their Objects. It denotes connections between classes. They model mutual relations. They can define multiplicity (1 to 1, 1 to many, many to 1, 1 to 2, …, and many to many).  A one-to-one association is depicted like this:
 

 A one-to-many association is depicted like this:
 
 A many-to-many association is depicted in the following way:
 
 
 
 
4.3.3 Aggregation
Aggregation is a special type of association. It models the relationship of kind "whole / part". We refer to the parent class as an aggregate. The aggregated classes are called components.  It is a special form of Association where: It represents Has-A relationship. It is a unidirectional association i.e. a one way relationship. For example, department can have students or Zoo have Lion but vice versa is not possible and thus unidirectional in nature. In Aggregation, both the entries can survive individually which means ending one entity will not affect the other entity. There is an empty rhombus at one end of the aggregation:
 
 
 
 
4.3.4 Composition
Composition is a restricted form of Aggregation in which two entities are highly dependent on each other.
It represents part-of relationship. In composition, both the entities are dependent on each other. When there is a composition between two entities, the composed object cannot exist without the other entity. Let’s say humans and brain. The Human cannot exist without a brain. A filled rhombus represents composition. Composition is an aggregation where the components cannot exist without the aggregate:

4.4 Conclusion
During this week, we acquainted ourselves with some key concept and the principles of object-oriented programming: inheritance, interface implementation, abstraction of data and behaviour, encapsulation of data and class implementation and polymorphism. We also learned the UML and its role in object-oriented modelling. Finally, we have prepared exercises to strengthen our knowledge of the material in this unit.








Skip to main content
Print book
12.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
12.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:54 AM
Table of contents
	•	Learning outcomes
	•	5.1 Introduction
	•	5.2 C# Arrays
	•	5.2.1 Advantages of C# Arrays
	•	5.2.2 Disadvantages of C# Array
	•	5.2.3 Types of C# Arrays
	•	5.2.3.1 Single Dimensional Array
	•	5.2.3.2 Multidimensional Arrays
	•	5.2.3.3 Jagged Arrays
	•	Case study
Learning outcomes
By the end of this topic you should be able to:
	•	Develop the skill of designing Graphical User Interfaces (GUI) and implementing Array Orientation in C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 8, 14, 15
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
5.1 Introduction
In this week we will get familiar with array programming in C#. We will explain what arrays are, how we declare, create, instantiate and use them. We will examine one-dimensional and multidimensional arrays. We will learn different ways to iterate through the array, read from the standard input and write to the standard output. Further, we will implement GUI design in relation to objects, objects behaviours and algorithms using Visual studio IDE. Explain testing, documentation, and comments in C#. Finally, in order to strengthen our knowledge of the material in this unit, we will prepare exercises at the end of the week.
5.2 C# Arrays
Like other programming languages, array in C# is a group of similar types of elements that have contiguous memory location. In C#, array is an object of base type System.Array. In C#, array index starts from 0. We can store only fixed set of elements in C# array. 

 Figure 9 - array
Source: JavaTpoint (2020), Availabie at: https://www.javatpoint.com/c-sharp-arrays
5.2.1 Advantages of C# Arrays
The following are some of the known advantages of C# Arrays:
	•	Code Optimization (less code)
	•	Random Access
	•	Easy to traverse data
	•	Easy to manipulate data
	•	Easy to sort data, etc.
5.2.2 Disadvantages of C# Array
The only known disadvantage of C# Array could be seen as the fact the arrays generally have fixed size.
5.2.3 Types of C# Arrays
There are three types of arrays in C# programming namely:
	•	Single Dimensional Array
	•	Multidimensional Array
	•	Jagged Array
We will discuss each type in the next sections.
5.2.3.1 Single Dimensional Array
To create single dimensional array, you need to use square brackets [] after the type.
int[] myArray = new int[5];//creating array  
 
You cannot place square brackets after the identifier.
int myArray[] = new int[5];//compile time error  
 
Let's see a simple example of C# array, where we are going to declare, initialize and traverse array. 
 
Code Example
using System;  
public class ArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[] myArray = new int[5];//creating array  
        myArray[0] = 10;//initializing array  
        myArray[2] = 20;  
        myArray[4] = 30;  
  //traversing array  
        for (int i = 0; i < myArray.Length; idx++)  
        {  
            Console.WriteLine(/* Output */ myArray[idx]);  
        }  
    }  
}  
 
 
 
Output:
Code Example
10
0
20
0
30
 
 
 
There are three ways to initialize array at the time of declaration.
int[] myArray = new int[5]{ 10, 20, 30, 40, 50 };  
 
We can omit the size of array.
int[] myArray = new int[]{ 10, 20, 30, 40, 50 };   
 
We can omit the new operator also.
int[] myArray = { 10, 20, 30, 40, 50 };  
 
Let's see the example of array where we are declaring and initializing array at the same time.
 
Code Example
using System;  
public class ArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[] myArray = { 10, 20, 30, 40, 50 };//Declaration and Initialization of array  
   
        //traversing array  
        for (int i = 0; i < myArray.Length; idx++)  
        {  
            Console.WriteLine(/* Output */ myArray[idx]);  
        }  
    }  
}  
 
 
 
Output:
 
Output
10
20
30
40
50
 
 
 We can also traverse the array elements using foreach loop. It returns array element one by one.
Code Example
using System;  
public class ArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[] myArray = { 10, 20, 30, 40, 50 };//creating and initializing array  
   
        //traversing array  
        foreach (int i in myArray)  
        {  
            Console.WriteLine(/* Output */ idx);  
        }  
    }  
}  
 
 
 
 Output:
Output
10
20
30
40
50
 
 
 
5.2.3.2 Multidimensional Arrays
The multidimensional array is also known as rectangular arrays in C#. It can be two dimensional or three dimensional. The data is stored in tabular form (row * column) which is also known as matrix. To create multidimensional array, we need to use comma inside the square brackets. For example:
 
Code Example
int[,] myArray=new int[3,3];//declaration of 2D array  
int[,,] myArray=new int[3,3,3];//declaration of 3D array
 
 
 
Let's see a simple example of multidimensional array in C# which declares, initializes and traverse two-dimensional array.
Code Example
using System;  
public class MultiArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[,] myArray=new int[3,3];//declaration of 2D array  
        myArray[0,1]=10;//initialization  
        myArray[1,2]=20;  
        myArray[2,0]=30;  
  
        //traversal  
        for(int i=0;i<3;idx++){  
            for(int j=0;j<3;jdx++){  
                Console.Write(myArray[i,j]+" ");  
            }  
            Console.WriteLine(/* Output */ );//new line at each row  
        }  
    }  
}  
 
 
 
Output:
Output
0 10 0
0 0 20
30 0 0
 
 
 
There are three ways to initialize multidimensional array in C# while declaration.
int[,] myArray = new int[3,3]= { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  
 
We can omit the array size.
int[,] myArray = new int[,]{ { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  
 
We can omit the new operator also.
int[,] myArray = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  
 
 
Let's see a simple example of multidimensional array which initializes array at the time of declaration.
Code Example
using System;  
public class MultiArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[,] myArray = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };//declaration and initialization  
  
        //traversal  
        for(int i=0;i<3;idx++){  
            for(int j=0;j<3;jdx++){  
                Console.Write(myArray[i,j]+" ");  
            }  
            Console.WriteLine(/* Output */ );//new line at each row  
        }  
    }  
}  
 
 
 
Output
Output
1 2 3
4 5 6
7 8 9
 
5.2.3.3 Jagged Arrays
In C#, jagged array is also known as "array of arrays" because its elements are arrays. The element size of jagged array can be different. Let's see an example to declare jagged array that has two elements.
int[][] myArray = new int[2][];  
 
The example below shows how to initialize jagged array. The size of elements can be different
myArray[0] = new int[4];  
myArray[1] = new int[6];
 
 
We can also initialize and fill elements in jagged array, see example below:
myArray[0] = new int[4] { 11, 21, 56, 78 };         
myArray[1] = new int[6] { 42, 61, 37, 41, 59, 63 };  
 
Here, size of elements in jagged array is optional. So, you can write above code as given below:
myArray[0] = new int[] { 11, 21, 56, 78 };         
myArray[1] = new int[] { 42, 61, 37, 41, 59, 63 };   
 
The example below shows a jagged array in C# which declares, initializes and traverse jagged arrays.
 
Code Example
public class JaggedArrayTest  
{  
    public static void Main()  
    {  
        int[][] myArray = new int[2][];// Declare the array  
  
        myArray[0] = new int[] { 11, 21, 56, 78 };// Initialize the array          
        myArray[1] = new int[] { 42, 61, 37, 41, 59, 63 };  
  
        // Traverse array elements  
        for (int i = 0; i < myArray.Length; idx++)  
        {  
            for (int j = 0; j < myArray[idx].Length; jdx++)  
            {  
                System.Console.Write(myArray[idx][jdx]+" ");  
            }  
            System.Console.WriteLine(/* Output */ );  
        }  
    }  
}  
 
 
 
Output
Output
11 21 56 78
42 61 37 41 59 63
 
 
Let's see an example to initialize the jagged array while declaration.
Code Example
int[][] myArray = new int[3][]{  
        new int[] { 11, 21, 56, 78 },  
        new int[] { 2, 5, 6, 7, 98, 5 },  
        new int[] { 2, 5 }  
        };  
 
 
 
 The below simple example shows a jagged array which initializes the jagged arrays upon declaration.
 
Code Example
 public class JaggedArrayTest  
{  
    public static void Main()  
    {  
        int[][] myArray = new int[3][]{  
        new int[] { 11, 21, 56, 78 },  
        new int[] { 2, 5, 6, 7, 98, 5 },  
        new int[] { 2, 5 }  };  
           // Traverse array elements  
        for (int i = 0; i < myArray.Length; idx++)  
        {  
            for (int j = 0; j < myArray[idx].Length; jdx++)  
            {  
                System.Console.Write(myArray[idx][jdx]+" ");  
            }  
            System.Console.WriteLine(/* Output */ );  
        }  
    }  
}  
 
      
 
 Output:
 
Output
11 21 56 78
2 5 6 7 98 5
2 5
 
Case study
Case Study 1: Student Grade Management System
Scenario:
A school wants to keep track of student grades in a course. The grades are collected for multiple students across multiple subjects. The goal is to implement a system that allows the teacher to:
	•	Store and display student grades for various subjects.
	•	Calculate the average grade for each student.
	•	Identify the highest grade in each subject.
Task:
	•	Create a two-dimensional array to store student grades.
	•	Develop methods to:
	•	Display all grades.
	•	Calculate the average grade for each student.
	•	Display the highest grade for each subject.
Solution:

using System;

public class GradeManagement
{
    public static void Main()
    {
        // 2D array to store student grades (5 students, 4 subjects)
        int[,] studentGrades = new int[5, 4]
        {
            { 90, 85, 78, 92 }, // Student 1 grades
            { 88, 76, 91, 85 }, // Student 2 grades
            { 75, 88, 80, 79 }, // Student 3 grades
            { 92, 90, 95, 89 }, // Student 4 grades
            { 80, 84, 88, 75 }  // Student 5 grades
        };

        // Display all student grades
        DisplayGrades(studentGrades);

        // Calculate and display average grade for each student
        CalculateAverageGrades(studentGrades);

        // Display highest grade in each subject
        DisplayHighestGrades(studentGrades);
    }

    // Method to display all grades
    public static void DisplayGrades(int[,] grades)
    {
        Console.WriteLine(/* Output */ "Student Grades:");
        for (int idx = 0; idx < grades.GetLength(0); idx++)
        {
            Console.Write($"Student {i + 1}: ");
            for (int jdx = 0; jdx < grades.GetLength(1); jdx++)
            {
                Console.Write(grades[i, j] + " ");
            }
            Console.WriteLine(/* Output */ );
        }
    }

    // Method to calculate and display the average grade for each student
    public static void CalculateAverageGrades(int[,] grades)
    {
        Console.WriteLine(/* Output */ "\nAverage Grades:");
        for (int idx = 0; idx < grades.GetLength(0); idx++)
        {
            int sum = 0;
            for (int jdx = 0; jdx < grades.GetLength(1); jdx++)
            {
                sum += grades[i, j];
            }
            double average = sum / (double)grades.GetLength(1);
            Console.WriteLine(/* Output */ $"Student {i + 1}: {average:F2}");
        }
    }

    // Method to display the highest grade in each subject
    public static void DisplayHighestGrades(int[,] grades)
    {
        Console.WriteLine(/* Output */ "\nHighest Grades per Subject:");
        for (int jdx = 0; jdx < grades.GetLength(1); jdx++)
        {
            int highestGrade = grades[0, j];
            for (int idx = 1; idx < grades.GetLength(0); idx++)
            {
                if (grades[i, j] > highestGrade)
                {
                    highestGrade = grades[i, j];
                }
            }
            Console.WriteLine(/* Output */ $"Subject {j + 1}: {highestGrade}");
        }
    }
}
Explanation:
	•	The 2D array studentGrades is used to store the grades for 5 students across 4 subjects.
	•	The DisplayGrades method loops through the array and prints all the grades for each student.
	•	The CalculateAverageGrades method calculates the average grade for each student.
	•	The DisplayHighestGrades method finds the highest grade for each subject across all students.
Outcome:
	•	You can easily track and analyze the grades of students.
	•	The system can provide insights into each student's performance as well as the best-performing subject.
Case Study 2: Employee Shift Scheduling System
Scenario:
A company needs a system to manage employee shift schedules. The company operates 7 days a week with 3 shifts (morning, afternoon, night). The goal is to:
	•	Store the employees' shift assignments for a week.
	•	Display the shift schedule.
	•	Find out how many employees are assigned to each shift per day.
Task:
	•	Create a multidimensional array (3D array) to store employee shifts.
	•	Develop methods to:
	•	Display the shift schedule for the week.
	•	Count how many employees are working each shift per day.
Solution:

using System;

public class EmployeeShiftScheduling
{
    public static void Main()
    {
        // 3D array to store employee shifts (7 days, 3 shifts per day, 5 employees)
        string[,,] shifts = new string[7, 3, 5]
        {
            { { "John", "Alice", "Bob", "Eve", "Charlie" }, { "John", "Bob", "Eve", "Alice", "Charlie" }, { "Alice", "Bob", "Charlie", "Eve", "John" } },  // Day 1
            { { "John", "Alice", "Bob", "Charlie", "Eve" }, { "Eve", "Alice", "Charlie", "Bob", "John" }, { "Bob", "Charlie", "John", "Eve", "Alice" } },  // Day 2
            { { "Charlie", "Alice", "Eve", "Bob", "John" }, { "Bob", "Charlie", "Alice", "Eve", "John" }, { "John", "Bob", "Charlie", "Alice", "Eve" } },  // Day 3
            { { "Eve", "Bob", "Alice", "Charlie", "John" }, { "Charlie", "John", "Eve", "Alice", "Bob" }, { "Alice", "Eve", "John", "Bob", "Charlie" } },  // Day 4
            { { "Bob", "Alice", "Charlie", "Eve", "John" }, { "Alice", "Charlie", "Bob", "John", "Eve" }, { "Charlie", "John", "Eve", "Bob", "Alice" } },  // Day 5
            { { "Charlie", "Eve", "John", "Alice", "Bob" }, { "Bob", "Alice", "Eve", "Charlie", "John" }, { "Alice", "John", "Charlie", "Bob", "Eve" } },  // Day 6
            { { "Eve", "Charlie", "Bob", "Alice", "John" }, { "Charlie", "Eve", "Alice", "Bob", "John" }, { "John", "Alice", "Bob", "Charlie", "Eve" } }   // Day 7
        };

        // Display the shift schedule for the week
        DisplayShiftSchedule(shifts);

        // Count and display how many employees are working each shift per day
        CountEmployeesPerShift(shifts);
    }

    // Method to display the shift schedule
    public static void DisplayShiftSchedule(string[,,] shifts)
    {
        Console.WriteLine(/* Output */ "Employee Shift Schedule for the Week:");

        for (int day = 0; day < shifts.GetLength(0); day++)
        {
            Console.WriteLine(/* Output */ $"Day {day + 1}:");
            for (int shift = 0; shift < shifts.GetLength(1); shift++)
            {
                Console.Write($"Shift {shift + 1}: ");
                for (int emp = 0; emp < shifts.GetLength(2); emp++)
                {
                    Console.Write(shifts[day, shift, emp] + " ");
                }
                Console.WriteLine(/* Output */ );
            }
            Console.WriteLine(/* Output */ );
        }
    }

    // Method to count how many employees are working each shift per day
    public static void CountEmployeesPerShift(string[,,] shifts)
    {
        Console.WriteLine(/* Output */ "Number of Employees Working Each Shift Per Day:");
        
        for (int day = 0; day < shifts.GetLength(0); day++)
        {
            Console.WriteLine(/* Output */ $"Day {day + 1}:");
            for (int shift = 0; shift < shifts.GetLength(1); shift++)
            {
                int employeeCount = shifts.GetLength(2);
                Console.WriteLine(/* Output */ $"Shift {shift + 1}: {employeeCount} employees");
            }
            Console.WriteLine(/* Output */ );
        }
    }
}
Explanation:
	•	The 3D array shifts stores the employee assignments for 7 days, 3 shifts per day, and 5 employees per shift.
	•	The DisplayShiftSchedule method prints out the schedule, showing which employees are assigned to which shifts on each day.
	•	The CountEmployeesPerShift method calculates how many employees are working each shift per day (since it's always 5 in this case, but this can be modified as needed).
Outcome:
	•	This system efficiently manages employee shift assignments, ensuring there is no overlap, and makes it easy to monitor shift distribution.









Skip to main content
Print book
14.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
14.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:55 AM
Table of contents
	•	Learning outcomes
	•	6.1 Introduction
	•	6.2 Database Operations in C#
	•	6.2.1 Database Creation in C#
	•	6.2.2 Connect to the Database with C#
	•	6.2.3 Accessing Data in the Database
	•	6.2.4 Insert into the Database with C#
	•	6.2.5 Update a Record in the Database with C#
	•	6.2.6 Delete a Record from the Database with C#
	•	6.3 Conclusion
	•	Case Study
Learning outcomes
By the end of this topic you should be able to:
	•	Develop the ability to write database applications in C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapter 22
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
6.1 Introduction
In this week, you learn how to perform basic database operations using system.data.SqlClient namespace in C#. You will also learn the basic database operations such as INSERT, UPDATE, SELECT and DELETE. Although the target database system is SQL Server Database, the same techniques can be applied to other database systems because the query syntax used is standard SQL that is generally supported by all relational database systems. We will also learn file handling operations in C#. We will explain what a File Stream, the two classes of file stream and how they work. At the end we will strengthen our knowledge of the material in this week with some exercises.
6.2 Database Operations in C#
A database is an organized collection of data, generally stored and accessed electronically from a computer system. Where databases are more complex they are often developed using formal design and modelling techniques. In this part we are concerned with the four basic database operation in C# such as INSERT, UPDATE, SELECT, and DELETE. Firstly we consider how to create a database and connect to the database with our C# code.
6.2.1 Database Creation in C#
To create a dataset in C#, let us under the format first.
 
Syntax:
 
Code Example
create database <database name>;
 
 
 
The database name in the angular brackets will be provided by the user. Then Open Microsoft SQL Server Management Studio and write the below script to create a database and table in it.
Code Example
create database Demodb;
 
use Demodb;
 
CREATE TABLE demo(
    articleID varchar(30) NOT NULL PRIMARY KEY,
    articleName varchar(30) NOT NULL,
);
 
insert into demo values(1, 'C#');
insert into demo values(2, 'C++');
 
 
 
 
After executing the above script the table named demo is created and it contains the following data as shown in below:
Output
articleID articleName
1          C#
2          C++
 
6.2.2 Connect to the Database with C#
After the data base creation, you need to connect your C# to the database. To work with a database, the first of all you required a connection. The connection to a database normally consists of the following parameters. Database name or Data Source: The database name to which the connection needs to be set up and connection can be made or you can say only work with one database at a time. Credentials: The username and password which needs to be used to establish a connection to the database. Optional Parameters: For each database type, you can specify optional parameters to provide more information on how .NET should connect to the database to handle the data.
 
The example below is to connect the database to C#
Code Example
// C# code to connect the database 
using System; 
using System.Data.SqlClient; 
namespace Database_Operation { 
class DBConn { 
    // Main Method 
    static void Main() 
    { 
        Connect(); 
        Console.ReadKey(); 
    } 
    static void Connect() 
    { 
        string constr; 
 
        // for the connection to 
        // sql server database 
        SqlConnection conn; 
// Data Source is the name of the 
        // server on which the database is stored. 
        // The Initial Catalog is used to specify 
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
 
        conn = new SqlConnection(constr); 
 
        // to open the connection 
        conn.Open(); 
 
        Console.WriteLine(/* Output */ "Connection Open!"); 
    
        // to close the connection 
        conn.Close(); 
    } 
} 
}
 
 
 
 
Output:
Output
Connection Open!
 
6.2.3 Accessing Data in the Database
To access data in the database, we use the SQL select statement and SqlDataReader for accessing the data in C#. This will enable us to retrieve some or all the data in the database depending on we use it. The C# code below demonstrate how we can retrieve all the data from the table demo in the database demodb.
Code Example
// C# code to demonstrate how 
// to use select statement 
using System; 
using System.Data.SqlClient; 
 
namespace Database_Operation { 
 
class SelectStatement{ 
 
    // Main Method 
    static void Main() 
    { 
        Read(); 
        Console.ReadKey(); 
    } 
 
    static void Read() 
    { 
        string constr; 
// for the connection to 
        // sql server database 
        SqlConnection conn; 
 
        // Data Source is the name of the 
        // server on which the database is stored. 
        // The Initial Catalog is used to specify 
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
 
        conn = new SqlConnection(constr); 
 
        // to open the connection 
        conn.Open(); 
 
        // use to perform read and write 
        // operations in the database 
        SqlCommand cmd; 
 
        // use to read a row in 
        // table one by one 
        SqlDataReader dreader; 
 
        // to sore SQL command and 
        // the output of SQL command 
        string sql, output = ""; 
 
        // use to fetch rwos from demo table 
        sql = "Select articleID, articleName from demo"; 
// to execute the sql statement 
        cmd = new SqlCommand(sql, conn); 
 
        // fetch all the rows 
        // from the demo table 
        dreader = cmd.ExecuteReader(); 
 
               // for one by one reading row 
        while (dreader.Read()) { 
            output = output + dreader.GetValue(0) + " - " + 
                                dreader.GetValue(1) + "\n"; 
        } 
 
        // to display the output 
        Console.Write(output); 
 
        // to close all the objects 
        dreader.Close(); 
        cmd.Dispose(); 
        conn.Close(); 
    } 
} 
}
 
 
 
 
 
 
 Output:
Output
1 - C#
2 - C++
     
6.2.4 Insert into the Database with C#
To insert data into the database table, we use the SQL insert statement in C#. The C# code below demonstrate how we can insert data to the table demo in the database demodb.
 
Code Example
// C# code for how to use Insert Statement 
using System; 
using System.Data.SqlClient; 
 
namespace Database_Operation { 
    
class InsertStatement { 
    
    // Main Method 
    static void Main() 
    { 
        Insert(); 
        Console.ReadKey(); 
    } 
 
    static void Insert() 
    { 
        string constr; 
 
        // for the connection to 
        // sql server database 
        SqlConnection conn; 
// Data Source is the name of the 
        // server on which the database is stored. 
        // The Initial Catalog is used to specify
          
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
 
conn = new SqlConnection(constr); 
 
        // to open the connection 
        conn.Open(); 
 
        // use to perform read and write 
        // operations in the database 
        SqlCommand cmd; 
        
        // data adapter object is use to 
        // insert, update or delete commands 
        SqlDataAdapter adap = new SqlDataAdapter(); 
        
        string sql = ""; 
 
// use the defined sql statement 
        // against our database 
        sql = "insert into demo values(3, 'Python')"; 
        
        // use to execute the sql command so we 
        // are passing query and connection object 
        cmd = new SqlCommand(sql, conn);    
        
// associate the insert SQL 
        // command to adapter object 
        adap.InsertCommand = new SqlCommand(sql, conn); 
        
        // use to execute the DML statement against 
        // our database
adap.InsertCommand.ExecuteNonQuery(); 
        
        // closing all the objects 
        cmd.Dispose(); 
        conn.Close(); 
 
         
    } 
} 
}   
    
 
 
Output:
 
Output
articleID articleName
1          C#
2          C++
3          Python
6.2.5 Update a Record in the Database with C#
In order to update a record in the database table, we use the SQL update statement in C#. The C# code below demonstrate how we can update a record in the table demo in the database demodb 
 
Code Example
// C# code for how to use Update Statement 
using System; 
using System.Data.SqlClient; 
   
namespace Database_Operation { 
      
class UpdateStatement { 
      
    // Main Method 
    static void Main() 
    { 
        Update(); 
        Console.ReadKey(); 
    }  
   static void Update() 
    { 
       string constr; 
    
        // for the connection to  
        // sql server database 
        SqlConnection conn;  
    
        // Data Source is the name of the  
        // server on which the database is stored. 
        // The Initial Catalog is used to specify 
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
    
        conn = new SqlConnection(constr); 
    
        // to open the connection 
        conn.Open();  
    
        // use to perform read and write 
        // operations in the database 
        SqlCommand cmd;  
           
        // data adapter object is use to  
        // insert, update or delete commands 
        SqlDataAdapter adap = new SqlDataAdapter();  
           
        string sql = ""; 
          
        // use the define sql  
        // statement against our database 
        sql = "update demo set articleName='django' where articleID=3";  
    
        // use to execute the sql command so we  
        // are passing query and connection object 
        cmd = new SqlCommand(sql, conn);  
          
        // associate the insert SQL 
        // command to adapter object 
        adap.InsertCommand = new SqlCommand(sql, conn);  
          
        // use to execute the DML statement against  
        // our database  
        adap.InsertCommand.ExecuteNonQuery();  
          
        // closing all the objects 
        cmd.Dispose(); 
        conn.Close(); 
    } 
} 
}   
   
 
 
 
Output:
Output
articleID articleName
1          C#
2          C++
3          django
 
6.2.6 Delete a Record from the Database with C#
In order to delete a record from the database table, we use the SQL delete statement in C#. The C# code below demonstrate how we can delete a record from the table demo in the database demodb. 
 
Code Example
// C# code for how to use Delete Statement 
using System; 
using System.Data.SqlClient; 
 
namespace Database_Operation { 
    
class DeleteStatement { 
    
    // Main Method 
    static void Main() 
    { 
        Delete(); 
        Console.ReadKey(); 
    } 
 
    static void Delete() 
    { 
    string constr; 
    
        // for the connection to 
        // sql server database 
        SqlConnection conn; 
// Data Source is the name of the 
        // server on which the database is stored. 
// The Initial Catalog is used to specify 
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
    
        conn = new SqlConnection(constr); 
    
        // to open the connection 
        conn.Open(); 
    
        // use to perform read and write 
        // operations in the database 
        SqlCommand cmd; 
        
        // data adapter object is use to 
        // insert, update or delete commands 
        SqlDataAdapter adap = new SqlDataAdapter();
string sql = ""; 
          
        // use the define SQL statement  
        // against our database 
        sql = "delete from demo where articleID=3";  
          
        // use to execute the sql command so we  
        // are passing query and connection object 
        cmd = new SqlCommand(sql, conn);  
          
        // associate the insert SQL  
        // command to adapter object 
        adap.InsertCommand = new SqlCommand(sql, conn);  
          
        // use to execute the DML statement 
        // against our database 
        adap.InsertCommand.ExecuteNonQuery();  
          
        // closing all the objects 
        cmd.Dispose(); 
        conn.Close(); 
    } 
} 
}
 
 
 
Output
articleID articleName
1          C#
	•	          C++
 
6.3 Conclusion
In this week we learnt about database operations in C#. You learnt database creation, how to connect to a SQL Server database. You also learnt how to perform CRUD operations on a database from within a C# program.
Case Study
Case Study 1: Employee Management System
In this case study, we will create an Employee Management System that allows users to:
	•	Add new employee records.
	•	View all employees.
	•	Update employee details.
	•	Delete employee records.

Scenario:
The company needs an application to manage employees' information such as their name, department, and salary. The system should allow administrators to:
	•	Add a new employee to the database.
	•	View the list of all employees.
	•	Edit existing employee information.
	•	Remove an employee from the database.

Database Schema:
The database will have a table named Employees with the following columns:
	•	EmployeeID (Primary Key)
	•	Name (Employee's name)
	•	Department (Employee's department)
	•	Salary (Employee's salary)

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY IDENTITY,
    Name NVARCHAR(100),
    Department NVARCHAR(100),
    Salary DECIMAL(18, 2)
);

C# Code for CRUD Operations:
1. Create New Employee:

using System;
using System.Data;
using System.Data.SqlClient;

public class EmployeeManagement
{
    private string connectionString = "your_connection_string_here";

    // Create operation: Add new employee to the database
    public void AddEmployee(string name, string department, decimal salary)
    {
        using (SqlConnection conn = new SqlConnection(connectionString))
        {
            conn.Open();
            string query = "INSERT INTO Employees (Name, Department, Salary) VALUES (@Name, @Department, @Salary)";
            using (SqlCommand cmd = new SqlCommand(query, conn))
            {
                cmd.Parameters.AddWithValue("@Name", name);
                cmd.Parameters.AddWithValue("@Department", department);
                cmd.Parameters.AddWithValue("@Salary", salary);
                cmd.ExecuteNonQuery();
            }
        }
    }
}

2. Read All Employees:

public void GetAllEmployees()
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "SELECT * FROM Employees";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            SqlDataReader reader = cmd.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(/* Output */ $"ID: {reader["EmployeeID"]}, Name: {reader["Name"]}, Department: {reader["Department"]}, Salary: {reader["Salary"]}");
            }
        }
    }
}

3. Update Employee Information:

public void UpdateEmployee(int employeeId, string name, string department, decimal salary)
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "UPDATE Employees SET Name = @Name, Department = @Department, Salary = @Salary WHERE EmployeeID = @EmployeeID";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@Name", name);
            cmd.Parameters.AddWithValue("@Department", department);
            cmd.Parameters.AddWithValue("@Salary", salary);
            cmd.Parameters.AddWithValue("@EmployeeID", employeeId);
            cmd.ExecuteNonQuery();
        }
    }
}

4. Delete Employee Record:

public void DeleteEmployee(int employeeId)
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "DELETE FROM Employees WHERE EmployeeID = @EmployeeID";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@EmployeeID", employeeId);
            cmd.ExecuteNonQuery();
        }
    }
}

Usage Example:

class MainProgram
{
    static void Main(string[] args)
    {
        EmployeeManagement empMgmt = new EmployeeManagement();

        // Add a new employee
        empMgmt.AddEmployee("John Doe", "IT", 50000);

        // View all employees
        empMgmt.GetAllEmployees();

        // Update an employee
        empMgmt.UpdateEmployee(1, "John Doe", "HR", 55000);

        // Delete an employee
        empMgmt.DeleteEmployee(1);

        Console.WriteLine(/* Output */ "Operations completed successfully!");
    }
}

Case Study 2: Product Inventory Management System
In this case study, we will create a Product Inventory Management System that allows users to:
	•	Add new products.
	•	View all products.
	•	Update product details.
	•	Remove products from the inventory.

Scenario:
The company needs an application to manage products in their inventory. Each product has:
	•	A unique product ID.
	•	A name.
	•	A description.
	•	A price.
	•	A quantity available in the inventory.

Database Schema:
The database will have a table named Products with the following columns:
	•	ProductID (Primary Key)
	•	ProductName (Name of the product)
	•	Description (Description of the product)
	•	Price (Price of the product)
	•	Quantity (Quantity of the product in stock)

CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY,
    ProductName NVARCHAR(100),
    Description NVARCHAR(200),
    Price DECIMAL(18, 2),
    Quantity INT
);

C# Code for CRUD Operations:
1. Create New Product:

public class ProductInventory
{
    private string connectionString = "your_connection_string_here";

    // Create operation: Add a new product to the inventory
    public void AddProduct(string productName, string description, decimal price, int quantity)
    {
        using (SqlConnection conn = new SqlConnection(connectionString))
        {
            conn.Open();
            string query = "INSERT INTO Products (ProductName, Description, Price, Quantity) VALUES (@ProductName, @Description, @Price, @Quantity)";
            using (SqlCommand cmd = new SqlCommand(query, conn))
            {
                cmd.Parameters.AddWithValue("@ProductName", productName);
                cmd.Parameters.AddWithValue("@Description", description);
                cmd.Parameters.AddWithValue("@Price", price);
                cmd.Parameters.AddWithValue("@Quantity", quantity);
                cmd.ExecuteNonQuery();
            }
        }
    }
}

2. Read All Products:

public void GetAllProducts()
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "SELECT * FROM Products";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            SqlDataReader reader = cmd.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(/* Output */ $"ID: {reader["ProductID"]}, Name: {reader["ProductName"]}, Price: {reader["Price"]}, Quantity: {reader["Quantity"]}");
            }
        }
    }
}

3. Update Product Information:

public void UpdateProduct(int productId, string productName, string description, decimal price, int quantity)
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "UPDATE Products SET ProductName = @ProductName, Description = @Description, Price = @Price, Quantity = @Quantity WHERE ProductID = @ProductID";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@ProductName", productName);
            cmd.Parameters.AddWithValue("@Description", description);
            cmd.Parameters.AddWithValue("@Price", price);
            cmd.Parameters.AddWithValue("@Quantity", quantity);
            cmd.Parameters.AddWithValue("@ProductID", productId);
            cmd.ExecuteNonQuery();
        }
    }
}

4. Delete Product Record:

public void DeleteProduct(int productId)
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "DELETE FROM Products WHERE ProductID = @ProductID";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@ProductID", productId);
            cmd.ExecuteNonQuery();
        }
    }
}

Usage Example:

class MainProgram
{
    static void Main(string[] args)
    {
        ProductInventory productInventory = new ProductInventory();

        // Add a new product
        productInventory.AddProduct("Laptop", "A high-performance laptop", 1200.50m, 100);

        // View all products
        productInventory.GetAllProducts();

        // Update a product
        productInventory.UpdateProduct(1, "Laptop", "A top-end laptop", 1250.00m, 80);

        // Delete a product
        productInventory.DeleteProduct(1);

        Console.WriteLine(/* Output */ "Operations completed successfully!");
    }
}








Skip to main content
Print book
15.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (First Block)
Book:
15.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:55 AM
Table of contents
	•	Learning outcomes
	•	7.1 File Handling
	•	7.1.1 StreamWriter Class
	•	7.1.2 StreamReader Class
	•	7.2 Conclusion
	•	Case Study
Learning outcomes
By the end of this topic you should be able to:
	•	Develop the ability to write database applications in C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 17
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
7.1 File Handling
In programming, a file is used to store the data. The term File Handling refers to the various operations like creating the file, reading from the file, writing to the file, appending the file, etc. There are two basic operation which is mostly used in file handling, they are: reading and writing of the file. The file becomes stream when we open the file for writing and reading. A stream is a sequence of bytes which is used for communication. In C#, System.IO namespace contains classes which handle input and output streams and provide information about file and directory structure. There are two major stream classes that are used for most of the operations in file handling. These classes are StreamWriter class and StreamReader class.
7.1.1 StreamWriter Class
The StreamWriter class implements TextWriter for writing character to stream in a particular format. The class contains the following method which are mostly used.
 
Method
Description
Close()
Closes the current StreamWriter object and stream associate with it.
Flush()
Clears all the data from the buffer and write it in the stream associate with it.
Write()
Write data to the stream. It has different overloads for different data types to write in stream.
WriteLine()
It is same as Write() but it adds the newline character at the end of the data.
 
Example:
Code Example
// C# program to write user input 
// to a file using StreamWriter Class 
using System; 
using System.IO; 
 
namespace GeeksforGeeks { 
    
class GFG { 
    
    class WriteToFile { 
        
        public void Data() 
        { 
            // This will create a file named sample.txt 
            // at the specified location 
            StreamWriter sw = new StreamWriter("C://Test.txt"); 
            
            // To write on the console screen 
            Console.WriteLine(/* Output */ "Enter the Text that you want to write on File"); 
            
            // To read the input from the user 
            string str = Console.ReadLine(); 
            
            // To write a line in buffer 
            sw.WriteLine(str); 
            
            // To write in output stream 
            sw.Flush(); 
            
            // To close the stream 
            sw.Close(); 
        } 
    } 
    
    // Main Method 
    static void Main(string[] args) 
    { 
        WriteToFile wr = new WriteToFile(); 
        wr.Data(); 
        Console.ReadKey(); 
    } 
} 
}
 
 
 
The C# example above will create a text file called Test.txt on the C: drive.  
 
Output: 
Output
You will find the file at the specified location having the content you entered.
 
7.1.2 StreamReader Class
The StreamReader class implements TextReader for reading character from the stream in a particular format. The class contains the following method which are mostly used.
Method
Description
Close()
Closes the current StreamReader object and stream associate with it.
Peek()
Returns the next available character but does not consume it.
Read()
Reads the next character in input stream and increment characters position by one in the stream
ReadLine()
Reads a line from the input stream and return the data in form of string
Seek()
It is use to read/write at the specific location from a file
 
Example:
Code Example
// C# program to read from a file 
// using StreamReader Class 
using System; 
using System.IO; 
 
namespace GeeksforGeeks { 
    
class GFG { 
    
    class ReadFile { 
        
        public void DataReading() 
        { 
            // Taking a new input stream i.e. 
            // geeksforgeeks.txt and opens it 
            StreamReader sr = new StreamReader("C://Test.txt"); 
            
            Console.WriteLine(/* Output */ "Content of the File"); 
            
            // This is used to specify from where 
            // to start reading input stream 
            sr.BaseStream.Seek(0, SeekOrigin.Begin); 
            
            // To read line from input stream 
            string str = sr.ReadLine(); 
            // To read the whole file line by line 
            while (str != null) 
            { 
                Console.WriteLine(/* Output */ str); 
                str = sr.ReadLine(); 
            } 
            Console.ReadLine(); 
            
            // to close the stream 
            sr.Close(); 
        } 
    }
// Main Method 
    static void Main(string[] args) 
    { 
        ReadFile wr = new ReadFile(); 
        wr.DataReading(); 
    } 
} 
}
 
             
    
    
 
 
 
Output
Output
You will find the context of the file at the specified location having the content you entered.
 
7.2 Conclusion
In this week we learnt about file handling, specifically the two classes for reading and writing textfiles. These are the StreamReader and StreamWriter classes. Examples were provided to show how to implement these classes.
Case Study
Case Study 1: Personal Notes Application
Scenario:
A user wants to manage personal notes by storing, reading, updating, and deleting notes in a simple file-based application. Each note is stored in a separate text file in a folder named Notes, with the file names representing the titles of the notes. The application should allow the user to:
	•	Create a new note by providing a title and content.
	•	View a list of all existing notes (file names).
	•	Read the content of a selected note.
	•	Delete a selected note.

Directory Structure:
All notes are stored in a folder called Notes (which should be created beforehand).

Notes
│
├── Note1.txt
├── Note2.txt
├── Note3.txt
...
C# Code for File Operations:
1. Create New Note:

using System;
using System.IO;

public class FileManager
{
    private string notesDirectory = @"C:\Notes\"; // Path to the Notes folder

    // Create operation: Add a new note
    public void CreateNote(string title, string content)
    {
        string filePath = Path.Combine(notesDirectory, title + ".txt");

        if (!File.Exists(filePath)) // Ensure the file doesn't already exist
        {
            File.WriteAllText(filePath, content);
            Console.WriteLine(/* Output */ "Note created successfully.");
        }
        else
        {
            Console.WriteLine(/* Output */ "A note with this title already exists.");
        }
    }
}

2. View All Notes:

public void ViewAllNotes()
{
    if (Directory.Exists(notesDirectory))
    {
        string[] noteFiles = Directory.GetFiles(notesDirectory, "*.txt");

        if (noteFiles.Length > 0)
        {
            Console.WriteLine(/* Output */ "Available notes:");
            foreach (var note in noteFiles)
            {
                string noteTitle = Path.GetFileNameWithoutExtension(note);
                Console.WriteLine(/* Output */ noteTitle);
            }
        }
        else
        {
            Console.WriteLine(/* Output */ "No notes available.");
        }
    }
    else
    {
        Console.WriteLine(/* Output */ "Notes directory not found.");
    }
}

3. Read Note Content:

public void ReadNoteContent(string title)
{
    string filePath = Path.Combine(notesDirectory, title + ".txt");

    if (File.Exists(filePath))
    {
        string content = File.ReadAllText(filePath);
        Console.WriteLine(/* Output */ $"Content of {title}:");
        Console.WriteLine(/* Output */ content);
    }
    else
    {
        Console.WriteLine(/* Output */ "Note not found.");
    }
}

4. Delete Note:

public void DeleteNote(string title)
{
    string filePath = Path.Combine(notesDirectory, title + ".txt");

    if (File.Exists(filePath))
    {
        File.Delete(filePath);
        Console.WriteLine(/* Output */ "Note deleted successfully.");
    }
    else
    {
        Console.WriteLine(/* Output */ "Note not found.");
    }
}

Usage Example:
class MainProgram
{
    static void Main(string[] args)
    {
        FileManager fileManager = new FileManager();

        // Create a new note
        fileManager.CreateNote("FirstNote", "This is the content of the first note.");

        // View all notes
        fileManager.ViewAllNotes();

        // Read a note's content
        fileManager.ReadNoteContent("FirstNote");

        // Delete a note
        fileManager.DeleteNote("FirstNote");

        Console.WriteLine(/* Output */ "Operations completed successfully.");
    }
}

Case Study 2: Student Report Management System
Scenario:
The school wants to manage student reports stored in text files. Each student has a report file named with their ID (e.g., 12345.txt for a student with ID 12345). The system should allow administrators to:
	•	Add a new report for a student.
	•	View all student reports.
	•	Update a student report.
	•	Delete a student's report.

Directory Structure:
The reports are stored in a folder called StudentReports.

StudentReports
│
├── 12345.txt
├── 67890.txt
├── 11223.txt
...
C# Code for File Operations:
1. Create New Report:

public class ReportManager
{
    private string reportsDirectory = @"C:\StudentReports\"; // Path to the Reports folder

    // Create operation: Add a new student report
    public void CreateReport(string studentId, string content)
    {
        string filePath = Path.Combine(reportsDirectory, studentId + ".txt");

        if (!File.Exists(filePath)) // Check if the report already exists
        {
            File.WriteAllText(filePath, content);
            Console.WriteLine(/* Output */ "Report created successfully.");
        }
        else
        {
            Console.WriteLine(/* Output */ "A report for this student already exists.");
        }
    }
}

2. View All Reports:

public void ViewAllReports()
{
    if (Directory.Exists(reportsDirectory))
    {
        string[] reportFiles = Directory.GetFiles(reportsDirectory, "*.txt");

        if (reportFiles.Length > 0)
        {
            Console.WriteLine(/* Output */ "Available student reports:");
            foreach (var report in reportFiles)
            {
                string studentId = Path.GetFileNameWithoutExtension(report);
                Console.WriteLine(/* Output */ studentId);
            }
        }
        else
        {
            Console.WriteLine(/* Output */ "No reports available.");
        }
    }
    else
    {
        Console.WriteLine(/* Output */ "Reports directory not found.");
    }
}

3. Read Report Content:

public void ReadReportContent(string studentId)
{
    string filePath = Path.Combine(reportsDirectory, studentId + ".txt");

    if (File.Exists(filePath))
    {
        string content = File.ReadAllText(filePath);
        Console.WriteLine(/* Output */ $"Report for student {studentId}:");
        Console.WriteLine(/* Output */ content);
    }
    else
    {
        Console.WriteLine(/* Output */ "Report not found.");
    }
}

4. Update Report:

public void UpdateReport(string studentId, string newContent)
{
    string filePath = Path.Combine(reportsDirectory, studentId + ".txt");

    if (File.Exists(filePath))
    {
        File.WriteAllText(filePath, newContent);
        Console.WriteLine(/* Output */ "Report updated successfully.");
    }
    else
    {
        Console.WriteLine(/* Output */ "Report not found.");
    }
}

5. Delete Report:

public void DeleteReport(string studentId)
{
    string filePath = Path.Combine(reportsDirectory, studentId + ".txt");

    if (File.Exists(filePath))
    {
        File.Delete(filePath);
        Console.WriteLine(/* Output */ "Report deleted successfully.");
    }
    else
    {
        Console.WriteLine(/* Output */ "Report not found.");
    }
}

Usage Example:

class MainProgram
{
    static void Main(string[] args)
    {
        ReportManager reportManager = new ReportManager();

        // Create a new student report
        reportManager.CreateReport("12345", "Student performance is excellent.");

        // View all student reports
        reportManager.ViewAllReports();

        // Read a student report
        reportManager.ReadReportContent("12345");

        // Update a student report
        reportManager.UpdateReport("12345", "Student performance has improved significantly.");

        // Delete a student report
        reportManager.DeleteReport("12345");

        Console.WriteLine(/* Output */ "Operations completed successfully.");
    }
}
















Skip to main content
Print book
1.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (Second Block)
Book:
1.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:58 AM
Table of contents
	•	1. Learning outcomes
	•	2. Collaborative Project
	•	3. Introduction to LINQ
	•	3.1. Application of LINQ
	•	3.2. The shared System.Linq namespace
	•	4. LINQ Standard Query operators
	•	4.1. The OrderBy() method.
	•	4.2. The Any() method.
	•	4.3. Case Studies
	•	4.4. WEEKLY ACTIVITY
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








Skip to main content
Print book
2.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (Second Block)
Book:
2.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:59 AM
Table of contents
	•	1. Learning outcomes
	•	2. Introduction to Generics
	•	3. Generic Methods
	•	4. Generic Classes
	•	5. Generic Interfaces
	•	6. Constraints on Generics
	•	7. Case Study 1: Student Grade Management System
	•	8. Case Study 2: Task Scheduling System (Using Queue)
	•	9. Case Study 3: Inventory Management System for a Retail Store
	•	10. Case Study 4: Library Book Loan Management System
	•	11. References
1. Learning outcomes

By the end of this lesson, you should be able to:
	•	Understand C# collections

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 
Chapter 9, 20 & 21
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Introduction to Generics
Generics in C# allow you to create classes, methods, and data structures that work with any data type while ensuring compile-time type safety. They prevent the need to write duplicate code and help reduce runtime errors. For instance, instead of writing separate versions of a function for integers, strings, etc., generics let you write one version that works with all data types.
Play Video
 
Example 1: Using a generic method to display any type
public class DisplayUtility
{
    public static void Show<T>(T value)
    {
        Console.WriteLine(/* Output */ $"Value: {value}");
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
    Console.WriteLine(/* Output */ n); // No boxing/unboxing needed
}
Output:
1  
2  
3


3. Generic Methods
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
        Console.WriteLine(/* Output */ $"x = {x}, y = {y}");
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
        Console.WriteLine(/* Output */ AreEqual(5, 5));
        Console.WriteLine(/* Output */ AreEqual("apple", "banana"));
    }
}
Output:
True  
False
4. Generic Classes
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
 
        Console.WriteLine(/* Output */ intBox.Content);
        Console.WriteLine(/* Output */ strBox.Content);
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
        Console.WriteLine(/* Output */ $"ID: {student.First}, Name: {student.Second}");
    }
}
Output:
ID: 101, Name: Alice
 
5. Generic Interfaces
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
 
        Console.WriteLine(/* Output */ p1.CompareTo(p2)); // Output depends on alphabetical order
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
            Console.WriteLine(/* Output */ item);
    }
}
Output:
1  
2  
3
 
6. Constraints on Generics
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
        Console.WriteLine(/* Output */ instance.Text);
    }
}
Output:
Created
Example 2: Using class constraint
public class ReferenceHandler<T> where T : class
{
    public void PrintTypeName()
    {
        Console.WriteLine(/* Output */ typeof(T).Name);
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
 
7. Case Study 1: Student Grade Management System
Case Study 1: Student Grade Management System
Problem Statement:
A university wants a system to manage student records and their corresponding grades. The system should:
	•	Store student data in a generic way.
	•	Use a dictionary to store student IDs and their grades.
	•	Calculate average grades and display student results.

Solution Approach:
	•	Create a generic Student<T> class to store student info (like ID and Name).
	•	Use a Dictionary<int, double> to map student IDs to their grades.
	•	Iterate over the dictionary and calculate the average

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
            Console.WriteLine(/* Output */ $"{student.Name} (ID: {student.ID}) - Grade: {grade}");
            total += grade;
        }
 
        double avg = total / students.Count;
        Console.WriteLine(/* Output */ $"\nAverage Grade: {avg:F2}");
    }
}

Output:
Alice (ID: 1) - Grade: 85.5  
Bob (ID: 2) - Grade: 78  
Charlie (ID: 3) - Grade: 92.3
 
Average Grade: 85.27
 
8. Case Study 2: Task Scheduling System (Using Queue)
Case Study 2: Task Scheduling System (Using Queue<T>)
Problem Statement:
A software project management tool needs a feature to schedule and execute tasks in the order they are added (FIFO). Each task includes a name and an estimated time. The system must:
	•	Store tasks in order.
	•	Process each task in FIFO manner using Queue<T>.

Solution Approach:
	•	Create a generic TaskItem<T> class.
	•	Use Queue<TaskItem<string>> to manage task execution.
	•	Print and simulate execution.

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
 
        Console.WriteLine(/* Output */ "Processing Tasks:\n");
 
        while (taskQueue.Count > 0)
        {
            var task = taskQueue.Dequeue();
            Console.WriteLine(/* Output */ $"Task: {task.Name}, Estimated Time: {task.TimeInMinutes} mins");
        }
    }
}

Output:
Processing Tasks:
 
Task: Compile Code, Estimated Time: 10 mins  
Task: Run Tests, Estimated Time: 20 mins  
Task: Deploy Build, Estimated Time: 15 mins
 
9. Case Study 3: Inventory Management System for a Retail Store
Case Study 3: Inventory Management System for a Retail Store
Problem Statement:
A retail store needs a system to manage its product inventory. Each product has a unique ID, name, and available quantity. The system should:
	•	Use a generic class to handle product information.
	•	Use a dictionary to store product IDs and their stock quantities.
	•	Allow updates to inventory (restocking or selling).
	•	Display product details and total stock available.

Solution Approach:
	•	Create a Product<T> class that stores the product ID, name, and price.
	•	Use Dictionary<int, int> to map product IDs to their current stock levels.
	•	Iterate through the inventory and display information.

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
            Console.WriteLine(/* Output */ $"{item.Name} (ID: {item.ProductID}) - Stock: {quantity}, Price: R{item.Price:F2}");
            totalStock += quantity;
        }

        Console.WriteLine(/* Output */ $"\nTotal Items in Inventory: {totalStock}");
    }
}
Output:
Laptop (ID: 101) - Stock: 15, Price: R899.99  
Mouse (ID: 102) - Stock: 50, Price: R25.50  
Keyboard (ID: 103) - Stock: 30, Price: R45.00  

Total Items in Inventory: 95


10. Case Study 4: Library Book Loan Management System
Case Study 4: Library Book Loan Management System
Problem Statement:
A library wants to track the borrowing of books by students. Each student can borrow multiple books. The system should:
	•	Use a generic class to store student details.
	•	Use a dictionary to map student IDs to lists of books they've borrowed.
	•	Display each student's borrowed books.

Solution Approach:
	•	Use a generic Student<T> class to hold student details.
	•	Use a Dictionary<int, List<string>> to map student IDs to book titles.
	•	Display all borrowings per student.

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
            Console.WriteLine(/* Output */ $"{student.Name} (ID: {student.ID}) has borrowed:");

            foreach (var book in borrowedBooks[student.ID])
            {
                Console.WriteLine(/* Output */ $"  - {book}");
            }
            Console.WriteLine(/* Output */ );
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
  
11. References
Deitel, H.M. and Deitel, P.J., 2017. C# How to Program. 6th ed. Boston: Pearson Education.
Microsoft, 2024. Generics in C#. [online] Microsoft Learn. Available at: https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/ [Accessed 11 April 2025].
Albahari, J. and Albahari, B., 2021. C# 10 in a Nutshell: The Definitive Reference. 7th ed. Sebastopol: O’Reilly Media.
Microsoft, 2024. Collections in .NET. [online] Microsoft Learn. Available at: https://learn.microsoft.com/en-us/dotnet/standard/collections/ [Accessed 11 April 2025].
 
Skip to main content
Print book
3.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (Second Block)
Book:
3.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 11:59 AM
Table of contents
	•	1. Learning outcomes
	•	2. Introduction to C# Collections
	•	3. List (Generic List)
	•	4. Dictionary
	•	5. Queue
	•	6. Stack
	•	7. HashSet
	•	8. Case Study 1: Student Record Management System
	•	9. Case Study 2: Student Grades Tracker
	•	10. Case Study 3: Online Shopping Cart
	•	11. Case Study 4: Call Center Queue
	•	12. Case Study 5: Recently Opened Documents
	•	13. Case Study 5: Library Book Borrowing System
	•	14. Scenario Question: Inventory Management System
	•	15. References
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



























Skip to main content
Print book
4.1.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (Second Block)
Book:
4.1.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 12:00 PM
Table of contents
	•	1. Learning outcomes
	•	2. Concurrency in C# - Multithreading and Parallelism
	•	3. Implementing Multithreading in C#
	•	4. Case Study 1: Asynchronous File Downloading
	•	5. Case Study 2: Parallel Processing of Large Data Set
	•	6. Case Study 3: Parallel Data Aggregation
	•	7. Case Study 4: Thread Safety in Bank Account Operations
	•	8. Case Study 5: Thread Safety in Bank Account Operations with Random Values
	•	9. Concept Overview
	•	10. Video
	•	11. Scenario 1: Concurrency in Processing Orders in an E-Commerce System
	•	12. References
1. Learning outcomes

By the end of this lesson, you should be able to:
	•	Develop the ability to implement concurrency and parallelism in C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469  Chapter 9 & 21
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Concurrency in C# - Multithreading and Parallelism
Overview:
Concurrency and parallelism are essential concepts for building efficient, high-performance applications in C#. Concurrency refers to the ability of a system to manage multiple tasks at once, while parallelism involves executing multiple tasks simultaneously on multiple processors or cores. In this week’s notes, we will explore methods for creating threads and implementing multithreading in C#.

Examine Different Methods to Create Threads in C#
Introduction to Threads:
In C#, threads are used for executing tasks concurrently, which can improve the performance of applications, especially in I/O-bound and CPU-bound operations. The .NET framework provides several ways to create and manage threads. Understanding these methods is crucial for building responsive and efficient applications.
1. Using the Thread Class:
The Thread class in C# is part of the System.Threading namespace and is one of the most direct ways to create and manage threads. You can create a new thread by providing a ThreadStart delegate, which points to the method that the thread will execute.
2. Using the Task Class (Recommended):
The Task class, introduced in .NET Framework 4.0, provides a more modern and flexible approach to working with threads. The Task class is part of the System.Threading.Tasks namespace and makes it easier to handle asynchronous operations and parallel tasks.
3. Using the ThreadPool:
The ThreadPool class provides a pool of worker threads that can be used to perform tasks without the need to manually create and manage individual threads. It is efficient for short-lived tasks, reducing the overhead of creating and destroying threads.

1. Example Using the Thread Class:
using System;
using System.Threading;
 
class ThreadExample
{
    // Method to be executed by the thread
    static void PrintNumbers()
    {
        for (int idx = 1; idx <= 5; idx++)
        {
            Console.WriteLine(/* Output */ $"Number {i}");
            Thread.Sleep(1000);  // Simulate some work by sleeping for 1 second
        }
    }
 
    static void Main()
    {
        // Create a new thread to execute the PrintNumbers method
        Thread thread = new Thread(new ThreadStart(PrintNumbers));
        thread.Start();  // Start the thread
 
        // Continue with the main thread
        Console.WriteLine(/* Output */ "Main thread is doing some work...");
        thread.Join();  // Wait for the created thread to finish
    }
}
Output:
Main thread is doing some work...
Number 1
Number 2
Number 3
Number 4
Number 5
Explanation:
	•	A new thread is created using the Thread class and starts executing the PrintNumbers method.
	•	The Join method is used to wait for the newly created thread to finish before continuing the main thread.

2. Example Using the Task Class:
using System;
using System.Threading.Tasks;
 
class TaskExample
{
    // Method to be executed by the task
    static void PrintNumbers()
    {
        for (int idx = 1; idx <= 5; idx++)
        {
            Console.WriteLine(/* Output */ $"Number {i}");
            Task.Delay(1000).Wait();  // Simulate some work by delaying for 1 second
        }
    }
 
    static void Main()
    {
        // Create a new task to execute the PrintNumbers method
        Task task = new Task(PrintNumbers);
        task.Start();  // Start the task
 
        // Continue with the main thread
        Console.WriteLine(/* Output */ "Main thread is doing some work...");
        task.Wait();  // Wait for the task to finish
    }
}
Output:
Main thread is doing some work...
Number 1
Number 2
Number 3
Number 4
Number 5
Explanation:
	•	A task is created and executed with the Task class.
	•	Task.Delay is used to simulate work, and the Wait method ensures that the main thread waits for the task to complete before continuing.

3. Example Using the ThreadPool:
using System;
using System.Threading;
 
class ThreadPoolExample
{
    // Method to be executed by the thread pool worker
    static void PrintNumbers(object state)
    {
        for (int idx = 1; idx <= 5; idx++)
        {
            Console.WriteLine(/* Output */ $"Number {i}");
            Thread.Sleep(1000);  // Simulate some work by sleeping for 1 second
        }
    }
 
    static void Main()
    {
        // Queue the work item to the thread pool
        ThreadPool.QueueUserWorkItem(PrintNumbers);
 
        // Continue with the main thread
        Console.WriteLine(/* Output */ "Main thread is doing some work...");
        Thread.Sleep(6000);  // Sleep for enough time to allow the thread pool to finish its work
    }
}
Output:
Main thread is doing some work...
Number 1
Number 2
Number 3
Number 4
Number 5
Explanation:
	•	The ThreadPool.QueueUserWorkItem method is used to queue a method to be executed by a worker thread from the thread pool.
	•	The main thread sleeps for a sufficient amount of time to ensure that the worker thread completes its task.

3. Implementing Multithreading in C#
Introduction to Multithreading:
Multithreading allows multiple tasks to run concurrently, which can significantly improve the performance of an application, especially when dealing with CPU-intensive operations. In C#, multithreading can be implemented using the Thread class, the Task class, and the ThreadPool.
Example: Running Multiple Tasks in Parallel
In this example, we will use multiple threads to calculate the sum of numArray in different ranges concurrently, and then combine the results:

using System;
using System.Threading;
using System.Threading.Tasks;
 
class MultithreadingExample
{
    static void CalculateSum(int start, int end, int threadNumber)
    {
        int sum = 0;
        for (int idx = start; idx <= end; idx++)
        {
            sum += i;
        }
        Console.WriteLine(/* Output */ $"Thread {threadNumber}: Sum = {sum}");
    }
 
    static void Main()
    {
        // Define ranges for each thread to calculate the sum
        Task task1 = Task.Run(() => CalculateSum(1, 1000, 1));  // Thread 1
        Task task2 = Task.Run(() => CalculateSum(1001, 2000, 2));  // Thread 2
        Task task3 = Task.Run(() => CalculateSum(2001, 3000, 3));  // Thread 3
 
        // Wait for all tasks to complete
        Task.WhenAll(task1, task2, task3).Wait();
    }
}
Output:
Thread 1: Sum = 500500
Thread 2: Sum = 1501500
Thread 3: Sum = 4501500
Explanation:
	•	Three tasks are created using Task.Run to calculate the sum of different ranges of numArray in parallel.
	•	The results are printed concurrently, and the main thread waits for all tasks to finish using Task.WhenAll.

Key Points:
	•	Thread Class: Provides low-level control over thread creation and execution. Best for simple tasks, but more complex handling is needed for synchronization.
	•	Task Class: A higher-level abstraction that simplifies multithreading and integrates with asynchronous programming.
	•	ThreadPool: Ideal for short-lived tasks to avoid overhead of creating and destroying threads manually.
	•	Multithreading Benefits: Multithreading can improve the responsiveness and performance of applications by utilizing multiple processors or cores.
	•	Synchronization: When using multithreading, it's essential to ensure proper synchronization (e.g., using locks or other synchronization techniques) to avoid race conditions.
 
4. Case Study 1: Asynchronous File Downloading
Case Study 1: Asynchronous File Downloading
Problem:
You are developing a file downloader that needs to download multiple files from the internet concurrently. This will improve the download speed and prevent the application from freezing while waiting for downloads to complete. You need to implement a solution using multithreading or tasks to handle the download process.
Solution:
We will use the Task class to download files concurrently. Each file will be downloaded in a separate task to improve performance and responsiveness.
using System;
using System.Net.Http;
using System.Threading.Tasks;
 
class FileDownloader
{
    // Method to simulate downloading a file
    static async Task DownloadFileAsync(string url, string filename)
    {
        using (HttpClient client = new HttpClient())
        {
            Console.WriteLine(/* Output */ $"Starting download for {filename} from {url}");
            var content = await client.GetStringAsync(url);  // Simulate downloading content
            Console.WriteLine(/* Output */ $"Downloaded {filename} successfully.");
        }
    }
 
    static async Task Main(string[] args)
    {
        string[] fileUrls = {
            "https://example.com/file1",
            "https://example.com/file2",
            "https://example.com/file3"
        };
        string[] filenames = { "file1", "file2", "file3" };
 
        // Start downloading files concurrently using tasks
        Task[] downloadTasks = new Task[fileUrls.Length];
 
        for (int idx = 0; idx < fileUrls.Length; idx++)
        {
            int index = i;
            downloadTasks[idx] = DownloadFileAsync(fileUrls[index], filenames[index]);
        }
 
        // Wait for all downloads to complete
        await Task.WhenAll(downloadTasks);
        Console.WriteLine(/* Output */ "All files downloaded successfully.");
    }
}
Explanation:
	•	The DownloadFileAsync method is asynchronous and uses HttpClient to simulate downloading a file.
	•	We start three concurrent tasks to download the files using Task.WhenAll, ensuring all downloads happen in parallel.
	•	The async and await keywords help us manage asynchronous operations efficiently.
Outcome:
Starting download for file1 from https://example.com/file1
Starting download for file2 from https://example.com/file2
Starting download for file3 from https://example.com/file3
Downloaded file1 successfully.
Downloaded file2 successfully.
Downloaded file3 successfully.
All files downloaded successfully.
 
5. Case Study 2: Parallel Processing of Large Data Set
Case Study 2: Parallel Processing of Large Data Set
Problem:
You need to process a large dataset of numArray and perform some intensive computation on each number (e.g., squaring the numArray). The dataset is too large to process in a single thread, and you want to speed up the process using parallelism.
Solution:
We can use the Parallel.For method to process the dataset concurrently in multiple threads.
using System;
using System.Linq;
using System.Threading.Tasks;
 
class ParallelProcessingExample
{
    static void ProcessData(int number)
    {
        // Simulate a time-consuming computation
        double result = Math.Pow(number, 2);  // Square the number
        Console.WriteLine(/* Output */ $"Processed number: {number}, Result: {result}");
    }
 
    static void Main()
    {
        // Simulate a large dataset of numArray from 1 to 100
        int[] numArray = Enumerable.Range(1, 100).ToArray();
 
        // Use Parallel.For to process the dataset concurrently
        Parallel.For(0, numArray.Length, i =>
        {
            ProcessData(numArray[idx]);
        });
 
        Console.WriteLine(/* Output */ "All data processed.");
    }
}
Explanation:
	•	We use Parallel.For to process each element of the array in parallel. This splits the work across multiple threads and speeds up the computation.
	•	Each number is squared in the ProcessData method, and the result is printed.
Outcome:
Processed number: 1, Result: 1
Processed number: 2, Result: 4
Processed number: 3, Result: 9
...
Processed number: 100, Result: 10000
All data processed.

 
6. Case Study 3: Parallel Data Aggregation
Case Study 3: Parallel Data Aggregation
Problem:
You are given a collection of numArray, and you need to compute the sum of all the numArray in the collection. However, the dataset is very large, and you want to leverage parallelism to compute the sum more quickly.
Solution:
Use Parallel.Aggregate or Parallel.For to aggregate the sum concurrently.
using System;
using System.Linq;
using System.Threading.Tasks;
 
class ParallelAggregationExample
{
    static void Main()
    {
        // Generate a large dataset of numArray
        int[] numArray = Enumerable.Range(1, 1000000).ToArray();
 
        // Use Parallel LINQ (PLINQ) for parallel aggregation
        int totalSum = numArray.AsParallel().Sum();
 
        Console.WriteLine(/* Output */ $"The total sum is: {totalSum}");
    }
}
Explanation:
	•	We use PLINQ (AsParallel()) to perform the summation in parallel, which automatically splits the work across multiple threads.
	•	The Sum() method computes the sum of the entire dataset efficiently using parallelism.
Outcome:
The total sum is: 500000500000

 
7. Case Study 4: Thread Safety in Bank Account Operations
Case Study 4: Thread Safety in Bank Account Operations
Problem:
You are building a bank account system where multiple users can access and update the account balance concurrently. You need to ensure thread safety when depositing or withdrawing money from the account.
Solution:
We will use locking to ensure that only one thread can access the critical section of the code (the account balance) at a time. This is achieved using lock in C#.
using System;
using System.Threading;
 
class BankAccount
{
    private decimal balance;
    private readonly object balanceLock = new object();  // Lock object for thread safety
 
    public BankAccount(decimal initialBalance)
    {
        balance = initialBalance;
    }
 
    public void Deposit(decimal amount)
    {
        lock (balanceLock)  // Lock to ensure thread safety
        {
            balance += amount;
            Console.WriteLine(/* Output */ $"Deposited {amount:C}. New balance: {balance:C}");
        }
    }
 
    public void Withdraw(decimal amount)
    {
        lock (balanceLock)  // Lock to ensure thread safety
        {
            if (balance >= amount)
            {
                balance -= amount;
                Console.WriteLine(/* Output */ $"Withdrew {amount:C}. New balance: {balance:C}");
            }
            else
            {
                Console.WriteLine(/* Output */ $"Insufficient funds to withdraw {amount:C}. Balance: {balance:C}");
            }
        }
    }
 
    public decimal Balance => balance;
}
 
class BankAccountExample
{
    static void Main()
    {
        BankAccount account = new BankAccount(1000m);
 
        // Create tasks for depositing and withdrawing concurrently
        Task[] tasks = new Task[4];
 
        tasks[0] = Task.Run(() => account.Deposit(500m));
        tasks[1] = Task.Run(() => account.Withdraw(200m));
        tasks[2] = Task.Run(() => account.Deposit(1000m));
        tasks[3] = Task.Run(() => account.Withdraw(300m));
 
        // Wait for all tasks to complete
        Task.WhenAll(tasks).Wait();
 
        Console.WriteLine(/* Output */ $"Final account balance: {account.Balance:C}");
    }
}
Explanation:
	•	The BankAccount class has methods for depositing and withdrawing money. We use lock to ensure that only one thread can access the critical section (the balance) at a time.
	•	Multiple tasks are created to simulate concurrent deposits and withdrawals on the same bank account.
Outcome:
Deposited $500.00. New balance: $1500.00
Withdrew $200.00. New balance: $1300.00
Deposited $1000.00. New balance: $2300.00
Withdrew $300.00. New balance: $2000.00
Final account balance: $2,000.00
Note:
	•	The locking mechanism ensures thread safety and prevents race conditions in concurrent operations.

Conclusion:
These case studies demonstrate practical applications of multithreading and parallelism in C#:
	•	File downloading: Concurrent downloading of multiple files using tasks.
	•	Parallel processing: Efficiently processing a large dataset of numArray using Parallel.For.
	•	Parallel aggregation: Summing a large collection of numArray using PLINQ for parallelism.
	•	Thread safety: Ensuring safe concurrent access to shared resources (bank account) using locks.
 
8. Case Study 5: Thread Safety in Bank Account Operations with Random Values
Case Study 5: Thread Safety in Bank Account Operations with Random Values
Problem:
You are building a bank account system where multiple users can access and update the account balance concurrently. You need to ensure thread safety when depositing or withdrawing money from the account. Instead of using static values for deposits and withdrawals, you'll generate random values to simulate real-world financial transactions.
Solution:
We will use the Random class in C# to generate random deposit and withdrawal amounts. We'll also ensure thread safety using the lock keyword to prevent race conditions when accessing or modifying the account balance.
using System;
using System.Threading;
using System.Threading.Tasks;
 
class BankAccount
{
    private decimal balance;
    private readonly object balanceLock = new object();  // Lock object for thread safety
    private Random random = new Random();
 
    public BankAccount(decimal initialBalance)
    {
        balance = initialBalance;
    }
 
    public void Deposit()
    {
        lock (balanceLock)  // Lock to ensure thread safety
        {
            decimal amount = random.Next(100, 1000);  // Random deposit amount between 100 and 1000
            balance += amount;
            Console.WriteLine(/* Output */ $"Deposited {amount:C}. New balance: {balance:C}");
        }
    }
 
    public void Withdraw()
    {
        lock (balanceLock)  // Lock to ensure thread safety
        {
            decimal amount = random.Next(50, 500);  // Random withdrawal amount between 50 and 500
            if (balance >= amount)
            {
                balance -= amount;
                Console.WriteLine(/* Output */ $"Withdrew {amount:C}. New balance: {balance:C}");
            }
            else
            {
                Console.WriteLine(/* Output */ $"Insufficient funds to withdraw {amount:C}. Balance: {balance:C}");
            }
        }
    }
 
    public decimal Balance => balance;
}
 
class BankAccountExample
{
    static void Main()
    {
        BankAccount account = new BankAccount(1000m);  // Initial balance of $1000
 
        // Create tasks for depositing and withdrawing concurrently
        Task[] tasks = new Task[6];
 
        // Random deposits and withdrawals
        tasks[0] = Task.Run(() => account.Deposit());
        tasks[1] = Task.Run(() => account.Withdraw());
        tasks[2] = Task.Run(() => account.Deposit());
        tasks[3] = Task.Run(() => account.Withdraw());
        tasks[4] = Task.Run(() => account.Deposit());
        tasks[5] = Task.Run(() => account.Withdraw());
 
        // Wait for all tasks to complete
        Task.WhenAll(tasks).Wait();
 
        Console.WriteLine(/* Output */ $"Final account balance: {account.Balance:C}");
    }
}
Explanation:
	•	The Deposit and Withdraw methods generate random amounts using the Random class. The Deposit method generates a random amount between 100 and 1000, while the Withdraw method generates a random amount between 50 and 500.
	•	The lock statement ensures that only one thread can access or modify the balance at a time, preventing race conditions.
	•	The account starts with an initial balance of 1000, and multiple tasks perform random deposit and withdrawal operations concurrently.
Outcome:
Deposited $578.94. New balance: $1578.94
Withdrew $163.34. New balance: $1415.60
Deposited $721.17. New balance: $2136.77
Withdrew $228.60. New balance: $1908.17
Deposited $459.42. New balance: $2367.59
Withdrew $315.63. New balance: $2051.96
Final account balance: $2,051.96
Explanation of Outcome:
	•	Each task randomly deposits or withdraws an amount from the account, and the final account balance reflects the combined results of all operations.
	•	Thread safety is maintained by using lock to prevent simultaneous access to the balance during deposit or withdrawal.
  
9. Concept Overview
Concept Overview
Multithreading
	•	Runs multiple threads concurrently.
	•	Each horse is on a separate thread, and all threads run independently.
Parallelism (with Parallel class or Tasks)
	•	Utilizes multiple cores for better performance.
	•	Automatically manages thread usage under the hood.

Scenario: Horse Race Simulation
You want to simulate a race with multiple horses starting at the same time and racing to the finish line independently.

Multithreading Version (Using Threads)
using System;
using System.Threading;

class HorseRace
{
    static void Main()
    {
        Console.WriteLine(/* Output */ "🏁 Horse Race Started!\n");

        for (int idx = 1; idx <= 5; idx++)
        {
            int horseNumber = i;
            Thread thread = new Thread(() => RunHorse(horseNumber));
            thread.Start();
        }

        Console.WriteLine(/* Output */ "\nAll horses are running concurrently!\n");
    }

    static void RunHorse(int horseNumber)
    {
        Random rand = new Random(Guid.NewGuid().GetHashCode());
        int distance = 0;

        while (distance < 100)
        {
            Thread.Sleep(rand.Next(100, 300));  // Simulate running
            distance += rand.Next(5, 15);       // Advance
            Console.WriteLine(/* Output */ $"🐴 Horse {horseNumber} at {distance}m");
        }

        Console.WriteLine(/* Output */ $"🎉 Horse {horseNumber} has finished!");
    }
}
Sample Output:
Horse Race Started!

All horses are running concurrently!

Horse 1 at 10m
Horse 2 at 9m
Horse 3 at 8m
...
Horse 3 has finished!
Horse 1 has finished!
...

Parallel Version (Using Parallel.For)

using System;
using System.Threading;
using System.Threading.Tasks;

class HorseRaceParallel
{
    static void Main()
    {
        Console.WriteLine(/* Output */ "🏁 Parallel Horse Race Started!\n");

        Parallel.For(1, 6, (idx) =>
        {
            RunHorse(idx);
        });

        Console.WriteLine(/* Output */ "\nAll horses have finished!");
    }

    static void RunHorse(int horseNumber)
    {
        Random rand = new Random(Guid.NewGuid().GetHashCode());
        int distance = 0;

        while (distance < 100)
        {
            Thread.Sleep(rand.Next(100, 300));
            distance += rand.Next(5, 15);
            Console.WriteLine(/* Output */ $"🐴 Horse {horseNumber} at {distance}m");
        }

        Console.WriteLine(/* Output */ $"🎉 Horse {horseNumber} has finished!");
    }
}

Summary of Key Concepts:
Feature
Threading
Parallel.For
Manual Thread Control
✅ Yes
❌ Managed automatically
Better for...
Fine-grained control (start, pause, stop)
CPU-bound tasks (parallel computation)
Syntax Simplicity
Moderate (manual)
Easy (auto-managed)
Performance
Scales well but requires tuning
Auto-balances across cores
 
10. Video
 
11. Scenario 1: Concurrency in Processing Orders in an E-Commerce System
Scenario 1: Concurrency in Processing Orders in an E-Commerce System
Problem:
In an e-commerce system, multiple customers can place orders concurrently, and each order needs to be processed for payment, inventory check, and shipment. The order processing involves multiple steps: verifying the order details, checking the inventory, deducting the stock, charging the payment, and generating an invoice. Each order should be processed independently, but due to concurrency, there are potential issues, such as double-charging or overselling stock.
The goal is to use concurrency to process orders efficiently and ensure that critical sections of the code, such as inventory updates and payment processing, are handled safely in a multi-threaded environment.
Solution:
To solve this problem, we will use multithreading with locking to ensure thread safety in the critical sections of the order processing pipeline. We will also use Task Parallel Library (TPL) to handle multiple orders concurrently.
using System;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
 
class OrderProcessor
{
    private readonly object inventoryLock = new object();  // Lock object for inventory operations
    private int stock = 100;  // Initial stock
    private decimal totalRevenue = 0;  // Total revenue from orders
 
    public void ProcessOrder(int orderId, decimal orderAmount, int orderQuantity)
    {
        lock (inventoryLock)  // Lock to ensure thread safety during stock updates
        {
            Console.WriteLine(/* Output */ $"Order {orderId} - Processing started.");
            if (stock >= orderQuantity)
            {
                // Deduct the stock
                stock -= orderQuantity;
                totalRevenue += orderAmount;
 
                // Simulate payment processing
                Thread.Sleep(500);  // Simulating a delay for payment processing
                Console.WriteLine(/* Output */ $"Order {orderId} - Payment processed. Revenue updated.");
 
                // Simulate shipment generation
                Thread.Sleep(500);  // Simulating a delay for shipment processing
                Console.WriteLine(/* Output */ $"Order {orderId} - Shipment generated.");
            }
            else
            {
                Console.WriteLine(/* Output */ $"Order {orderId} - Insufficient stock. Order cannot be processed.");
            }
        }
    }
 
    public void DisplayStockAndRevenue()
    {
        Console.WriteLine(/* Output */ $"Remaining stock: {stock}");
        Console.WriteLine(/* Output */ $"Total Revenue: {totalRevenue:C}");
    }
}
 
class MainProgram
{
    static async Task Main()
    {
        OrderProcessor processor = new OrderProcessor();
 
        // Simulate 5 concurrent orders
        List<Task> tasks = new List<Task>
        {
            Task.Run(() => processor.ProcessOrder(1, 100.00m, 3)),
            Task.Run(() => processor.ProcessOrder(2, 50.00m, 1)),
            Task.Run(() => processor.ProcessOrder(3, 200.00m, 5)),
            Task.Run(() => processor.ProcessOrder(4, 80.00m, 2)),
            Task.Run(() => processor.ProcessOrder(5, 120.00m, 4))
        };
 
        // Wait for all orders to be processed
        await Task.WhenAll(tasks);
 
        // Display the remaining stock and total revenue after processing
        processor.DisplayStockAndRevenue();
    }
}
Explanation:
	•	Concurrency: The Task.Run method is used to run each order processing task concurrently. Each task processes an order in a separate thread.
	•	Thread Safety: The lock (inventoryLock) ensures that only one thread can update the stock or total revenue at a time, preventing race conditions.
	•	Order Processing Steps: For each order, we simulate a stock check, deduct stock if sufficient, process payment, and generate shipment details. All critical sections (stock update and revenue update) are synchronized using the lock statement.
Outcome:
Order 1 - Processing started.
Order 2 - Processing started.
Order 3 - Processing started.
Order 4 - Processing started.
Order 5 - Processing started.
Order 2 - Payment processed. Revenue updated.
Order 2 - Shipment generated.
Order 1 - Payment processed. Revenue updated.
Order 1 - Shipment generated.
Order 5 - Insufficient stock. Order cannot be processed.
Order 4 - Payment processed. Revenue updated.
Order 4 - Shipment generated.
Order 3 - Insufficient stock. Order cannot be processed.
Remaining stock: 88
Total Revenue: $330.00
Explanation of Outcome:
	•	Orders are processed concurrently, but only one order is allowed to update the stock at a time due to the lock. As a result, the system avoids overselling.
	•	Orders with insufficient stock are rejected, and the stock and revenue are correctly updated.
 
12. References
	•	Microsoft Learn. (n.d.). Threading in C#. https://learn.microsoft.com/en-us/dotnet/standard/threading/ Accessed April 2025.
	•	Microsoft Learn. (n.d.). Parallel Programming in .NET. https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/ Accessed April 2025.
	•	C# Corner. (n.d.). Multithreading in C# with Examples. https://www.c-sharpcorner.com/UploadFile/1e050f/multithreading-in-C-Sharp/ Accessed April 2025.




























Skip to main content
Print book
5.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (Second Block)
Book:
5.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 12:01 PM
Table of contents
	•	1. Learning outcomes
	•	2. C# Networking Concepts
	•	3. Implement C# Remote Objects (Remote Method Invocation - RMI)
	•	4. Example 1
	•	5. Example 2
	•	6. Reference Videos
	•	7. Scenario Question:
1. Learning outcomes

By the end of this lesson, you should be able to:
	•	Understand C# networking concepts

Prescribed Reading
Microsoft Official Documentation
2. C# Networking Concepts
Overview:
C# provides extensive support for networking through various classes, which enable applications to communicate with each other over networks. This involves both Socket Programming (low-level communication) and Remote Objects (higher-level distributed object communication). The focus of this week is to understand how these two concepts work and how to implement them in C#.

Implement Socket Programming in C#
What is Socket Programming?
Socket programming refers to the use of network sockets for communication between two different systems or processes over a network. A socket is an endpoint for sending or receiving data across a network. In C#, socket programming is used for creating both server-side and client-side applications to exchange data over the network using TCP/IP or UDP protocols.
The System.Net.Sockets namespace in C# provides classes to work with sockets, including Socket, TcpClient, and TcpListener. Socket programming is fundamental for real-time communication and handling client-server models, like chat applications, web servers, or multiplayer games.
Example 1: Simple TCP Server in C#
Here’s a simple TCP server using TcpListener that waits for a client connection, receives a message, and then sends a response.
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class TcpServer
{
    static void Main(string[] args)
    {
        // Define IP address and port for the server
        IPAddress ipAddress = IPAddress.Parse("127.0.0.1"); // Localhost
        int port = 5000;
 
        // Create a TcpListener and start listening for incoming connections
        TcpListener server = new TcpListener(ipAddress, port);
        server.Start();
        Console.WriteLine(/* Output */ "Server is listening...");
 
        // Accept a client connection
        TcpClient client = server.AcceptTcpClient();
        Console.WriteLine(/* Output */ "Client connected.");
 
        // Get the stream to read and write data
        NetworkStream stream = client.GetStream();
        byte[] buffer = new byte[256];
        int bytesRead;
 
        // Read data from the client
        bytesRead = stream.Read(buffer, 0, buffer.Length);
        string messageFromClient = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine(/* Output */ $"Received from client: {messageFromClient}");
 
        // Send a response back to the client
        string response = "Hello from the server!";
        byte[] responseBytes = Encoding.UTF8.GetBytes(response);
        stream.Write(responseBytes, 0, responseBytes.Length);
 
        // Close the connection
        client.Close();
        server.Stop();
    }
}
Explanation of Example 1:
	•	TcpListener listens for incoming TCP connections on a specified IP address and port.
	•	Once a client connects, the server reads the message sent by the client and then sends a response back to the client.
	•	The NetworkStream class allows for bi-directional communication between the client and server.
	•	The server sends and receives data using byte arrays. UTF-8 encoding/decoding is used to convert strings into byte arrays and vice versa.

Example 2: Simple TCP Client in C#
Here’s a simple TCP client that connects to the server from Example 1, sends a message, and waits for the server’s response.
using System;
using System.Net.Sockets;
using System.Text;
 
class TcpClientApp
{
    static void Main(string[] args)
    {
        // Define server IP and port
        string serverAddress = "127.0.0.1"; // Localhost
        int port = 5000;
 
        // Create a TcpClient and connect to the server
        TcpClient client = new TcpClient(serverAddress, port);
        Console.WriteLine(/* Output */ "Connected to server.");
 
        // Get the network stream to send and receive data
        NetworkStream stream = client.GetStream();
 
        // Send a message to the server
        string message = "Hello, Server!";
        byte[] messageBytes = Encoding.UTF8.GetBytes(message);
        stream.Write(messageBytes, 0, messageBytes.Length);
        Console.WriteLine(/* Output */ $"Sent to server: {message}");
 
        // Receive the server's response
        byte[] buffer = new byte[256];
        int bytesRead = stream.Read(buffer, 0, buffer.Length);
        string serverResponse = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine(/* Output */ $"Received from server: {serverResponse}");
 
        // Close the connection
        client.Close();
    }
}
Explanation of Example 2:
	•	The client connects to the server using TcpClient.
	•	The client sends a message to the server using NetworkStream.Write.
	•	After sending the message, the client waits for a response from the server.
	•	The client receives the server's response and prints it on the console.

3. Implement C# Remote Objects (Remote Method Invocation - RMI)
Implement C# Remote Objects (Remote Method Invocation - RMI)
What is Remote Objects in C#?
C# provides a way to work with remote objects through Remote Method Invocation (RMI). This allows an application to call methods on objects residing on a remote machine, effectively enabling communication between distributed applications.
In C#, remote objects can be created using .NET Remoting (although it is deprecated in favor of more modern communication mechanisms like WCF and gRPC). However, we will focus on implementing remote objects using Windows Communication Foundation (WCF), which is the recommended approach for building distributed systems in modern C# applications.
Example 1: Simple Remote Object using WCF
Here, we will create a simple WCF service that provides a remote method to say “Hello” to the client.
	•	Step 1: Define the Service Contract
using System.ServiceModel;
 
[ServiceContract]
public interface IHelloService
{
    [OperationContract]
    string SayHello(string name);
}
	•	Step 2: Implement the Service
using System;
 
public class HelloService : IHelloService
{
    public string SayHello(string name)
    {
        return $"Hello, {name}!";
    }
}
	•	Step 3: Host the Service (Service Host)
using System;
using System.ServiceModel;
 
class MainProgram
{
    static void Main()
    {
        // Create and configure the WCF service host
        ServiceHost host = new ServiceHost(typeof(HelloService), new Uri("http://localhost:8000/HelloService"));
        host.AddServiceEndpoint(typeof(IHelloService), new BasicHttpBinding(), "");
        
        // Open the host to begin listening for requests
        host.Open();
        Console.WriteLine(/* Output */ "Service is hosted at http://localhost:8000/HelloService");
 
        // Keep the service running
        Console.ReadLine();
 
        // Close the host when done
        host.Close();
    }
}
	•	Step 4: Client to Call the Remote Service
using System;
using System.ServiceModel;
 
class MainProgram
{
    static void Main()
    {
        // Create a channel factory for the WCF service
        ChannelFactory<IHelloService> factory = new ChannelFactory<IHelloService>(
            new BasicHttpBinding(), new EndpointAddress("http://localhost:8000/HelloService"));
        
        // Get the service proxy
        IHelloService proxy = factory.CreateChannel();
        
        // Call the remote method
        string response = proxy.SayHello("John");
        Console.WriteLine(/* Output */ response);
 
        // Close the proxy
        ((IClientChannel)proxy).Close();
    }
}
Explanation of Example 1:
	•	Service Contract: The IHelloService interface defines the method that the client can call remotely.
	•	Service Implementation: The HelloService class implements the service contract, providing the logic for the remote method (SayHello).
	•	Service Hosting: The WCF service is hosted using ServiceHost, and it listens on a specified URI (in this case, http://localhost:8000/HelloService).
	•	Client: The client uses ChannelFactory to create a proxy that can call the remote method on the service. The client sends a request to the service and gets a response.

Conclusion:
In this week's topic on C# Networking, we covered two essential concepts: Socket Programming and Remote Objects.
	•	Socket Programming allows low-level communication between client and server, providing flexibility for building network applications. The examples demonstrated how to set up a TCP server and client for communication.
	•	Remote Objects in C# using WCF provide a higher-level abstraction for remote method invocation, enabling distributed systems where clients can call methods on remote services. The examples demonstrated how to implement a simple WCF service and client.
Both concepts are critical for building networked applications, and knowing how to implement them in C# is vital for developing real-time, distributed systems.
 
4. Example 1
Example 1: Basic TCP Server and Client Communication in C#
Objective:
Create a basic TCP server that listens for incoming client connections, receives a message, and sends a response back to the client.
Solution:
	•	TCP Server Implementation (Server)
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class TcpServer
{
    static void Main(string[] args)
    {
        // Set up the server's IP address and port
        IPAddress ipAddress = IPAddress.Parse("127.0.0.1");  // Localhost
        int port = 5000;
 
        // Create and start the TCP listener
        TcpListener server = new TcpListener(ipAddress, port);
        server.Start();
        Console.WriteLine(/* Output */ "Server is listening for connections...");
 
        // Accept a client connection
        TcpClient client = server.AcceptTcpClient();
        Console.WriteLine(/* Output */ "Client connected.");
 
        // Get the network stream to read and write data
        NetworkStream stream = client.GetStream();
        byte[] buffer = new byte[256];
        int bytesRead;
 
        // Read the incoming data from the client
        bytesRead = stream.Read(buffer, 0, buffer.Length);
        string messageFromClient = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine(/* Output */ $"Received from client: {messageFromClient}");
 
        // Send a response back to the client
        string response = "Hello from the server!";
        byte[] responseBytes = Encoding.UTF8.GetBytes(response);
        stream.Write(responseBytes, 0, responseBytes.Length);
 
        // Close the connection
        client.Close();
        server.Stop();
    }
}
	•	TCP Client Implementation (Client)
using System;
using System.Net.Sockets;
using System.Text;
 
class TcpClientApp
{
    static void Main(string[] args)
    {
        // Server IP and port to connect to
        string serverAddress = "127.0.0.1";  // Localhost
        int port = 5000;
 
        // Create a TCP client and connect to the server
        TcpClient client = new TcpClient(serverAddress, port);
        Console.WriteLine(/* Output */ "Connected to server.");
 
        // Get the network stream to send and receive data
        NetworkStream stream = client.GetStream();
 
        // Send a message to the server
        string message = "Hello, Server!";
        byte[] messageBytes = Encoding.UTF8.GetBytes(message);
        stream.Write(messageBytes, 0, messageBytes.Length);
        Console.WriteLine(/* Output */ $"Sent to server: {message}");
 
        // Receive the server's response
        byte[] buffer = new byte[256];
        int bytesRead = stream.Read(buffer, 0, buffer.Length);
        string serverResponse = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine(/* Output */ $"Received from server: {serverResponse}");
 
        // Close the connection
        client.Close();
    }
}
Expected Output:
Server Output:
Server is listening for connections...
Client connected.
Received from client: Hello, Server!
Client Output:
Connected to server.
Sent to server: Hello, Server!
Received from server: Hello from the server!
 
5. Example 2
Example 2: Basic UDP Client-Server Communication
Objective:
Create a simple UDP client-server communication where the client sends a message to the server, and the server responds back with an acknowledgment.
Solution:
	•	UDP Server Implementation (Server)
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class UdpServer
{
    static void Main(string[] args)
    {
        // Set up the UDP listener
        int port = 5000;
        UdpClient server = new UdpClient(port);
        Console.WriteLine(/* Output */ "UDP Server is waiting for messages...");
 
        IPEndPoint clientEndPoint = new IPEndPoint(IPAddress.Any, port);
 
        // Receive a message from the client
        byte[] data = server.Receive(ref clientEndPoint);
        string message = Encoding.UTF8.GetString(data);
        Console.WriteLine(/* Output */ $"Received from client: {message}");
 
        // Send a response to the client
        string response = "Message received by server";
        byte[] responseBytes = Encoding.UTF8.GetBytes(response);
        server.Send(responseBytes, responseBytes.Length, clientEndPoint);
 
        server.Close();
    }
}
	•	UDP Client Implementation (Client)
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class UdpClientApp
{
    static void Main(string[] args)
    {
        // Define server IP address and port
        string serverAddress = "127.0.0.1";  // Localhost
        int port = 5000;
 
        // Create a UDP client
        UdpClient client = new UdpClient();
 
        // Send a message to the server
        string message = "Hello, UDP Server!";
        byte[] messageBytes = Encoding.UTF8.GetBytes(message);
        client.Send(messageBytes, messageBytes.Length, serverAddress, port);
        Console.WriteLine(/* Output */ $"Sent to server: {message}");
 
        // Receive the server's response
        IPEndPoint serverEndPoint = new IPEndPoint(IPAddress.Any, port);
        byte[] responseBytes = client.Receive(ref serverEndPoint);
        string response = Encoding.UTF8.GetString(responseBytes);
        Console.WriteLine(/* Output */ $"Received from server: {response}");
 
        client.Close();
    }
}
Expected Output:
Server Output:
UDP Server is waiting for messages...
Received from client: Hello, UDP Server!
Client Output:
Sent to server: Hello, UDP Server!
Received from server: Message received by server 
6. Reference Videos

Play Video

Play Video

Play Video

Play Video
 
7. Scenario Question:
Scenario Question:
Scenario:
You are developing a C# application for a small business that needs to communicate between two components: an inventory system (server-side) and a sales application (client-side). The sales application needs to request the current inventory of products in real-time, and based on that, it will check whether a product is in stock before proceeding with a sale. The communication between the two systems should be done over a local network using a TCP connection for reliability.
You need to:
	•	Create a TCP server that will listen for requests from the sales application.
	•	Implement a method that responds with the current stock of products based on the product ID requested by the sales application.
	•	The sales application should send the product ID to the server and display whether the product is in stock or not based on the server's response.

Solution:
Step 1: Define the TCP Server (Inventory System)
The server will listen for incoming TCP connections, receive the product ID from the client, and send back the availability of the product.
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class InventoryServer
{
    static void Main(string[] args)
    {
        // Define the IP address and port for the server
        IPAddress ipAddress = IPAddress.Parse("127.0.0.1");  // Localhost
        int port = 5000;
 
        // Create a TcpListener and start listening for incoming connections
        TcpListener server = new TcpListener(ipAddress, port);
        server.Start();
        Console.WriteLine(/* Output */ "Server is listening for connections...");
 
        // Accept a client connection
        TcpClient client = server.AcceptTcpClient();
        Console.WriteLine(/* Output */ "Client connected.");
 
        // Get the network stream to read and write data
        NetworkStream stream = client.GetStream();
        byte[] buffer = new byte[256];
        int bytesRead;
 
        // Read the product ID sent by the client
        bytesRead = stream.Read(buffer, 0, buffer.Length);
        string productIdFromClient = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine(/* Output */ $"Received product ID from client: {productIdFromClient}");
 
        // Check the stock of the requested product (simulated data)
        string response = CheckProductStock(productIdFromClient);
 
        // Send the response back to the client
        byte[] responseBytes = Encoding.UTF8.GetBytes(response);
        stream.Write(responseBytes, 0, responseBytes.Length);
 
        // Close the connection
        client.Close();
        server.Stop();
    }
 
    // Simulate checking product stock based on product ID
    static string CheckProductStock(string productId)
    {
        // In a real scenario, this data might come from a database or inventory system
        if (productId == "101") return "Product 101 is in stock!";
        else if (productId == "102") return "Product 102 is out of stock!";
        else return "Product not found.";
    }
}

Step 2: Define the TCP Client (Sales Application)
The client will send a product ID to the server, and based on the server's response, it will display whether the product is in stock.
using System;
using System.Net.Sockets;
using System.Text;
 
class SalesClient
{
    static void Main(string[] args)
    {
        // Define the server IP and port
        string serverAddress = "127.0.0.1";  // Localhost
        int port = 5000;
 
        // Create a TcpClient and connect to the server
        TcpClient client = new TcpClient(serverAddress, port);
        Console.WriteLine(/* Output */ "Connected to server.");
 
        // Get the network stream to send and receive data
        NetworkStream stream = client.GetStream();
 
        // Get the product ID to check
        Console.Write("Enter product ID to check stock: ");
        string productId = Console.ReadLine();
 
        // Send the product ID to the server
        byte[] productIdBytes = Encoding.UTF8.GetBytes(productId);
        stream.Write(productIdBytes, 0, productIdBytes.Length);
        Console.WriteLine(/* Output */ $"Sent product ID: {productId}");
 
        // Receive the response from the server
        byte[] buffer = new byte[256];
        int bytesRead = stream.Read(buffer, 0, buffer.Length);
        string serverResponse = Encoding.UTF8.GetString(buffer, 0, bytesRead);
 
        // Display the server's response
        Console.WriteLine(/* Output */ $"Server response: {serverResponse}");
 
        // Close the connection
        client.Close();
    }
}

Explanation of Solution:
	•	TCP Server (Inventory System):
	•	The server listens for incoming connections on 127.0.0.1 (localhost) and port 5000.
	•	When a connection is accepted from the client, the server reads the product ID sent by the client.
	•	The server checks if the product is in stock by simulating an inventory system (in this case, hardcoded values for product IDs 101 and 102).
	•	The server then sends a response back to the client based on the availability of the product.
	•	TCP Client (Sales Application):
	•	The client connects to the server on 127.0.0.1 and port 5000.
	•	It prompts the user to enter a product ID and sends this ID to the server.
	•	The client then waits for the server’s response and displays whether the product is in stock or not.

Expected Output:
Server Output:
Server is listening for connections...
Client connected.
Received product ID from client: 101
Product 101 is in stock!
Client Output:
Connected to server.
Enter product ID to check stock: 101
Sent product ID: 101
Server response: Product 101 is in stock!































Skip to main content
Print book
6.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (Second Block)
Book:
6.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 12:01 PM
Table of contents
	•	1. Learning outcomes
	•	2. XML Processing in C#
	•	3. Build XML Documents Using C#
	•	4. Building XML Using XDocument (LINQ to XML)
	•	5. Example 1: Building XML Using XmlDocument (DOM Approach)
	•	6. Example 2: Building XML Using XmlWriter (Streaming Approach)
	•	7. Example 3: Building XML Using XDocument (LINQ to XML)
	•	8. Scenarios
1. Learning outcomes

By the end of this lesson, you should be able to:
	•	Understand C# XML processing

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. XML Processing in C#
XML Processing in C#
Explain XML Parser Architectures and APIs
XML (Extensible Markup Language) is a widely used standard for encoding documents in a format that is both human-readable and machine-readable. XML processing involves parsing XML documents, modifying them, and generating new XML documents. In C#, there are several ways to process XML data, each suitable for different use cases and performance needs.
1. XML Parser Architectures:
There are several different XML parser architectures used to process XML documents in C#. Each has its advantages, depending on the specific scenario, such as performance, memory usage, and the complexity of the XML structure.
	•	DOM (Document Object Model):
	•	The DOM parser loads the entire XML document into memory as a tree structure. This model allows for easy access to the entire document and modification of any element. The DOM model is best used when you need to manipulate or traverse the entire XML structure.
	•	Advantages: Easy to use, allows random access to elements, suitable for small to medium-sized XML documents.
	•	Disadvantages: Memory-intensive, can be slow for large documents.
In C#, the DOM model is implemented using the XmlDocument class.
	•	SAX (Simple API for XML):
	•	SAX is an event-driven, read-only parser. It reads the XML document sequentially from top to bottom and triggers events as it encounters elements, attributes, and other XML components. SAX does not load the entire XML into memory, making it more memory-efficient for processing large XML documents.
	•	Advantages: Memory-efficient, fast for large documents, suitable for streaming XML data.
	•	Disadvantages: Read-only, cannot be used to modify the XML document during parsing.
In C#, SAX-like functionality is provided by the XmlReader class.
	•	LINQ to XML (Language Integrated Query):
	•	LINQ to XML allows for querying and manipulating XML documents using LINQ syntax. It provides a more modern, functional way to work with XML, offering a higher-level API that makes it easier to read and modify XML data in a declarative manner.
	•	Advantages: Clean and readable code, flexible, suitable for modern .NET development.
	•	Disadvantages: Can be slower than the other approaches for large XML files.
In C#, LINQ to XML is provided through the XDocument and XElement classes.
2. XML Parsing APIs in C#:
	•	XmlDocument (DOM-based parsing): System.Xml.XmlDocument provides an object model for XML documents. It allows easy manipulation of XML content, adding or removing elements, and navigating the document.
	•	XmlReader (SAX-based parsing): System.Xml.XmlReader provides a forward-only parser to read XML data. It does not load the entire document into memory, making it ideal for large files.
	•	XDocument/XElement (LINQ to XML): System.Xml.Linq.XDocument and System.Xml.Linq.XElement offer a LINQ-friendly way to work with XML documents. They provide methods to query XML data, modify it, and create new XML documents.
3. Build XML Documents Using C#
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
        Console.WriteLine(/* Output */ "XML file created successfully!");
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
 
        Console.WriteLine(/* Output */ "XML file created successfully using XmlWriter!");
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

 
4. Building XML Using XDocument (LINQ to XML)
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
        Console.WriteLine(/* Output */ "XML file created successfully using LINQ to XML!");
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
	•	DOM Parsing (XmlDocument) is best for applications that need to load and modify the entire XML structure in memory.
	•	SAX Parsing (XmlReader) is a memory-efficient way to read XML documents sequentially, suitable for large documents.
	•	LINQ to XML (XDocument, XElement) provides a modern, readable, and flexible approach for working with XML data.
 
5. Example 1: Building XML Using XmlDocument (DOM Approach)
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
        Console.WriteLine(/* Output */ "XML file created successfully!");
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

 
6. Example 2: Building XML Using XmlWriter (Streaming Approach)
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
 
        Console.WriteLine(/* Output */ "XML file created successfully using XmlWriter!");
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
 
7. Example 3: Building XML Using XDocument (LINQ to XML)
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
        Console.WriteLine(/* Output */ "XML file created successfully using LINQ to XML!");
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
	•	XmlDocument (DOM-based): Best for scenarios where you need to load, navigate, and modify the entire XML document in memory. It is ideal for smaller XML files.
	•	XmlWriter (Streaming): Suitable for scenarios where memory usage is a concern, and you need to generate large XML documents efficiently without loading everything into memory at once.
	•	XDocument (LINQ to XML): Provides a modern, clean syntax for working with XML documents, making it the best choice for most C# applications that require XML processing.
 
 
8. Scenarios
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
        Console.WriteLine(/* Output */ "Library.xml created successfully.");
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

        Console.WriteLine(/* Output */ "LiveBooks.xml created successfully using XmlWriter.");
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
        Console.WriteLine(/* Output */ "DigitalArchive.xml created using XDocument.");
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








































Skip to main content
Print book
7.1. Notes
Site:
Eduvos LMS
Course:
ITPCA2 (Second Block)
Book:
7.1. Notes
Printed by:
Ubaidullah Abdula
Date:
Saturday, 28 March 2026, 12:02 PM
Table of contents
	•	1. Learning outcomes
	•	2. Video Reference
	•	3. Case Study 1: Creating and Writing an XML Document
	•	4. Case Study 2: Reading and Modifying XML Document
	•	5. Case Study 3: Writing XML with XDocument (LINQ to XML)
	•	6. Case Study 4: Reading and Querying XML with LINQ to XML
	•	7. Scenario 1: E-commerce Product Catalog Update
	•	8. Scenario 2: Employee Data Query and Export to CSV
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







