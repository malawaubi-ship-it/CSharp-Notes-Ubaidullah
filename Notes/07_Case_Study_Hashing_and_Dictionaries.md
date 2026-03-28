# Module 07: Case Study — Hashing, Hash Tables, and Dictionaries

## Learning Outcomes

By the end of this module you should be able to:
- Explain how hashing works and what a hash collision is.
- Use C#'s `Hashtable`, `Dictionary<K,V>`, `SortedDictionary<K,V>`, `HashSet<T>`, and `SortedSet<T>`.
- Analyse the time complexity of hash-based operations.

---

## The Problem: Fast Lookup

A retail point-of-sale system needs to retrieve a product's price by scanning its barcode.
With thousands of products, iterating through a list for each scan would be unacceptably slow (O(n)).

**Hashing** solves this by mapping a key directly to a location (called a **bucket**) in constant time — O(1).

---

## How Hashing Works

1. A **hash function** takes a key (e.g. a barcode number) and returns an index.
2. The value is stored at that index in an array of buckets.
3. When you look up the key, the same hash function is applied to find the bucket instantly.

```
Key: 12345   →   hash(12345) % 10  =  5   →   bucket[5] = "Bread, £1.50"
```

**Hash collisions** occur when two keys map to the same bucket.
Collisions are handled by storing multiple items in the same bucket (using a list or tree within the bucket).

For a good hash function, the average lookup time remains O(1). In the absolute worst case
(all keys in one bucket), it degrades to O(n).

---

## HashTable (Non-Generic)

`Hashtable` is the older, non-generic implementation — it accepts any object as key and value.
It has been largely superseded by `Dictionary<K,V>`.

```csharp
using System;
using System.Collections;

Hashtable products = new Hashtable();
products.Add("001", "Milk - £1.20");
products.Add("002", "Bread - £0.90");
products.Add("003", "Coffee - £3.50");

if (products.ContainsKey("002"))
    Console.WriteLine(products["002"]); // Output: Bread - £0.90

// Iterate all entries
foreach (DictionaryEntry entry in products)
    Console.WriteLine($"{entry.Key}: {entry.Value}");
```

---

## Dictionary<TKey, TValue> (Recommended)

`Dictionary<K,V>` is the generic, type-safe alternative and is strongly preferred.

```csharp
using System;
using System.Collections.Generic;

Dictionary<string, double> prices = new Dictionary<string, double>();
prices["001"] = 1.20;
prices["002"] = 0.90;
prices["003"] = 3.50;

// Safe lookup
if (prices.TryGetValue("002", out double price))
    Console.WriteLine($"Bread costs £{price}"); // £0.90

// Add or update
prices["004"] = 2.75;
prices["001"] = 1.35; // updates existing

// Remove
prices.Remove("003");

// Iterate
foreach (var kvp in prices)
    Console.WriteLine($"Barcode {kvp.Key}: £{kvp.Value}");
```

**Time complexity:** O(1) average for insert, lookup, and delete.

---

## SortedDictionary<TKey, TValue>

`SortedDictionary` works like `Dictionary` but keeps keys in **sorted order** at all times.
This is useful when you need to output keys alphabetically or numerically.

```csharp
using System.Collections.Generic;

SortedDictionary<string, int> wordCount = new SortedDictionary<string, int>();
wordCount["banana"] = 3;
wordCount["apple"]  = 7;
wordCount["cherry"] = 1;

foreach (var kvp in wordCount)
    Console.WriteLine($"{kvp.Key}: {kvp.Value}");
// Output (alphabetically sorted):
// apple: 7
// banana: 3
// cherry: 1
```

**Trade-off:** Lookup, insert, and delete are all O(log n) — slower than `Dictionary` but always sorted.

---

## HashSet<T>

A `HashSet<T>` stores a collection of **unique values** — no duplicates allowed.
It supports efficient mathematical set operations.

```csharp
using System;
using System.Collections.Generic;

HashSet<string> setA = new HashSet<string> { "apple", "banana", "cherry" };
HashSet<string> setB = new HashSet<string> { "banana", "cherry", "date" };

// Attempts to add a duplicate are silently ignored
setA.Add("apple"); // no effect

// Set operations
setA.UnionWith(setB);      // setA now contains all unique items from both
setA.IntersectWith(setB);  // only items in both
setA.ExceptWith(setB);     // items in setA but not setB

Console.WriteLine(setA.Contains("banana")); // True
```

---

## SortedSet<T>

Like `HashSet<T>` but elements are always kept sorted.

```csharp
using System.Collections.Generic;

SortedSet<int> sortedSet = new SortedSet<int> { 5, 2, 8, 1, 9, 3 };

foreach (int val in sortedSet)
    Console.Write($"{val} "); // Output: 1 2 3 5 8 9
```

---

## Comparison Table

| Type | Duplicates | Key-Value Pairs | Sorted | Lookups |
|------|-----------|-----------------|--------|---------|
| `Hashtable` | No (keys) | Yes | No | O(1) |
| `Dictionary<K,V>` | No (keys) | Yes | No | O(1) |
| `SortedDictionary<K,V>` | No (keys) | Yes | Yes (by key) | O(log n) |
| `HashSet<T>` | No | No | No | O(1) |
| `SortedSet<T>` | No | No | Yes | O(log n) |

---

## Summary

Hash-based structures allow O(1) average-time lookup, making them ideal wherever fast key-based
retrieval is needed. Use `Dictionary<K,V>` as your default choice. Reach for `SortedDictionary` when
sorted key order matters, `HashSet` for unique-item collections, and `SortedSet` when uniqueness and sorting are both needed.

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*, Chapter: Dictionaries and Sets. Packt Publishing.
