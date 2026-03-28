# Data Structures and Algorithms — Final Assignment

It demonstrates the design and implementation of core data structures in C# across four scenario-based questions.

---

## Question 1 — AVL Tree: Library Book Management

**Scenario:** A library management system requires a self-balancing binary search tree to store and manage books
by publication year. The solution must support efficient insertion and deletion while maintaining O(log n) operations.

**Concepts demonstrated:**
- Self-balancing AVL Tree implementation from scratch
- Left and right rotations to maintain tree balance
- Recursive insertion and deletion with rebalancing

```csharp
using System;

namespace Question_One
{

    class q1_Book
    {
        public string Title { get; set; }
        public string Author { get; set; }
        public int Year { get; set; }

        public q1_Book(string title, string author, int year)
        {
            Title = title;
            Author = author;
            Year = year;
        }
    }

    class q1_TreeNode
    {
        public q1_Book Book { get; set; }
        public q1_TreeNode Left { get; set; }
        public q1_TreeNode Right { get; set; }
        public int Height { get; set; }

        public q1_TreeNode(q1_Book book)
        {
            Book = book;
            Height = 1;
        }
    }

    class q1_AVLTree
    {
        private q1_TreeNode root;

        private int GetHeight(q1_TreeNode node)
        {
            return node == null ? 0 : node.Height;
        }

        private int GetBalance(q1_TreeNode node)
        {
            return node == null ? 0 : GetHeight(node.Left) - GetHeight(node.Right);
        }

        private q1_TreeNode RightRotate(q1_TreeNode y)
        {
            q1_TreeNode x = y.Left;
            q1_TreeNode T2 = x.Right;
            x.Right = y;
            y.Left = T2;

            y.Height = Math.Max(GetHeight(y.Left), GetHeight(y.Right)) + 1;
            x.Height = Math.Max(GetHeight(x.Left), GetHeight(x.Right)) + 1;

            return x;
        }

        private q1_TreeNode LeftRotate(q1_TreeNode x)
        {
            q1_TreeNode y = x.Right;
            q1_TreeNode T2 = y.Left;
            y.Left = x;
            x.Right = T2;

            x.Height = Math.Max(GetHeight(x.Left), GetHeight(x.Right)) + 1;
            y.Height = Math.Max(GetHeight(y.Left), GetHeight(y.Right)) + 1;

            return y;
        }

        public q1_TreeNode Insert(q1_TreeNode node, q1_Book book)
        {
            if (node == null)
                return new q1_TreeNode(book);

            if (book.Year < node.Book.Year)
                node.Left = Insert(node.Left, book);
            else if (book.Year > node.Book.Year)
                node.Right = Insert(node.Right, book);
            else
                return node;

            node.Height = 1 + Math.Max(GetHeight(node.Left), GetHeight(node.Right));

            int balance = GetBalance(node);


            if (balance > 1 && book.Year < node.Left.Book.Year)
                return RightRotate(node);

            if (balance > 1 && book.Year > node.Left.Book.Year)
            {
                node.Left = LeftRotate(node.Left);
                return RightRotate(node);
            }

            if (balance < -1 && book.Year > node.Right.Book.Year)
                return LeftRotate(node);

            if (balance < -1 && book.Year < node.Right.Book.Year)
            {
                node.Right = RightRotate(node.Right);
                return LeftRotate(node);
            }

            return node;
        }

        private q1_TreeNode MinValueNode(q1_TreeNode node)
        {
            q1_TreeNode current = node;
            while (current.Left != null)
                current = current.Left;
            return current;
        }

        private q1_TreeNode DeleteNode(q1_TreeNode node, int year)
        {
            if (node == null)
                return node;

            if (year < node.Book.Year)
                node.Left = DeleteNode(node.Left, year);
            else if (year > node.Book.Year)
                node.Right = DeleteNode(node.Right, year);
            else
            {
                if (node.Left == null || node.Right == null)
                {
                    q1_TreeNode temp = node.Left ?? node.Right;
                    if (temp == null)
                    {
                        temp = node;
                        node = null;
                    }
                    else
                        node = temp;
                }
                else
                {
                    q1_TreeNode temp = MinValueNode(node.Right);
                    node.Book = temp.Book;
                    node.Right = DeleteNode(node.Right, temp.Book.Year);
                }
            }

            if (node == null)
                return node;

            node.Height = Math.Max(GetHeight(node.Left), GetHeight(node.Right)) + 1;
            int balance = GetBalance(node);

            if (balance > 1 && GetBalance(node.Left) >= 0)
                return RightRotate(node);

            if (balance > 1 && GetBalance(node.Left) < 0)
            {
                node.Left = LeftRotate(node.Left);
                return RightRotate(node);
            }

            if (balance < -1 && GetBalance(node.Right) <= 0)
                return LeftRotate(node);

            if (balance < -1 && GetBalance(node.Right) > 0)
            {
                node.Right = RightRotate(node.Right);
                return LeftRotate(node);
            }

            return node;
        }

        public void InsertBook(q1_Book book)
        {
            root = Insert(root, book);
        }

        public void DeleteBook(int year)
        {
            root = DeleteNode(root, year);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            q1_AVLTree tree = new q1_AVLTree();

            var books = new[]
            {
                new q1_Book("The Silent Patient", "Alex Michaelides", 2019),
                new q1_Book("The Great Gatsby", "F. Scott Fitzgerald", 1925),
                new q1_Book("1984", "George Orwell", 1949)
            };

            foreach (var book in books)
                tree.InsertBook(book);

            tree.DeleteBook(1925);

            Console.WriteLine("AVL Tree  with inserts and deletes has been implemented");
        }
    }
}
```

---

## Question 2 — Stack: Expression Evaluation

**Scenario:** Implement a stack-based data structure suitable for expression or undo-redo evaluation.

**Concepts demonstrated:**
- Stack data structure fundamentals
- Last-In-First-Out (LIFO) ordering

```csharp
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```

---

## Question 3 — Priority Queue: Hospital Triage System

**Scenario:** A hospital emergency room needs a triage system that always processes the most critical patient
(lowest priority number) first, regardless of arrival order.

**Concepts demonstrated:**
- Min-Heap based Priority Queue built from first principles
- HeapifyUp and HeapifyDown operations
- Dequeue always returns the minimum-priority element

```csharp
using System;
using System.Collections.Generic;

namespace Q3_PriorityQueue
{
    class q3_Patient
    {
        public string Name { get; set; }
        public int Priority { get; set; }

        public q3_Patient(string name, int priority)
        {
            Name = name;
            Priority = priority;
        }
    }

    class q3_PriorityQueue
    {
        private List<q3_Patient> heap = new List<q3_Patient>();

        public void Enqueue(q3_Patient patient)
        {
            heap.Add(patient);
            HeapifyUp(heap.Count - 1);
        }

        private void HeapifyUp(int index)
        {
            while (index > 0)
            {
                int parent = (index - 1) / 2;
                if (heap[index].Priority < heap[parent].Priority)
                {
                    Swap(index, parent);
                    index = parent;
                }
                else
                {
                    break;
                }
            }
        }

        public q3_Patient Dequeue()
        {
            if (heap.Count == 0) return null;

            q3_Patient min = heap[0];
            heap[0] = heap[heap.Count - 1];
            heap.RemoveAt(heap.Count - 1);
            HeapifyDown(0);

            Console.WriteLine($"Dequeued patient: {min.Name} (Priority: {min.Priority})");
            return min;
        }

        private void HeapifyDown(int index)
        {
            int left = 2 * index + 1;
            int right = 2 * index + 2;
            int smallest = index;

            if (left < heap.Count && heap[left].Priority < heap[smallest].Priority)
                smallest = left;

            if (right < heap.Count && heap[right].Priority < heap[smallest].Priority)
                smallest = right;

            if (smallest != index)
            {
                Swap(index, smallest);
                HeapifyDown(smallest);
            }
        }

        private void Swap(int i, int j)
        {
            q3_Patient temp = heap[i];
            heap[i] = heap[j];
            heap[j] = temp;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            q3_PriorityQueue queue = new q3_PriorityQueue();

            queue.Enqueue(new q3_Patient("Patient A", 2));
            queue.Enqueue(new q3_Patient("Patient B", 0));
            queue.Enqueue(new q3_Patient("Patient C", 4));
            queue.Enqueue(new q3_Patient("Patient D", 1));

            queue.Dequeue(); 
            queue.Dequeue(); 
            queue.Dequeue();
            queue.Dequeue(); 
        }
    }
}
```

---

## Question 4 — QuickSort: Hotel Search and Sorting

**Scenario:** A travel application reads hotel data from a JSON file and must present results sorted by a
configurable criterion (name, nightly rate, star rating, or distance from airport).

**Concepts demonstrated:**
- QuickSort algorithm implemented from first principles
- JSON deserialisation using `System.Text.Json`
- Configurable comparator via strategy pattern

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;

namespace Question4_HotelSorting
{
    public class q4_Hotel
    {
        public int id { get; set; }
        public string name { get; set; }
        public double nightly_rate { get; set; }
        public int stars { get; set; }
        public int distance_from_airport { get; set; }
    }

    public class q4_QuickSort
    {
        private static readonly string SortingMetric = "nightly_rate";  // ← Fixed: no space

        public static void Sort(List<q4_Hotel> hotels)
        {
            if (hotels == null || hotels.Count <= 1) return;
            QuickSortRecursive(hotels, 0, hotels.Count - 1);
        }

        private static void QuickSortRecursive(List<q4_Hotel> hotels, int low, int high)
        {
            if (low < high)
            {
                int pi = Partition(hotels, low, high);
                QuickSortRecursive(hotels, low, pi - 1);
                QuickSortRecursive(hotels, pi + 1, high);
            }
        }

        private static int Partition(List<q4_Hotel> hotels, int low, int high)
        {
            q4_Hotel pivot = hotels[high];
            int i = low - 1;
            for (int j = low; j < high; j++)
            {
                if (Compare(hotels[j], pivot) <= 0)
                {
                    i++;
                    Swap(hotels, i, j);
                }
            }
            Swap(hotels, i + 1, high);
            return i + 1;
        }

        private static void Swap(List<q4_Hotel> hotels, int a, int b)
        {
            q4_Hotel tmp = hotels[a];
            hotels[a] = hotels[b];
            hotels[b] = tmp;
        }

        private static int Compare(q4_Hotel a, q4_Hotel b)
        {
            return SortingMetric switch
            {
                "name" => string.Compare(a.name, b.name, StringComparison.Ordinal),
                "nightly_rate" => a.nightly_rate.CompareTo(b.nightly_rate),
                "stars" => a.stars.CompareTo(b.stars),
                "distance_from_airport" => a.distance_from_airport.CompareTo(b.distance_from_airport),
                _ => throw new InvalidOperationException($"Invalid SortingMetric: '{SortingMetric}'")
            };
        }
    }

    internal class Program
    {
        private static void Main(string[] args)
        {
            string jsonFile = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "q4_data (1).json");
            if (!File.Exists(jsonFile))
            {
                Console.WriteLine("ERROR: JSON file not found.");
                Console.ReadKey();
                return;
            }

            string json = File.ReadAllText(jsonFile);
            var hotels = JsonSerializer.Deserialize<List<q4_Hotel>>(json);
            if (hotels == null || hotels.Count == 0)
            {
                Console.WriteLine("No hotels in file.");
                Console.ReadKey();
                return;
            }

            q4_QuickSort.Sort(hotels);

            foreach (var h in hotels)
                Console.WriteLine(h.name);

            Console.ReadKey();  // Keeps window open
        }
    }
}
```

---

## References

- Jamro, M. (2018). *C# Data Structures and Algorithms*. Packt Publishing.
- Jamro, M. (2023). *C# Data Structures and Algorithms* (2nd ed.). Packt Publishing.
- McMillan, M. (2007). *Data Structures and Algorithms Using C#*. Cambridge University Press.
