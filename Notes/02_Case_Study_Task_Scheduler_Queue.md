# Module 2: Case Study Task Scheduler Using Queue

## 1. Learning outcomes
 
By the end of this topic you should be able to:
	-	Acquire the skill to interpret data structures and algorithms.
	-	Implement data structures in C#.
	-	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd.






## 2. Case Study: Task Scheduler Using Queue
Understanding the Problem
Imagine you are developing a task scheduling system for a company. The system needs to handle background tasks, such as sending emails, backing up databases, and generating reports. However, these tasks must be executed in the order they were received—First-In, First-Out (FIFO).
This is a common problem in computing where jobs are queued up and processed in sequence. A real-world example of this would be a printer queue: when multiple users send documents to a shared printer, the printer processes the documents in the order they were submitted.
Solution: Using a Queue
A queue is the ideal data structure for this scenario. A queue follows the FIFO (First-In, First-Out) principle, meaning that the first task added will be the first one to be processed.
Queues provide two main operations:
	-	Enqueue – Adds a task to the queue.
	-	Dequeue – Removes and processes the first task in the queue.
Example: Task Scheduler Using Queue
Let’s implement a simple task scheduler using a queue in C#.

using System;
using System.Collections.Generic;
 
public class TaskScheduler {
    private Queue<string> taskQueue = new Queue<string>();
 
    public void AddTask(string task) {
        taskQueue.Enqueue(task);
        Console.WriteLine( $"Task added: {task}");
    }
 
    public void ProcessTask() {
        if (taskQueue.Count > 0) {
            Console.WriteLine( $"Processing: {taskQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No tasks to process.");
        }
    }
 
    public void ShowTasks() {
        if (taskQueue.Count == 0) {
            Console.WriteLine( "No pending tasks.");
            return;
        }
        Console.WriteLine( "Pending tasks:");
        foreach (var task in taskQueue) {
            Console.WriteLine( task);
        }
    }
}
 
// Test Program
class MainProgram {
    static void Main() {
        TaskScheduler scheduler = new TaskScheduler();
        scheduler.AddTask("Email Report");
        scheduler.AddTask("Database Backup");
        scheduler.ShowTasks();
        scheduler.ProcessTask();
        scheduler.ShowTasks();
    }
}
Output
Task added: Email Report  
Task added: Database Backup  
Pending tasks:  
Email Report  
Database Backup  
Processing: Email Report  
Pending tasks:  
Database Backup  
In this example, we use a Queue<string> to store tasks. The program allows adding tasks to the queue, processing them one by one, and displaying the remaining tasks.

## 3. Data Structures and Input/Output in C#
C# provides a variety of data structures that allow us to store, manage, and manipulate data efficiently. Understanding these structures is crucial for developing robust applications. In this lesson, we will explore different types of lists in C#, understand how to perform input and output operations, and learn how to implement a task scheduler using a queue.
By the end of this lesson, you will be able to:
 Understand different types of lists and their usage.
 Use queues to implement a simple task scheduler.
 Perform input and output operations in C#.
 Work with ArrayLists, Generic Lists, Sorted Lists, Linked Lists, and Circular Linked Lists.
 Complete two hands-on activities to reinforce learning.

## 4. Lists in C#
A list is a data structure that stores a collection of elements. Unlike arrays, which have a fixed size, lists can dynamically grow and shrink. Lists allow easy insertion, deletion, and searching of elements, making them more flexible than arrays.
C# provides different types of lists, including ArrayList, Generic List, Sorted List, Linked List, and Circular Linked List. Each type has its own advantages and use cases. Let’s explore them one by one.

4.1. Input and Output in C#
Understanding Input and Output
Input and Output (I/O) operations allow a program to interact with users. Input refers to data received from the user, while output refers to data displayed to the user. C# provides the Console.ReadLine() method to read input and Console.WriteLine( ) to display output.
Example: Basic Input and Output
Console.Write("Enter your name: ");
string name = Console.ReadLine();
Console.WriteLine( "Hello, " + name);
Output
Enter your name: John  
Hello, John  



4.2. ArrayList in C#
An ArrayList is a non-generic collection that can store different types of data. Unlike arrays, ArrayList can dynamically grow and shrink. However, because it stores objects, type safety is not enforced.
Example: Using ArrayList
using System;
using System.Collections;
 
class MainProgram {
    static void Main() {
        ArrayList arrList = new ArrayList();
        arrList.Add(10);
        arrList.Add("Hello");
        arrList.Add(3.14);
        
        foreach (var item in arrList) {
            Console.WriteLine( item);
        }
    }
}
Output
10  
Hello  
3.14  



4.3. Generic List in C#
A Generic List (List<T>) is a strongly typed collection that provides better performance and type safety compared to ArrayList.
Example: Using Generic List

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        List<int> numArray = new List<int> { 10, 20, 30 };
        numArray.Add(40);
 
        foreach (int num in numArray) {
            Console.WriteLine( num);
        }
    }
}
Output
10  
20  
30  
40  



4.4. Linked List
Introduction:
A Linked List is a linear data structure where each element (called a node) is connected to the next one. Unlike arrays, linked lists do not require contiguous memory, making them efficient for dynamic memory allocation. In C#, linked lists are commonly implemented using the LinkedList<T> class, which is part of the System.Collections.Generic namespace.
Structure of a Linked List:
	-	Node: Each node contains two parts:
	-	Data: The actual data stored in the node.
	-	Next: A reference (or pointer) to the next node in the list.
	-	Head: The first node of the list.
	-	Tail: The last node of the list (which typically points to null).
Types of Linked Lists:
	-	Singly Linked List: Each node has a reference to the next node. The last node points to null.
	-	Doubly Linked List: Each node contains two references: one to the next node and another to the previous node.
	-	Circular Linked List: The last node points back to the head node, forming a circular structure.
Basic Operations:
	-	Insertion:
	-	At the beginning: Add a new node as the head.
	-	At the end: Traverse to the last node and append the new node.
	-	At a given position: Traverse the list and insert the node at the required position.
	-	Deletion:
	-	From the beginning: Remove the head node.
	-	From the end: Traverse to the second-to-last node and set its next reference to null.
	-	From a given position: Traverse the list, update the references to bypass the node to be deleted.
	-	Traversal: Starting from the head node, visit each node until null is reached (for singly linked lists) or the desired condition is met.
	-	Search: Traverse the list to find a node with specific data.
C# Implementation (Singly Linked List Example):

using System;

public class Node {
    public int Data;
    public Node Next;

    public Node(int data) {
        Data = data;
        Next = null;
    }
}

public class LinkedList {
    public Node Head;

    // Insert a node at the beginning
    public void InsertAtBeginning(int data) {
        Node newNode = new Node(data);
        newNode.Next = Head;
        Head = newNode;
    }

    // Print the list
    public void PrintList() {
        Node current = Head;
        while (current != null) {
            Console.Write(current.Data + " ");
            current = current.Next;
        }
        Console.WriteLine( );
    }

    // Delete a node with a specific value
    public void Delete(int value) {
        if (Head == null) return;

        if (Head.Data == value) {
            Head = Head.Next; // Remove head
            return;
        }

        Node current = Head;
        while (current.Next != null && current.Next.Data != value) {
            current = current.Next;
        }

        if (current.Next != null) {
            current.Next = current.Next.Next; // Remove node
        }
    }
}

class MainProgram {
    static void Main() {
        LinkedList list = new LinkedList();
        list.InsertAtBeginning(10);
        list.InsertAtBeginning(20);
        list.InsertAtBeginning(30);

        Console.WriteLine( "List: ");
        list.PrintList();

        list.Delete(20);
        Console.WriteLine( "After Deleting 20: ");
        list.PrintList();
    }
}
Expected Output:
List:
30 20 10
After Deleting 20:
30 10

4.5. Circular-linked List
Introduction:
A Circular Linked List is a variation of the linked list where the last node points back to the first node, creating a loop. This makes it a circular structure. Circular linked lists can be either singly or doubly linked.
Key Characteristics:
	-	The last node’s Next points to the first node.
	-	There is no null node in a circular linked list; the list is circular, meaning you can traverse it endlessly.
	-	Circular Singly Linked List: Each node has a reference to the next node, and the last node points to the head node.
	-	Circular Doubly Linked List: Each node has two references: one to the next node and another to the previous node. Both the head and tail nodes point to each other, completing the loop.
Advantages:
	-	Circular linked lists are especially useful for implementing applications like round-robin scheduling, playing a playlist of songs, or managing a circular buffer.
	-	Can be useful in situations where the list is frequently traversed and you want to avoid rechecking the starting point after reaching the end.
Basic Operations in Circular Linked List:
	-	Insertion at the beginning, end, or specific position: Similar to regular linked lists, but ensuring that the last node’s Next points to the first node.
	-	Traversal: To avoid infinite loops, traversal should stop when we reach the starting node again.
	-	Deletion: Remove a node, ensuring the circular structure is maintained by adjusting the Next pointer of the previous node.
C# Implementation (Circular Singly Linked List Example):

using System;

public class Node {
    public int Data;
    public Node Next;

    public Node(int data) {
        Data = data;
        Next = null;
    }
}

public class CircularLinkedList {
    private Node head;

    // Insert a node at the end of the list (circular)
    public void InsertAtEnd(int data) {
        Node newNode = new Node(data);
        
        if (head == null) {
            head = newNode;
            newNode.Next = head; // Point to itself
        } else {
            Node tempVal = head;
            while (tempVal.Next != head) { // Traverse until we reach the last node
                tempVal = tempVal.Next;
            }
            tempVal.Next = newNode;
            newNode.Next = head; // Make the list circular again
        }
    }

    // Print the circular list
    public void PrintList() {
        if (head == null) {
            Console.WriteLine( "List is empty.");
            return;
        }

        Node current = head;
        do {
            Console.Write(current.Data + " ");
            current = current.Next;
        } while (current != head); // Stop when we loop back to the head
        Console.WriteLine( );
    }

    // Delete a node with a specific value
    public void Delete(int value) {
        if (head == null) return;

        if (head.Data == value) {
            // If there's only one node
            if (head.Next == head) {
                head = null;
            } else {
                Node tempVal = head;
                while (tempVal.Next != head) { // Traverse to the last node
                    tempVal = tempVal.Next;
                }
                head = head.Next; // Move head to the next node
                tempVal.Next = head; // Adjust the last node to point to the new head
            }
            return;
        }

        Node current = head;
        while (current.Next != head && current.Next.Data != value) {
            current = current.Next;
        }

        if (current.Next != head) {
            current.Next = current.Next.Next; // Remove the node
        }
    }
}

class MainProgram {
    static void Main() {
        CircularLinkedList list = new CircularLinkedList();
        list.InsertAtEnd(10);
        list.InsertAtEnd(20);
        list.InsertAtEnd(30);

        Console.WriteLine( "Circular List: ");
        list.PrintList();

        list.Delete(20);
        Console.WriteLine( "After Deleting 20: ");
        list.PrintList();
    }
}
Expected Output:
Circular List:
10 20 30
After Deleting 20:
10 30

Comparison of Linked List and Circular Linked List:
Feature
Linked List
Circular Linked List
End of List
The last node points to null.
The last node points to the head.
Traversal
Stops when null is encountered.
Loops infinitely, requires careful stopping.
Use Cases
Good for dynamically changing data.
Ideal for round-robin scheduling, circular buffers, etc.
Memory Management
No circular references, easy to delete.
More complex due to circular references.
Conclusion:
	-	A Linked List is a basic dynamic data structure ideal for applications that need efficient insertions and deletions.
	-	A Circular Linked List is a variation where the last node points back to the first node, making it suitable for scenarios where the data needs to be processed in a cyclic manner.
Both structures provide efficient ways of handling dynamic data with flexible memory usage, depending on the specific problem requirements.


4.6. Case Study 1
Problem:
You need to develop a simple task management application where tasks can have mixed data types (e.g., string for task description, integer for priority, and DateTime for deadlines). For this, an ArrayList is suitable because it can hold elements of any data type, allowing you to store these varied properties for each task.
Solution:
We will use an ArrayList to store tasks, where each task is a combination of task description (string), priority (int), and deadline (DateTime). We'll implement functionality to add new tasks, display tasks, and remove a task.
Code Solution:
using System;
using System.Collections;
 
public class Task {
    public string Description { get; set; }
    public int Priority { get; set; }
    public DateTime Deadline { get; set; }
 
    public Task(string description, int priority, DateTime deadline) {
        Description = description;
        Priority = priority;
        Deadline = deadline;
    }
}
 
class MainProgram {
    static void Main() {
        ArrayList taskList = new ArrayList();
        
        // Adding tasks with mixed data types
        taskList.Add(new Task("Send Email", 1, DateTime.Now.AddHours(2)));
        taskList.Add(new Task("Backup Database", 2, DateTime.Now.AddDays(1)));
        taskList.Add(new Task("Generate Report", 3, DateTime.Now.AddHours(5)));
        
        // Displaying tasks
        foreach (Task task in taskList) {
            Console.WriteLine( $"Task: {task.Description}, Priority: {task.Priority}, Deadline: {task.Deadline}");
        }
 
        // Removing a task
        taskList.RemoveAt(1); // Remove second task
        Console.WriteLine( "\nAfter removing second task:\n");
        
        // Displaying tasks after removal
        foreach (Task task in taskList) {
            Console.WriteLine( $"Task: {task.Description}, Priority: {task.Priority}, Deadline: {task.Deadline}");
        }
    }
}
Expected Output:

Task: Send Email, Priority: 1, Deadline: [DateTime]
Task: Backup Database, Priority: 2, Deadline: [DateTime]
Task: Generate Report, Priority: 3, Deadline: [DateTime]
 
After removing second task:
 
Task: Send Email, Priority: 1, Deadline: [DateTime]
Task: Generate Report, Priority: 3, Deadline: [DateTime]



4.7. Case Study 2
Problem:
You are tasked with developing a simple grade management system for a class. You need to store students' grades, which will be integers. A Generic List<int> is suitable as it ensures type safety and provides flexible manipulation of the grade data.
Solution:
We'll use a Generic List<int> to store the student grades and implement functions to add, remove, and display grades.
Code Solution:

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        // Creating a generic list to store student grades
        List<int> grades = new List<int> { 85, 92, 76, 88, 95 };
 
        // Adding a new grade
        grades.Add(89);
 
        // Removing a grade
        grades.Remove(76);
 
        // Displaying all grades
        Console.WriteLine( "Student Grades:");
        foreach (int grade in grades) {
            Console.WriteLine( grade);
        }
 
        // Calculating average grade
        double average = CalculateAverage(grades);
        Console.WriteLine( $"\nAverage Grade: {average:F2}");
    }
 
    static double CalculateAverage(List<int> grades) {
        double sum = 0;
        foreach (int grade in grades) {
            sum += grade;
        }
        return sum / grades.Count;
    }
}
Expected Output:

Student Grades:
85
92
88
95
89
 
Average Grade: 89.80



4.8. Case Study 3
Problem:
You need to develop a music player application where users can dynamically add or remove songs from the playlist. A Linked List is ideal because it allows efficient insertion and removal of songs from the beginning, middle, or end of the list.
Solution:
We'll use a LinkedList<string> to represent the playlist. We will implement methods to add new songs, remove songs, and display the entire playlist.
Code Solution:

using System;
using System.Collections.Generic;
 
public class Playlist {
    private LinkedList<string> songs = new LinkedList<string>();
 
    // Add a song to the playlist
    public void AddSong(string song) {
        songs.AddLast(song);
        Console.WriteLine( $"Song added: {song}");
    }
 
    // Remove a song from the playlist
    public void RemoveSong(string song) {
        if (songs.Contains(song)) {
            songs.Remove(song);
            Console.WriteLine( $"Song removed: {song}");
        } else {
            Console.WriteLine( "Song not found in the playlist.");
        }
    }
 
    // Display all songs in the playlist
    public void ShowPlaylist() {
        Console.WriteLine( "\nCurrent Playlist:");
        foreach (var song in songs) {
            Console.WriteLine( song);
        }
    }
}
 
class MainProgram {
    static void Main() {
        Playlist playlist = new Playlist();
        
        // Adding songs to the playlist
        playlist.AddSong("Song A");
        playlist.AddSong("Song B");
        playlist.AddSong("Song C");
        
        // Displaying the playlist
        playlist.ShowPlaylist();
        
        // Removing a song
        playlist.RemoveSong("Song B");
        
        // Displaying the playlist after removal
        playlist.ShowPlaylist();
    }
}
Expected Output:

Song added: Song A
Song added: Song B
Song added: Song C
 
Current Playlist:
Song A
Song B
Song C
 
Song removed: Song B
 
Current Playlist:
Song A
Song C



4.9. Case Study 4
Problem:
You are designing a game where players can navigate through different levels, and the navigation should loop back to the first level after reaching the last one. A Circular Linked Listis ideal to model this behavior.
Solution:
We'll create a Circular Linked List where each node represents a level in the game. The last node will point back to the first node, creating a circular structure for navigation.
Code Solution:

using System;
 
public class Level {
    public string LevelName { get; set; }
    public Level NextLevel { get; set; }
 
    public Level(string levelName) {
        LevelName = levelName;
    }
}
 
public class CircularLinkedList {
    private Level head;
 
    public void AddLevel(string levelName) {
        Level newLevel = new Level(levelName);
        if (head == null) {
            head = newLevel;
            head.NextLevel = head; // Point to itself, circular link
        } else {
            Level tempVal = head;
            while (tempVal.NextLevel != head) {
                tempVal = tempVal.NextLevel;
            }
            tempVal.NextLevel = newLevel;
            newLevel.NextLevel = head; // Complete the circular link
        }
    }
 
    public void ShowLevels() {
        if (head == null) {
            Console.WriteLine( "No levels in the game.");
            return;
        }
 
        Level current = head;
        do {
            Console.WriteLine( current.LevelName);
            current = current.NextLevel;
        } while (current != head); // Stop when we loop back to the first level
    }
}
 
class MainProgram {
    static void Main() {
        CircularLinkedList gameLevels = new CircularLinkedList();
        
        // Adding levels to the game
        gameLevels.AddLevel("Level 1");
        gameLevels.AddLevel("Level 2");
        gameLevels.AddLevel("Level 3");
        
        // Displaying all levels in a circular fashion
        gameLevels.ShowLevels();
    }
}
Expected Output:

Level 1
Level 2
Level 3

These case studies demonstrate how to apply different data structures in real-world scenarios using C#:
	-	ArrayList for heterogeneous task data.
	-	Generic List for managing student grades.
	-	Linked List for dynamic playlist management.
	-	Circular Linked List for looping through game levels.
Each solution provides an efficient way to handle the problem using the most appropriate data structure.
 


## 5. Activity
Activity 1: Implement a Stack for Undo Feature
Task:
Create a C# program that simulates an Undo feature using a Stack. The user should be able to add actions, undo the last action, and view all actions.
using System;
using System.Collections.Generic;
 
class UndoSystem {
    private Stack<string> actions = new Stack<string>();
 
    public void AddAction(string action) {
        actions.Push(action);
        Console.WriteLine( $"Action added: {action}");
    }
 
    public void UndoAction() {
        if (actions.Count > 0) {
            Console.WriteLine( $"Undoing: {actions.Pop()}");
        } else {
            Console.WriteLine( "No actions to undo.");
        }
    }
 
    public void ShowActions() {
        Console.WriteLine( "Actions:");
        foreach (var action in actions) {
            Console.WriteLine( action);
        }
    }
}
 
// Test Program
class MainProgram {
    static void Main() {
        UndoSystem undoSystem = new UndoSystem();
        undoSystem.AddAction("Opened File");
        undoSystem.AddAction("Edited Text");
        undoSystem.ShowActions();
        undoSystem.UndoAction();
        undoSystem.ShowActions();
    }
}
 
	-	2. Introduction
	-	3. Using Stack in C#:
	-	4. Advantages of Using Stacks:
	-	5. Disadvantages of Using Stacks:
	-	9. Conclusion
	-	10. Activity
