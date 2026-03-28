# Module 17: Concurrency, Multithreading, and Parallelism

## Learning Outcomes

By the end of this module you should be able to:
- Explain the difference between concurrency, multithreading, and parallelism.
- Create and manage threads in C#.
- Use `Task` and `async/await` for asynchronous programming.
- Apply the Task Parallel Library (TPL) for parallel workloads.

---

## Key Concepts

| Term | Definition |
|------|-----------|
| **Concurrency** | Multiple tasks making progress — does not require simultaneous execution |
| **Multithreading** | Running multiple threads within a single process |
| **Parallelism** | Multiple computations executing at exactly the same time (multiple CPU cores) |
| **Asynchronous** | Starting a task and continuing other work while waiting for it to finish |

---

## Threads

A **thread** is the smallest unit of execution within a process.
The .NET runtime allows you to create threads explicitly using `System.Threading.Thread`.

```csharp
using System;
using System.Threading;

public static void PrintNumbers(string label)
{
    for (int idx = 1; idx <= 5; idx++)
    {
        Console.WriteLine($"{label}: {idx}");
        Thread.Sleep(100); // simulate work
    }
}

Thread t1 = new Thread(() => PrintNumbers("Thread A"));
Thread t2 = new Thread(() => PrintNumbers("Thread B"));

t1.Start();
t2.Start();

// Wait for both threads to complete before continuing
t1.Join();
t2.Join();

Console.WriteLine("Both threads finished.");
```

**Note:** The output order of Thread A and Thread B will be non-deterministic — the OS scheduler decides.

---

## Thread Safety and Locking

When multiple threads access shared data, **race conditions** can produce incorrect results.
Use `lock` to ensure only one thread can enter a critical section at a time.

```csharp
using System;
using System.Threading;

public class BankAccount
{
    private decimal balance;
    private readonly object lockObj = new object();

    public BankAccount(decimal initial) { balance = initial; }

    public void Deposit(decimal amount)
    {
        lock (lockObj) // only one thread executes this block at a time
        {
            balance += amount;
            Console.WriteLine($"Deposited {amount:C}. Balance: {balance:C}");
        }
    }

    public decimal GetBalance()
    {
        lock (lockObj) { return balance; }
    }
}
```

---

## Tasks and the Task Parallel Library (TPL)

`Task` is a higher-level abstraction over threads.
The TPL manages a thread pool, reducing overhead versus creating raw threads.

```csharp
using System;
using System.Threading.Tasks;

// Run work on a background thread
Task task1 = Task.Run(() =>
{
    Console.WriteLine("Task 1 running...");
    Task.Delay(500).Wait();
    Console.WriteLine("Task 1 done.");
});

Task task2 = Task.Run(() =>
{
    Console.WriteLine("Task 2 running...");
    Task.Delay(300).Wait();
    Console.WriteLine("Task 2 done.");
});

// Wait for all tasks to complete
Task.WaitAll(task1, task2);
Console.WriteLine("All tasks complete.");

// A task that returns a value
Task<int> calcTask = Task.Run(() =>
{
    // Simulate a long calculation
    Thread.Sleep(100);
    return 42;
});

int result = calcTask.Result; // Blocks until the task finishes
Console.WriteLine($"Result: {result}");
```

---

## Async/Await

`async` and `await` allow you to write asynchronous code that reads like synchronous code.
This is the modern, preferred approach for I/O-bound tasks (file access, HTTP requests, database queries).

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public static async Task<string> FetchDataAsync(string url)
{
    using HttpClient client = new HttpClient();

    // await releases the calling thread while waiting for the HTTP response
    string content = await client.GetStringAsync(url);
    return content;
}

// Calling code
public static async Task Main()
{
    Console.WriteLine("Fetching data...");
    string data = await FetchDataAsync("https://example.com");
    Console.WriteLine($"Received {data.Length} characters.");
}
```

**Key rules:**
- `async` marks a method as asynchronous.
- `await` suspends the method until the awaited task completes — without blocking the thread.
- Always return `Task` or `Task<T>` from async methods (never `void`, except for event handlers).

---

## Parallel.For and Parallel.ForEach

For CPU-bound work that can be split into independent chunks, use `Parallel.For`
to automatically distribute work across multiple CPU cores.

```csharp
using System;
using System.Threading.Tasks;

int[] data = new int[100_000];

// Fill the array in parallel across all available CPU cores
Parallel.For(0, data.Length, idx =>
{
    data[idx] = idx * idx; // purely independent work per element
});

Console.WriteLine($"First 5: {data[0]}, {data[1]}, {data[2]}, {data[3]}, {data[4]}");
// 0, 1, 4, 9, 16

// Parallel.ForEach for iterating collections
var items = new string[] { "apple", "banana", "cherry", "date" };
Parallel.ForEach(items, item =>
{
    Console.WriteLine($"Processing: {item} on thread {Task.CurrentId}");
});
```

**Important:** Parallel work is only beneficial when tasks are independent.
If tasks share state without proper locking, race conditions will occur.

---

## Choosing the Right Approach

| Approach | Best For |
|----------|----------|
| `Thread` | Low-level control, rarely needed in modern C# |
| `Task` / TPL | CPU-bound background work |
| `async` / `await` | I/O-bound work (network, files, databases) |
| `Parallel.For` | Independent data-parallel loops |

---

## Summary

Concurrency and parallelism are essential for building responsive, high-performance applications.
C# provides multiple layers of abstraction: raw `Thread` for maximum control,
`Task` and the TPL for general background work, `async/await` for clean asynchronous I/O,
and `Parallel.For` for data-parallel CPU work.

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*, Chapter: Concurrency. Packt Publishing.
