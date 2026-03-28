# Module 9: Relevance Connection

1. Learning outcomes
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). Arrays and Lists, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p48-p60
  
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Relevance Connection
Find 5 examples of when sorting data structures is required.
3. Sorting
Sorting is a method of arranging a list or array in a specific order, either ascending or descending. There are many different types of sorting algorithms, that work in different ways, which gives characteristics that may be beneficial or even negative in certain circumstances.
 
Time complexity is an important description of algorithms that describes the amount of time taken by an algorithm, by focusing on the number of operations required, that is independent of computer hardware. Sorting algorithms are often compared to each other using their time complexity.
 
Space complexity describes the amount of space required by an algorithm. The space complexity, in particular, mentioned here describes auxiliary space, i.e. additional space required by the sorting algorithm, excluding the array itself. This is an important descriptor when a sorting algorithm is required for a space constrain environment.
 
Sorting stability describes how a sorting algorithm will treat elements that are equal in value. A stable algorithm will maintain the order of equal items, relative to each other. An unstable algorithm is not guaranteed to maintain the order of equal items relative to each other.
3.1. Selection Sort
Selection Sort has been known long before the invention of modern computers and cannot be attributed to a single inventor. However, computer scientists have developed many variants over time. Heapsort is a popular example invented by JWJ Williams in 1964[1]. In the same paper, he also proposed the heap data structure, which we looked at last week.
 
In Selection Sort, the array can be categorised into 2 parts: sorted and unsorted. In each iteration, the smallest element (for ascending order) or largest element (for descending order) in the unsorted part is found and this element is then swapped with the leftmost unsorted element in the array.
 
The algorithm has a best-case, average-case and worst-case time complexity of .
 
Sorting can be done in-place, therefore the worst-case space complexity is .
 
Selection sort is not stable.
 
Virginia Tech has a useful visualisation tool for Selection Sort[2].
 

[1] Williams, J. (1964) 'Algorithm 232 : HEAPSORT,' Communications of the ACM, 7, pp. 347–348. https://ci.nii.ac.jp/naid/10010193304.
[2] Selection sort visualization (2024). https://opendsa-server.cs.vt.edu/embed/selectionsortAV.
3.2. Insertion Sort
Insertion sort predates modern computers and been in use in non-computer scenarios for a long time. However, many optimisations have been made by computer scientists. A popular example is a variant of Insertion Sort, called Shell Sort, developed by Donald Shell in 1959[1].
 
In Insertion Sort, the array can be categorised into 2 parts: sorted and unsorted. In each iteration, the algorithm will find a suitable position of an element, relative to elements already in the sorted section of the array.
 
Its best-case time complexity is . This occurs when the list is already sorted.
 
Its average and worst-case time complexity is . The worst-case scenario occurs when the array is in reverse order.
 
Sorting can be done in-place iteratively, therefore, Insertion Sort has a worst-case space complexity of .
 
Insertion Sort is also stable.
 
Virginia Tech has a useful visualisation tool for Insertion Sort[2].
 

[1] Shell, D.L. (1959) 'A high-speed sorting procedure,' Communications of the ACM, 2(7), pp. 30–32. https://doi.org/10.1145/368370.368387.
[2] Insertion sort visualization (2024). https://opendsa-server.cs.vt.edu/OpenDSA/AV/Sorting/insertionsortAV.html.


10.1. Notes
10.1. Notes
	•	2. Relevance Connection
	•	3. Bubble Sort
	•	4. Quicksort
