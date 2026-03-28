# Module 13: Strings and Text Processing

## Learning Outcomes

By the end of this module you should be able to:
- Create and manipulate strings in C#.
- Apply common string operations: concatenation, searching, splitting, and replacing.
- Use `StringBuilder` for efficient string construction.
- Write basic regular expressions.

---

## Strings in C#

A `string` in C# is an **immutable** sequence of Unicode characters.
Immutable means that once a string is created, it cannot be modified — any operation that
appears to change a string actually creates a new string object in memory.

```csharp
string greeting = "Hello, World!";

Console.WriteLine(greeting.Length);             // 13
Console.WriteLine(greeting.ToUpper());          // HELLO, WORLD!
Console.WriteLine(greeting.ToLower());          // hello, world!
Console.WriteLine(greeting.Contains("World")); // True
Console.WriteLine(greeting.StartsWith("He"));  // True
Console.WriteLine(greeting.EndsWith("!"));     // True
```

---

## Creating Strings

```csharp
// String literal
string name = "Alice";

// String interpolation (recommended for readability)
int age = 21;
string intro = $"My name is {name} and I am {age} years old.";
Console.WriteLine(intro);

// Concatenation
string firstName = "John";
string lastName  = "Smith";
string fullName  = firstName + " " + lastName;

// Verbatim string (ignores escape sequences — useful for file paths)
string path = @"C:\Users\Alice\Documents";
```

---

## Common String Operations

```csharp
string sentence = "  The quick brown fox jumps over the lazy dog  ";

// Remove leading/trailing whitespace
string trimmed = sentence.Trim();

// Find index of a substring (-1 if not found)
int idx = trimmed.IndexOf("fox"); // returns position of 'f'

// Extract a portion of a string
string sub = trimmed.Substring(4, 5); // "quick"

// Replace part of a string
string replaced = trimmed.Replace("fox", "cat");

// Split into an array by a delimiter
string csv = "Alice,Bob,Charlie,Dave";
string[] names = csv.Split(',');
foreach (string n in names)
    Console.WriteLine(n);

// Join an array back into a string
string joined = string.Join(" | ", names);
Console.WriteLine(joined); // Alice | Bob | Charlie | Dave
```

---

## String Comparison

```csharp
string a = "Hello";
string b = "hello";

// Case-sensitive comparison (== operator)
Console.WriteLine(a == b);  // False

// Case-insensitive comparison
Console.WriteLine(string.Equals(a, b, StringComparison.OrdinalIgnoreCase)); // True

// Lexicographic comparison (useful for sorting)
int result = string.Compare("apple", "banana", StringComparison.Ordinal);
// Negative = "apple" comes before "banana"
```

---

## StringBuilder — Efficient String Construction

Because strings are immutable, concatenating many strings in a loop creates many temporary objects.
`StringBuilder` avoids this by maintaining a mutable buffer.

```csharp
using System.Text;

// Inefficient — creates a new string object each iteration
string result1 = "";
for (int idx = 0; idx < 10000; idx++)
    result1 += idx.ToString(); // O(n^2) total work

// Efficient — StringBuilder modifies its internal buffer
StringBuilder sb = new StringBuilder();
for (int idx = 0; idx < 10000; idx++)
    sb.Append(idx);
string result2 = sb.ToString(); // O(n) total work

// Other StringBuilder operations
sb.Insert(0, "Start: ");
sb.Replace("5000", "FIVE-THOUSAND");
sb.AppendLine("\nEnd.");
```

**Rule of thumb:** Use `+` for a small number of concatenations. Use `StringBuilder` when building
strings in loops or combining many pieces.

---

## String Formatting

```csharp
double pi = 3.14159265358979;

Console.WriteLine($"Pi to 2 decimal places: {pi:F2}");     // 3.14
Console.WriteLine($"Pi in scientific notation: {pi:E2}");   // 3.14E+000
Console.WriteLine($"Padded left  (10 chars): {pi,10:F2}"); // right-aligned
Console.WriteLine($"Padded right (10 chars): {pi,-10:F2}");// left-aligned

int number = 1234567;
Console.WriteLine($"With thousands separator: {number:N0}"); // 1,234,567
```

---

## Regular Expressions

A **regular expression (regex)** is a pattern used to match and manipulate text.

```csharp
using System;
using System.Text.RegularExpressions;

// Check if a string matches a pattern
string email   = "alice@example.com";
string pattern = @"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$";

bool isValid = Regex.IsMatch(email, pattern);
Console.WriteLine($"Valid email: {isValid}"); // True

// Extract all numbers from a string
string text    = "I have 3 cats and 12 books and 1 dog.";
MatchCollection matches = Regex.Matches(text, @"\d+");
foreach (Match m in matches)
    Console.Write($"{m.Value} "); // 3 12 1

// Replace pattern matches
string cleaned = Regex.Replace("Hello  World   !!", @"\s+", " ");
Console.WriteLine(cleaned); // Hello World !!
```

---

## Summary

Strings are fundamental in nearly every application.
C# provides a rich API for working with them through `System.String` and `System.Text.StringBuilder`.
For pattern matching, `System.Text.RegularExpressions` provides a powerful regex engine.

Reference: Microsoft Docs. "System.String Class." docs.microsoft.com
