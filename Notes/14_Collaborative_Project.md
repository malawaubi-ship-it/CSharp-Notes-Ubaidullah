# Module 14: Applied Case Studies — Mixed Data Structures

## Learning Outcomes

By the end of this module you should be able to:
- Select and justify an appropriate data structure for a given problem.
- Combine multiple data structures in a single solution.
- Explain the trade-offs between different implementation choices.

---

## Case Study 1 — Contact Book (Dictionary + Sorted List)

A contact book needs fast lookup by name and the ability to display contacts alphabetically.

```csharp
using System;
using System.Collections.Generic;

public class ContactBook
{
    // O(1) lookup by name
    private Dictionary<string, string> contacts = new Dictionary<string, string>(StringComparer.OrdinalIgnoreCase);

    public void AddContact(string name, string phone)
    {
        contacts[name] = phone;
        Console.WriteLine($"Added: {name} - {phone}");
    }

    public void LookUp(string name)
    {
        if (contacts.TryGetValue(name, out string phone))
            Console.WriteLine($"{name}: {phone}");
        else
            Console.WriteLine($"{name} not found.");
    }

    public void DisplayAll()
    {
        // SortedDictionary gives alphabetical order during iteration
        SortedDictionary<string, string> sorted = new SortedDictionary<string, string>(contacts);

        Console.WriteLine("\nAll contacts (A-Z):");
        foreach (var kvp in sorted)
            Console.WriteLine($"  {kvp.Key}: {kvp.Value}");
    }

    public void RemoveContact(string name) => contacts.Remove(name);
}

class Program
{
    static void Main()
    {
        ContactBook book = new ContactBook();
        book.AddContact("Zara", "083 000 0001");
        book.AddContact("Alice", "082 000 0002");
        book.AddContact("Bob", "081 000 0003");

        book.LookUp("alice"); // case-insensitive
        book.DisplayAll();
    }
}
```

---

## Case Study 2 — Web Crawler BFS

A web crawler visits every page on a website starting from the homepage.
BFS ensures pages closest to the homepage are visited first.

```csharp
using System;
using System.Collections.Generic;

public class WebCrawler
{
    // Adjacency list representing hyperlinks between pages
    private Dictionary<string, List<string>> links = new Dictionary<string, List<string>>();

    public void AddLink(string page, string linkedPage)
    {
        if (!links.ContainsKey(page))
            links[page] = new List<string>();
        links[page].Add(linkedPage);
    }

    public void Crawl(string startPage)
    {
        HashSet<string> visited = new HashSet<string>();
        Queue<string>   queue   = new Queue<string>();

        queue.Enqueue(startPage);
        visited.Add(startPage);

        Console.WriteLine($"Crawling from: {startPage}");
        int order = 1;

        while (queue.Count > 0)
        {
            string page = queue.Dequeue();
            Console.WriteLine($"  [{order++}] Visiting: {page}");

            if (!links.ContainsKey(page)) continue;

            foreach (string linkedPage in links[page])
            {
                if (!visited.Contains(linkedPage))
                {
                    visited.Add(linkedPage);
                    queue.Enqueue(linkedPage);
                }
            }
        }
    }
}

class Program
{
    static void Main()
    {
        WebCrawler crawler = new WebCrawler();
        crawler.AddLink("/home",    "/about");
        crawler.AddLink("/home",    "/products");
        crawler.AddLink("/products", "/product-1");
        crawler.AddLink("/products", "/product-2");
        crawler.AddLink("/about",   "/team");

        crawler.Crawl("/home");
    }
}
```

---

## Case Study 3 — Expression Evaluator (Stack)

Evaluate arithmetic expressions in infix notation by converting to postfix first.

```csharp
using System;
using System.Collections.Generic;

public static class InfixEvaluator
{
    private static int Precedence(char op) => (op == '+' || op == '-') ? 1 : 2;

    public static string InfixToPostfix(string expression)
    {
        Stack<char> opStack = new Stack<char>();
        List<string> output = new List<string>();

        foreach (char ch in expression.Replace(" ", ""))
        {
            if (char.IsDigit(ch))
            {
                output.Add(ch.ToString());
            }
            else if (ch == '(')
            {
                opStack.Push(ch);
            }
            else if (ch == ')')
            {
                while (opStack.Peek() != '(')
                    output.Add(opStack.Pop().ToString());
                opStack.Pop(); // remove '('
            }
            else // operator
            {
                while (opStack.Count > 0 && opStack.Peek() != '(' &&
                       Precedence(opStack.Peek()) >= Precedence(ch))
                    output.Add(opStack.Pop().ToString());
                opStack.Push(ch);
            }
        }

        while (opStack.Count > 0)
            output.Add(opStack.Pop().ToString());

        return string.Join(" ", output);
    }
}

Console.WriteLine(InfixEvaluator.InfixToPostfix("3 + 4 * 2"));     // 3 4 2 * +
Console.WriteLine(InfixEvaluator.InfixToPostfix("(3 + 4) * 2"));   // 3 4 + 2 *
```

---

## Choosing the Right Data Structure

| Problem | Recommended Structure | Reason |
|---------|----------------------|--------|
| Fast key lookup | Dictionary<K,V> | O(1) average |
| Sorted key iteration | SortedDictionary | Sorted keys |
| Unique items | HashSet | O(1) duplicate check |
| FIFO processing | Queue<T> | Ordered removal |
| LIFO / backtracking | Stack<T> | Reversal operations |
| Sorted data, fast search | BST / SortedSet | O(log n) |

---

## Summary

Real applications rarely use just one data structure. The skill lies in recognising which combination
of structures achieves the correct behaviour at the required performance level.
Always analyse time complexity, memory usage, and ordering requirements before choosing.
