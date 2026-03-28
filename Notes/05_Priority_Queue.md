# Module 05: Priority Queues

## Learning Outcomes

By the end of this module you should be able to:
- Explain the difference between a regular queue and a priority queue.
- Implement a priority queue using a min-heap.
- Use C# 6's built-in `PriorityQueue<TElement, TPriority>` class.

---

## What is a Priority Queue?

A **priority queue** is a data structure where each element has an associated **priority**.
Instead of strictly following FIFO order, the element with the **highest priority** (or lowest priority number, depending on convention) is dequeued first.

Example: In a hospital, a critical patient (priority 1) is treated before a minor case (priority 5),
regardless of arrival order.

---

## Under the Hood: The Min-Heap

Priority queues are most efficiently implemented using a **binary heap** — specifically a **min-heap**,
where the parent node is always smaller than its children.

This guarantees that the minimum-priority element is always at the root, and can be extracted in O(log n) time.

```
         1           Root is always the minimum
       /   \
      3     2
     / \   /
    5   4 6
```

---

## Using C#'s Built-in PriorityQueue<T, TPriority>

Available in .NET 6+. The element with the **smallest** priority value is dequeued first.

```csharp
using System;
using System.Collections.Generic;

PriorityQueue<string, int> pq = new PriorityQueue<string, int>();

pq.Enqueue("Low urgency task",    3);
pq.Enqueue("Critical alert",     1);
pq.Enqueue("Medium urgency task", 2);

while (pq.Count > 0)
{
    string item = pq.Dequeue();
    Console.WriteLine($"Processing: {item}");
}
```

**Output:**
```
Processing: Critical alert
Processing: Medium urgency task
Processing: Low urgency task
```

---

## Custom Min-Heap Priority Queue

```csharp
using System;
using System.Collections.Generic;

public class Patient
{
    public string Name     { get; set; }
    public int    Priority { get; set; } // Lower = more urgent

    public Patient(string name, int priority)
    {
        Name     = name;
        Priority = priority;
    }
}

public class PatientQueue
{
    private List<Patient> heap = new List<Patient>();

    public int Count => heap.Count;

    public void Enqueue(Patient patient)
    {
        heap.Add(patient);
        HeapifyUp(heap.Count - 1);
    }

    public Patient Dequeue()
    {
        if (heap.Count == 0) throw new InvalidOperationException("Queue is empty.");

        Patient top = heap[0];
        heap[0] = heap[heap.Count - 1];
        heap.RemoveAt(heap.Count - 1);
        HeapifyDown(0);
        return top;
    }

    private void HeapifyUp(int index)
    {
        while (index > 0)
        {
            int parent = (index - 1) / 2;
            if (heap[index].Priority < heap[parent].Priority)
            {
                Swap(index, parent);
                index = parent;
            }
            else break;
        }
    }

    private void HeapifyDown(int index)
    {
        int left    = 2 * index + 1;
        int right   = 2 * index + 2;
        int smallest = index;

        if (left  < heap.Count && heap[left].Priority  < heap[smallest].Priority) smallest = left;
        if (right < heap.Count && heap[right].Priority < heap[smallest].Priority) smallest = right;

        if (smallest != index)
        {
            Swap(index, smallest);
            HeapifyDown(smallest);
        }
    }

    private void Swap(int a, int b)
    {
        Patient temp = heap[a];
        heap[a]      = heap[b];
        heap[b]      = temp;
    }
}

class Program
{
    static void Main()
    {
        PatientQueue er = new PatientQueue();
        er.Enqueue(new Patient("Alice", 3));   // minor
        er.Enqueue(new Patient("Bob",   1));   // critical
        er.Enqueue(new Patient("Carol", 2));   // moderate
        er.Enqueue(new Patient("Dave",  1));   // critical

        while (er.Count > 0)
        {
            Patient p = er.Dequeue();
            Console.WriteLine($"Treating: {p.Name} (priority {p.Priority})");
        }
    }
}
```

**Expected output:**
```
Treating: Bob (priority 1)
Treating: Dave (priority 1)
Treating: Carol (priority 2)
Treating: Alice (priority 3)
```

---

## Time Complexity

| Operation | Time Complexity |
|-----------|-----------------|
| Enqueue (insert) | O(log n) |
| Dequeue (remove min) | O(log n) |
| Peek (view min) | O(1) |

---

## When to Use a Priority Queue

Use a priority queue when:
- Items must be processed in order of importance rather than arrival order.
- You need very fast access to the highest/lowest priority element.

Common applications: Dijkstra's shortest-path algorithm, A* search, OS task scheduling, real-time event simulation.

---

## Summary

A priority queue always gives you the most important element first.
The min-heap implementation provides O(log n) insert and remove, making it highly efficient.
In C#, .NET 6+ provides `PriorityQueue<TElement, TPriority>` as a ready-to-use implementation.

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*. Packt Publishing.
