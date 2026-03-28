# Module 3: Introduction

1. Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire the skill to interpret data structures and algorithms.
	•	Implement data structures in C#.
	•	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Prescribed Reading
Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd.

   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2. Introduction
A Stack is a linear data structure that follows the Last-In, First-Out (LIFO) principle. In a stack, the last element added (pushed) is the first one to be removed (popped). You can think of it like a stack of plates in a cafeteria where the last plate placed on the top is the first one you take off.

Stack Operations:
	•	Push: Adds an element to the top of the stack.
	•	Pop: Removes and returns the top element from the stack.
	•	Peek: Returns the top element without removing it from the stack.
	•	IsEmpty: Checks whether the stack is empty or not.
	•	Clear: Clears all elements in the stack.
Stacks are typically used in scenarios where you need to reverse the order of elements or maintain the execution order, such as undo/redo operations, expression evaluation, etc.
Real-World Examples of Stacks:
	•	Undo/Redo Mechanism in Text Editors: Each action is pushed onto the stack. When an undo operation is requested, the last action is popped.
	•	Function Call Stack in Programming: The call stack stores information about the active subroutines or functions in a program. When a function is called, its context is pushed onto the stack. When it finishes execution, the context is popped off.
	•	Expression Evaluation (Postfix/Infix): Stacks are commonly used to evaluate expressions in different notations (infix, postfix).

Play Video
3. Using Stack in C#:
C# provides a built-in Stack<T> class in the System.Collections.Generic namespace that allows easy manipulation of stack elements. This class is a generic type, meaning it can hold elements of any type.
Basic Stack Operations in C#:
1.     Creating a Stack: You can create a stack by simply using the Stack<T> class.

Stack<int> stack = new Stack<int>();
2.     Push Operation: The Push method adds an element to the top of the stack.

stack.Push(10);
stack.Push(20);
stack.Push(30);
3.     Pop Operation: The Pop method removes and returns the top element from the stack.

int topElement = stack.Pop();
Console.WriteLine(/* Output */ topElement); // Output: 30
4.     Peek Operation: The Peek method returns the top element without removing it from the stack.

int topElement = stack.Peek();
Console.WriteLine(/* Output */ topElement); // Output: 20
5.     IsEmpty Operation: The IsEmpty property checks if the stack is empty.

bool isEmpty = stack.Count == 0;
Console.WriteLine(/* Output */ isEmpty); // Output: False
6.     Clear Operation: The Clear method removes all elements from the stack.

stack.Clear();
Console.WriteLine(/* Output */ stack.Count); // Output: 0

Example Code: Basic Stack Operations in C#

using System;
using System.Collections.Generic;
 
class MainProgram {
    static void Main() {
        // Create a stack of integers
        Stack<int> stack = new Stack<int>();
 
        // Push elements onto the stack
        stack.Push(10);
        stack.Push(20);
        stack.Push(30);
 
        // Peek the top element
        Console.WriteLine(/* Output */ "Top element: " + stack.Peek()); // Output: 30
 
        // Pop the top element
        Console.WriteLine(/* Output */ "Popped element: " + stack.Pop()); // Output: 30
 
        // Check if the stack is empty
        Console.WriteLine(/* Output */ "Is the stack empty? " + (stack.Count == 0 ? "Yes" : "No")); // Output: No
 
        // Pop remaining elements
        stack.Pop();
        stack.Pop();
 
        // After popping all elements, check if the stack is empty
        Console.WriteLine(/* Output */ "Is the stack empty now? " + (stack.Count == 0 ? "Yes" : "No")); // Output: Yes
    }
}
Output:

Top element: 30
Popped element: 30
Is the stack empty? No
Is the stack empty now? Yes

Advanced Use Cases of Stacks:
1. Undo/Redo Functionality:
Stacks are often used to implement undo and redo functionality. Each user action is pushed onto the stack. If the user presses "Undo," the most recent action is popped from the stack.

using System;
using System.Collections.Generic;
 
class UndoRedoSystem {
    private Stack<string> undoStack = new Stack<string>();
    private Stack<string> redoStack = new Stack<string>();
 
    public void PerformAction(string action) {
        undoStack.Push(action);
        Console.WriteLine(/* Output */ $"Action performed: {action}");
        redoStack.Clear(); // Clear redo stack after a new action
    }
 
    public void Undo() {
        if (undoStack.Count > 0) {
            string lastAction = undoStack.Pop();
            redoStack.Push(lastAction);
            Console.WriteLine(/* Output */ $"Undo: {lastAction}");
        } else {
            Console.WriteLine(/* Output */ "Nothing to undo.");
        }
    }
 
    public void Redo() {
        if (redoStack.Count > 0) {
            string lastUndoneAction = redoStack.Pop();
            undoStack.Push(lastUndoneAction);
            Console.WriteLine(/* Output */ $"Redo: {lastUndoneAction}");
        } else {
            Console.WriteLine(/* Output */ "Nothing to redo.");
        }
    }
}
 
class MainProgram {
    static void Main() {
        UndoRedoSystem system = new UndoRedoSystem();
        
        system.PerformAction("Action 1");
        system.PerformAction("Action 2");
        
        system.Undo();  // Undo Action 2
        system.Redo();  // Redo Action 2
    }
}
Expected Output:

Action performed: Action 1
Action performed: Action 2
Undo: Action 2
Redo: Action 2
2. Balanced Parentheses (Expression Validation):
Stacks can be used to check if parentheses in an expression are balanced. A balanced expression means that every opening parenthesis has a corresponding closing parenthesis.

using System;
using System.Collections.Generic;
 
class MainProgram {
    static bool IsBalanced(string expression) {
        Stack<char> stack = new Stack<char>();
 
        foreach (char ch in expression) {
            if (ch == '(') {
                stack.Push(ch); // Push opening parentheses onto stack
            } else if (ch == ')') {
                if (stack.Count == 0 || stack.Pop() != '(') {
                    return false; // Unmatched closing parentheses
                }
            }
        }
        return stack.Count == 0; // Stack should be empty if balanced
    }
 
    static void Main() {
        string expression = "(a + b) * (c + d)";
        Console.WriteLine(/* Output */ $"Is the expression '{expression}' balanced? {IsBalanced(expression)}");
    }
}
Expected Output:
Is the expression '(a + b) * (c + d)' balanced? True

4. Advantages of Using Stacks:
	•	LIFO Access: Allows processing of elements in reverse order.
	•	Memory Efficiency: Stack elements are managed using memory that is dynamically allocated.
	•	Simple Operations: Stack operations are very simple to implement and are typically constant-time operations (O(1)).
	•	Reversing Data: Stacks can be used to reverse data efficiently, such as in string reversal or expression evaluation.
 
5. Disadvantages of Using Stacks:
	•	Limited Access: You can only access the top element of the stack at a given time. This is restrictive compared to other data structures like arrays or lists, where you can access any element.
	•	Fixed Size (if implemented with an array): If a stack is implemented using an array, the size may be fixed, and you'd need to resize the array when it exceeds capacity.
 
6. Case Study 1
Problem:
You are developing a simple text editor and need to implement an Undo/Redo functionality. Each time the user types something, the editor should push the action onto a stack. The user should be able to undo and redo actions. The stack will help you manage the history of text changes.
Solution:
To implement this feature, we need two stacks:
	•	Undo Stack to store actions that can be undone.
	•	Redo Stack to store undone actions that can be redone.
When the user types, the action is pushed onto the undo stack. If the user clicks "Undo", the most recent action is popped from the undo stack and pushed onto the redo stack. If the user clicks "Redo", the action is popped from the redo stack and pushed back onto the undo stack.

using System;
using System.Collections.Generic;
 
class TextEditor {
    private Stack<string> undoStack = new Stack<string>();
    private Stack<string> redoStack = new Stack<string>();
 
    public void PerformAction(string action) {
        undoStack.Push(action);
        Console.WriteLine(/* Output */ $"Action performed: {action}");
        redoStack.Clear(); // Clear redo stack after new action
    }
 
    public void Undo() {
        if (undoStack.Count > 0) {
            string lastAction = undoStack.Pop();
            redoStack.Push(lastAction);
            Console.WriteLine(/* Output */ $"Undo: {lastAction}");
        } else {
            Console.WriteLine(/* Output */ "Nothing to undo.");
        }
    }
 
    public void Redo() {
        if (redoStack.Count > 0) {
            string lastUndoneAction = redoStack.Pop();
            undoStack.Push(lastUndoneAction);
            Console.WriteLine(/* Output */ $"Redo: {lastUndoneAction}");
        } else {
            Console.WriteLine(/* Output */ "Nothing to redo.");
        }
    }
}
 
class MainProgram {
    static void Main() {
        TextEditor editor = new TextEditor();
 
        // Perform actions
        editor.PerformAction("Typed 'Hello'");
        editor.PerformAction("Typed 'World'");
        editor.PerformAction("Typed '!'");
 
        // Undo actions
        editor.Undo(); // Undo '!'
        editor.Undo(); // Undo 'World'
 
        // Redo actions
        editor.Redo(); // Redo 'World'
        editor.Redo(); // Redo '!'
    }
}
Expected Output:

Action performed: Typed 'Hello'
Action performed: Typed 'World'
Action performed: Typed '!'
Undo: Typed '!'
Undo: Typed 'World'
Redo: Typed 'World'
Redo: Typed '!'

 
7. Case Study 2
Problem:
You are tasked with validating mathematical expressions to check if the parentheses are balanced. The expression might contain parentheses like (), {}, and []. You need to ensure that every opening parenthesis has a corresponding closing parenthesis in the correct order.
Solution:
The stack data structure can help efficiently solve this problem. As we encounter an opening parenthesis, we push it onto the stack. When we encounter a closing parenthesis, we pop the stack and check if the top element matches the corresponding opening parenthesis. If it does, the parentheses are balanced for that pair. If not, the expression is unbalanced.

using System;
using System.Collections.Generic;
 
class ParenthesesValidator {
    public bool IsBalanced(string expression) {
        Stack<char> stack = new Stack<char>();
 
        foreach (char ch in expression) {
            if (ch == '(' || ch == '{' || ch == '[') {
                stack.Push(ch); // Push opening parentheses onto stack
            } else if (ch == ')' || ch == '}' || ch == ']') {
                if (stack.Count == 0) {
                    return false; // No matching opening parenthesis
                }
                char top = stack.Pop();
                if (!Matches(top, ch)) {
                    return false; // Mismatched parentheses
                }
            }
        }
        return stack.Count == 0; // Stack should be empty if balanced
    }
 
    private bool Matches(char open, char close) {
        return (open == '(' && close == ')') || 
               (open == '{' && close == '}') || 
               (open == '[' && close == ']');
    }
}
 
class MainProgram {
    static void Main() {
        ParenthesesValidator validator = new ParenthesesValidator();
 
        string expression1 = "(a + b) * (c + d)";
        string expression2 = "{[a + b] * (c + d}";
        string expression3 = "[(a + b) * {c + d}]";
 
        Console.WriteLine(/* Output */ $"Is the expression '{expression1}' balanced? {validator.IsBalanced(expression1)}");
        Console.WriteLine(/* Output */ $"Is the expression '{expression2}' balanced? {validator.IsBalanced(expression2)}");
        Console.WriteLine(/* Output */ $"Is the expression '{expression3}' balanced? {validator.IsBalanced(expression3)}");
    }
}
Expected Output:

Is the expression '(a + b) * (c + d)' balanced? True
Is the expression '{[a + b] * (c + d}' balanced? False
Is the expression '[(a + b) * {c + d}]' balanced? True

 
8. Case Study 3
Problem:
You are developing a simple browser navigation system where a user can visit multiple web pages. The user should be able to navigate back to the previous pages using a back button. Implementing this feature using a Stack will allow efficient tracking of the visited pages and navigation backward.
Solution:
We can use a stack to keep track of the history of visited pages. Every time a new page is visited, the page URL is pushed onto the stack. When the back button is clicked, the most recent page URL is popped from the stack and displayed.

using System;
using System.Collections.Generic;
 
class BrowserHistory {
    private Stack<string> historyStack = new Stack<string>();
    private string currentPage;
 
    public void VisitPage(string url) {
        if (currentPage != null) {
            historyStack.Push(currentPage); // Push current page to history stack before visiting a new page
        }
        currentPage = url;
        Console.WriteLine(/* Output */ $"Visited: {url}");
    }
 
    public void GoBack() {
        if (historyStack.Count > 0) {
            currentPage = historyStack.Pop(); // Pop the most recent page
            Console.WriteLine(/* Output */ $"Back to: {currentPage}");
        } else {
            Console.WriteLine(/* Output */ "No pages in history.");
        }
    }
}
 
class MainProgram {
    static void Main() {
        BrowserHistory browser = new BrowserHistory();
 
        // Simulate visiting pages
        browser.VisitPage("www.google.com");
        browser.VisitPage("www.facebook.com");
        browser.VisitPage("www.github.com");
 
        // Simulate going back
        browser.GoBack(); // Go back to www.facebook.com
        browser.GoBack(); // Go back to www.google.com
        browser.GoBack(); // No pages in history
    }
}
Expected Output:

Visited: www.google.com
Visited: www.facebook.com
Visited: www.github.com
Back to: www.facebook.com
Back to: www.google.com
No pages in history.

Summary:
	•	Undo/Redo Functionality: A text editor's undo/redo feature can be efficiently implemented using two stacks: one for undo actions and another for redo actions.
	•	Balanced Parentheses Check: Stacks help efficiently validate whether a string has balanced parentheses by matching opening and closing parentheses as they are encountered.
	•	Browser History Navigation: The stack is used to store visited pages, and the user can navigate back by popping pages from the stack.
Each of these case studies illustrates a practical use of stacks in solving real-world problems, showcasing their versatility and importance in various applications.
 
9. Conclusion
Stacks are an essential data structure in programming, with many real-world applications such as undo/redo functionality, expression evaluation, and maintaining function calls in the program. In C#, you can use the built-in Stack<T> class to efficiently manage stack operations. Understanding stacks and their use cases will help in solving problems that involve managing ordered data in a LIFO manner.
10. Activity
Create a stack in C# that will mimic the browser forward and backward functionality. Each tab will be represented by a string.


	•	2. Introduction to Queues
	•	3. Implementing Queues in C#
	•	4. Types of Queues in C#
	•	5. Practical Use Cases of Queues
	•	6. Case study 1
	•	7. Case study 2
	•	9. Activity
