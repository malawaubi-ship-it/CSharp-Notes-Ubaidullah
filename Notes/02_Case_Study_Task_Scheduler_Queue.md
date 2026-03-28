# Module 02: Case Study — Task Scheduling with Queues

## Learning Outcomes

By the end of this module you should be able to:
- Apply queues to model real-world scheduling problems.
- Implement a queue-based task scheduler in C#.
- Understand when a queue is the appropriate choice over other data structures.

---

## The Problem

Many systems need to handle work items in the order they arrive — exactly what a queue provides.
Examples include: print spoolers, web server request handling, background job runners, and CPU scheduling.

This case study builds a task scheduling system that processes jobs in FIFO order.

---

## Queue Fundamentals Recap

A queue follows **First In, First Out (FIFO)**: the first item added is the first item processed.

The two primary operations are:
- **Enqueue** — add an item to the back of the queue.
- **Dequeue** — remove and return the item at the front.

Both operations run in O(1) time, making queues extremely efficient for scheduling.

---

## Implementation: Task Scheduler Using Queue

```csharp
using System;
using System.Collections.Generic;

// Represents a single task in the system
public class Task
{
    public int Id       { get; set; }
    public string Name  { get; set; }
    public int Priority { get; set; }

    public Task(int id, string name, int priority)
    {
        Id       = id;
        Name     = name;
        Priority = priority;
    }

    public override string ToString() => $"[Task {Id}] {Name} (Priority: {Priority})";
}

// A simple FIFO task queue
public class TaskQueue
{
    private Queue<Task> queue = new Queue<Task>();

    public void Submit(Task task)
    {
        queue.Enqueue(task);
        Console.WriteLine($"Submitted: {task}");
    }

    public void ProcessAll()
    {
        if (queue.Count == 0)
        {
            Console.WriteLine("No tasks to process.");
            return;
        }

        Console.WriteLine("\nProcessing tasks...");
        while (queue.Count > 0)
        {
            Task next = queue.Dequeue();
            Console.WriteLine($"  Processing: {next}");
        }
        Console.WriteLine("All tasks complete.");
    }

    public void ShowPending()
    {
        if (queue.Count == 0) { Console.WriteLine("Queue is empty."); return; }

        Console.WriteLine($"\nPending tasks ({queue.Count}):");
        foreach (Task t in queue)
            Console.WriteLine($"  - {t}");
    }
}

class Program
{
    static void Main()
    {
        TaskQueue scheduler = new TaskQueue();

        scheduler.Submit(new Task(1, "Send daily report", 2));
        scheduler.Submit(new Task(2, "Database backup", 1));
        scheduler.Submit(new Task(3, "Clear temp files", 3));

        scheduler.ShowPending();
        scheduler.ProcessAll();
    }
}
```

**Expected output:**
```
Submitted: [Task 1] Send daily report (Priority: 2)
Submitted: [Task 2] Database backup (Priority: 1)
Submitted: [Task 3] Clear temp files (Priority: 3)

Pending tasks (3):
  - [Task 1] Send daily report (Priority: 2)
  - [Task 2] Database backup (Priority: 1)
  - [Task 3] Clear temp files (Priority: 3)

Processing tasks...
  Processing: [Task 1] Send daily report (Priority: 2)
  Processing: [Task 2] Database backup (Priority: 1)
  Processing: [Task 3] Clear temp files (Priority: 3)
All tasks complete.
```

---

## When to Use a Queue

Use a queue when:
- Order of processing must match order of arrival (FIFO).
- You need fast O(1) add/remove.
- Items should not be skipped or reordered.

Use a **Priority Queue** instead (see Module 05) when tasks have different urgency levels and the most critical task should always be processed first.

---

## Summary

Queues are one of the most frequently used data structures in software engineering, particularly for
systems that need to handle work in a fair, ordered manner. The C# standard library provides
`Queue<T>` which is ready to use without any custom implementation needed.

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*. Packt Publishing.
