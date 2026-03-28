# Module 8: Case Study

1. Learning outcomes
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). Variants of Trees, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p145-p200
  
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Case Study
In a word processing application, users often require an efficient and accurate spell checker to detect and correct spelling errors in their documents. Binary trees can be utilized to implement a dictionary data structure for storing valid words, enabling fast and accurate spell checking functionality.
3. Binary Trees
So far, we have looked at unitary data structures, such as linked-lists, which is made up of nodes that are linked together, where each node will have at most 2 connections: forwards and backwards. There are data structures that allow for nodes to more than 2 connections. One such example is a tree structure.
 
In a tree structure, a node is connected to one or more child nodes. The node at the beginning of the tree, with no parent node is called the root. The nodes at the end of the tree, with no children nodes are called leaves. Nodes that share a parent are known as siblings. We will only look at a type of tree called a binary tree in this module, where every node can have at most 2 child nodes.
 
In the image below, node 1 is the root, whilst nodes 5, 6 and 3 are leaves. Note how the structure branches out from the root.

4. Tree Traversal
When iterating through a unitary structure, such as a linked-list, we just proceed in either a forward or backward direction, as there is only one path. However, with binary trees, the structure is more complicated, thus, there are multiple paths to choose when iterating.
 
There are 3 ways for traversing a binary tree: pre-order, post-order and in-order.
4.1. Pre-order
In pre-order traversal, the root is visited first, followed by the left child node. The next left child node is visited until there is no left child node (a recursive operation), in which case, the right child node is visited, and we reverse up the tree[1].
 
The image below shows you pre-order traversal. The numArray represent the order in which the nodes are visited.  
 

[1] GeeksforGeeks (2023a) Preorder traversal of binary tree. https://www.geeksforgeeks.org/preorder-traversal-of-binary-tree/.
4.2. Post-order
In post-order traversal, the left child is visited first (recursively), followed by the right child, and then the root is visited last.[1]
 
The image below shows you post-order traversal. The numArray represent the order in which the nodes are visited.
 
 
[1] GeeksforGeeks (2023a) Postorder traversal of binary tree. https://www.geeksforgeeks.org/postorder-traversal-of-binary-tree/.
4.3. In-order
In in-order traversal, we visit the left child node first (recursively), then visit its parent, then visit the right child node.[1]
 
The image below shows you in-order traversal. The numArray represent the order in which the nodes are visited.
 

[1] GeeksforGeeks (2023a) Inorder traversal of binary tree. https://www.geeksforgeeks.org/inorder-traversal-of-binary-tree/.
5. Binary Search Trees
Regular binary trees do not specify any relationship between the values of nodes. When searching for an element, in the worst case, we must traverse the entire tree, leading to a time complexity of O(n).
 
We can specify rules in a binary tree:
	•	The value of a node’s left child must be smaller than it.
	•	The value of a node’s right child must be larger than it. 
 
The rules above must hold true for every node. When these rules are implemented, the tree becomes sorted, and such a tree is called a binary search tree.
 
This is advantageous because this allows us to perform a binary search. When searching for an element in a binary search tree, we compare the value with that of the node, and one of 3 outcomes will be produced:
	•	The values are equal: in which case, the element has been found.
	•	The value is less than the node: in which case we search the left node.
	•	The value is greater than the node: in which case we search the right node. 
 
This search is done recursively. If a left or right node doesn’t exist (or is null), it means we have reached the end of the tree and the element does not exist.
 
Let us look at the diagram below:

 
Suppose we are searching for 20:
	•	We compare 20 with the first node: 20 < 45, so we proceed to the left child.
	•	We compare 20 with the node: 20 > 15, so we proceed to the right child.
	•	We compare 20 with the node: 20 == 20. The element has been found. 
Suppose we are searching for 51:
	•	We compare 51 with the first node: 51 > 45, so we proceed to the right node.
	•	We compare 51 with the node: 51 < 79, so we proceed to the left node.
	•	We compare 51 to the node: 51 < 55, so we proceed to the left node.
	•	We compare 51 to the node: 51 > 50, so we proceed to the right node.
	•	The node is null (it does not exist). We have reached the end of the tree. Therefore, 51 does not exist. 
From the tree above, we see that at every subtree, half of the subtree gets discarded after a comparison is made, which does not need to be searched. This gives binary search a O(logn) lookup time. You can find a useful visualisation on the University of San Francisco website[1].
 

[1] Binary Search Tree Visualization (2024). https://www.cs.usfca.edu/~galles/visualization/BST.html.
6. AVL Trees
One of the issues with binary search trees is that its structure depends on when elements are added and removed. A tree created with the insertion of [1,2,3] will look different than a tree with the insertion of [2,1,3], even though they have the same elements. An extreme problem occurs when each node only has a left node or each node only has a right node. This refers to the balance of a tree.
 
The following image shows an unbalanced tree where each node only has a right child node.  
When this occurs, we cannot benefit from binary search, since the structure becomes unitary. The lookup time will become O(n).
 
To solve this, we need an algorithm that balances trees for us, or trees that will balance themselves. Such a tree is called an AVL tree[1], named after its inventors, Adelson-Velsky and Landis.
 
In AVL trees, the height (distance from leaf to root) between leave nodes is allowed to differ by at most 1 level. If the tree breaks this rule, rotations to subtrees are made until the tree is in compliance with this rule. AVL trees are a special type of binary search tree, so it must comply with binary search tree rules as well. The University of San Francisco has a useful visualisation[2].
 

[1] GeeksforGeeks (2023a) AVL Tree Data Structure. https://www.geeksforgeeks.org/introduction-to-avl-tree/.
[2] AVL Tree Visualzation (2024). https://www.cs.usfca.edu/~galles/visualization/AVLtree.html.
7. Red-Black Trees
Red-black trees[1] are another special type of binary search tree that is self-balanced. Each node is assigned a colour, either red or black. It follows the following rules:
	•	Nodes with values cannot be leave nodes (leaf nodes must be null)
	•	Both children of red nodes must be black
	•	Every path from the root to any leaf must have the same number of black nodes. 
 
The self-balancing feature allows Red-Black trees to maintain the same time complexity as AVL trees. In practice, however, AVL trees perform faster in retrieval operations as they are stricter about balancing. Red-black trees perform better in insertion and deletion as these are less complicated than in AVL trees.
 
The University of San Franciso has a useful visualisation[2].
 

[1] GeeksforGeeks (2023b) Introduction to Red Black Tree. https://www.geeksforgeeks.org/introduction-to-red-black-tree/.
[2] Red/Black tree visualization (2024). https://www.cs.usfca.edu/~galles/visualization/RedBlack.html.
8. Binary Heaps
Heaps are a type of binary tree (note, not binary search tree) that maintains a relationship between the child and parent node. There are two types of binary heaps: min-heap and max-heap.
8.1. Min-Heap
In a min-heap, parent nodes are smaller than their child nodes. The root node contains the minimum value.

8.2. Max-Heap
In a max-heap, parent nodes are larger than their child nodes. The root node contains the maximum value.


	•	2. Relevance Connection
	•	3. Sorting
	•	3.1. Selection Sort
	•	3.2. Insertion Sort
