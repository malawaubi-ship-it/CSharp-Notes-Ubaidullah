# Module 16: The C# Collections Framework

## Learning Outcomes

By the end of this module you should be able to:
- Use the key collection types in `System.Collections.Generic`.
- Understand LINQ and use it to query and transform collections.
- Choose between collection types based on performance characteristics.

---

## Overview

The .NET Collections Framework provides ready-to-use, generic, high-performance data structures.
All the classes below live in `System.Collections.Generic`.

---

## List<T>

A dynamic array — automatically resizes as you add elements.
The most commonly used collection in C#.

```csharp
using System;
using System.Collections.Generic;

List<string> fruits = new List<string> { "apple", "banana", "cherry" };

fruits.Add("date");
fruits.Insert(1, "avocado"); // insert at index 1
fruits.Remove("banana");

Console.WriteLine(fruits.Count); // 4
Console.WriteLine(fruits[2]);    // cherry

// Sort alphabetically
fruits.Sort();

// Check existence
Console.WriteLine(fruits.Contains("apple")); // True

// Convert to array
string[] arr = fruits.ToArray();
```

**Time complexity:** Add = O(1) amortised; Insert/Remove at index = O(n); Lookup by index = O(1).

---

## LinkedList<T>

A doubly linked list — efficient insertion and removal from any position when you already have the node reference.

```csharp
LinkedList<int> linked = new LinkedList<int>();

linked.AddFirst(10);           // [10]
linked.AddLast(30);            // [10, 30]
linked.AddAfter(linked.First, 20); // [10, 20, 30]

Console.WriteLine(linked.First.Value); // 10
Console.WriteLine(linked.Last.Value);  // 30

linked.RemoveFirst();
foreach (int val in linked)
    Console.Write($"{val} "); // 20 30
```

---

## Dictionary<TKey, TValue>

Fast key-value storage. See Module 07 for a full treatment.

```csharp
Dictionary<string, int> scores = new Dictionary<string, int>();
scores["Alice"] = 95;
scores["Bob"]   = 87;

// Iterate key-value pairs
foreach (var (name, score) in scores)
    Console.WriteLine($"{name}: {score}");

// Check if key exists before reading
if (scores.TryGetValue("Alice", out int aliceScore))
    Console.WriteLine($"Alice scored {aliceScore}");
```

---

## HashSet<T>

A collection of **unique** items with O(1) add, remove, and lookup.

```csharp
HashSet<int> setA = new HashSet<int> { 1, 2, 3, 4, 5 };
HashSet<int> setB = new HashSet<int> { 3, 4, 5, 6, 7 };

setA.Add(6);         // { 1, 2, 3, 4, 5, 6 }
setA.Add(3);         // no-op: 3 already exists

// Set operations
HashSet<int> union        = new HashSet<int>(setA); union.UnionWith(setB);
HashSet<int> intersection = new HashSet<int>(setA); intersection.IntersectWith(setB);
HashSet<int> difference   = new HashSet<int>(setA); difference.ExceptWith(setB);

Console.WriteLine(string.Join(", ", intersection)); // 3, 4, 5, 6
```

---

## Queue<T> and Stack<T>

Used exactly as described in Modules 01 and 12.

```csharp
Queue<string> queue = new Queue<string>();
queue.Enqueue("First"); queue.Enqueue("Second");
Console.WriteLine(queue.Dequeue()); // First

Stack<string> stack = new Stack<string>();
stack.Push("A"); stack.Push("B");
Console.WriteLine(stack.Pop()); // B
```

---

## LINQ — Language Integrated Query

LINQ allows you to query, filter, sort, and transform collections using a clean, declarative syntax.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

// Filter: only even numbers
var evens = numbers.Where(n => n % 2 == 0);
Console.WriteLine(string.Join(", ", evens)); // 2, 4, 6, 8, 10

// Transform: square each number
var squares = numbers.Select(n => n * n);
Console.WriteLine(string.Join(", ", squares)); // 1, 4, 9, 16, 25, 36, 49, 64, 81, 100

// Sort descending
var desc = numbers.OrderByDescending(n => n);

// Aggregation
Console.WriteLine(numbers.Sum());      // 55
Console.WriteLine(numbers.Average());  // 5.5
Console.WriteLine(numbers.Max());      // 10
Console.WriteLine(numbers.Min());      // 1

// First matching element or default
int firstBig = numbers.FirstOrDefault(n => n > 7); // 8

// LINQ with objects
var students = new List<(string Name, int Grade)>
{
    ("Alice", 78), ("Bob", 92), ("Carol", 85), ("Dave", 60)
};

var passed = students
    .Where(s => s.Grade >= 70)
    .OrderByDescending(s => s.Grade)
    .Select(s => $"{s.Name}: {s.Grade}");

foreach (string record in passed)
    Console.WriteLine(record);
// Bob: 92
// Carol: 85
// Alice: 78
```

---

## Collection Comparison

| Collection | Ordered | Duplicates | Key-Value | Lookup | Best Use |
|------------|---------|------------|-----------|--------|----------|
| `List<T>` | Yes (index) | Yes | No | O(1) index | General sequence |
| `LinkedList<T>` | Yes | Yes | No | O(n) | Frequent mid-list insert/delete |
| `Dictionary<K,V>` | No | No (keys) | Yes | O(1) | Fast key lookup |
| `HashSet<T>` | No | No | No | O(1) | Unique items, set operations |
| `SortedSet<T>` | Yes | No | No | O(log n) | Unique + sorted |
| `Queue<T>` | FIFO | Yes | No | O(1) front | Scheduling |
| `Stack<T>` | LIFO | Yes | No | O(1) top | Undo, backtracking |

---

## Summary

C#'s generic collections eliminate the need to write most custom data structures from scratch.
LINQ further reduces boilerplate by letting you query collections in a readable, functional style.

Reference: Microsoft Docs. "System.Collections.Generic Namespace." docs.microsoft.com
