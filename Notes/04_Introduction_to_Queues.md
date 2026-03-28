# Module 4: Introduction to Queues

## 1. Learning outcomes
 
By the end of this topic you should be able to:
	-	Acquire the skill to interpret data structures and algorithms.
	-	Implement data structures in C#.
	-	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

 
Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd.





## 2. Introduction to Queues
Introduction to Queues
A queue is a linear data structure that follows the First-In, First-Out (FIFO) principle. This means that the first element added to the queue will be the first one to be removed. Queues are widely used in programming for managing tasks that must be processed in order.

Real-World Examples of Queues
	-	Print Queue: Documents sent to a printer are printed in the order they were received.
	-	Call Center Queue: Calls are answered in the order they were received.
	-	Task Scheduling: Background tasks like sending emails or processing orders are executed in the order they were added.
	-	CPU Scheduling: The operating system manages processes in a queue.

## 3. Implementing Queues in C#
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

## 2. Implementing a Queue in C#
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
 
        Console.WriteLine( "Queue after Enqueue operations:");
        foreach (var person in queue)
            Console.WriteLine( person);
 
        // Peek - Check first element
        Console.WriteLine( "\nFront of the queue: " + queue.Peek());
 
        // Dequeue - Removing elements
        Console.WriteLine( "\nProcessing: " + queue.Dequeue());
        Console.WriteLine( "Processing: " + queue.Dequeue());
 
        Console.WriteLine( "\nQueue after Dequeue operations:");
        foreach (var person in queue)
            Console.WriteLine( person);
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



## 4. Types of Queues in C#
C# supports different types of queues, depending on the use case:
3.1 Standard Queue (FIFO)
The Queue<T> class implements a simple FIFO queue where elements are added to the back and removed from the front.

Queue<int> queue = new Queue<int>();
queue.Enqueue(1);
queue.Enqueue(2);
queue.Enqueue(3);
Console.WriteLine( queue.Dequeue()); // Output: 1

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
 
        Console.WriteLine( "Processing tasks in priority order:");
        while (taskQueue.Count > 0) {
            Console.WriteLine( taskQueue.Dequeue());
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
 
        Console.WriteLine( "Deque after operations:");
        foreach (var item in deque)
            Console.WriteLine( item);
    }
}
Output:
Deque after operations:
1



## 5. Practical Use Cases of Queues
Task Scheduler Using Queue
Problem: Background tasks (e.g., email notifications, database backups) must be executed in the order they were added.
Solution: Use a Queue<string> to manage tasks.

using System;
using System.Collections.Generic;
 
class TaskScheduler {
    private Queue<string> taskQueue = new Queue<string>();
 
    public void AddTask(string task) {
        taskQueue.Enqueue(task);
        Console.WriteLine( $"Task added: {task}");
    }
 
    public void ProcessTask() {
        if (taskQueue.Count > 0) {
            Console.WriteLine( $"Processing: {taskQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No tasks to process.");
        }
    }
 
    public void ShowTasks() {
        Console.WriteLine( "Pending tasks:");
        foreach (var task in taskQueue)
            Console.WriteLine( task);
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
        Console.WriteLine( $"Call received from: {caller}");
    }
 
    public void AnswerCall() {
        if (callQueue.Count > 0) {
            Console.WriteLine( $"Answering call from: {callQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No calls in queue.");
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

## 6. Case study 1
Problem Statement
A telecom company needs a Customer Service Call Queue system where customer calls are answered in the order they were received. The system should:
	-	Allow new customer calls to be added to the queue.
	-	Process calls in a First-In, First-Out (FIFO) manner.
	-	Display the current queue of waiting calls.

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
        Console.WriteLine( $"Call received from: {caller}");
    }
 
    // Method to answer and remove a call from the queue
    public void AnswerCall() {
        if (callQueue.Count > 0) {
            Console.WriteLine( $"Answering call from: {callQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No calls in the queue.");
        }
    }
 
    // Display all pending calls
    public void ShowQueue() {
        if (callQueue.Count == 0) {
            Console.WriteLine( "No pending calls.");
        } else {
            Console.WriteLine( "Pending Calls:");
            foreach (var caller in callQueue) {
                Console.WriteLine( caller);
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
 Queue ensures that customers are served in order!



## 7. Case study 2
Problem Statement
A university computer lab has multiple students sending print requests to a shared network printer. The printer must:
	-	Accept multiple print jobs.
	-	Process the print jobs in order of submission.
	-	Display the current print queue.

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
        Console.WriteLine( $"Print job added: {document}");
    }
 
    // Method to process the next print job
    public void ProcessPrintJob() {
        if (jobQueue.Count > 0) {
            Console.WriteLine( $"Printing: {jobQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No print jobs in the queue.");
        }
    }
 
    // Show all pending print jobs
    public void ShowQueue() {
        if (jobQueue.Count == 0) {
            Console.WriteLine( "No pending print jobs.");
        } else {
            Console.WriteLine( "Pending Print Jobs:");
            foreach (var job in jobQueue) {
                Console.WriteLine( job);
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
 The queue ensures print jobs are processed in the order they were added!



## 8. Case Study 3
Problem Statement
A fast-food restaurant processes orders from customers. The system should:
	-	Accept new orders and add them to a queue.
	-	Process orders in the order they were placed.
	-	Display the list of pending orders.

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
        Console.WriteLine( $"Order placed: {order}");
    }
 
    // Method to serve an order
    public void ServeOrder() {
        if (orderQueue.Count > 0) {
            Console.WriteLine( $"Serving order: {orderQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No orders in the queue.");
        }
    }
 
    // Show all pending orders
    public void ShowPendingOrders() {
        if (orderQueue.Count == 0) {
            Console.WriteLine( "No pending orders.");
        } else {
            Console.WriteLine( "Pending Orders:");
            foreach (var order in orderQueue) {
                Console.WriteLine( order);
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
 Orders are served in the same sequence they were placed!

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
 


## 9. Activity
Create a queue in C# that will schedule customers in a pharmacy. Customers will enqueue and get a ticket. Their ticket number will then be called when it’s their turn to use the counter.


Description
 
 
	-	1. Lesson Outcomes
	-	2. Priority Queue
	-	3. Priority Queues
	-	4. Using the Built-in PriorityQueue in C#
	-	5. Scenario 1: Customer Support Ticket System
	-	6. Scenario 2: Airline Check-in System
	-	7. Activity
