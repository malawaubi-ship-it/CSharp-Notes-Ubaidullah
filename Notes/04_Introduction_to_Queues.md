# Module 04: Queues — Implementation and Operations

## Learning Outcomes

By the end of this module you should be able to:
- Implement a queue from scratch in C# using arrays and linked lists.
- Use C#'s built-in `Queue<T>` class.
- Identify the different types of queues and their use cases.

---

## Queue Basics

A **queue** is a linear data structure that follows the **First In, First Out (FIFO)** principle.

Elements are added at the **rear (back)** and removed from the **front**.

```
Front → [ A | B | C | D ] ← Rear
         Dequeue          Enqueue
```

---

## Core Operations

| Operation | Description | Time Complexity |
|-----------|-------------|-----------------|
| Enqueue | Add element to rear | O(1) |
| Dequeue | Remove element from front | O(1) |
| Peek / Front | View front element without removing | O(1) |
| IsEmpty | Check if queue has no elements | O(1) |
| Count | Number of elements | O(1) |

---

## Using C#'s Built-in Queue<T>

```csharp
using System;
using System.Collections.Generic;

Queue<string> queue = new Queue<string>();

// Add elements
queue.Enqueue("First");
queue.Enqueue("Second");
queue.Enqueue("Third");

// View the front without removing
Console.WriteLine(queue.Peek()); // Output: First

// Remove elements in FIFO order
Console.WriteLine(queue.Dequeue()); // Output: First
Console.WriteLine(queue.Dequeue()); // Output: Second

Console.WriteLine($"Remaining: {queue.Count}"); // Output: 1
```

---

## Implementing a Queue from Scratch (Array-Based)

```csharp
public class ArrayQueue
{
    private int[] data;
    private int front, rear, count, capacity;

    public ArrayQueue(int capacity)
    {
        this.capacity = capacity;
        data  = new int[capacity];
        front = 0;
        rear  = -1;
        count = 0;
    }

    public bool IsEmpty => count == 0;
    public bool IsFull  => count == capacity;

    public void Enqueue(int value)
    {
        if (IsFull) { Console.WriteLine("Queue is full."); return; }
        rear = (rear + 1) % capacity; // circular wrap
        data[rear] = value;
        count++;
    }

    public int Dequeue()
    {
        if (IsEmpty) { Console.WriteLine("Queue is empty."); return -1; }
        int value = data[front];
        front = (front + 1) % capacity;
        count--;
        return value;
    }

    public int Peek()
    {
        if (IsEmpty) { Console.WriteLine("Queue is empty."); return -1; }
        return data[front];
    }
}
```

---

## Implementing a Queue from Scratch (Linked List-Based)

```csharp
public class QueueNode
{
    public int Value;
    public QueueNode Next;
    public QueueNode(int value) { Value = value; Next = null; }
}

public class LinkedQueue
{
    private QueueNode front, rear;
    public int Count { get; private set; }

    public void Enqueue(int value)
    {
        QueueNode node = new QueueNode(value);
        if (rear == null) { front = rear = node; }
        else { rear.Next = node; rear = node; }
        Count++;
    }

    public int Dequeue()
    {
        if (front == null) throw new InvalidOperationException("Queue is empty.");
        int value = front.Value;
        front = front.Next;
        if (front == null) rear = null;
        Count--;
        return value;
    }
}
```

---

## Types of Queues

### Simple Queue
Standard FIFO queue as described above.

### Circular Queue
The rear wraps around to the front of the array, making efficient use of space.
The array-based implementation above already uses this technique with the `% capacity` operation.

### Double-Ended Queue (Deque)
Elements can be added or removed from both ends.

```csharp
using System.Collections.Generic;

LinkedList<int> deque = new LinkedList<int>();

deque.AddFirst(10); // add to front
deque.AddLast(20);  // add to rear
deque.AddFirst(5);  // add to front: [5, 10, 20]

Console.WriteLine(deque.First.Value); // Output: 5
Console.WriteLine(deque.Last.Value);  // Output: 20

deque.RemoveFirst(); // [10, 20]
deque.RemoveLast();  // [10]
```

### Priority Queue
Elements are removed based on their priority rather than their arrival order.
See Module 05 for a full treatment of Priority Queues.

---

## Practical Use Cases

| Use Case | Why a Queue? |
|----------|-------------|
| Print spooler | Documents print in submission order |
| Web server request handling | Requests served in arrival order |
| CPU process scheduling | Processes get CPU time in order |
| Breadth-first graph search | BFS processes neighbours level by level |
| Keyboard input buffer | Keystrokes processed in order typed |

---

## Summary

Queues are a fundamental structure for any system that must process items in arrival order.
C# provides the efficient `Queue<T>` class in `System.Collections.Generic`. When you need more control
(such as a bounded queue or a circular buffer), you can implement one from scratch using an array or linked list.

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*. Packt Publishing.
