# Module 12: Stack

## 1. Learning outcomes

By the end of this topic you should be able to:c
you will learn about classification of data structures. Also, the diversity of some real-world applications in relation to arrays, lists, stacks, queues, dictionaries, sets, trees, heaps and graphs will be treated.
 

Prescribed Reading
Jamro, M., 2018. C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd. 
Page 258 – 269. 
Time Allocation:
2 Hours
 
## 2. Stack

 
Stack is a special type of collection that stores elements in LIFO style (Last In First Out). C# includes the generic Stack<T> and non-generic Stack collection classes. It is recommended to use the generic Stack<T> collection.
 
Stack is useful to store temporary data in LIFO style, and you might want to delete an element after retrieving its value.
 
Stack<T> Characteristics
Stack<T> is Last In First Out collection.
It comes under System.Collection.Generic namespace.
Stack<T> can contain elements of the specified type. It provides compile-time type checking and doesn't perform boxing-unboxing because it is generic.
Elements can be added using the Push() method. Cannot use collection-initializer syntax.
Elements can be retrieved using the Pop() and the Peek() methods. It does not support an indexer.
## 3. Queue

Queue represents a first-in, first out (FIFO) collection of object. It is used when you need a first-in, first-out access of items. When you add an item in the list, it is called enqueue, and when you remove an item, it is called dequeue . This class comes under System.Collections namespace and implements ICollection, IEnumerable, and ICloneable interfaces.
 Characteristics of Queue Class:
Enqueue adds an element to the end of the Queue.
Dequeue removes the oldest element from the start of the Queue.
Peek returns the oldest element that is at the start of the Queue but does not remove it from the Queue.
The capacity of a Queue is the number of elements the Queue can hold.
As elements are added to a Queue, the capacity is automatically increased as required by reallocating the internal array.
Queue accepts null as a valid value for reference types and allows duplicate elements.


	-	3. Creating String Object
