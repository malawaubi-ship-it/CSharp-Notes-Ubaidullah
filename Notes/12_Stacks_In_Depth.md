# Module 12: Stacks In Depth

## Learning Outcomes

By the end of this module you should be able to:
- Explain the LIFO principle and describe all core stack operations.
- Implement a generic stack in C# from scratch.
- Apply stacks to practical problems such as expression evaluation and backtracking.

---

## Stack Operations Review

A stack operates on the **Last In, First Out (LIFO)** principle.

| Operation | Description | Complexity |
|-----------|-------------|-----------|
| `Push(x)` | Add x to the top | O(1) |
| `Pop()` | Remove and return the top element | O(1) |
| `Peek()` | Return top element without removing | O(1) |
| `IsEmpty` | True if stack has no elements | O(1) |
| `Count` | Number of elements | O(1) |

---

## Generic Stack Implementation

```csharp
public class Stack<T>
{
    private T[] data;
    private int top;
    private int capacity;

    public Stack(int capacity = 16)
    {
        this.capacity = capacity;
        data = new T[capacity];
        top  = -1;
    }

    public bool IsEmpty => top == -1;
    public int  Count   => top + 1;

    public void Push(T value)
    {
        if (top == capacity - 1)
        {
            // Double the capacity when full
            T[] larger = new T[capacity * 2];
            Array.Copy(data, larger, capacity);
            data = larger;
            capacity *= 2;
        }
        data[++top] = value;
    }

    public T Pop()
    {
        if (IsEmpty) throw new InvalidOperationException("Stack is empty.");
        return data[top--];
    }

    public T Peek()
    {
        if (IsEmpty) throw new InvalidOperationException("Stack is empty.");
        return data[top];
    }
}
```

---

## Application 1 — Evaluating Postfix Expressions

Postfix (Reverse Polish Notation) avoids the need for brackets.
`3 4 + 2 *` means `(3 + 4) * 2 = 14`.

```csharp
using System;
using System.Collections.Generic;

public static int EvaluatePostfix(string expression)
{
    Stack<int> stack = new Stack<int>();
    string[] tokens = expression.Split(' ');

    foreach (string token in tokens)
    {
        if (int.TryParse(token, out int number))
        {
            stack.Push(number);
        }
        else
        {
            int b = stack.Pop();
            int a = stack.Pop();
            int result = token switch
            {
                "+" => a + b,
                "-" => a - b,
                "*" => a * b,
                "/" => a / b,
                _   => throw new InvalidOperationException($"Unknown operator: {token}")
            };
            stack.Push(result);
        }
    }
    return stack.Pop();
}

Console.WriteLine(EvaluatePostfix("3 4 + 2 *")); // Output: 14
Console.WriteLine(EvaluatePostfix("5 1 2 + 4 * + 3 -")); // Output: 14
```

---

## Application 2 — Undo/Redo Functionality

Many applications implement undo/redo using two stacks.

```csharp
using System;
using System.Collections.Generic;

public class TextEditor
{
    private string text = "";
    private Stack<string> undoStack = new Stack<string>();
    private Stack<string> redoStack = new Stack<string>();

    public void Type(string input)
    {
        undoStack.Push(text);
        redoStack.Clear();
        text += input;
        Console.WriteLine($"Text: '{text}'");
    }

    public void Undo()
    {
        if (undoStack.Count == 0) { Console.WriteLine("Nothing to undo."); return; }
        redoStack.Push(text);
        text = undoStack.Pop();
        Console.WriteLine($"Undo -> Text: '{text}'");
    }

    public void Redo()
    {
        if (redoStack.Count == 0) { Console.WriteLine("Nothing to redo."); return; }
        undoStack.Push(text);
        text = redoStack.Pop();
        Console.WriteLine($"Redo -> Text: '{text}'");
    }
}

class Program
{
    static void Main()
    {
        TextEditor editor = new TextEditor();
        editor.Type("Hello");
        editor.Type(" World");
        editor.Undo();   // Text: 'Hello'
        editor.Redo();   // Text: 'Hello World'
        editor.Type("!"); // Text: 'Hello World!'
    }
}
```

---

## Application 3 — Depth-First Search (Non-Recursive)

DFS can be implemented iteratively using an explicit stack instead of recursion.

```csharp
using System;
using System.Collections.Generic;

public static void IterativeDFS(Dictionary<int, List<int>> graph, int start)
{
    HashSet<int> visited = new HashSet<int>();
    Stack<int> stack = new Stack<int>();

    stack.Push(start);

    Console.Write("DFS: ");
    while (stack.Count > 0)
    {
        int vertex = stack.Pop();
        if (visited.Contains(vertex)) continue;

        visited.Add(vertex);
        Console.Write($"{vertex} ");

        foreach (int neighbour in graph[vertex])
            if (!visited.Contains(neighbour))
                stack.Push(neighbour);
    }
    Console.WriteLine();
}
```

---

## Summary

Stacks are deceptively simple but extremely powerful. Their LIFO property makes them
the natural choice for any algorithm that needs to track a sequence in reverse or
maintain a "current state" while exploring alternatives (backtracking, DFS, expression parsing).

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*. Packt Publishing.
