# Module 1: Data structures

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


	•	3. Data Structures and Input/Output in C#
	•	4. Lists in C#
	•	4.1. Input and Output in C#
	•	4.2. ArrayList in C#
	•	4.3. Generic List in C#
	•	4.4. Linked List
	•	4.5. Circular-linked List
	•	5. Activity
