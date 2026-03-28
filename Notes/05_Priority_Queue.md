# Module 5: Priority Queue

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


	•	2. Activity
	•	3. Practice Activities
