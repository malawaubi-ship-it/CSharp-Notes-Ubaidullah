# Module 15: Generics in C#

## Learning Outcomes

By the end of this module you should be able to:
- Explain what generics are and why they exist.
- Write generic classes and methods in C#.
- Apply generic constraints to restrict type parameters.

---

## The Problem Generics Solve

Without generics, you would need to either:
1. Write separate versions of a class for each data type (verbose and repetitive), or
2. Use `object` for everything (loses type safety and requires casting).

```csharp
// Non-generic approach — must be cast by the caller, error-prone
public class Box
{
    public object Value { get; set; }
}

Box box = new Box();
box.Value = 42;
int n = (int)box.Value; // runtime error if wrong type
```

Generics solve this by letting you write **type-independent code** that is still **type-safe** and **compiled efficiently**.

---

## Generic Classes

```csharp
// A generic container class — works with any type
public class Box<T>
{
    public T Value { get; set; }

    public Box(T value) { Value = value; }

    public void Display() => Console.WriteLine($"Box contains: {Value}");
}

// Usage — the compiler creates a specific version for each type used
Box<int>    intBox    = new Box<int>(42);
Box<string> stringBox = new Box<string>("Hello");
Box<double> doubleBox = new Box<double>(3.14);

intBox.Display();    // Box contains: 42
stringBox.Display(); // Box contains: Hello
doubleBox.Display(); // Box contains: 3.14
```

---

## Generic Methods

```csharp
// A generic swap method — works for any type
public static void Swap<T>(ref T a, ref T b)
{
    T temp = a;
    a = b;
    b = temp;
}

int x = 10, y = 20;
Swap(ref x, ref y);
Console.WriteLine($"x={x}, y={y}"); // x=20, y=10

string s1 = "Hello", s2 = "World";
Swap(ref s1, ref s2);
Console.WriteLine($"{s1}, {s2}"); // World, Hello
```

---

## Generic Constraints

Use constraints to restrict what types can be used with a generic class or method.

```csharp
// where T : IComparable<T> — ensures T has a CompareTo method
public static T Max<T>(T a, T b) where T : IComparable<T>
{
    return a.CompareTo(b) >= 0 ? a : b;
}

Console.WriteLine(Max(3, 7));       // 7
Console.WriteLine(Max("apple", "banana")); // banana (lexicographic)

// where T : class — T must be a reference type
public static T FirstOrNull<T>(T[] arr) where T : class
{
    return arr.Length > 0 ? arr[0] : null;
}

// where T : new() — T must have a parameterless constructor
public static T Create<T>() where T : new()
{
    return new T();
}
```

---

## Generic Stack Implementation

```csharp
public class GenericStack<T>
{
    private List<T> items = new List<T>();

    public void Push(T item)   => items.Add(item);
    public T    Pop()          {
        if (items.Count == 0) throw new InvalidOperationException("Stack is empty.");
        T item = items[items.Count - 1];
        items.RemoveAt(items.Count - 1);
        return item;
    }
    public T    Peek()         => items.Count > 0
                                    ? items[items.Count - 1]
                                    : throw new InvalidOperationException("Stack is empty.");
    public bool IsEmpty        => items.Count == 0;
    public int  Count          => items.Count;
}

GenericStack<int>    intStack = new GenericStack<int>();
intStack.Push(1); intStack.Push(2); intStack.Push(3);
Console.WriteLine(intStack.Pop()); // 3

GenericStack<string> strStack = new GenericStack<string>();
strStack.Push("A"); strStack.Push("B");
Console.WriteLine(strStack.Peek()); // B
```

---

## Why C#\'s Built-in Collections Are Generic

All of C#'s standard library collections (`List<T>`, `Dictionary<K,V>`, `Queue<T>`, `Stack<T>`, etc.)
are generic. This means they are type-safe without any boxing/unboxing overhead,
making them both safe and fast.

---

## Summary

Generics are one of C#'s most powerful features.
They allow you to write flexible, reusable code without sacrificing type safety or runtime performance.
Whenever you find yourself writing the same logic for different types, a generic is likely the solution.

Reference: Microsoft Docs. "Generics in C# (C# Programming Guide)." docs.microsoft.com
