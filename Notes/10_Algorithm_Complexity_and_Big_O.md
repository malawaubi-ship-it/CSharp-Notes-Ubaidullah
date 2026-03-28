# Module 10: Relevance Connection

## 1. Learning outcomes
 
By the end of this topic you should be able to:
	-	Acquire the skill to interpret data structures and algorithms.
	-	Implement data structures in C#.
	-	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Jamro, M., (2018). Arrays and Lists, C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd, p48-p60



## 2. Relevance Connection
We will continue investigating sorting, We have looked at 2 types of sorting, research at least 3 more types of sorting.
## 3. Bubble Sort
The sorting algorithm was published in 1956 by Edward Harry Friend[1]. Due to its inefficiency, it is not in common use in real world scenarios, however, as it is a very simple algorithm, it is used in educational contexts.
 
In the algorithm, a “bubble” consists of 2 adjacent elements. If the elements in the bubble are in the incorrect order relative to each other, they are swapped. If they are in the correct order, their order is maintained. The bubble then steps 1 element forward and the algorithm is repeated. The algorithm will stop when the iteration counter reaches  However, an improvement can be made to the algorithm to stop when no swaps are made in an iteration, as this implies that the array is sorted.
 
Its best-case time complexity is . This occurs when the list is already sorted.
Its average and worst-case time complexity is . The worst-case scenario occurs when the array is in reverse order.
 
As Bubble Sort is an in-place iterative sorting algorithm, its worst-case space complexity is 
.
Another advantage of the algorithm is that it is stable.
 
Virginia Tech has a useful visualisation tool for Bubble Sort[2].



[1] Friend, E.H. (1956) 'Sorting on electronic computer systems,' Journal of the ACM, 3(3), pp. 134–168. https://doi.org/10.1145/320831.320833.
[2] Bubble Sort Visualization (2024). https://opendsa-server.cs.vt.edu/embed/bubblesortAV.
## 4. Quicksort
This sorting algorithm was published in 1961 by Tony Hoare[1], and is in common use today as it is efficient.
It follows the divide and conquer paradigm. A pivot element is selected in the array. Elements are then partitioned into two subarrays depending on whether they are greater than or less than the pivot. The subarrays are then sorted recursively.
 
It’s best and average case time complexity is . The best-case scenario occurs when the subarrays are equal in length in each recursive call (when the pivots are the median value).
its worst -case time complexity is This occurs when a subarray is size  in length in each recursive call (when the pivots are either the smallest or largest value).
 
An advantage to this type of sorting is that is can be done in place. It has a worst-case space complexity of , due to stack space requirement of the recursive calls made by the algorithm.
 
A disadvantage of Quicksort is that it is not stable.
 
Virginia Tech has a useful visualisation tool for Quicksort[2].



[1] Hoare, C. a. R. (1961) 'Algorithm 64: Quicksort,' Communications of the ACM, 4(7), p. 321. https://doi.org/10.1145/366622.366644.
[2] Quicksort Visualization (2024). https://opendsa-server.cs.vt.edu/embed/quicksortAV.


	-	2. Exploring Graphs
	-	3. Search Algorithms
