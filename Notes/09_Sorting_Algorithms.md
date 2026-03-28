# Module 09: Sorting Algorithms

## Learning Outcomes

By the end of this module you should be able to:
- Implement Selection Sort and Insertion Sort in C#.
- Explain the time and space complexity of each algorithm.
- Compare sorting algorithms and choose appropriately for a given scenario.

---

## Why Sorting Matters

Sorting is one of the most frequently performed operations in software.
Sorted data is required for binary search, and many algorithms assume sorted input.
Understanding sorting algorithms teaches recursive thinking, comparison strategies, and complexity analysis.

---

## Selection Sort

**Idea:** Find the smallest element in the unsorted portion and swap it to its correct position.
Repeat until the array is sorted.

**Time complexity:** O(n²) — always, regardless of input.
**Space complexity:** O(1) — in-place.

```csharp
public static void SelectionSort(int[] arr)
{
    int n = arr.Length;
    for (int idx = 0; idx < n - 1; idx++)
    {
        // Find the minimum element in the unsorted section
        int minIdx = idx;
        for (int jdx = idx + 1; jdx < n; jdx++)
        {
            if (arr[jdx] < arr[minIdx])
                minIdx = jdx;
        }

        // Swap the found minimum with the first unsorted element
        (arr[minIdx], arr[idx]) = (arr[idx], arr[minIdx]);
    }
}

class Program
{
    static void Main()
    {
        int[] data = { 64, 25, 12, 22, 11 };
        SelectionSort(data);
        Console.WriteLine(string.Join(", ", data)); // 11, 12, 22, 25, 64
    }
}
```

---

## Insertion Sort

**Idea:** Build the sorted section one element at a time. Take the next unsorted element and insert it
into its correct position in the sorted section by shifting larger elements right.

**Time complexity:** O(n²) worst/average, O(n) best (already sorted).
**Space complexity:** O(1) — in-place.
**Advantage:** Very efficient on small or nearly sorted datasets.

```csharp
public static void InsertionSort(int[] arr)
{
    int n = arr.Length;
    for (int idx = 1; idx < n; idx++)
    {
        int key = arr[idx]; // the element to insert
        int jdx = idx - 1;

        // Shift elements larger than key one position to the right
        while (jdx >= 0 && arr[jdx] > key)
        {
            arr[jdx + 1] = arr[jdx];
            jdx--;
        }

        arr[jdx + 1] = key; // place key in correct position
    }
}

class Program
{
    static void Main()
    {
        int[] data = { 12, 11, 13, 5, 6 };
        InsertionSort(data);
        Console.WriteLine(string.Join(", ", data)); // 5, 6, 11, 12, 13
    }
}
```

---

## Merge Sort

**Idea:** A divide-and-conquer algorithm. Recursively split the array in half, sort each half,
then merge the two sorted halves together.

**Time complexity:** O(n log n) — always.
**Space complexity:** O(n) — requires auxiliary arrays.

```csharp
public static void MergeSort(int[] arr, int left, int right)
{
    if (left >= right) return;

    int mid = (left + right) / 2;
    MergeSort(arr, left, mid);
    MergeSort(arr, mid + 1, right);
    Merge(arr, left, mid, right);
}

private static void Merge(int[] arr, int left, int mid, int right)
{
    int n1 = mid - left + 1;
    int n2 = right - mid;

    int[] L = new int[n1];
    int[] R = new int[n2];

    Array.Copy(arr, left,     L, 0, n1);
    Array.Copy(arr, mid + 1,  R, 0, n2);

    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2)
        arr[k++] = L[i] <= R[j] ? L[i++] : R[j++];

    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

class Program
{
    static void Main()
    {
        int[] data = { 38, 27, 43, 3, 9, 82, 10 };
        MergeSort(data, 0, data.Length - 1);
        Console.WriteLine(string.Join(", ", data)); // 3, 9, 10, 27, 38, 43, 82
    }
}
```

---

## Quick Sort

**Idea:** Select a **pivot** element, partition the array so all elements smaller than the pivot come before it
and all larger elements come after, then recursively sort each partition.

**Time complexity:** O(n log n) average, O(n²) worst case (when pivot is always the smallest/largest).
**Space complexity:** O(log n) average for the call stack.

```csharp
public static void QuickSort(int[] arr, int low, int high)
{
    if (low < high)
    {
        int pivot = Partition(arr, low, high);
        QuickSort(arr, low, pivot - 1);
        QuickSort(arr, pivot + 1, high);
    }
}

private static int Partition(int[] arr, int low, int high)
{
    int pivot = arr[high]; // choose last element as pivot
    int i = low - 1;

    for (int j = low; j < high; j++)
    {
        if (arr[j] <= pivot)
        {
            i++;
            (arr[i], arr[j]) = (arr[j], arr[i]);
        }
    }
    (arr[i + 1], arr[high]) = (arr[high], arr[i + 1]);
    return i + 1;
}

class Program
{
    static void Main()
    {
        int[] data = { 10, 80, 30, 90, 40, 50, 70 };
        QuickSort(data, 0, data.Length - 1);
        Console.WriteLine(string.Join(", ", data)); // 10, 30, 40, 50, 70, 80, 90
    }
}
```

---

## Summary Comparison

| Algorithm | Best | Average | Worst | Space | Stable? |
|-----------|------|---------|-------|-------|---------|
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |

**Stable** means equal elements maintain their original relative order after sorting.

For large datasets, prefer **Merge Sort** (guaranteed O(n log n)) or **Quick Sort** (O(n log n) average, faster in practice).
For small or nearly-sorted data, **Insertion Sort** is surprisingly effective.

In C# you will typically use `Array.Sort()` or `List<T>.Sort()`, which uses an introspective sort
(combines Quick Sort, Heap Sort, and Insertion Sort depending on data size).
