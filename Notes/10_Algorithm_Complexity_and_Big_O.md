# Module 10: Algorithm Complexity and Big O Notation

## Learning Outcomes

By the end of this module you should be able to:
- Define time and space complexity.
- Read and write Big O notation.
- Identify the complexity class of a given algorithm.
- Compare algorithms using their complexity.

---

## Why Complexity Analysis Matters

Two programs that produce the same output may differ radically in performance as inputs grow.
An algorithm that takes one second on 1,000 items might take 1,000 seconds on 1,000,000 items
if it is O(n²). Complexity analysis lets you predict this behaviour before you write a single line of code.

---

## Big O Notation

**Big O** expresses how the runtime (or memory usage) of an algorithm grows as the input size **n** increases,
ignoring constants and low-order terms because they become insignificant for large n.

```
f(n) = 3n² + 7n + 12    →    O(n²)
f(n) = 2n + 100          →    O(n)
f(n) = 8                 →    O(1)
```

---

## Common Complexity Classes

### O(1) — Constant Time

Runtime does not change regardless of input size.

```csharp
// Accessing an array element is always instant, no matter how large the array
int[] arr = { 10, 20, 30, 40, 50 };
int value = arr[3]; // O(1)
```

### O(log n) — Logarithmic Time

Each step halves the problem size. Very efficient for large data.

```csharp
// Binary search: eliminates half the remaining elements each step
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
// For 1,000,000 elements, at most ~20 iterations are needed
```

### O(n) — Linear Time

Runtime grows proportionally with input size.

```csharp
// Linear search: checks every element in the worst case
public static int LinearSearch(int[] arr, int target)
{
    for (int idx = 0; idx < arr.Length; idx++)
        if (arr[idx] == target) return idx;
    return -1;
}
// For 1,000,000 elements: up to 1,000,000 comparisons
```

### O(n log n) — Linearithmic Time

Typical for efficient sorting algorithms like Merge Sort and Quick Sort.

```csharp
// C# Array.Sort() runs in O(n log n) on average
int[] data = { 5, 2, 8, 1, 9 };
Array.Sort(data); // O(n log n)
```

### O(n²) — Quadratic Time

A loop nested inside another loop over n elements.

```csharp
// Count all pairs in an array — O(n²)
public static int CountPairs(int[] arr)
{
    int count = 0;
    for (int idx = 0; idx < arr.Length; idx++)
        for (int jdx = idx + 1; jdx < arr.Length; jdx++)
            count++;
    return count;
}
// For 1,000 elements: ~500,000 operations
// For 10,000 elements: ~50,000,000 operations
```

### O(2ⁿ) — Exponential Time

Typically seen in brute-force algorithms that explore every possible combination.
Becomes impractical very quickly — for n=50, that is over a quadrillion operations.

---

## Growth Rate Comparison

| n | O(1) | O(log n) | O(n) | O(n log n) | O(n²) |
|---|------|----------|------|------------|-------|
| 10 | 1 | 3 | 10 | 33 | 100 |
| 100 | 1 | 7 | 100 | 664 | 10,000 |
| 1,000 | 1 | 10 | 1,000 | 9,966 | 1,000,000 |
| 1,000,000 | 1 | 20 | 1,000,000 | ~20M | 10¹² |

---

## Best, Average, and Worst Case

An algorithm's complexity can vary depending on the input.

- **Best case** — the most favourable input (e.g. the target is the first element in linear search).
- **Worst case** — the most unfavourable input (e.g. target not present).
- **Average case** — the expected performance over all possible inputs.

We usually use **worst-case** analysis because it gives an upper bound guarantee.

```
Linear search:
  Best case:  O(1)  — target is at index 0
  Worst case: O(n)  — target is last or not present
  Average:    O(n/2) = O(n)
```

---

## Space Complexity

Space complexity measures how much **extra memory** an algorithm uses, not counting the input.

```csharp
// O(1) space — only uses a fixed number of variables
public static int Sum(int[] arr)
{
    int total = 0;
    foreach (int x in arr) total += x;
    return total;
}

// O(n) space — creates a new array proportional to input size
public static int[] DoubleAll(int[] arr)
{
    int[] result = new int[arr.Length]; // n extra space
    for (int idx = 0; idx < arr.Length; idx++)
        result[idx] = arr[idx] * 2;
    return result;
}
```

---

## Summary

Understanding Big O helps you make informed decisions about which data structure or algorithm to use.
Always aim for the lowest complexity class that is practical for your problem.

| Use this | When | Complexity |
|----------|------|-----------|
| Hash table lookup | Fast key-based retrieval | O(1) |
| Binary search | Sorted array lookup | O(log n) |
| Merge sort / Quick sort | General sorting | O(n log n) |
| Bubble / Selection sort | Only for tiny datasets | O(n²) |
