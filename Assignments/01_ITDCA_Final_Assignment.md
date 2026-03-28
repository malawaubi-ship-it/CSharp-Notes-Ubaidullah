
Individual Assessment Coversheet
To be attached to the front of the assessment.

Campus:			Bedfordview campus		 Faculty:		 Information Technology		 Module Code:		ITDCA		  Group:	1		  Lecturer’s Name:	 Mr Mosingathi	 Student Full Name: Ubaidullah Abdula	  Student Number: EDUV4957588		 

Indicate
Yes
No
Plagiarism report attached


Declaration:
I declare that this assessment is my own original work except for source material explicitly acknowledged. I also declare that this assessment or any other of my original work related to it has not been previously, or is not being simultaneously, submitted for this or any other course. I am aware of the AI policy and acknowledge that I have not used any AI technology to generate or manipulate data, other than as permitted by the assessment instructions. I also declare that I am aware of the Institution’s policy and regulations on honesty in academic work as set out in the Conditions of Enrolment, and of the disciplinary guidelines applicable to breaches of such policy and regulations.

Signature
Ubaidullah Abdula
Date
31 October 2025

Lecturer’s Comments:
	Marks Awarded:	%
Marks Awarded:	%






1
1
Date
Signature
Date
Signature

Eduvos (Pty) Ltd. (formerly Pearson Institute of Higher Education) is registered with the Department of Higher Education and Training as a private higher education institution under the Higher Education Act, 101, of 1997. Registration Certificate number: 2001/HE07/008

Contents
No table of contents entries found.

Question 1
I implemented a self- I implemented a self-balancing AVL tree to store and manage book records sorted by publication year. The solution consists of three classes: q1_Book, q1_TreeNode, and q1_AVLTree. The q1_Book
class encapsulates the book’s title, author, and year. The q1_TreeNode class includes references to left and right children along with a height field to track balance. The q1_AVLTree class provides insert and delete operations with full rotation support (LL, LR, RR, RL) to maintain balance after every modification. Sample books were
inserted and one was deleted to demonstrate functionality. No console output is required, and the tree remains balanced throughout all operations.

Question 2
I extended the AVL tree from Question 1 using new q2_ prefixed classes to include additional functionality. The tree still balances on insert, but now supports four new operations. In-order traversal prints all book titles in
ascending order of publication year. Binary search efficiently determines whether a book from a given year exists. The most recent book is retrieved by accessing the rightmost node. The total number of books is calculated using recursive traversal. Multiple sample books were inserted to test all features, and the program displays clear,
formated results for traversal, search, most recent book, and total count.


Question 3
I implemented a min-heap-based priority queue to manage clinic patients according to urgency levels. The
q3_Patient class stores each patient’s name and priority (0 = most urgent, 4 = least urgent). The q3_PriorityQueue class supports enqueue and dequeue operations with proper heap maintenance. When a patient is enqueued, the heap bubbles up to preserve the min-heap property. When a patient is dequeued, the highest-priority patient is removed, the heap is restored by bubbling down, and the patient’s name is printed to the console. Four test patients were processed in correct priority order, with each dequeued name displayed as required.


Question 4
I developed a complete hotel sorting system that reads data from a JSON file and sorts it using QuickSort
implemented from first principles. The q4_Hotel class matches the JSON structure with fields for ID, name, nightly rate, stars, and distance from the airport. The q4_QuickSort class contains a full QuickSort algorithm with recursive partitioning. A single string variable, SortingMetric, controls the sorting criterion. The marker can change this value to "name", "nightly_rate", "stars", or "distance_from_airport" to sort in ascending order. The main program uses System.Text.Json to deserialize q4_data (1).json, applies QuickSort, and prints only the hotel names—one per
line—in the selected sorted order.











Reference Page
Jamro, M. (2018) C# data structures and algorithms: explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing. Available at: https://www.amazon.com/Data-Structures-Algorithms- possibilities-applications/dp/1788833732
Jamro, M. (2023) C# data structures and algorithms: harness the power of C# to build a diverse range of efficient applications. Packt Publishing. Available at: https://www.amazon.com/Data-Structures-Algorithms-efficient- applications/dp/1803248270 (Accessed: 7 November 2025).
Lewis, H.R. and Denenberg, L. (n.d.) Data structures and their algorithms. HarperCollins. Available at: https://paperguide.ai/papers/top/research-papers-data-structures-and-algorithms-pdf/
McMillan, M. (2007) Data structures and algorithms using C#. Cambridge University Press. Available at: https://www.cambridge.org/core/books/data-structures-and-algorithms-using-
c/B5BF0A10FEF6710B02F5A9C7C14B7BD2
McMillan, M. (2007) Data structures and algorithms using C#. Cambridge University Press. Available at:
https://www.cambridge.org/us/universitypress/subjects/computer-science/algorithmics-complexity-computer- algebra-and-computational-g/data-structures-and-algorithms-using-c
Reddit community (2022) How you learn data structure and algorithms in C#?, 2 May. Available at:
https://www.reddit.com/r/dotnet/comments/ugj3fl/how_you_learn_data_structure_and_algorithms_in_c/
Sharma, R. (2023) Most recommended data structure and algorithms books using C#. Dot Net Tutorials, 5 February. Available at: https://dotnettutorials.net/lesson/most-recommended-data-structure-and-algorithms- books-using-csharp/
Udemy (n.d.) Data structures and algorithms in C# (DSA). Available at: https://www.udemy.com/course/data- structures-and-algorithms-in-csharp/
UC San Diego Division of Extended Studies (n.d.) Master data structures and algorithms in C# | optimize code & prepare for programming interviews. Available at: https://extendedstudies.ucsd.edu/courses/data-structures-and- algorithms-in-c-cse-41338
Adavidoaiei, A. (2021) Fundamental data structures and algorithms in C#. DEV Community, 4 February. Available at: https://dev.to/adavidoaiei/fundamental-data-structures-and-algorithms-in-c-4ocf

CodeSignal (n.d.) Mastering algorithms and data structures in C#. Available at:
https://codesignal.com/learn/paths/mastering-algorithms-and-data-structures-in-csharp
C# Star (2017) Datastructures and algorithms in C#. Available at: https://csharpstar.com/csharp-algorithms/
