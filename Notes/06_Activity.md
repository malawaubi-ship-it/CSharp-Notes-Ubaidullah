# Module 06: Applied Activities — Data Structures

## Learning Outcomes

By the end of this module you should be able to:
- Apply your knowledge of arrays, linked lists, stacks, and queues to coding exercises.
- Implement data structure operations from scratch.
- Reason about why different data structures fit different types of problems.

---

## Activity 1 — Implement a Stack Using an Array

Implement a stack in C# **without** using the built-in `Stack<T>` class.
Your implementation must support: `Push`, `Pop`, `Peek`, and `IsEmpty`.

```csharp
public class ArrayStack
{
    private int[] data;
    private int top;
    private int capacity;

    public ArrayStack(int capacity)
    {
        this.capacity = capacity;
        data = new int[capacity];
        top  = -1;
    }

    public bool IsEmpty => top == -1;
    public bool IsFull  => top == capacity - 1;

    public void Push(int value)
    {
        if (IsFull) { Console.WriteLine("Stack overflow."); return; }
        data[++top] = value;
    }

    public int Pop()
    {
        if (IsEmpty) { Console.WriteLine("Stack underflow."); return -1; }
        return data[top--];
    }

    public int Peek()
    {
        if (IsEmpty) { Console.WriteLine("Stack is empty."); return -1; }
        return data[top];
    }
}

class Program
{
    static void Main()
    {
        ArrayStack stack = new ArrayStack(5);
        stack.Push(10);
        stack.Push(20);
        stack.Push(30);

        Console.WriteLine(stack.Peek()); // 30
        Console.WriteLine(stack.Pop());  // 30
        Console.WriteLine(stack.Pop());  // 20
        Console.WriteLine(stack.Pop());  // 10
        Console.WriteLine(stack.Pop());  // Stack underflow.
    }
}
```

---

## Activity 2 — Implement a Queue Using a Linked List

Implement a queue using a singly linked list **without** using `Queue<T>`.

```csharp
public class Node
{
    public int Value;
    public Node Next;
    public Node(int value) { Value = value; Next = null; }
}

public class LinkedQueue
{
    private Node front;
    private Node rear;
    public  int  Count { get; private set; }

    public bool IsEmpty => front == null;

    public void Enqueue(int value)
    {
        Node newNode = new Node(value);
        if (rear == null) { front = rear = newNode; }
        else              { rear.Next = newNode; rear = newNode; }
        Count++;
    }

    public int Dequeue()
    {
        if (IsEmpty) { Console.WriteLine("Queue is empty."); return -1; }
        int value = front.Value;
        front = front.Next;
        if (front == null) rear = null;
        Count--;
        return value;
    }

    public int Peek()
    {
        if (IsEmpty) throw new InvalidOperationException("Queue is empty.");
        return front.Value;
    }
}

class Program
{
    static void Main()
    {
        LinkedQueue queue = new LinkedQueue();
        queue.Enqueue(5);
        queue.Enqueue(10);
        queue.Enqueue(15);

        Console.WriteLine(queue.Dequeue()); // 5
        Console.WriteLine(queue.Peek());    // 10
        Console.WriteLine(queue.Count);     // 2
    }
}
```

---

## Activity 3 — Reverse a String Using a Stack

A classic interview-style problem: reverse a string using a stack.

```csharp
using System;
using System.Collections.Generic;

public static string Reverse(string input)
{
    Stack<char> stack = new Stack<char>();

    foreach (char ch in input)
        stack.Push(ch);

    char[] reversed = new char[input.Length];
    for (int idx = 0; idx < input.Length; idx++)
        reversed[idx] = stack.Pop();

    return new string(reversed);
}

Console.WriteLine(Reverse("Hello")); // Output: olleH
Console.WriteLine(Reverse("Data Structures")); // Output: serutcurtS ataD
```

---

## Activity 4 — Balanced Parentheses Checker

Determine whether a mathematical expression has balanced brackets using a stack.

```csharp
using System;
using System.Collections.Generic;

public static bool IsBalanced(string expression)
{
    Stack<char> stack = new Stack<char>();

    foreach (char ch in expression)
    {
        if (ch == '(' || ch == '[' || ch == '{')
        {
            stack.Push(ch);
        }
        else if (ch == ')' || ch == ']' || ch == '}')
        {
            if (stack.Count == 0) return false;

            char top = stack.Pop();
            if ((ch == ')' && top != '(') ||
                (ch == ']' && top != '[') ||
                (ch == '}' && top != '{'))
                return false;
        }
    }

    return stack.Count == 0;
}

Console.WriteLine(IsBalanced("(a + b) * [c - d]")); // True
Console.WriteLine(IsBalanced("((a + b)"));           // False — unmatched
Console.WriteLine(IsBalanced("{[()]}"));              // True
Console.WriteLine(IsBalanced("{[(])}"));              // False — wrong order
```

---

## Summary

These activities reinforce the core operations of stacks and queues through practical implementation.
Notice how stacks are especially useful for problems involving **reversal** and **matching**,
while queues shine in **sequential processing** problems.
