# Module 7: Case Study

## 1. Learning outcomes
By the end of this topic you should be able to:
	-	Acquire the skill to interpret data structures and algorithms.
	-	Implement data structures in C#.
	-	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Jamro, M., (2018). Dictionaries and Sets, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p115-p143



## 2. Case Study
Clothing One Ltd is a department shop that sells many different products. They need to have a system that stores information about the different products they sell. This system must be able to retrieve information quickly, as it is used by the point-of-sale computers to retrieve price information, when customers checkout. The company uses hashing for this. Each product is assigned a unique identification number, that can be represented using a barcode. When a user scans the barcode, the computer reads in the unique identifier number, and queries this in the data system. The computer then returns the relevant product information.
## 3. Hashing
The idea behind hashing is that an input value is used to obtain some output value. The input  value is know as a key. The output value is known as a value. Together, they are commonly called a key-value pair. A hashing algorithm is then used to map the key to its corresponding value. These values are present in a structure known as buckets. The key doesn’t map to the value itself, rather it maps to a bucket, in which the value is stored. This allows users to retrieve elements from the data structure like they do in arrays, except with hashing, a key is used instead of an index.
 
The image below shows keys being mapped to values, present in buckets, with a hash function.
Ideally, each bucket will only have one key pointing to it, however, implementing such a system is often complex. Realistically, buckets will have multiple keys pointing to them. Such an event is known as a hash collision. When this occurs, values are stored in arrays, lists or binary trees (or another suitable data structure) within the bucket. A separate search must then be done to retrieve the value corresponding to the key. A key will only ever point to one bucket.
 
Hashing functions can be complicated, or as simple as a modulus operation. Here is a visualisation of hashing done using modulus[1].
 
As values are retrieved using a key, hashing offers a best and worst case retrieval, insertion and deletion time of O(1). However, in a worst case scenario, when extreme hash collisions takes place, and all elements are present in a single bucket, hashing will offer a worst case retrieval, insertion and deletion of O(n).



[1] Open Hashing visualization (2024). https://www.cs.usfca.edu/~galles/visualization/OpenHash.html.
3.1. Hash Tables
Hashing algorithms can be complicated to implement. Fortunately, C# includes a few data structures based on hashing. HashTable is a non-generic data structure, which means values can be any type. The documentation[1] and implementation[2] can be found on the Microsoft website.



[1] Dotnet-Bot (2024) Hashtable Class (System.Collections). https://learn.microsoft.com/en-us/dotnet/api/system.collections.hashtable?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#mscorlib/system/collections/hashtable.cs,10fefb6e0ae510dd.
3.2. Dictionaries
Dictionaries are another hash implementation offered by C#. It is a generic alternative to HashTable, and it is recommended to use this over HashTable. The documentation[1] and implementation[2] can be found on the Microsoft website.



[1] Dotnet-Bot (2024) Dictionary Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#mscorlib/system/collections/generic/dictionary.cs,d3599058f8d79be0.
3.3. Sorted Dictionaries
SortedDictionary is a class that, to the user, acts like a dictionary, and keeps its keys always sorted. The documentation[1] and implementation[2] can be viewed on the Microsoft website. While having keys always sorted can be advantageous in certain scenarios, sorted dictionaries have the disadvantage of slow performance, having a retrieval, insertion and deletion time of O(logn).



[1] Dotnet-Bot (2024) SortedDictionary Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.sorteddictionary-2?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#System/compmod/system/collections/generic/sorteddictionary.cs,ba6f0c7de63e2c74.
3.4. Hash Sets
A set is a data structure that stores a single type (generic) of data. Unlike HashTable and Dictionary, a set only requires a single value, not a key-value pair. Each element in a sett must be unique. It is useful for performing mathematical operations such as unions, intersections, subtractions, etc. The documentation[1] and implementation[2] for HashSets can be viewed on the Microsoft website.



[1] Dotnet-Bot (2024) HashSet Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#System.Core/System/Collections/Generic/HashSet.cs,50c894a3f7ad7bd0.
3.5. Sorted Sets
Much like with SortDictionary, HashSets have a sorted equivalent, SortedSet. This performs similarly to HashSet, except that the elements are always sorted. The documentation[1] and C# implementation[2] can be viewed on the Microsoft website.



[1] Dotnet-Bot (2024) SortedSet Class (System.Collections.Generic). https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.sortedset-1?view=net-8.0.
[2] Reference source (2024). https://referencesource.microsoft.com/#System/compmod/system/collections/generic/sortedset.cs,bae1c41b842726a2.


	-	3. Binary Trees
	-	4. Tree Traversal
	-	4.1. Pre-order
	-	4.2. Post-order
	-	4.3. In-order
	-	5. Binary Search Trees
	-	6. AVL Trees
	-	7. Red-Black Trees
	-	8. Binary Heaps
	-	8.1. Min-Heap
	-	8.2. Max-Heap
