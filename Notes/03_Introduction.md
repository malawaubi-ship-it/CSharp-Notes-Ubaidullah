# Module 03: Introduction to Algorithms

## Learning Outcomes

By the end of this module you should be able to:
- Define what an algorithm is.
- Explain the properties that make an algorithm correct and efficient.
- Describe common algorithm design strategies.
- Understand how to reason about algorithm performance.

---

## What is an Algorithm?

An **algorithm** is a finite, ordered sequence of well-defined instructions for solving a problem or
performing a computation.

Every algorithm must have:
- **Input** — zero or more values given to the algorithm.
- **Output** — at least one result produced.
- **Definiteness** — each step is precisely defined with no ambiguity.
- **Finiteness** — the algorithm terminates after a finite number of steps.
- **Effectiveness** — each step can be performed by a person with pen and paper.

---

## Measuring Algorithm Performance

When comparing algorithms, we care about two things:
- **Time complexity** — how long does it take as the input grows?
- **Space complexity** — how much memory does it use?

We use **Big O notation** to express these, ignoring constants and focusing on the dominant term.

| Notation | Name | Example |
|----------|------|---------|
| O(1) | Constant | Array index access |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search |
| O(n log n) | Linearithmic | Merge sort |
| O(n²) | Quadratic | Bubble sort |
| O(2ⁿ) | Exponential | Brute-force subsets |

See Module 10 for a full dedicated section on Big O notation and complexity analysis.

---

## Algorithm Design Strategies

### Divide and Conquer
Break the problem into smaller sub-problems, solve each recursively, and combine the results.

Example: Merge Sort divides an array in half, sorts each half, then merges them.

```csharp
// Simple demonstration of divide and conquer: finding the maximum in an array
public static int FindMax(int[] arr, int left, int right)
{
    if (left == right)
        return arr[left]; // Base case: single element

    int mid = (left + right) / 2;
    int leftMax  = FindMax(arr, left, mid);
    int rightMax = FindMax(arr, mid + 1, right);

    return Math.Max(leftMax, rightMax);
}

// Usage
int[] values = { 3, 7, 1, 9, 4, 6 };
Console.WriteLine(FindMax(values, 0, values.Length - 1)); // Output: 9
```

### Greedy Algorithms
Make the locally optimal choice at each step, hoping it leads to a global optimum.

Example: When making change, always pick the largest coin that fits.

```csharp
// Greedy coin change: return minimum number of coins for a given amount
public static void MakeChange(int amount)
{
    int[] coins = { 100, 50, 20, 10, 5, 2, 1 }; // descending order
    int total = 0;

    foreach (int coin in coins)
    {
        int count = amount / coin;
        if (count > 0)
        {
            Console.WriteLine($"{count} x {coin}c");
            amount -= count * coin;
            total  += count;
        }
    }
    Console.WriteLine($"Total coins used: {total}");
}
```

### Dynamic Programming
Solve a problem by combining solutions to overlapping sub-problems, storing results to avoid recomputation.

Example: Fibonacci with memoisation.

```csharp
using System.Collections.Generic;

public static long Fibonacci(int n, Dictionary<int, long> memo = null)
{
    if (memo == null) memo = new Dictionary<int, long>();
    if (n <= 1)       return n;
    if (memo.ContainsKey(n)) return memo[n];

    memo[n] = Fibonacci(n - 1, memo) + Fibonacci(n - 2, memo);
    return memo[n];
}

Console.WriteLine(Fibonacci(40)); // Output: 102334155 (fast, no repeated work)
```

---

## Linear Search vs Binary Search

Linear search checks every element one by one — O(n) worst case.
Binary search works only on **sorted** data but eliminates half the search space each step — O(log n).

```csharp
// Linear search — works on unsorted data
public static int LinearSearch(int[] arr, int target)
{
    for (int idx = 0; idx < arr.Length; idx++)
        if (arr[idx] == target) return idx;
    return -1; // not found
}

// Binary search — requires sorted data
public static int BinarySearch(int[] arr, int target)
{
    int low = 0, high = arr.Length - 1;
    while (low <= high)
    {
        int mid = (low + high) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target)  low  = mid + 1;
        else                    high = mid - 1;
    }
    return -1;
}

int[] sorted = { 2, 5, 8, 12, 16, 23, 38, 56, 72, 91 };
Console.WriteLine(BinarySearch(sorted, 23)); // Output: 5 (index)
```

---

## Summary

Algorithms are the core logic of every program. Understanding how to evaluate their efficiency
using Big O notation and how to apply design strategies (divide and conquer, greedy, dynamic programming)
gives you the tools to write programs that scale.

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*. Packt Publishing.
