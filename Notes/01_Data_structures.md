# Module 01: Data Structures Overview

## Learning Outcomes

By the end of this module you should be able to:
- Explain what a data structure is and why they matter.
- Identify and compare the core data structures: arrays, linked lists, stacks, and queues.
- Implement basic data structures in C#.
- Select an appropriate data structure for a given problem.

---

## What is a Data Structure?

A **data structure** is a way of organising and storing data so that it can be accessed and modified efficiently.
Choosing the right one can dramatically affect the performance and readability of your program.

Data structures are broadly divided into two categories:

| Category | Description | Examples |
|----------|-------------|---------|
| Linear | Elements arranged sequentially | Arrays, Linked Lists, Stacks, Queues |
| Non-Linear | Elements arranged hierarchically | Trees, Graphs |

---

## Arrays

An array stores elements in **contiguous memory locations**, meaning they sit next to each other in memory.
Elements are accessed directly by their **index**, making retrieval very fast.

**Advantages:** O(1) direct access by index.
**Disadvantages:** Fixed size — you cannot grow or shrink an array after creation. Inserting or removing elements is slow (O(n)) because elements must be shifted.

```csharp
// Declare and initialise a fixed-size array of 5 integers
int[] scores = new int[5] { 10, 20, 30, 40, 50 };

// Access the element at index 2
Console.WriteLine(scores[2]); // Output: 30

// Loop through all elements
for (int idx = 0; idx < scores.Length; idx++)
{
    Console.WriteLine(scores[idx]);
}
```

---

## Linked Lists

A **linked list** is a sequence of **nodes**, where each node holds a piece of data and a reference (pointer) to the next node.
Unlike arrays, linked lists do not need contiguous memory — each node can sit anywhere in memory.

**Advantages:** Dynamic size; efficient insertion and deletion (O(1) if you have the node reference).
**Disadvantages:** No direct access by index — you must traverse from the head, giving O(n) search time. More memory overhead due to storing pointers.

```csharp
// A node holds data and a link to the next node
public class Node
{
    public int Data;
    public Node Next;

    public Node(int data)
    {
        Data = data;
        Next = null;
    }
}

// Build a small linked list manually
Node head = new Node(10);
head.Next = new Node(20);
head.Next.Next = new Node(30);

// Traverse and print
Node current = head;
while (current != null)
{
    Console.WriteLine(current.Data);
    current = current.Next;
}
// Output: 10, 20, 30
```

---

## Stacks

A **stack** is a **Last In, First Out (LIFO)** data structure — the last item pushed onto the stack is the first one removed.
Think of a stack of plates: you always add and remove from the top.

**Core operations:**
- `Push(item)` — adds an item to the top.
- `Pop()` — removes and returns the top item.
- `Peek()` — returns the top item without removing it.

**Use cases:** Undo/redo functionality, expression evaluation, backtracking algorithms.

```csharp
using System.Collections.Generic;

Stack<int> stack = new Stack<int>();

stack.Push(10);
stack.Push(20);
stack.Push(30);

Console.WriteLine(stack.Peek()); // Output: 30 (top, not removed)
Console.WriteLine(stack.Pop());  // Output: 30
Console.WriteLine(stack.Pop());  // Output: 20
Console.WriteLine(stack.Count);  // Output: 1
```

---

## Queues

A **queue** is a **First In, First Out (FIFO)** data structure — the first item added is the first one removed.
Think of a queue at a ticket counter: the person who arrived first gets served first.

**Core operations:**
- `Enqueue(item)` — adds an item to the back.
- `Dequeue()` — removes and returns the item from the front.
- `Peek()` — returns the front item without removing it.

**Use cases:** Task scheduling, print queues, breadth-first search.

```csharp
using System.Collections.Generic;

Queue<string> queue = new Queue<string>();

queue.Enqueue("Task A");
queue.Enqueue("Task B");
queue.Enqueue("Task C");

Console.WriteLine(queue.Dequeue()); // Output: Task A
Console.WriteLine(queue.Peek());    // Output: Task B (still in queue)
Console.WriteLine(queue.Count);     // Output: 2
```

---

## Case Study 1 — Employee Management System (Linked List)

A company needs a dynamic list of employees where records can be added and removed without knowing the size upfront.
A linked list is ideal because it grows and shrinks as needed.

```csharp
using System;

public class Employee
{
    public int ID;
    public string Name;
    public Employee Next;

    public Employee(int id, string name)
    {
        ID = id;
        Name = name;
        Next = null;
    }
}

public class EmployeeList
{
    private Employee head;

    public void AddEmployee(int id, string name)
    {
        Employee newEmployee = new Employee(id, name);
        if (head == null)
        {
            head = newEmployee;
        }
        else
        {
            Employee temp = head;
            while (temp.Next != null)
                temp = temp.Next;
            temp.Next = newEmployee;
        }
        Console.WriteLine($"Employee {name} added.");
    }

    public void RemoveEmployee(int id)
    {
        if (head == null) { Console.WriteLine("List is empty."); return; }

        if (head.ID == id) { head = head.Next; Console.WriteLine($"Employee {id} removed."); return; }

        Employee temp = head;
        while (temp.Next != null && temp.Next.ID != id)
            temp = temp.Next;

        if (temp.Next == null)
            Console.WriteLine("Employee not found.");
        else
        {
            temp.Next = temp.Next.Next;
            Console.WriteLine($"Employee {id} removed.");
        }
    }

    public void DisplayAll()
    {
        Employee temp = head;
        while (temp != null)
        {
            Console.WriteLine($"ID: {temp.ID}  Name: {temp.Name}");
            temp = temp.Next;
        }
    }
}

class Program
{
    static void Main()
    {
        EmployeeList list = new EmployeeList();
        list.AddEmployee(101, "Alice");
        list.AddEmployee(102, "Bob");
        list.DisplayAll();
        list.RemoveEmployee(101);
        list.DisplayAll();
    }
}
```

**Expected output:**
```
Employee Alice added.
Employee Bob added.
ID: 101  Name: Alice
ID: 102  Name: Bob
Employee 101 removed.
ID: 102  Name: Bob
```

---

## Case Study 2 — Browser Back/Forward Navigation (Stack)

A web browser keeps a history of visited pages. The back/forward buttons use two stacks to navigate.

```csharp
using System;
using System.Collections.Generic;

public class BrowserHistory
{
    private Stack<string> backStack    = new Stack<string>();
    private Stack<string> forwardStack = new Stack<string>();
    private string currentPage = "Home";

    public void Visit(string page)
    {
        backStack.Push(currentPage);
        currentPage = page;
        forwardStack.Clear(); // Clear forward history when visiting a new page
        Console.WriteLine($"Visited: {currentPage}");
    }

    public void Back()
    {
        if (backStack.Count > 0)
        {
            forwardStack.Push(currentPage);
            currentPage = backStack.Pop();
            Console.WriteLine($"Back to: {currentPage}");
        }
        else Console.WriteLine("No back history.");
    }

    public void Forward()
    {
        if (forwardStack.Count > 0)
        {
            backStack.Push(currentPage);
            currentPage = forwardStack.Pop();
            Console.WriteLine($"Forward to: {currentPage}");
        }
        else Console.WriteLine("No forward history.");
    }
}

class Program
{
    static void Main()
    {
        BrowserHistory browser = new BrowserHistory();
        browser.Visit("Page1");
        browser.Visit("Page2");
        browser.Back();    // Back to Page1
        browser.Forward(); // Forward to Page2
        browser.Visit("Page3");
        browser.Back();    // Back to Page2
    }
}
```

---

## Case Study 3 — Task Scheduler (Queue)

A background processing system needs to handle tasks in the order they are submitted.

```csharp
using System;
using System.Collections.Generic;

public class TaskScheduler
{
    private Queue<string> taskQueue = new Queue<string>();

    public void AddTask(string task)
    {
        taskQueue.Enqueue(task);
        Console.WriteLine($"Added: {task}");
    }

    public void ProcessNextTask()
    {
        if (taskQueue.Count > 0)
            Console.WriteLine($"Processing: {taskQueue.Dequeue()}");
        else
            Console.WriteLine("No tasks in queue.");
    }
}

class Program
{
    static void Main()
    {
        TaskScheduler scheduler = new TaskScheduler();
        scheduler.AddTask("Send Email Report");
        scheduler.AddTask("Run Database Backup");
        scheduler.ProcessNextTask(); // Send Email Report
        scheduler.ProcessNextTask(); // Run Database Backup
    }
}
```

---

## Summary

| Data Structure | Order | Access Time | Insert/Delete | Best For |
|---------------|-------|-------------|---------------|----------|
| Array | Index | O(1) | O(n) | Fixed-size collections, fast lookup |
| Linked List | Sequential | O(n) | O(1) at known node | Dynamic collections, frequent updates |
| Stack | LIFO | O(1) top only | O(1) | Undo, backtracking, parsing |
| Queue | FIFO | O(1) front only | O(1) | Scheduling, BFS, buffering |
