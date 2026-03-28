# Module 08: Case Study — Binary Trees and Tree Traversal

## Learning Outcomes

By the end of this module you should be able to:
- Describe the structure of a binary tree and its key terminology.
- Implement pre-order, post-order, and in-order tree traversal.
- Explain binary search trees, AVL trees, Red-Black trees, and binary heaps.

---

## The Problem: Efficient Spell Checking

A word-processing application needs a dictionary of valid words that can be searched quickly.
A binary tree is the ideal structure: it can hold a large vocabulary and locate any word in O(log n) time
when balanced — far faster than a linear list.

---

## Tree Terminology

- **Root** — the topmost node, which has no parent.
- **Node** — an element of the tree containing data and references to children.
- **Leaf** — a node with no children.
- **Height** — the number of levels from a node to its deepest leaf.
- **Binary tree** — each node has **at most two** children (left and right).

---

## Implementing a Binary Tree Node in C#

```csharp
public class TreeNode
{
    public int    Value { get; set; }
    public TreeNode Left  { get; set; }
    public TreeNode Right { get; set; }

    public TreeNode(int value)
    {
        Value = value;
        Left  = null;
        Right = null;
    }
}
```

---

## Tree Traversal

There are three standard ways to visit every node in a binary tree.

### Pre-Order (Root, Left, Right)

Visit the current node first, then recurse left, then recurse right.
Useful for creating a copy of the tree or serialising it.

```csharp
public static void PreOrder(TreeNode node)
{
    if (node == null) return;
    Console.Write($"{node.Value} "); // Visit root first
    PreOrder(node.Left);
    PreOrder(node.Right);
}
```

### In-Order (Left, Root, Right)

Recurse left first, visit the node, then recurse right.
On a binary search tree this visits nodes in **sorted ascending order**.

```csharp
public static void InOrder(TreeNode node)
{
    if (node == null) return;
    InOrder(node.Left);
    Console.Write($"{node.Value} "); // Visit in the middle
    InOrder(node.Right);
}
```

### Post-Order (Left, Right, Root)

Recurse left, then right, then visit the node.
Useful for deletion (delete children before parent) and expression evaluation.

```csharp
public static void PostOrder(TreeNode node)
{
    if (node == null) return;
    PostOrder(node.Left);
    PostOrder(node.Right);
    Console.Write($"{node.Value} "); // Visit root last
}
```

---

## Full Traversal Example

```csharp
class Program
{
    static void Main()
    {
        // Build a small tree manually:
        //       10
        //      /  \
        //     5    15
        //    / \
        //   3   7

        TreeNode root = new TreeNode(10);
        root.Left        = new TreeNode(5);
        root.Right       = new TreeNode(15);
        root.Left.Left   = new TreeNode(3);
        root.Left.Right  = new TreeNode(7);

        Console.Write("Pre-order:  "); PreOrder(root);  Console.WriteLine();
        Console.Write("In-order:   "); InOrder(root);   Console.WriteLine();
        Console.Write("Post-order: "); PostOrder(root); Console.WriteLine();
    }
}
```

**Output:**
```
Pre-order:  10 5 3 7 15
In-order:   3 5 7 10 15
Post-order: 3 7 5 15 10
```

Notice that in-order produces a sorted sequence on a binary search tree.

---

## Binary Search Tree (BST)

A BST enforces a rule: every left child is **smaller** than its parent, and every right child is **larger**.
This means binary search can be applied during lookup, reducing it to O(log n) average.

```csharp
public class BST
{
    private TreeNode root;

    public void Insert(int value)
    {
        root = InsertRec(root, value);
    }

    private TreeNode InsertRec(TreeNode node, int value)
    {
        if (node == null) return new TreeNode(value);
        if (value < node.Value) node.Left  = InsertRec(node.Left,  value);
        else if (value > node.Value) node.Right = InsertRec(node.Right, value);
        return node; // duplicate values ignored
    }

    public bool Search(int value)
    {
        return SearchRec(root, value);
    }

    private bool SearchRec(TreeNode node, int value)
    {
        if (node == null) return false;
        if (value == node.Value) return true;
        if (value < node.Value)  return SearchRec(node.Left,  value);
        return SearchRec(node.Right, value);
    }
}

class Program
{
    static void Main()
    {
        BST tree = new BST();
        foreach (int val in new[] { 10, 5, 15, 3, 7 })
            tree.Insert(val);

        Console.WriteLine(tree.Search(7));  // True
        Console.WriteLine(tree.Search(12)); // False
    }
}
```

---

## AVL Trees

A BST's performance depends on being balanced. If you insert elements in sorted order (e.g. 1, 2, 3, 4),
the tree degenerates into a linked list and lookups drop to O(n).

An **AVL tree** (named after Adelson-Velsky and Landis) automatically **rebalances** after every insert
and delete by performing rotations. The height difference between any node's left and right subtrees
is always at most 1.

AVL trees guarantee **O(log n)** for all operations. This is the tree used in Module 01's assignment (Question 1).

---

## Red-Black Trees

A **Red-Black tree** is another self-balancing BST. Each node is coloured red or black, and a set
of colour rules ensures the tree stays roughly balanced. The rules are:
- All leaves (null nodes) are black.
- Both children of every red node are black.
- All paths from any node to its leaf descendants have the same number of black nodes.

Red-Black trees are used in .NET's `SortedDictionary<K,V>` and `SortedSet<T>` internally
because they have slightly better performance for frequent insertions and deletions than AVL trees.

---

## Binary Heaps

A **binary heap** is a complete binary tree (all levels fully filled except possibly the last, filled left-to-right).

- **Min-Heap**: parent ≤ children — root always holds the minimum value.
- **Max-Heap**: parent ≥ children — root always holds the maximum value.

Heaps are the foundation of the Priority Queue (see Module 05) and the Heap Sort algorithm.

```
Min-Heap example:
         1
       /   \
      3     2
     / \   /
    5   4 6
```

---

## Summary

| Structure | Lookup | Insert | Delete | Sorted? |
|-----------|--------|--------|--------|---------|
| Unbalanced BST | O(n) worst | O(n) worst | O(n) worst | In-order yes |
| AVL Tree | O(log n) | O(log n) | O(log n) | Yes |
| Red-Black Tree | O(log n) | O(log n) | O(log n) | Yes |
| Binary Heap | O(n) | O(log n) | O(log n) (min only) | Partial |

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*, Chapter: Variants of Trees. Packt Publishing.
