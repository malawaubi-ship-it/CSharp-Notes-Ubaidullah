# Module 13: Collaborative Project   Case Study   Relevance Connection

1. Learning outcomes

By the end of this topic you should be able to:
you will explore strings, strings operations, operations for manipulating strings, strings concatenation, switching to uppercase and lowercase letters, searching for a string within another string, extracting a portion of a string, splitting the string by a separator, replacing a substring, and regular expressions.
 

Prescribed Reading
Introduction to Programming with C# / Java Books » Chapter 13. Strings and Text Processing (introprogramming.info).
Time Allocation:
4 Hours
 
2. Collaborative Project / Case Study / Relevance Connection:

A string is an object of type String whose value is text. Internally, the text is stored as a sequential read-only collection of Char objects. There's no null-terminating character at the end of a C# string; therefore a C# string can contain any number of embedded null characters ('\0'). The Length property of a string represents the number of Char objects it contains, not the number of Unicode characters. To access the individual Unicode code points in a string, use the StringInfo object.
In C#, string is an object of System.String class that represent sequence of characters. We can perform many operations on strings such as concatenation, comparision, getting substring, search, trim, replacement etc. 
3. Creating String Object

Creating a String Object
You can create string object using one of the following methods −
	•	By assigning a string literal to a String variable
	•	By using a String class constructor
	•	By using the string concatenation operator (+)
	•	By retrieving a property or calling a method that returns a string
	•	By calling a formatting method to convert a value or an object to its string representation
3.1. Notes
ITPCA2 (First Block)
3.1. Notes
	•	1.3 Our First C# Program
	•	1.3.1 How Does Our First C# Program Work?
	•	1.3.2 Keywords
	•	1.4 Datatypes and Operators
	•	1.4.1 Datatypes
	•	1.4.1.1 Integer Types
	•	1.4.1.2 Real Floating-Point Types
	•	1.4.1.3 Boolean Type
	•	1.4.1.4 Character Type
	•	1.4.1.5 String Type
	•	1.4.1.6 Object Type
	•	1.4.2 Operators
	•	1.4.2.1 Arithmetic Operators
	•	1.4.2.2 Assignment Operators
	•	1.4.2.3 Comparison Operators
	•	1.4.2.4 Logical Operators
	•	1.4.2.5 Bitwise Operators
	•	1.4.2.6 Type Conversion
Learning outcomes
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 1, 2 & 3
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
1.3 Our First C# Program
Before we continue with an in-depth description of the C# language and the .NET platform, let’s take a look at a simple example, illustrating how a program written in C# looks like:
 
Code Example
class HelloCSharp 
{ 
static void Main(string[] args) 
{ 
System.Console.WriteLine(/* Output */ "Hello C#!");
 } 
 
 
The only thing this program does is to print the message "Hello, C#!" on the default output. It is still early to execute it, which is why we will only take a look at its structure. Later we will describe in full how to compile and run a given program from the command prompt as well as from a development environment. 
1.3.1 How Does Our First C# Program Work?
Our first program consists of three logical parts:
	•	Definition of a class HelloCSharp;
	•	Definition of a method Main();
	•	Contents of the method Main().
Defining a Class 
On the first line of our program we define a class called HelloCSharp. The simplest definition of a class consists of the keyword class, followed by its name. In our case the name of the class is HelloCSharp. The content of the class is located in a block of program lines, surrounded by curly brackets: {}. 
Defining the Main() Method 
On the third line we define a method with the name Main(), which is the starting point for our program. Every program written in C# starts from a Main() method with the following title (signature):
static void Main(string[] args) 
The method must be declared as shown above, it must be static and void, it must have a name Main and as a list of parameters it must have only one parameter of type array of string. In our example the parameter is called args but that is not mandatory. This parameter is not used in most cases so it can be omitted (it is optional). In that case the entry point of the program can be simplified and will look like this:
static void Main() 
If any of the aforementioned requirements is not met, the program will compile but it will not start because the starting point is not defined correctly. 
Contents of the Main() Method 
The content of every method is found after its signature, surrounded by opening and closing curly brackets. On the next line of our sample program we use the system object System.Console and its method WriteLine() to print a message on the default output (the console), in this case "Hello, C#!". 
In the Main() method we can write a random sequence of expressions and they will be executed in the order we assigned to them.
1.3.2 Keywords
C# uses the following keywords to build its programming constructs: 
abstract
as
base
bool
break
byte
case
catch
char
checked
class
const
continue
decimal
default
delegate
do
double
else
enum
event
explicit
extern
false
finally
fixed
float
for
foreach
goto
if
implicit
in
int
interface
internal
is
lock
long
namespace
new
null
object
operator
out
override
params
private
protected
public
readonly
ref
return
sbyte
sealed
short
sizeof
stackalloc
static
string
struct
switch
this
throw
true
try
typeof
uint
ulong
unchecked
unsafe
ushort
using
virtual
void
volatile
while
 
 
Since the creation of the first version of the C# language, not all keywords are in use. Some of them were added in later versions. The main program elements in C# (which are defined and used with the help of keywords) are classes, methods, operators, expressions, conditional statements, loops, data types, exceptions and few others. In the next few chapters of this book, we will review in details all these programming constructs along with the use of the most of the keywords from the table above
1.4 Datatypes and Operators
In this section we will discuss the various datatypes and operators in C#.  We will familiarize what they are and how to work with them. First we will consider the data types – integer types, real types with floating-point, Boolean, character, string, and object type. We will continue with the variables, with their characteristics, how to declare them, how they are assigned a value and what a variable initialization is.  Finally, we will get acquainted with the operators in C# and the actions they can perform when used with the different data types.
1.4.1 Datatypes
Data types are sets (ranges) of values that have similar characteristics. For instance byte type specifies the set of integers in the range of [0 … 255]. Data types are characterized by Name (for example, int), Size (how much memory they use)- for example, 4 bytes, and Default value (for example 0). 
Basic data types in C# are distributed into the following types:
-       Integer types – sbyte, byte, short, ushort, int, uint, long, ulong;
-       Real floating-point types – float, double;
-       Real type with decimal precision – decimal;
-       Boolean type – bool;
-       Character type – char;
-       String – string;
-       Object type – object. 
These data types are called primitive (built-in types), because they are embedded in C# language at the lowest level. We now discuss each of the primitive datatypes.
1.4.1.1 Integer Types
Integer types represent integer numArray and are sbyte, byte, short, ushort, int, uint, long and ulong. Let’s examine them one by one. 
 
The sbyte type is an 8-bit signed integer. This means that the number of possible values for it is 28, i.e. 256 values altogether, and they can be both, positive and negative. The minimum value that can be stored in sbyte is SByte.MinValue = -128 (-27), and the maximum value is SByte.MaxValue = 127 (27-1). The default value is the number 0. 
 
The byte type is an 8-bit unsigned integer type. It also has 256 different integer values (28) that can only be nonnegative. Its default value is the number 0. The minimal taken value is Byte.MinValue = 0, and the maximum is Byte.MaxValue = 255 (28-1). 
 
The short type is a 16-bit signed integer. Its minimal value is Int16.MinValue = -32768 (-215), and the maximum is Int16.MaxValue = 32767 (215-1). The default value for short type is the number 0. 
 
The ushort type is 16-bit unsigned integer. The minimum value that it can store is UInt16.MinValue = 0, and the minimum value is – UInt16.MaxValue = 65535 (216-1). Its default value is the number 0. 
 
The next integer type that we will consider is int. It is a 32-bit signed integer. As we can notice, the growth of bits increases the possible values that a type can store. The default value for int is 0. Its minimal value is Int32.MinValue = -2,147,483,648 (-231), and its maximum value is Int32.MaxValue = 2,147,483,647 (231-1).
 
The int type is the most often used type in programming. Usually programmers use int when they work with integers because this type is natural for the 32-bit microprocessor and is sufficiently "big" for most of the calculations performed in everyday life. 
 
The uint type is 32-bit unsigned integer type. Its default value is the number 0u or 0U (the two are equivalent). The 'u' letter indicates that the number is of type uint (otherwise it is understood as int). The minimum value that it can take is UInt32.MinValue = 0, and the maximum value is UInt32.MaxValue = 4,294,967,295 (232-1).
The long type is a 64-bit signed type with a default value of 0l or 0L (the two are equivalent but it is preferable to use 'L' because the letter 'l' is easily mistaken for the digit one '1'). The 'L' letter indicates that the number is of type long (otherwise it is understood int). The minimal value that can be stored in the long type is Int64.MinValue = -9,223,372,036,854,775,808 (-263) and its maximum value is Int64.MaxValue = 9,223,372,036,854, 775,807 (263-1). 
 
The biggest integer type is the ulong type. It is a 64-bit unsigned type, which has as a default value – the number 0u, or 0U (the two are equivalent). The suffix 'u' indicates that the number is of type ulong (otherwise it is understood as long). The minimum value that can be recorded in the ulong type is UInt64.MinValue = 0 and the maximum is UInt64.MaxValue = 18,446,744,073,709,551,615 (264-1).
 
Integer Types – Example 
 
Consider an example in which we declare several variables of the integer types we know, we initialize them and print their values to the console:
Code Example
// Declare some variables 
byte centuries = 20; 
ushort years = 2000; 
uint days = 730480; 
ulong hours = 17531520; 
// Print the result on the console 
Console.WriteLine(/* Output */ centuries + " centuries are " + years + 
" years, or " + days + " days, or " + hours + " hours."); 
 
// Console output: 
// 20 centuries are 2000 years, or 730480 days, or 17531520 
// hours. 
ulong maxIntValue = UInt64.MaxValue; 
Console.WriteLine(/* Output */ maxIntValue); // 18446744073709551615 
 
1.4.1.2 Real Floating-Point Types
Real types in C# are the real numArray we know from mathematics. They are represented by a floating-point according to the standard IEEE 754 and are float and double. Let’s consider in details these two data types and understand what their similarities and differences are. 
Real Type Float 
The first type we will consider is the 32-bit real floating-point type float. It is also known as a single precision real number. Its default value is 0.0f or 0.0F (both are equivalent). The character 'f' when put at the end explicitly indicates that the number is of type float (because by default all real numArray are considered double). More about this special suffix we can read bellow in the "Real Literals" section. The considered type has accuracy up to seven decimal places (the others are lost). For instance, if the number 0.123456789 is stored as type float it will be rounded to 0.1234568. The range of values, which can be included in a float type (rounded with accuracy of 7 significant decimal digits), range from ±1.5 × 10-45 to ±3.4 × 1038. 
 
Special Values of the Real Types 
The real data types have also several special values that are not real numArray but are mathematical abstractions: 
- Negative infinity -∞ (Single.NegativeInfinity). It is obtained when for instance we are dividing -1.0f by 0.0f. 
- Positive infinity +∞ (Single.PositiveInfinity). It is obtained when for instance we are dividing 1.0f by 0.0f. 
- Uncertainty (Single.NaN) – means that an invalid operation is performed on real numArray. It is obtained when for example we divide 0.0f by 0.0f, as well as when calculating square root of a negative number. 
 
Real Type Double 
The second real floating-point type in the C# language is the double type. It is also called double precision real number and is a 64-bit type with a default value of 0.0d and 0.0D (the suffix 'd' is not mandatory because by default all real numArray in C# are of type double). This type has precision of 15 to 16 decimal digits. The range of values, which can be recorded in double (rounded with precision of 15-16 significant decimal digits), is from ±5.0 × 10-324 to ±1.7 × 10308. 
 
The smallest real value of type double is the constant Double.MinValue = -1.79769e+308 and the largest is Double.MaxValue = 1.79769e+308. The closest to 0 positive number of type double is Double.Epsilon = 4.94066e-324. As with the type float the variables of type double can take the special values: Double.PositiveInfinity (+∞), Double.NegativeInfinity (-∞) and Double.NaN (invalid number). 
Real Floating-Point Types – Example 
Here is an example in which we declare variables of real number types, assign values to them and print them: 
Code Example
float floatPI = 3.14f; 
Console.WriteLine(/* Output */ floatPI); // 3.14 
double doublePI = 3.14; 
Console.WriteLine(/* Output */ doublePI); // 3.14 
double nan = Double.NaN; 
Console.WriteLine(/* Output */ nan); // NaN 
double infinity = Double.PositiveInfinity; 
Console.WriteLine(/* Output */ infinity); // Infinity 
 
1.4.1.3 Boolean Type
Boolean type is declared with the keyword bool. It has two possible values: true and false. Its default value is false. It is used most often to store the calculation result of logical expressions.
Code Example
// Declare some variables 
 
int a = 1; 
int b = 2; 
// Which one is greater? 
bool greaterAB = (a > b); 
// Is 'a' equal to 1? 
bool equalA1 = (a == 1); 
// Print the results on the console 
if (greaterAB) 
{ 
Console.WriteLine(/* Output */ "A > B"); 
} 
else 
{ 
Console.WriteLine(/* Output */ "A <= B"); 
} 
Console.WriteLine(/* Output */ "greaterAB = " + greaterAB); 
Console.WriteLine(/* Output */ "equalA1 = " + equalA1); 
// Console output: 
// A <= B 
// greaterAB = False 
// equalA1 = True  

 
In the example above, we declare two variables of type int, compare them and assign the result to the bool variable greaterAB. Similarly, we do the same for the variable equalA1. If the variable greaterAB is true, then A > B is printed on the console, otherwise A <= B is printed.
1.4.1.4 Character Type
Character type is a single character (16-bit number of a Unicode table character). It is declared in C# with the keyword char. The Unicode table is a technological standard that represents any character (letter, punctuation, etc.) from all human languages as writing systems (all languages and alphabets) with an integer or a sequence of integersThe smallest possible value of a char variable is 0, and the largest one is 65535. The values of type char are letters or other characters, and are enclosed in apostrophes. 
 
Character Type – Example 
Consider an example in which we declare one variable of type char, initialize it with value 'a', then 'b', then 'A' and print the Unicode values of these letters to the console:
Code Example
// Declare a variable 
char ch = 'a'; 
// Print the results on the console 
Console.WriteLine(/* Output */  
"The code of '" + ch + "' is: " + (int)ch); 
ch = 'b'; 
Console.WriteLine(/* Output */  
"The code of '" + ch + "' is: " + (int)ch); 
ch = 'A'; 
Console.WriteLine(/* Output */  
"The code of '" + ch + "' is: " + (int)ch); 
// Console output: 
// The code of 'a' is: 97 
// The code of 'b' is: 98 
// The code of 'A' is: 65
 

1.4.1.5 String Type
Strings are sequences of characters. In C# they are declared by the keyword string. Their default value is null. Strings are enclosed in quotation marks. Various text-processing operations can be performed using strings: concatenation (joining one string with another), splitting by a given separator, searching, replacement of characters and others. 
 
Strings – Example 
Consider an example in which we declare several variables of type string, initialize them and print their values on the console: 
Code Example
// Declare some variables 
string firstName = "John"; 
string lastName = "Smith"; 
string fullName = firstName + " " + lastName; 
// Print the results on the console 
Console.WriteLine(/* Output */ "Hello, " + firstName + "!"); 
Console.WriteLine(/* Output */ "Your full name is " + fullName + "."); 
// Console output: 
// Hello, John! 
// Your full name is John Smith.  
 

1.4.1.6 Object Type
Object type is a special type, which is the parent of all other types in the .NET Framework. Declared with the keyword object, it can take values from any other type. It is a reference type, i.e. an index (address) of a memory area which stores the actual value. 
 
Using Objects – Example 
Consider an example in which we declare several variables of type object, initialize them and print their values on the console:
 
Code Example
int i = 5; 
int? ni = i; 
Console.WriteLine(/* Output */ ni); // 5 
// i = ni; // this will fail to compile 
Console.WriteLine(/* Output */ ni.HasValue); // True 
i = ni.Value; 
Console.WriteLine(/* Output */ idx); // 5 
ni = null; 
Console.WriteLine(/* Output */ ni.HasValue); // False 
//i = ni.Value; // System.InvalidOperationException 
i = ni.GetValueOrDefault(); 
Console.WriteLine(/* Output */ idx); // 0 
 
As you can see from the example, we can store the value of any other type in an object type variable. This makes the object type a universal data container.
1.4.2 Operators
Every programming language uses operators, through which we can perform different actions on the data.
Operators in C# can be separated in several different categories: 
- Arithmetic operators – they are used to perform simple mathematical operations.
-Assignment operators – allow assigning values to variables.
- Comparison operators – allow comparison of two literals and/or variables.
- Logical operators – operators that work with Boolean data types and Boolean expressions.
- Binary operators – used to perform operations on the binary representation of numerical data.
- Type conversion operators – allow conversion of data from one type to another. 
Below is a list of the operators, separated into categories: 
Category 
Operators 
arithmetic
-, +, *, /, %, ++, -- 
logical
&&, ||, !, ^ 
binary
&, |, ^, ~, <<, >> 
comparison
==,!=, >, <, >=, <= 
assignment
=, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>= 
string concatenation
+ 
type conversion
(type), as, is, typeof, sizeof 
other
., new, (), [], ?:, ?? 
 
Some operators have precedence (priority) over others. For example, in math multiplication has precedence over addition. The operators with a higher precedence are calculated before those with lower. The operator () is used to change the precedence and like in math, it is calculated first.
 
The following table illustrates the precedence of the operators in C#:
Priority 
Operators 
Highest priority
 
(, ) 

++, -- (as postfix), new, (type), typeof, sizeof 

++, -- (as prefix), +, - (unary), !, ~ 

*, /, % 

+ (string concatenation) 

+, - 

<<, >> 

<, >, <=, >=, is, as 

==, != 

&, ^, | 

&& 

|| 

?:, ?? 

=, *=, /=, %=, +=, -=, <<=, >>=, &=, ^=, |= 
 
The operators located upper in the table have higher precedence than those below them, and respectively they have an advantage in the calculation of an expression. To change the precedence of an operator we can use brackets. When we write expressions that are more complex or have many operators, it is recommended to use brackets to avoid difficulties in reading and understanding the code.
1.4.2.1 Arithmetic Operators
The arithmetic operators in C# +, -, * are the same like the ones in math. They perform addition, subtraction and multiplication on numerical values and the result is also a numerical value. The division operator / has different effect on integer and real numArray. When we divide an integer by an integer (like int, long and sbyte) the returned value is an integer (no rounding, the fractional part is cut). Such division is called an integer division. Example of integer division: 7 / 3 = 2. 
 
Integer division by 0 is not allowed and causes a runtime exception DivideByZeroException. The remainder of integer division of integers can be obtained by the operator %. For example, 7 % 3 = 1, and –10 % 2 = 0. When dividing two real numArray or two numArray, one of which is real (e.g. float, double, etc.), a real division is done (not integer), and the result is a real number with a whole and a fractional part. For example: 5.0 / 2 = 2.5. In the division of real numArray it is allowed to divide by 0.0 and respectively the result is +∞ (Infinity), -∞ (-Infinity) or NaN (invalid value).  Here are some examples of arithmetic operators and their effect:
 
Code Example
int squarePerimeter = 17; 
double squareSide = squarePerimeter / 4.0; 
double squareArea = squareSide * squareSide; 
Console.WriteLine(/* Output */ squareSide); // 4.25 
Console.WriteLine(/* Output */ squareArea); // 18.0625
 
int a = 5; 
int b = 4; 
Console.WriteLine(/* Output */ a + b); // 9 
Console.WriteLine(/* Output */ a + (b++)); // 9 
Console.WriteLine(/* Output */ a + b); // 10 
Console.WriteLine(/* Output */ a + (++b)); // 11 
Console.WriteLine(/* Output */ a + b); // 11 
Console.WriteLine(/* Output */ 14 / a); // 2 
Console.WriteLine(/* Output */ 14 % a); // 4 
int one = 1; 
int zero = 0; 
 
// Console.WriteLine(/* Output */ one / zero); // DivideByZeroException 
double dMinusOne = -1.0; 
double dZero = 0.0; 
Console.WriteLine(/* Output */ dMinusOne / zero); // -Infinity 
Console.WriteLine(/* Output */ one / dZero); // Infinity 
1.4.2.2 Assignment Operators
The operator for assigning value to a variable is "=" (the character for mathematical equation). The syntax used for assigning value is as it follows:
operand1 = literal, expression or operand2; 
Here is an example to show the usage of the assignment operator: 
int x = 6;
string helloString = "Hello string.";
int y = x;
 In the example we assign value 6 to the variable x. On the second line we assign a text literal to the variable helloString, and on the third line we copy the value of the variable x to the variable y. The assignment operator can be used in cascade (more than once in the same expression). In this case assignments are carried out consecutively from right to left. Here’s an example:
int x, y, z;
x = y = z = 25; 
 On the first line in the example we initialize three variables and on the second line we assign them the value 25. 
The assignment operator in C# is "=", while the comparison operator is "==". The exchange of the two operators is a common error when we are writing code. Be careful not to confuse the comparison operator and the assignment operator as they look very similar. 
1.4.2.3 Comparison Operators
Comparison operators in C# are used to compare two or more operands. C# supports the following comparison operators: 
- greater than (>) 
- less than (<) 
- greater than or equal to (>=) 
- less than or equal to (<=) 
- equality (==) 
- difference (!=) 
 
All comparison operators in C# are binary (take two operands) and the returned result is a Boolean value (true or false). Comparison operators have lower priority than arithmetical operators but higher than the assignment operators. The following example demonstrates the usage of comparison operators in C#:
Code Example
int x = 10, y = 5; 
Console.WriteLine(/* Output */ "x > y : " + (x > y)); // True 
Console.WriteLine(/* Output */ "x < y : " + (x < y)); // False 
Console.WriteLine(/* Output */ "x >= y : " + (x >= y)); // True 
Console.WriteLine(/* Output */ "x <= y : " + (x <= y)); // False 
Console.WriteLine(/* Output */ "x == y : " + (x == y)); // False 
Console.WriteLine(/* Output */ "x != y : " + (x != y)); // True 
 
 
In the example, first we create two variables x and y and we assign them the values 10 and 5. On the next line we print on the console using the method Console.WriteLine(/* Output */ …) the result from comparing the two variables x and y using the operator >. The returned value is true because x has a greater value than y. Similarly, in the next rows the results from the other 5 comparison operators, used to compare the variables x and y, are printed.
1.4.2.4 Logical Operators
Logical (Boolean) operators take Boolean values and return a Boolean result (true or false). The basic Boolean operators are "AND" (&&), "OR" (||), "exclusive OR" (^) and logical negation (!). 
 
The following table contains the logical operators in C# and the operations that they perform:
x 
y 
!x 
x && y 
x || y 
x ^ y 
true 
true 
false 
true 
true 
false 
true 
false 
false 
false 
true 
true 
false 
true 
true 
false 
true 
true 
false 
false 
true 
false 
false 
false 
Source: Nakov et al (2013)
 
The table and the following example show that the logical "AND" (&&) returns true only when both variables contain truth. Logical "OR" (||) returns true when at least one of the operands is true. The logical negation operator (!) changes the value of the argument. For example, if the operand has a value true and a negation operator is applied, the new value will be false. The negation operator is a unary operator and it is placed before the argument. Exclusive "OR" (^) returns true if only one of the two operands has the value true. If the two operands have different values, exclusive "OR" will return the result true, if they have the same values it will return false. The following example illustrates the usage of the logical operators and their actions:
Code Example
bool a = true; 
bool b = false; 
Console.WriteLine(/* Output */ a && b); // False 
Console.WriteLine(/* Output */ a || b); // True 
Console.WriteLine(/* Output */ !b); // True 
Console.WriteLine(/* Output */ b || true); // True 
Console.WriteLine(/* Output */ (5 > 7) ^ (a == b)); // False 

1.4.2.5 Bitwise Operators
A bitwise operator is an operator that acts on the binary representation of numeric types. In computers all the data and particularly numerical data is represented as a series of ones and zeros. The binary numeral system is used for this purpose. For example, number 55 in the binary numeral system is represented as 00110111. 
 
Binary representation of data is convenient because zero and one in electronics can be implemented by Boolean circuits, in which zero is represented as "no electricity" or for example with a voltage of -5V and the one is presented as "have electricity" or say with voltage +5V.
 
Bitwise operators are very similar to the logical ones. In fact, we can imagine that the logical and bitwise operators perform the same thing but using different data types. Logical operators work with the values true and false (Boolean values), while bitwise operators work with numerical values and are applied bitwise over their binary representation, i.e., they work with the bits of the number (the digits 0 and 1 of which it consists). Just like the logical operators in C#, there are bitwise operators "AND" (&), bitwise "OR" (|), bitwise negation (~) and excluding "OR" (^). The bitwise operators' performance on binary digits 0 and 1 is shown in the following table:
 
x 
y 
~x 
x & y 
x | y 
x ^ y 
1 
1 
0 
1 
1 
0 
1 
0 
0 
0 
1 
1 
0 
1 
1 
0 
1 
1 
0 
0 
1 
0 
0 
0 
Source: Nakov et al (2013)
 
As we see bitwise and logical operators are very much alike. The difference in the writing of "AND" and "OR" is that the logical operators are written with double ampersand (&&) and double vertical bar (||), and the bitwise – with a single ampersand or vertical bar (& and |). Bitwise and logical operators for exclusive "OR" are the same "^". For logical negation we use "!", while for bitwise negation (inversion) the "~" operator is used. 
In programming there are two bitwise operators that have no analogue in logical operators. These are the bit shift left (<<) and bit shift right (>>). Used on numerical values, they move all the bits of the value to the left or right. The bits that fall outside the number are lost and replaced with 0. 
 
The bit shifting operators are used in the following way: on the left side of the operator we place the variable (operand) with which we want to use the operator, on the right side we put a numerical value, indicating how many bits we want to offset. For example, 3 << 2 means that we want to move the bits of the number three, twice to the left. The number 3 presented in bits looks like this: "0000 0011". When you move twice left, the binary value will look like this: "0000 1100", and this sequence of bits is the number 12. If we look at the example we can see that actually we have multiplied the number by 4. Bit shifting itself can be represented as multiplication (bitwise shifting left) or division (bitwise shifting right) by a power of 2. This occurrence is due to the nature of the binary numeral system. Example of moving to the right is 6 >> 2, which means to move the binary number "0000 0110" with two positions to the right. This means that we will lose two right-most digits and feed them with zeros on the left. The end result will be "0000 0001" which is 1.
 
Here is an example of using bitwise operators. The binary representation of the numArray and the results of the bitwise operators are shown in the comments (green text):
 
Code Example
byte a = 3; // 0000 0011 = 3 
byte b = 5; // 0000 0101 = 5 
Console.WriteLine(/* Output */ a | b); // 0000 0111 = 7 
Console.WriteLine(/* Output */ a & b); // 0000 0001 = 1 
Console.WriteLine(/* Output */ a ^ b); // 0000 0110 = 6 
Console.WriteLine(/* Output */ ~a & b); // 0000 0100 = 4 
Console.WriteLine(/* Output */ a << 1); // 0000 0110 = 6 
Console.WriteLine(/* Output */ a << 2); // 0000 1100 = 12 
Console.WriteLine(/* Output */ a >> 1); // 0000 0001 = 1 
 
In the example we first create and initialize the values of two variables a and b. Then we print on the console the results of some bitwise operations on the two variables. The first operation that we apply is "OR". The example shows that for all positions where there was 1 in the binary representation of the variables a and b, there is also 1 in the result. The second operation is "AND". The result of the operation contains 1 only in the right-most bit, because the only place where a and b have 1 at the same time is their right-most bit. Exclusive "OR" returns ones only in positions where a and b have different values in their binary bits. Finally, the logical negation and bitwise shifting: left and right, are illustrated.
1.4.2.6 Type Conversion
Generally, operators work over arguments with the same data type. However, C# has a wide variety of data types from which we can choose the most appropriate for a particular purpose. To perform an operation on variables of two different data types we need to convert both to the same data type. Type conversion (typecasting) can be explicit and implicit. 
 
All expressions in C# have a type. This type can derive from the expression structure and the types, variables and literals used in it. It is possible to write an expression which type is inappropriate for the current context. In some cases this will lead to a compilation error, but in other cases the context can get a type that is similar or related to the type of the expression. In this case the program performs a hidden type conversion.
 
Specific conversion from type S to type T allows the expression of type S to be treated as an expression of type T during the execution of the program. In some cases this will require a validation of the transformation. In C# not all types can be converted to all other types, but only to some of them. For convenience, we shall group some of the possible transformations in C# according to their type into three categories: 
- implicit conversion; 
- explicit conversion; 
- conversion to or from string; 
 
A.        Implicit Type Conversion
Implicit (hidden) type conversion is possible only when there is no risk of data loss during the conversion, i.e. when converting from a lower range type to a larger range (e.g. from int to long). To make an implicit conversion it is not necessary to use any operator and therefore such transformation is called implicit. The implicit conversion is done automatically by the compiler when you assign a value with lower range to a variable with larger range or if the expression has several types with different ranges. In such case the conversion is executed into the type with the highest range. Here is an example of implicit type conversion:
 
Code Example
int myInt = 5; 
Console.WriteLine(/* Output */ myInt); // 5 
long myLong = myInt; 
Console.WriteLine(/* Output */ myLong); // 5 
Console.WriteLine(/* Output */ myLong + myInt); // 10 
 
In the example we create a variable myInt of type int and assign it the value 5. After that we create a variable myLong of type long and assign it the value contained in myInt. The value stored in myLong is automatically converted from type int to type long. Finally, we output the result from adding the two variables. Because the variables are from different types they are automatically converted to the type with the greater range, i.e. to type long and the result that is printed on the console is long again. Indeed, the given parameter to the method Console.WriteLine(/* Output */ ) is of type long, but inside the method it will be converted again, this time to type string, so it can be printed on the console. This transformation is performed by the method Long.ToString().
 
B.        Explicit Type Conversion
Explicit type conversion is used whenever there is a possibility of data loss. When converting floating point type to integer type there is always a loss of data coming from the elimination of the fractional part and an explicit conversion is obligatory (e.g. double to long). To make such a conversion it is necessary to use the operator for data conversion (type). There may also be data loss when converting a type with a wider range to type with a narrower one (double to float or long to int). The following example illustrates the use of explicit type conversion and data loss that may occur in some cases:
 
Code Example
double myDouble = 5.1d; 
Console.WriteLine(/* Output */ myDouble); // 5.1 
 
long myLong = (long)myDouble; 
Console.WriteLine(/* Output */ myLong); // 5 
 
myDouble = 5e9d; // 5 * 10^9 
Console.WriteLine(/* Output */ myDouble); // 5000000000 
 
int myInt = (int)myDouble; 
Console.WriteLine(/* Output */ myInt); // -2147483648 
Console.WriteLine(/* Output */ int.MinValue); // -2147483648 
 
 
In the first line of the example we assign a value 5.1 to the variable myDouble. After we convert (explicitly) to type long using the operator (long) and print on the console the variable myLong we see that the variable has lost its fractional part, because long is an integer. Then we assign to the real double precision variable myDouble the value 5 billion. Finally, we convert myDouble to int by the operator (int) and print variable myInt. The result is the same like when we print int.MinValue because myDouble contains a value bigger than the range of int.
 
It is not always possible to predict what the value of a variable will be after its scope overflows! Therefore, use sufficiently large types and be careful when switching to a "smaller" type. 
 
C.        Conversion to String
If it is necessary we can convert any type of data, including the value null, to string. The conversion of strings is done automatically whenever you use the concatenation operator (+) and one of the arguments is not of type string. In this case the argument is converted to a string and the operator returns a new string representing the concatenation of the two strings.  Another way to convert different objects to type string is to call the method ToString() of the variable or the value. It is valid for all data types in .NET Framework. Even calling 3.ToString() is fully valid in C# and the result will return the string "3". Let’s take a look on several examples for converting different data types to string:
Code Example
int a = 5; 
int b = 7; 
 
string sum = "Sum = " + (a + b); 
Console.WriteLine(/* Output */ sum); 
 
String incorrect = "Sum = " + a + b; 
Console.WriteLine(/* Output */ incorrect); 
 
Console.WriteLine(/* Output */  
"Perimeter = " + 2 * (a + b) + ". Area = " + (a * b) + "."); 
 
 
From the results it is obvious, that concatenating a number to a character string returns in result the string followed by the text representation of the number. Note that the "+" for concatenating strings can cause unpleasant effects on the addition of numArray, because it has equal priority with the operator "+" for mathematical addition. Unless the priorities of the operations are changed by placing the brackets, they will always be executed from left to right.


4.1. Notes
ITPCA2 (First Block)
4.1. Notes
	•	1.5 Variables
	•	1.5.1 Naming Variables - Rules
	•	1.5.2 Naming Variables - Recommendations
	•	1.5.3 Declaring Variables
	•	1.5.4 Assigning a Value to Variables
	•	1.5.5 Initialization of Variables
	•	1.6 Conclusion
Learning outcomes
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 1, 2 & 3
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
1.5 Variables
A variable is a container of information, which can change its value during the cause of program execution. It is a named area of memory, which stores a value from a particular data type, and that area of memory is accessible in the program by its name. It provides means for storing information, retrieving the stored information, and modifying the stored information. In C# programming, you will use variables to store and process information all the time. 
Variables are characterized by name (identifier), for example age; type (of the information preserved in them), for example int; value (stored information), for example 25.
1.5.1 Naming Variables - Rules
When we want the compiler to allocate a memory area for some information which is used in our program we must provide a name for it. It works like an identifier and allows referring to the relevant memory area.
The name of the variable can be any of our choice but must follow certain rules defined in the C# language specification:
- Variable names can contain the letters a-z, A-Z, the digits 0-9 as well as the character '_'.
- Variable names cannot start with a digit.
- Variable names cannot coincide with a keyword of the C# language. For example, base, char, default, int, object, this, null and many others cannot be used as variable names. 
A list of the C# keywords can be found in the section "Keywords" in chapter "Introduction to Programming". If we want to name a variable like a keyword, we can add a prefix to the name – "@". For example, @char and @null are valid variable names while char and null are invalid. Some examples of proper names are name, first_Name, name1. Improper names (will lead to compilation error):  example 1 (digit), if (keyword), 1name (starts with a digit).
1.5.2 Naming Variables - Recommendations
We will provide some recommendations how to name your variables, since not all names, allowed by the compiler, are appropriate for the variables. 
- The names should be descriptive and explain what the variable is used for. For example, an appropriate name for a variable storing a person’s name is personName and inappropriate name is a37.
- Only Latin characters should be used. Although Cyrillic is allowed by the compiler, it is not a good practice to use it in variable names or in the rest of the identifiers within the program.
- In C# it is generally accepted that variable names should start with a small letter and include small letters, every new word, however, starts with a capital letter. For instance, the name firstName is correct and better to use than firstname or first_name. Usage of the character _ in the variable names is considered a bad naming style.
- Variable names should be neither too long nor too short – they just need to clarify the purpose of the variable within its context.
- Uppercase and lowercase letters should be used carefully as C# distinguishes them. For instance, age and Age are different variables. 
Here are some examples of well-named variables:
- firstName 
- age 
- startIndex 
- lastNegativeNumberIndex 
And here are some examples for poorly named variables (although the names are correct from the C# compiler’s perspective):
- _firstName (starts with _)
- last_name (contains _)
- AGE (is written with capital letters)
- Start_Index (starts with capital letter and contains _)
- lastNegativeNumber_Index (contains _)
- a37 (the name is not descriptive and does not clearly provide the purpose of the variable)
- fullName23, fullName24, etc. (it is not appropriate for a variable name to contain digits unless this improves the clarity of the variable used; if you need to have multiple variables with similar names ending in a different number, storing the same or similar type of data, it may be more appropriate to create a single collection or array variable and name it fullNamesList, for example).
1.5.3 Declaring Variables
When you declare a variable, you perform the following steps:
- specify its type (such as int);
- specify its name (identifier, such as age);
- optionally specify initial value (such as 25) but this is not obligatory.
The syntax for declaring variables in C# is as follows:
<data type> <identifier> [= <initialization>]; 
Here is an example of declaring variables:
Code Example
string name;
int age;
1.5.4 Assigning a Value to Variables
Assigning a value to a variable is the act of providing a value that must be stored in the variable. This operation is performed by the assignment operator "=". On the left side of the operator we put the variable name and on the right side – its new value. 
Here is an example of assigning values to variables:
Code Example
name = "John Smith";
age = 25;
1.5.5 Initialization of Variables
The word initialization in programming means specifying an initial value. When setting value to variables at the time of their declaration we actually initialize them. 
 
Each data type in C# has a default value (default initialization) which is used when there is no explicitly set value for a given variable. Let’s summarize how to declare variables, initialize them and assign values to them with the following example:
Code Example
// Declare and initialize some variables 
byte centuries = 20; 
ushort years = 2000; 
decimal decimalPI = 3.141592653589793238m; 
bool isEmpty = true; 
char ch = 'a'; 
string firstName = "John"; 
ch = (char)5; 
char secondChar; 
// Here we use an already initialized variable and reassign it 
secondChar = ch; 
 
1.6 Conclusion
In this week, we discussed the principles, characteristics and features in using Visual Studio IDE. In addition, we critically evaluated the Visual Studio environment. Further, our first C# program was demonstrated and explained. C# datatypes and operators were discussed. Lastly, we discussed variables and their declaration in C#.


5.1. Notes
ITPCA2 (First Block)
5.1. Notes
	•	2.1 Introduction
	•	2.2 Control Statements
	•	2.2.1 Selection Statements
	•	2.2.2 Iteration Statements
	•	2.2.3 Jump Statement
	•	Case study
Learning outcomes
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 5 & 6
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
2.1 Introduction
In this week we will discuss control structures in C# and give corresponding examples to demonstrate how they work. We will also discuss various relational operators in C# also give the corresponding examples to demonstrate them.

2.2 Control Statements
Control statements give additional means to control the processing within the applications being developed. This section explores the syntax and function of the the three major control statement C# offers. These statement are categorise as: 
	•	Selection Statement
	•	Iteration Statements
	•	Jump statement.
2.2.1 Selection Statements
The selection statements consist of the if, else, switch-case branching. The if and if-else are conditional control statements. Because of them the program can behave differently based on a defined condition checked during the execution of the statement. 
 
2.2.1.1       “if” Statements
The main format of the conditional statements if is as follows:
Code Example
if (Boolean expression) 
{ 
Body of the conditional statement; 
} 
 
 
It includes: if-clause, Boolean expression and body of the conditional statement. The Boolean expression can be a Boolean variable or Boolean logical expression. The body of the statement is the part locked between the curly brackets: {}. It may consist of one or more operations (statements). When there are several operations, we have a complex block operator, i.e. series of commands that follow one after the other, enclosed in curly brackets. 
 
The expression in the brackets which follows the keyword if must return the Boolean value true or false. If the expression is calculated to the value true, then the body of a conditional statement is executed. If the result is false, then the operators in the body will be skipped. Let’s take a look at an example of using a conditional statement if:
Code Example
static void Main() 
{ 
Console.WriteLine(/* Output */ "Enter two numArray."); 
Console.Write("Enter first number: "); 
int firstNumber = int.Parse(Console.ReadLine()); 
Console.Write("Enter second number: "); 
int secondNumber = int.Parse(Console.ReadLine()); 
int biggerNumber = firstNumber; 
if (secondNumber > firstNumber) 
{ 
biggerNumber = secondNumber; 
} 
Console.WriteLine(/* Output */ "The bigger number is: {0}", biggerNumber); 
} 
 
 
If we start the example and enter the numArray 4 and 5 we will get the following result:
Output
Enter two numArray. 
Enter first number: 4 
Enter second number: 5 
The bigger number is: 5 
 
2.2.1.2                  “if-else” Statements
In C#, as in most of the programming languages there is a conditional statement with else clause: the if-else statement. Its format is the following:
Code Example
if (Boolean expression) 
{ 
Body of the conditional statement; 
} 
else 
{ 
Body of the else statement; 
} 
 
 
The format of the if-else structure consists of the reserved word if, Boolean expression, body of a conditional statement, reserved word else and else-body statement. The body of else-structure may consist of one or more operators, enclosed in curly brackets, same as the body of a conditional statement.
 
This statement works as follows: the expression in the brackets (a Boolean expression) is calculated. The calculation result must be Boolean – true or false. Depending on the result there are two possible outcomes. If the Boolean expression is calculated to true, the body of the conditional statement is executed and the else-statement is omitted and its operators do not execute. Otherwise, if the Boolean expression is calculated to false, the else-body is executed, the main body of the conditional statement is omitted and the operators in it are not executed. Let’s take a look at the next example and illustrate how the if-else statement works:
Code Example
static void Main() 
{ 
int x = 2; 
if (x > 3) 
{ 
Console.WriteLine(/* Output */ "x is greater than 3"); 
} 
else 
{ 
Console.WriteLine(/* Output */ "x is not greater than 3"); 
} 
} 
 
 
The program code can be interpreted as follows: if x>3, the result at the end is: "x is greater than 3", otherwise (else) the result is: "x is not greater than 3". In this case, since x=2, after the calculation of the Boolean expression the operator of the else structure will be executed. The result of the example is:
Output
x is not greater than 3 
 
 
2.2.1.3                 Nested “if” Statements
Sometimes the programming logic in a program or an application needs to be represented by multiple if-structures contained in each other. We call them nested if or nested if-else structures.  We call nesting the placement of an if or if-else structure in the body of another if or else structure. In such situations every else clause corresponds to the closest previous if clause. This is how we understand which else clause relates to which if clause.
 
It’s not a good practice to exceed three nested levels, i.e. we should not nest more than three conditional statements into one another. If for some reason we need to nest more than three structures, we should export a part of the code in a separate method. Here is an example of using nested if structures:
Code Example
int first = 5; 
int second = 3; 
if (first == second) 
{ 
Console.WriteLine(/* Output */ "These two numArray are equal."); 
} 
else 
{ 
if (first > second) 
{ 
Console.WriteLine(/* Output */ "The first number is greater."); 
} 
else 
{ 
Console.WriteLine(/* Output */ "The second number is greater."); 
} 
} 
 
 
In the example above we have two numArray and compare them in two steps: first we compare whether they are equal and if not, we compare again, to determine which one is the greater. Here is the result of the execution of the code above:
Output
The first number is greater. 
 
 
2.2.1.4       Conditional Statements “switch-case”
In the following section we will cover the conditional statement switch. It is used for choosing among a list of possibilities. The structure switch-case chooses which part of the programming code to execute based on the calculated value of a certain expression (most often of integer type). The format of the structure for choosing an option is as follows:
 
Code Example
switch (integer_selector) 
{ 
case integer_value_1: 
statements; 
break; 
case integer_value_2: 
statements; 
break; 
// … 
default: 
statements; 
break; 
} 
 
The selector is an expression returning a resulting value that can be compared, like a number or string. The switch operator compares the result of the selector to every value listed in the case labels in the body of the switch structure. If a match is found in a case label, the corresponding structure is executed (simple or complex). If no match is found, the default statement is executed (when such exists). The value of the selector must be calculated before comparing it to the values inside the switch structure. The labels should not have repeating values, they must be unique. 
 
As it can be seen from the definition above, every case ends with the operator break, which ends the body of the switch structure. The C# compiler requires the word break at the end of each case-section containing code. If no code is found after a case-statement, the break can be omitted and the execution passes to the next case-statement and continues until it finds a break operator. After the default structure break is obligatory.  It is not necessary for the default clause to be last, but it’s recommended to put it at the end, and not in the middle of the switch structure.
 
The switch statement is a clear way to implement selection among many options (namely, a choice among a few alternative ways for executing the code). It requires a selector, which is calculated to a certain value. The selector type could be an integer number, char, string or enum. If we want to use for example an array or a float as a selector, it will not work. For non-integer data types, we should use a series of if statements. 
 
Using multiple labels is appropriate, when we want to execute the same structure in more than one case. Let’s look at the following example:
Code Example
int number = 6; 
switch (number) 
{ 
case 1: 
case 4: 
case 6: 
case 8: 
case 10: 
Console.WriteLine(/* Output */ "The number is not prime!"); break; 
case 2: 
case 3: 
case 5: 
case 7: 
Console.WriteLine(/* Output */ "The number is prime!"); break; 
default: 
Console.WriteLine(/* Output */ "Unknown number!"); break; 
} 
 
 
In the above example, we implement multiple labels by using case statements without break after them. In this case, first the integer value of the selector is calculated – that is 6, and then this value is compared to every integer value in the case statements. When a match is found, the code block after it is executed. If no match is found, the default block is executed. The result of the example above is as follows:
 
Output
The number is not prime! 
 
2.2.2 Iteration Statements
Iteration statement also called loop is a basic programming construct that allows repeated execution of a fragment of source code. Depending on the type of the loop, the code in it is repeated a fixed number of times or repeats until a given condition is true (exists).  Loops that never end are called infinite loops. Using an infinite loop is rarely needed except in cases where somewhere in the body of the loop a break operator is used to terminate its execution prematurely. This is categorised into do, for, for-each, and while loops.
  
2.2.2.1       Do-While Loops
The do-while loop is similar to the while loop, but it checks the condition after each execution of its loop body. This type of loops is called loops with condition at the end (post-test loop). A do-while loop looks like this:
Code Example
do 
{ 
executable code; 
} while (condition); 
 
  
By design do-while loops are executed according to the following scheme:
 
 
   Figure 3- do- while loops
Source: Nakov et al (2013)
 
Initially the loop body is executed. Then its condition is checked. If it is true, the loop’s body is repeated, otherwise the loop ends. This logic is repeated until the condition of the loop is broken. The body of the loop is executed at least once. If the loop’s condition is constantly true, the loop never ends.  The below is the example of a do while loop. In this example we will calculate the factorial of a given number n. 
 
 
Code Example
Console.Write("n = "); 
int n = int.Parse(Console.ReadLine()); 
decimal factorial = 1; 
do 
{ 
factorial *= n; 
n--; 
} while (n > 0); 
Console.WriteLine(/* Output */ "n! = " + factorial);  
 
 
 At the beginning we start with a result of 1 and multiply consecutively the result at each iteration by n, and reduce n by one unit, until n reaches 0. This gives us the product n*(n-1)*…*1. Finally, we print the result on the console. This algorithm always performs at least one multiplication and that’s why it will not work properly when n ≤ 0. 
 
Here is the result of the above example’s execution for n=7:
Output
n = 7
n! = 5040
 
 
2.2.2.2       For Loops
For-loops are a slightly more complicated than while and do-while loops but on the other hand they can solve more complicated tasks with less code. Here is the scheme describing for-loops:

 
 Figure 4- For loops
 
Source: Nakov et al (2013)
 
Let us look at how the program code of a for-loop looks like:
Code Example
for (initialization; condition; update) 
{ 
loop's body; 
} 
 
 
It consists of an initialization part for the counter (in the pattern int idx = 0), a Boolean condition (idx < 10), an expression for updating the counter (idx++, it might be i-- or for instance, i = i + 3) and body of the loop. 
The counter of the loop distinguishes it from other types of loops. Most often the counter changes from a given initial value to a final one in ascending order, for example from 1 to 100. The number of iterations of a given for-loop is usually known before its execution starts. A for-loop can have one or several loop variables that move in ascending or descending order or with a step. It is possible one loop variable to increase and the other – to decrease. It is even possible to make a loop from 2 to 1024 in steps of multiplication by 2, since the update of the loop variables can contain not only addition, but any other arithmetic (as well as other) operations.
 
Here is a complete example of a for-loop:
 
Code Example
for (int i = 0; idx <= 10; idx++) 
{ 
Console.Write(i + " "); 
} 
 
 
The result of its execution is the following:
Output
0 1 2 3 4 5 6 7 8 9 10 
 
The nested loops are programming constructs consisting of several loops located into each other. The innermost loop is executed more times, and the outermost – less times. Let’s see how two nested loops look like:
Code Example
for (initialization, verification, update) 
{ 
for (initialization, verification, update) 
{ 
executable code 
} 
… 
} 
 
 
After initialization of the first for loop, the execution of its body will start, which contains the second (nested) loop. Its variable will be initialized, its condition will be checked and the code within its body will be executed, then the variable will be updated and execution will continue until the condition returns false. After that the second iteration of the first for loop will continue, its variable will be updated and the whole second loop will be performed once again. The inner loop will be fully executed as many times as the body of the outer loop. Example: 
Code Example
int n = int.Parse(Console.ReadLine()); 
for (int row = 1; row <= n; row++) 
{ 
for (int col = 1; col <= row; col++) 
{ 
Console.Write(col + " "); 
} 
Console.WriteLine(/* Output */ ); 
}     
 
 
If we execute it, we will make sure that it works correctly. Here is how the result for n=7 looks like:
 
Output
1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5 
1 2 3 4 5 6 
1 2 3 4 5 6 7 
 
 
2.2.2.3       For Each Loops
The foreach loop (extended for-loop) is new for the C/C++/C# family of languages, but is well known for the VB and PHP programmers. This programming construct serves to iterate over all elements of an array, list or other collection of elements (IEnumerable). It passes through all the elements of the specified collection even if the collection is not indexed. Here is how a foreach loop looks like:
Code Example
foreach (type variable in collection) 
{ 
statements; 
} 
 
 
As we see, it is significantly simpler than the standard for-loop and therefore is very often preferred by developers because it saves writing when you need to go through all the elements of a given collection. Here is an example that shows how we can use foreach:
Code Example
int[] numArray = { 2, 3, 5, 7, 11, 13, 17, 19 }; 
foreach (int i in numArray) 
{ 
Console.Write(" " + i); 
} 
Console.WriteLine(/* Output */ ); 
string[] towns = { "London", "Paris", "Milan", "New York" }; 
foreach (string town in towns) 
{ 
Console.Write(" " + town); 
} 
 
 
In the example we create an array of numArray, which are after that went through with a foreach loop, and its elements are printed on the console. Then an array of city names (strings) is created and in the same way it is went through and its elements are printed on the console. The result of the example is:
 
Output
2 3 5 7 11 13 17 19 
London Paris Milan New York 
 
 
2.2.2.4       While Loops
One of the simplest and most commonly used loops is while.
 
Code Example
while (condition) 
{ 
loop body; 
} 
 
In the code above example, condition is any expression that returns a Boolean result – true or false. It determines how long the loop body will be repeated and is called the loop condition. In this example the loop body is the programming code executed at each iteration of the loop, i.e. whenever the input condition is true. The behaviour of while loops can be represented by the following scheme:
 

Figure 5- While Loop
 
Source: Nakov et al (2013)
 In the while loop, first of all the Boolean expression is calculated and if it is true the sequence of operations in the body of the loop is executed. Then again the input condition is checked and if it is true again the body of the loop is executed. All this is repeated again and again until at some point the conditional expression returns value false. At this point the loop stops and the program continues to the next line, immediately after the body of the loop. 
 
The body of the while loop may not be executed even once if in the beginning the condition of the cycle returns false. If the condition of the cycle is never broken the loop will be executed indefinitely. Let’s consider a very simple example of using the while loop. The purpose of the loop is to print on the console the numArray in the range from 0 to 9 in ascending order:
Code Example
// Initialize the counter 
int counter = 0; 
// Execute the loop body while the loop condition holds 
while (counter <= 9) 
{ 
// Print the counter value 
Console.WriteLine(/* Output */ "Number : " + counter); 
// Increment the counter 
counter++; 
} 
 
 
When executing the sample code we obtain the following result:
 
Output
Number : 0 
Number : 1 
Number : 2 
Number : 3 
Number : 4 
Number : 5 
Number : 6 
Number : 7 
Number : 8 
Number : 9 
 
2.2.3 Jump Statement
The Jump statements helps to transfer control during the cause of program execution. There are four Jump statements in C# such as Goto, Break, Continue, and Return.
 
2.2.3.1       Goto Statement
The goto statement can be used to jump to a specific segment of code. Goto can also be used for jumping to switch cases and default labels inside switch blocks. The overuse of goto could make the code difficult to read and maintain if you have many goto jumps within your code.
Code Example
1.   label1:  
2.         ;     
3.         //...     
4.         if (x == 0)  
5.             goto label1;  
6.         //...     
 
 
2.2.3.2       Break Statement
The break statement, used within for, while, and do-while blocks, causes processing to exit the innermost loop immediately. When a break statement is used, the code jumps to the next line following the loop block, see example below.
Code Example
1.   while (true)  
2.   {  
3.       //...     
4.       if (x == 0)  
5.           break;  
6.       //...     
7.   }  
8.   Console.WriteLine(/* Output */ "break");
 
2.2.3.3       Continue Statement
The continue statement (shown in example below) is used to jump to the end of the loop immediately and process the next iteration of the loop.
 
Code Example
1.   int x = 0;  
2.   while (true)  
3.   {  
4.       //...     
5.       if (x == 0)  
6.       {  
7.           x = 5;  
8.           continue;  
9.       }  
10.      //...     
11.    
12.      if (x == 5)  
13.             Console.WriteLine(/* Output */ "continue");  
14.      //...     
15.  }  
 
2.2.3.4       Return Statement
The return statement is used to prematurely return from a method. The return statement can return empty or with a value on the stack, depending upon the return value definition in the method, see example below. Void methods do not require a return value. For other functions, you need to return an appropriate value of the type you declared in the method signature
 
Code Example
1.   void MyFunc1() {  
2.       // ...     
3.       if (x == 1) return;  
4.       // ...     
5.   }  
6.   int MyFunc2() {  
7.       // ...     
8.       if (x == 2) return 1919;  
9.       // ...     
10.  }  
 
Case study
Case Study 1: E-Commerce Order Processing System
Scenario: You are tasked with developing a simple order processing system for an e-commerce platform. The system needs to apply different discounts based on certain conditions, check the stock availability, and ensure that the payment process is completed successfully.
Control Structures Used:
	•	If-Else Statements
	•	Switch Statement
	•	While Loop
	•	For Loop
Solution:

using System;

public class OrderProcessor
{
    public double ProcessOrder(int productId, int quantity, bool isPaymentSuccessful)
    {
        // Check if the product exists and quantity is available
        if (productId < 1 || quantity < 1)
        {
            Console.WriteLine(/* Output */ "Invalid product or quantity.");
            return 0;
        }

        double price = GetProductPrice(productId);
        double totalPrice = price * quantity;

        // Apply discount based on order quantity
        if (quantity > 10)
        {
            totalPrice *= 0.9; // 10% discount for orders with more than 10 items
        }
        else if (quantity >= 5)
        {
            totalPrice *= 0.95; // 5% discount for orders with 5-10 items
        }

        // Check stock availability
        int stock = GetProductStock(productId);
        if (quantity > stock)
        {
            Console.WriteLine(/* Output */ "Not enough stock available.");
            return 0;
        }

        // Check if payment was successful
        if (!isPaymentSuccessful)
        {
            Console.WriteLine(/* Output */ "Payment failed.");
            return 0;
        }

        return totalPrice;
    }

    private double GetProductPrice(int productId)
    {
        // Assume a product price based on its ID
        return 100.0; // Just for the example
    }

    private int GetProductStock(int productId)
    {
        // Assume stock availability based on product ID
        return 20; // Just for the example
    }
}

public class MainProgram
{
    public static void Main()
    {
        OrderProcessor processor = new OrderProcessor();
        
        // Case 1: Valid order with discount
        double price1 = processor.ProcessOrder(1, 6, true);
        Console.WriteLine(/* Output */ $"Total price: {price1:C}");

        // Case 2: Invalid order (out of stock)
        double price2 = processor.ProcessOrder(1, 25, true);
        Console.WriteLine(/* Output */ $"Total price: {price2:C}");

        // Case 3: Payment failure
        double price3 = processor.ProcessOrder(1, 6, false);
        Console.WriteLine(/* Output */ $"Total price: {price3:C}");
    }
}
Explanation:
	•	If-Else Statements are used to check the quantity of items, whether a discount should apply, and if the payment was successful.
	•	Switch Statement could be used in place of multiple if-else branches to select actions based on specific product IDs (if applicable).
	•	While Loop could be used for checking a condition until it's met, such as checking if a customer's payment method is valid.
	•	For Loop could be employed to iterate over a list of products for bulk processing, like applying discounts across multiple products.

Case Study 2: Student Grade Classification
Scenario: You are developing a student grading system where you need to categorize students into different grade categories based on their exam scores. The system should print out appropriate messages for students who pass or fail, and those who are eligible for special honors.
Control Structures Used:
	•	If-Else Statements
	•	Switch Statement
	•	For Loop
Solution:

using System;

public class GradeProcessor
{
    public string GetGrade(int score)
    {
        // Determine grade based on score
        if (score >= 90)
            return "A";
        else if (score >= 80)
            return "B";
        else if (score >= 70)
            return "C";
        else if (score >= 60)
            return "D";
        else
            return "F";
    }

    public string GetHonorStatus(int score)
    {
        // Special honor status
        if (score >= 85)
            return "Eligible for Honors";
        else
            return "Not eligible for Honors";
    }

    public void ProcessGrades(int[] studentScores)
    {
        foreach (var score in studentScores)
        {
            string grade = GetGrade(score);
            string honorStatus = GetHonorStatus(score);
            Console.WriteLine(/* Output */ $"Score: {score}, Grade: {grade}, Status: {honorStatus}");
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        GradeProcessor processor = new GradeProcessor();

        int[] studentScores = { 95, 88, 72, 65, 55, 100 };

        processor.ProcessGrades(studentScores);
    }
}
Explanation:
	•	If-Else Statements determine the grade based on the student's score and check whether the student is eligible for honors.
	•	Switch Statement could be used if you want to create multiple specific conditions (e.g., student classes, subjects) to categorize students based on their grades.
	•	For Loop is used to iterate through the array of student scores and apply the logic of categorizing each student's performance.


7.1. Notes
ITPCA2 (First Block)
7.1. Notes
	•	3.1 Introduction
	•	3.1.1 What is an Exception
	•	3.1.2 Why an exception occurs?
	•	3.1.3 Advantages of Exception Handling
	•	3.1.4 Difference between Error and Exception
	•	3.1.5 Types of Exception
	•	3.2 Catching and Handling Exceptions
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 8 & 13
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
3.1 Introduction
When we write a program, we describe step-by-step what the computer must do and in most of the cases we rely that the program will execute normally. Indeed, most of the time, programs are following this normal pattern, but there are some exceptions. Let’s say we want to read a file and display its contents on the screen. Let’s assume the file is located on a remote server and during the process of reading it, the connection goes down. The file then will be only partially loaded. The program will not be able to execute normally and show file’s contents on the screen. In this case, we have an exception from the normal (and correct) program execution and this exception must be reported to the user and/or the administrator.

Play Video
3.1.1 What is an Exception
An Exception is an unwanted event that interrupts the normal flow of the program. When an exception occurs program execution gets terminated.  In such cases we get a system generated message which may not be meaningful. The good thing about exceptions is that they can be handled in C#.  By handling the exceptions we can provide a meaningful message to the user about the issue rather than a system generated message, which may not be understandable to a user.
3.1.2 Why an exception occurs?
There can be several reasons that can cause a program to throw exception. For example:
	•	Opening a non-existing file in your program,
	•	Network connection problem,
	•	bad input data provided by user, etc.
3.1.3 Advantages of Exception Handling
	•	Exception handling ensures that the flow of the program doesn’t break when an exception occurs.
	•	For example, if a program has bunch of statements and an exception occurs mid-way after executing certain statements then the statements after the exception will not execute and the program will terminate abruptly.
	•	By handling we make sure that all the statements execute and the flow of program doesn’t break
3.1.4 Difference between Error and Exception
	•	Errors: indicate that something severe enough has gone wrong, the application should crash rather than try to handle the error.
	•	Exceptions: are events that occurs in the code.
	•	A programmer can handle such conditions and take necessary corrective actions.
3.1.5 Types of Exception
C# statements can execute in either checked or unchecked context. In a checked context, arithmetic overflow raises an exception. In an unchecked context, arithmetic overflow is ignored and the result is truncated by discarding any high-order bits that don't fit in the destination type. 
3.1.5.1       Checked Exception
The checked keyword is used to explicitly enable overflow checking for integral-type arithmetic operations and conversions. By default, an expression that contains only constant values causes a compiler error if the expression produces a value that is outside the range of the destination type. If the expression contains one or more non-constant values, the compiler does not detect the overflow. Evaluating the expression assigned to i2 in the following example does not cause a compiler error.
Code Example
// The following example causes compiler error CS0220 because 2147483647
// is the maximum value for integers.
//int i1 = 2147483647 + 10;
 
// The following example, which includes variable ten, does not cause
// a compiler error.
int ten = 10;
int i2 = 2147483647 + ten;
 
// By default, the overflow in the previous statement also does
// not cause a run-time exception. The following line displays
// -2,147,483,639 as the sum of 2,147,483,647 and 10.
Console.WriteLine(/* Output */ i2);
 
 
 By default, these non-constant expressions are not checked for overflow at run time either, and they do not raise overflow exceptions. The above example displays -2,147,483,639 as the sum of two positive integers.
Overflow checking can be enabled by compiler options, environment configuration, or use of the checked keyword. The example below demonstrate how to use a checked expression or a checked block to detect the overflow that is produced by the previous sum at run time. The example raise an overflow exception.
 
Code Example
// If the previous sum is attempted in a checked environment, an
// OverflowException error is raised.
 
// Checked expression.
Console.WriteLine(/* Output */ checked(2147483647 + ten));
 
// Checked block.
checked
{
    int i3 = 2147483647 + ten;
    Console.WriteLine(/* Output */ i3);
}
 
 
The program below is an example of a C# checked exception. This program throws an exception and stops program execution.
Code Example
	•	1. using System;  
	•	2. namespace CSharpProgram  
	•	3. {  
	•	4.     class Program  
	•	5.     {  
	•	6.         static void Main(string[] args)   
	•	7.         {  
	•	8.             checked  
	•	9.             {  
                int val = int.MaxValue;  
               Console.WriteLine(/* Output */ val + 2);  
           }  
        }  
    }  
}  
 
 
The output is given below:
 
Code Example
Unhandled Exception: System.OverflowException: Arithmetic operation resulted in an overflow.
 
 
3.1.5.2       Unchecked Exception
The unchecked keyword is used to suppress overflow-checking for integral-type arithmetic operations and conversions. In an unchecked context, if an expression produces a value that is outside the range of the destination type, the overflow is not flagged. For example, because the calculation in the following example is performed in an unchecked block or expression, the fact that the result is too large for an integer is ignored, and int1 is assigned the value -2,147,483,639.
 
Code Example
unchecked
{
    int1 = 2147483647 + 10;
}
int1 = unchecked(ConstantMax + 10);
 
 
If the unchecked environment is removed, a compilation error occurs. The overflow can be detected at compile time because all the terms of the expression are constants. Expressions that contain non-constant terms are unchecked by default at compile time and run time. Because checking for overflow takes time, the use of unchecked code in situations where there is no danger of overflow might improve performance. However, if overflow is a possibility, a checked environment should be used. Below is an example of unchecked exception.
Code Example
	•	1. using System;  
	•	2. namespace CSharpProgram  
	•	3. {  
	•	4.     class Program  
	•	5.     {  
	•	6.         static void Main(string[] args)   
	•	7.         {  
	•	8.             unchecked  
	•	9.             {  
                int val = int.MaxValue;  
                Console.WriteLine(/* Output */ val + 2);  
            }  
        }  
    }  
}  
 
 
Output
Code Example
-2147483647
3.2 Catching and Handling Exceptions
Exception handling is a mechanism, which allows exceptions to be thrown and caught. This mechanism is provided internally by the CLR (Common Language Runtime). Parts of the exception handling infrastructure are the language constructs in C# for throwing and catching exceptions. CLR takes care to propagate each exception to the code that can handle it. A general syntax of handling an exception is illustrated below.
try
{
          // Any number of statements;
          // some might cause an exception
}
catch(XxxException anExceptionInstance)
{
           // Do something about it
}

// Statements here execute whether there was an exception or not

An example of how an exception can be handles is as follows:

using System;
class MilesPerGallon
{
          static void Main()
           {
                  int milesDriven;
                  int gallonsOfGas;
                  int mpg;
                  try
                           {
                                  Write("Enter miles driven ");
                                   milesDriven = Convert.ToInt32(ReadLine());
                                   Write("Enter gallons of gas purchased ");
                                   gallonsOfGas = Convert.ToInt32(ReadLine());
                                   mpg = milesDriven / gallonsOfGas;
                             }
                     catch(Exception e)
                            {
                                   mpg = 0;
                                   WriteLine(e.message);
                             }
                         WriteLine("You got {0} miles per gallon", mpg);
                 }
}


Case Study
Case Study 1: Handling Invalid User Input in a Login System
Scenario: In a login system, the user is prompted to enter their username and password. If the username or password is empty, an exception should be thrown. Additionally, if the entered username does not match the stored username, a LoginException should be raised.
Exception Handling Used:
	•	try-catch block to handle input validation and login errors.
	•	throw to explicitly raise exceptions.
	•	custom exception class to handle specific login-related errors.
Solution:

using System;

public class LoginException : Exception
{
    public LoginException(string message) : base(message) { }
}

public class UserLoginSystem
{
    private string storedUsername = "admin";
    private string storedPassword = "password123";

    public void Login(string username, string password)
    {
        try
        {
            ValidateCredentials(username, password);
            Console.WriteLine(/* Output */ "Login successful.");
        }
        catch (LoginException ex)
        {
            Console.WriteLine(/* Output */ $"Login failed: {ex.Message}");
        }
    }

    private void ValidateCredentials(string username, string password)
    {
        if (string.IsNullOrEmpty(username) || string.IsNullOrEmpty(password))
        {
            throw new LoginException("Username and password cannot be empty.");
        }

        if (username != storedUsername)
        {
            throw new LoginException("Invalid username.");
        }

        if (password != storedPassword)
        {
            throw new LoginException("Incorrect password.");
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        UserLoginSystem loginSystem = new UserLoginSystem();

        // Case 1: Successful login
        loginSystem.Login("admin", "password123");

        // Case 2: Empty username
        loginSystem.Login("", "password123");

        // Case 3: Invalid username
        loginSystem.Login("user", "password123");

        // Case 4: Incorrect password
        loginSystem.Login("admin", "wrongpassword");
    }
}
Explanation:
	•	try-catch block: The try block contains the code that may throw exceptions. If an exception is thrown, the catch block handles it. In this case, the exception is a LoginExceptionthat catches specific errors like invalid credentials or empty input.
	•	throw keyword: Used to explicitly raise a LoginException when the conditions are met, such as an empty username or incorrect credentials.
	•	Custom LoginException class: A custom exception to handle login-specific errors with a descriptive message.


8.1. Notes
ITPCA2 (First Block)
8.1. Notes
	•	3.3 Exceptions Handling Classes
	•	3.4 Exceptions Handling Methods
	•	3.4.1 Try …Catch Block
	•	3.4.2 Nested Try …Catch Block
	•	3.4.3 Try…Finally Block
	•	3.4.4 Throw Keyword
	•	3.5 Conclusion
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire programming skills in core C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 8 & 13
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
3.3 Exceptions Handling Classes
When you have to throw an exception, you can often use an existing exception type in the .NET Framework instead of implementing a custom exception. You should use a standard exception type under these two conditions:
	•	You are throwing an exception that is caused by a usage error (that is, by an error in program logic made by the developer who is calling your method). Typically, you would throw an exception such as ArgumentException, ArgumentNullException, InvalidOperationException, or NotSupportedException. The string you supply to the exception object's constructor when instantiating the exception object should describe the error so that the developer can fix it.
	•	You are handling an error that can be communicated to the caller with an existing .NET Framework exception. You should throw the most derived exception possible. For example, if a method requires an argument to be a valid member of an enumeration type, you should throw an InvalidEnumArgumentException (the most derived class) rather than an ArgumentException.
The following table lists popular exception class and the conditions and meaning under which you would throw them.
Exception
Condition
NullPointerException
When you try to use a reference that points to null
ArithmeticException
When bad data is provided by user, for example, when you try to divide a number by zero this exception occurs because dividing a number by zero is undefined.
ArrayIndexOutOfBoundsException
When you try to access the elements of an array out of its bounds, for example array size is 5 (which means it has five elements) and you are trying to access the 10th element.
SQLException,
This class is created whenever the . NET Framework Data Provider for SQL Server encounters an error generated from the server. (Client side errors are thrown as standard common language runtime exceptions.) SqlException always contains at least one instance of SqlError.
ClassNotFoundException
ClassNotFoundException is an exception that occurs when you try to load a class at run time using Class. forName() or loadClass() methods and mentioned classes are not found in the classpath. 
IOException,
IOException is the base class for exceptions thrown while accessing information using streams, files and directories. The Base Class Library includes the following types, each of which is a derived class of IOException : DirectoryNotFoundException. EndOfStreamException. FileNotFoundException.
NullReferenceException
Handles errors generated from referencing a null object.
DivideByZeroException
Handles errors generated from dividing a dividend with zero.
ArrayTypeMismatchException
Handles errors generated when type is mismatched with the array type.

Play Video
3.4 Exceptions Handling Methods
An exception is a problem that arises during the execution of a program. A C# exception is a response to an exceptional circumstance that arises while a program is running, such as an attempt to divide by zero. Exceptions provide a way to transfer control from one part of a program to another. C# exception handling is built upon four keywords: try, catch, finally, and throw.
3.4.1 Try …Catch Block

 
A try block identifies a block of code for which particular exceptions is activated. The try block contains set of statements where an exception can occur. It is always followed by a catch block, which handles the exception that occurs in associated try block. A try block must be followed by catch blocks or finally block or both.
 
Syntax
Code Example
try
{
     //statements that may cause an exception
}
catch (exception(type) e(object))‏
{
     //error handling code
}
 
 
Consider the following example, where we create an array of three integers:
Code Example
int[] myNumbers = {1, 2, 3}
Console.WriteLine(/* Output */ myNumber[10]); // error!
 
 
The error message will be something like this:
Error
System.IndexOutOfRangeException: 'Index was outside the bounds of the array.'
 
 
If an error occurs, we can use try...catch to catch the error and execute some code to handle it. In the following example, we use the variable inside the catch block (e) together with the built-in Message property, which outputs a message that describes the exception:
Code Example
 
try
{
  int[] myNumbers = {1, 2, 3};
  Console.WriteLine(/* Output */ myNumbers[10]);
}
catch (Exception e)
{
  Console.WriteLine(/* Output */ e.Message);
}
 
 
The output will be:
 
Output
Index was outside the bounds of the array.
 
 
However, you can customise the message to fit your choice using the following example.
Code Example
try
{
  int[] myNumbers = {1, 2, 3};
  Console.WriteLine(/* Output */ myNumbers[10]);
}
catch (Exception e)
{
  Console.WriteLine(/* Output */ "Something went wrong.");
}
 
 
The output will be:
 
Output
Something went wrong.
 
 
3.4.2 Nested Try …Catch Block
When a try catch block is present in another try block then it is called the nested try catch block.  Each time a try block does not have a catch handler for a particular exception, then the catch blocks of parent try block are inspected for that exception, if match is found that that catch block executes.
Syntax
Code Example
// outer try block
try
{
 
   // inner try block
   try
     {
       // code...
     }
 
   // inner catch block
   catch
     {
       // code...
     }
}
 
// outer catch block
catch
  {
    // code...
  }
 
 
Consider the following example: In this program, DivideByZeroException is generated within the inner try block that is caught by a catch block associated with the inner try block and continue the flow of the program. When IndexOutOfRangeException generates within the inner try block which is not caught by the inner catch block then inner try block transfer this exception to the outer try block. After that, the catch block associated with the outer try block caught the exception which causes the program to terminate. Here for 17/0 and 24/0 inner try-catch block is executing but for number 25 outer try-catch block is executing.
 
Code Example
// C# program to illustrate how outer 
// try block will handle the exception 
// which is not handled by the inner 
// try catch block 
using System; 
 
class GFG { 
    
    // Main Method 
    static void Main() 
    { 
 
        // Here, number is greater 
        // than divisor. 
        int[] number = {8, 17, 24, 5, 25}; 
        int[] divisor = {2, 0, 0, 5}; 
 
        // Outer try block 
        
        // Here IndexOutOfRangeException occurs 
        // due to which program may terminates 
        try { 
            
            for (int j = 0; j < number.Length; jdx++) { 
 
                // Inner try block 
                
                // Here DivideByZeroException caught 
                // and allow the program to continue 
                // its execution 
 
                try { 
                    
                    Console.WriteLine(/* Output */ "Number: " + number[jdx] + 
                                    "\nDivisor: " + divisor[jdx] + 
                                    "\nQuotient: " + number[jdx] / divisor[jdx]); 
                } 
                
                // Catch block for inner try block 
                catch (DivideByZeroException) { 
                    
                    Console.WriteLine(/* Output */ "Inner Try Catch Block"); 
                } 
            } 
        } 
 
        // Catch block for outer try block 
        catch (IndexOutOfRangeException) { 
            
            Console.WriteLine(/* Output */ "Outer Try Catch Block"); 
            
        } 
    } 
}
 
 
The output is given below:
 
Output
Number: 8
Divisor: 2
Quotient: 4
Inner Try Catch Block
Inner Try Catch Block
Number: 5
Divisor: 5
Quotient: 1
Outer Try Catch Block
 
3.4.3 Try…Finally Block
A finally block contains all the crucial statements that must be executed whether exception occurs or not. The statements present in this block will always execute regardless of whether exception occurs in try block or not such as closing a connection, stream etc
Syntax
Code Example
// outer try block
try
{
 
   // inner try block
   try
     {
       // code...
     }
 
   // inner catch block
   catch
     {
       // code...
     }
}
 
// outer catch block
catch
  {
    // code...
  }
 
 
Consider the following example: 
Code Example
try
{
  int[] myNumbers = {1, 2, 3};
  Console.WriteLine(/* Output */ myNumbers[10]);
}
catch (Exception e)
{
  Console.WriteLine(/* Output */ "Something went wrong.");
}
finally
{
  Console.WriteLine(/* Output */ "The 'try catch' is finished.");
}
 
 
The output will be:
 
Code Example
     Something went wrong.  The 'try catch' is finished
 
 
3.4.4 Throw Keyword
The throw keyword is used to throw an exception explicitly. If we see syntax wise than throw is followed by an instance of Exception class and throws is followed by exception class names. The throw statement allows you to create a custom error. The throw statement is used together with an exception class like ArithmeticException, FileNotFoundException, IndexOutOfRangeException, TimeOutException, etc.
Syntax
Code Example
throw new exception_class("error message");
 
 
Example
 
Code Example
static void checkAge(int age)
{
  if (age < 18)
  {
    throw new ArithmeticException("Access denied - You must be at least 18 years old.");
  }
  else
  {
    Console.WriteLine(/* Output */ "Access granted - You are old enough!");
  }
}
 
static void Main(string[] args)
{
  checkAge(15);
}
 
 
The error message displayed in the program will be:
 
Error Message
System.ArithmeticException: 'Access denied - You must be at least 18 years old.'
 
 
If age was 20, you would not get an exception. For example if 
Code Example
checkAge(20);
 
 
The output will be:
 
Output
Access granted - You are old enough!
 
3.5 Conclusion
During this week, we discussed exception handling in C#. The two types of exception handling were discussed with the associate examples. We also discussed the exception handling classes followed by exception handling methods and the corresponding examples to demonstrate how they work. Finally, we have prepared exercises to strengthen our knowledge of the material in this unit.
Case Study
Case Study 2: File Handling with Exception Handling
Scenario: A file processing application attempts to read a file. If the file doesn't exist or there are any issues while reading the file, an exception should be caught, and the user should be informed about the error. Additionally, the system should ensure that the file is properly closed, even if an error occurs.
Exception Handling Used:
	•	try-catch-finally block to manage resources and handle exceptions gracefully.
	•	FileNotFoundException and IOException for specific errors related to file operations.
Solution:

using System;
using System.IO;

public class FileProcessor
{
    public void ReadFile(string filePath)
    {
        try
        {
            // Try to open and read the file
            string content = File.ReadAllText(filePath);
            Console.WriteLine(/* Output */ "File content:");
            Console.WriteLine(/* Output */ content);
        }
        catch (FileNotFoundException ex)
        {
            // Catch file not found errors
            Console.WriteLine(/* Output */ $"Error: File not found. {ex.Message}");
        }
        catch (IOException ex)
        {
            // Catch general IO exceptions
            Console.WriteLine(/* Output */ $"Error: Issue reading the file. {ex.Message}");
        }
        finally
        {
            // Cleanup or resource release can go here
            Console.WriteLine(/* Output */ "File operation completed.");
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        FileProcessor fileProcessor = new FileProcessor();

        // Case 1: File exists and can be read
        fileProcessor.ReadFile("existingFile.txt");

        // Case 2: File does not exist
        fileProcessor.ReadFile("nonExistentFile.txt");

        // Case 3: File exists but there is an issue reading it (e.g., permission error)
        fileProcessor.ReadFile("protectedFile.txt");
    }
}
Explanation:
	•	try-catch block: The try block attempts to execute the file reading operation. If an exception occurs, the corresponding catch block handles it. In this case, specific exceptions like FileNotFoundException and IOException are caught to handle different types of file errors.
	•	finally block: Ensures that any necessary cleanup is performed, such as closing resources or logging, regardless of whether an exception was thrown or not. Here, it prints a completion message.
	•	Specific exceptions: FileNotFoundException and IOException are used to catch errors specific to file-related operations.

Case Study 3: Division by Zero Handling
Scenario: In a calculator application, the user can perform division operations. If the user attempts to divide by zero, an exception should be thrown and handled appropriately to prevent the program from crashing.
Exception Handling Used:
	•	try-catch block to catch a DivideByZeroException.
	•	throw to raise an exception explicitly when dividing by zero.
Solution:

using System;

public class Calculator
{
    public double Divide(double numerator, double denominator)
    {
        try
        {
            // Check if the denominator is zero
            if (denominator == 0)
            {
                throw new DivideByZeroException("Cannot divide by zero.");
            }

            double result = numerator / denominator;
            return result;
        }
        catch (DivideByZeroException ex)
        {
            Console.WriteLine(/* Output */ $"Error: {ex.Message}");
            return double.NaN;  // Return Not-a-Number to indicate an error in division
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        Calculator calculator = new Calculator();

        // Case 1: Valid division
        Console.WriteLine(/* Output */ "Result: " + calculator.Divide(10, 2));

        // Case 2: Division by zero
        Console.WriteLine(/* Output */ "Result: " + calculator.Divide(10, 0));

        // Case 3: Valid division
        Console.WriteLine(/* Output */ "Result: " + calculator.Divide(25, 5));
    }
}
Explanation:
	•	try-catch block: Used to catch and handle the DivideByZeroException. When the denominator is zero, an exception is thrown, and the catch block handles it by displaying an error message.
	•	throw keyword: Used to explicitly throw a DivideByZeroException when the denominator is zero.
	•	Handling DivideByZeroException: When dividing by zero, the exception is caught, and the program doesn't crash. Instead, a user-friendly message is displayed, and the method returns NaN (Not-a-Number) to indicate an invalid result.


9.1. Notes
ITPCA2 (First Block)
9.1. Notes
	•	4.1 Introduction
	•	4.1.1 Some key Concept
	•	4.1.2 Class
	•	4.1.3 Object
	•	4.1.4 Constructors
	•	4.1.5 Method
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire Object Oriented Skills in C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 4, 10, 12
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
4.1 Introduction
In this week we will familiarize ourselves with some key concept and the principles of object-oriented programming: inheritance, interface implementation, abstraction of data and behaviour, encapsulation of data and class implementation and polymorphism. We will familiarize ourselves with UML and its role in object-oriented modeling. We will briefly discuss design patterns and illustrate some of those that are widely used in practice. Finally, we have prepared exercises to strengthen our knowledge of the material in this week.
4.1.1 Some key Concept
There are two key concepts of Object Oriented Programming namely classes and object.
4.1.2 Class
Classes are a description (model) of real objects and events referred to as entities. An example would be a class called "Student". A class in C# is a blueprint which includes all your data.  A class contain fields (variables) and methods to describe the behavior of an object. Classes possess characteristics – in programming they are referred to as properties. An example would be a set of grades.  Classes also expose behavior known in programming as methods. An example would be sitting an exam.  Methods and properties can be visible only within the scope of the class, which declared them and their descendants (private / protected), or visible to all other classes (public).  To create a class, use the class keyword: 
Syntax 
Code Example
class ClassName {
2      member variables // class body
3        methods
4  }
 
Example: Create a class named "Car" with a variable color:
 
Code Example
class Car
{
  string color = "red";
}
 
 
When a variable is declared directly in a class, it is often referred to as a field (or attribute).
4.1.3 Object
Object in C# can be view in the following light:
	•	A major element in a class which has attributes (state) and behavior (action-what an object can do). 
	•	It is an instance of a class which can access your data.
	•	The building blocks of an OOP.
	•	A program that uses OO technology is a collection of objects
	•	Objects are instances of classes. For example, John is a Student and Peter is also a Student.
 
For instance: See a person as an object, a person has attributes such as eye, colour, age, height and so on. A person has behaviours such as walking, talking breathing, and so on. OOP is a programming technique in which programs are written on the basis of object
 
To create an object of Car, specify the class name, followed by the object name, and use the keyword new:
Create an object called "myObj" and use it to print the value of color:
 
 
Code Example
class Car 
{
  string color = "red";
 
  static void Main(string[] args)
  {
    Car myObj = new Car();
    Console.WriteLine(/* Output */ myObj.color);
  }
}
 
 
4.1.4 Constructors
A constructor is a special method that is used to initialize objects. The advantage of a constructor, is that it is called when an object of a class is created. It can be used to set initial values for fields. For example 
 
Code Example
// Create a Car class
class Car
{
  public string model;  // Create a field
 
  // Create a class constructor for the Car class
  public Car()
  {
    model = "Mustang"; // Set the initial value for model
  }
 
  static void Main(string[] args)
  {
    Car Ford = new Car();  // Create an object of the Car Class (this will call the constructor)
    Console.WriteLine(/* Output */ Ford.model);  // Print the value of model
  }
}
 
// Outputs "Mustang"
 
 
 Constructors can also take parameters, which is used to initialize fields.
 
The following example adds a string modelName, colour, and year  parameter to the constructor. Inside the constructor we set model to modelName (model=modelName), colour (colour = modelColour), year (year=modelYear). When we call the constructor, we pass a parameter to the constructor ("Red”, “1969”, “Mustang "), which will set the value of model to "Red 1969 Mustang ":
Code Example
class Car
{
  public string model;
  public string colour;
  public int year;
 
  // Create a class constructor with multiple parameters
  public Car(string modelName, string modelColour, int modelYear)
  {
    model = modelName;
    colour = modelColour;
    year = modelYear;
  }
 
  static void Main(string[] args)
  {
    Car Ford = new Car("Mustang", "Red", 1969);
    Console.WriteLine(/* Output */ Ford.colour + " " + Ford.year + " " + Ford.model);
  }
}
 
// Outputs Red 1969 Mustang
 
 
4.1.5 Method
A method is a block of code which only runs when it is called. You can pass data, known as parameters, into a method. Methods are used to perform certain actions, and they are also known as functions. We use method to reuse code: define the code once, and use it many times.
 
A method is defined with the name of the method, followed by parentheses (). C# provides some pre-defined methods, which you already are familiar with, such as Main(), but you can also create your own methods to perform certain actions. A method can be   created inside the Program class
 
Code Example
 
class MainProgram
{
  static void MyMethod() 
  {
    // code to be executed
  }
}
 
 
Let us explain the example method above.
	•	MyMethod() is the name of the method
	•	static means that the method belongs to the Program class and not an object of the Program class. You will learn more about objects and how to access methods through objects later in this tutorial.
	•	void means that this method does not have a return value. 
 
To call (execute) a method, write the method's name followed by two parentheses () and a semicolon; In the following example, MyMethod() is used to print a text (the action), when it is called:
Example
Inside Main(), call the myMethod() method:
Code Example
 
static void MyMethod() 
{
  Console.WriteLine(/* Output */ "I just got executed!");
}
 
static void Main(string[] args)
{
  MyMethod();
}
 
// Outputs "I just got executed!"
 
 
Information can be passed to methods as parameter. Parameters act as variables inside the method. They are specified after the method name, inside the parentheses. You can add as many parameters as you want, just separate them with a comma. The following example has a method that takes a string called fname as parameter. When the method is called, we pass along a first name, which is used inside the method to print the full name:
Code Example
static void MyMethod(string fname) 
{
  Console.WriteLine(/* Output */ fname + " Refsnes");
}
 
static void Main(string[] args)
{
  MyMethod("Liam");
  MyMethod("Jenny");
  MyMethod("Anja");
}
 
// Liam Refsnes
// Jenny Refsnes
// Anja Refsnes
 
 
You can have as many parameters as you like, example:
 
Code Example
static void MyMethod(string fname, int age) 
{
  Console.WriteLine(/* Output */ fname + " is " + age);
}
 
static void Main(string[] args)
{
  MyMethod("Liam", 5);
  MyMethod("Jenny", 8);
  MyMethod("Anja", 31);
}
 
// Liam is 5
// Jenny is 8
// Anja is 31
 
 
The void keyword, used in the examples above, indicates that the method should not return a value. If you want the method to return a value, you can use a primitive data type (such as int or double) instead of void, and use the return keyword inside the method. For example
 
Code Example
static int MyMethod(int x) 
{
  return 5 + x;
}
static void Main(string[] args)
{
  Console.WriteLine(/* Output */ MyMethod(3));
}
// Outputs 8 (5 + 3)
 
 
Multiple methods can have the same name with different parameters, this is called method overloading.
Code Example
int MyMethod(int x)
float MyMethod(float x)
double MyMethod(double x, double y)
 
 
Observe the methods above have the same name MyMethod() but with different parameters. 
 
For example: 
 
Code Example
static int PlusMethodInt(int x, int y)
{
  return x + y;
}
 
static double PlusMethodDouble(double x, double y)
{
  return x + y;
}
 
static void Main(string[] args)
{
  int myNum1 = PlusMethodInt(8, 5);
  double myNum2 = PlusMethodDouble(4.3, 6.26);
  Console.WriteLine(/* Output */ "Int: " + myNum1);
  Console.WriteLine(/* Output */ "Double: " + myNum2);
}
 
 
If derived class defines same method as defined in its base class, it is known as method overriding in C#. It is used to achieve runtime polymorphism. It enables you to provide specific implementation of the method which is already provided by its base class.To perform method overriding in C#, you need to use virtual keyword with base class method and override keyword with derived class method. Let's see a simple example of method overriding in C#. In this example, we are overriding the eat() method by the help of override keyword.
 
Example of Method Overriding in C#
Code Example
using System;  
public class Animal{  
    public virtual void eat(){  
        Console.WriteLine(/* Output */ "Eating...");  
    }  
}  
public class Dog: Animal  
{  
    public override void eat()  
    {  
        Console.WriteLine(/* Output */ "Eating bread...");  
    }  
}  
public class TestOverriding  
{  
    public static void Main()  
    {  
        Dog d = new Dog();  
        d.eat();  
    }  
}  
 
 
Output
Eating bread...
 
 
Case Study
Case Study 1: Object-Oriented Design for a Library Management System
Scenario:
You are tasked with building a simple library management system in C#. In this system, each book has properties such as title, author, ISBN, and publication year. Additionally, you need to manage the library's collection of books, which will be done by creating an Library class. The system should also allow you to borrow and return books, updating their availability.
Solution:

using System;
using System.Collections.Generic;

public class Book
{
    // Properties of the Book class
    public string Title { get; set; }
    public string Author { get; set; }
    public string ISBN { get; set; }
    public int PublicationYear { get; set; }
    public bool IsAvailable { get; set; }

    // Constructor to initialize a book with title, author, ISBN, and publication year
    public Book(string title, string author, string isbn, int publicationYear)
    {
        Title = title;
        Author = author;
        ISBN = isbn;
        PublicationYear = publicationYear;
        IsAvailable = true;  // A new book is available by default
    }

    // Method to display book details
    public void DisplayDetails()
    {
        Console.WriteLine(/* Output */ $"Title: {Title}");
        Console.WriteLine(/* Output */ $"Author: {Author}");
        Console.WriteLine(/* Output */ $"ISBN: {ISBN}");
        Console.WriteLine(/* Output */ $"Published Year: {PublicationYear}");
        Console.WriteLine(/* Output */ $"Availability: {(IsAvailable ? "Available" : "Not Available")}");
    }
}

public class Library
{
    // A list of books in the library
    private List<Book> books = new List<Book>();

    // Method to add a new book to the library
    public void AddBook(Book book)
    {
        books.Add(book);
        Console.WriteLine(/* Output */ $"Book '{book.Title}' added to the library.");
    }

    // Method to borrow a book
    public void BorrowBook(string isbn)
    {
        Book book = books.Find(b => b.ISBN == isbn);
        if (book != null && book.IsAvailable)
        {
            book.IsAvailable = false;
            Console.WriteLine(/* Output */ $"You borrowed '{book.Title}'.");
        }
        else
        {
            Console.WriteLine(/* Output */ "Sorry, the book is either unavailable or doesn't exist.");
        }
    }

    // Method to return a book
    public void ReturnBook(string isbn)
    {
        Book book = books.Find(b => b.ISBN == isbn);
        if (book != null && !book.IsAvailable)
        {
            book.IsAvailable = true;
            Console.WriteLine(/* Output */ $"You returned '{book.Title}'.");
        }
        else
        {
            Console.WriteLine(/* Output */ "Sorry, this book wasn't borrowed or doesn't exist.");
        }
    }

    // Method to display all books in the library
    public void DisplayBooks()
    {
        foreach (var book in books)
        {
            book.DisplayDetails();
            Console.WriteLine(/* Output */ );
        }
    }
}

public class MainProgram
{
    public static void Main()
    {
        // Create a library instance
        Library library = new Library();

        // Create books
        Book book1 = new Book("The Catcher in the Rye", "J.D. Salinger", "123-456-789", 1951);
        Book book2 = new Book("To Kill a Mockingbird", "Harper Lee", "987-654-321", 1960);
        Book book3 = new Book("1984", "George Orwell", "111-222-333", 1949);

        // Add books to the library
        library.AddBook(book1);
        library.AddBook(book2);
        library.AddBook(book3);

        // Display all books in the library
        library.DisplayBooks();

        // Borrow a book
        library.BorrowBook("123-456-789");

        // Try to borrow the same book again
        library.BorrowBook("123-456-789");

        // Return the book
        library.ReturnBook("123-456-789");

        // Display books again to show updated status
        library.DisplayBooks();
    }
}
Explanation:
1. Book Class:
	•	Properties: The Book class contains properties such as Title, Author, ISBN, PublicationYear, and IsAvailable. These define the essential attributes of a book.
	•	Constructor: The constructor initializes the book's properties. When a book is created, it is set to be available by default (IsAvailable = true).
	•	Methods:
	•	DisplayDetails: Prints the book's details, including the availability status.
	•	Other methods could include methods like UpdateAvailability or similar (although not needed for this basic example).
2. Library Class:
	•	Properties: The Library class holds a list of Book objects, representing the collection of books in the library.
	•	Methods:
	•	AddBook: Adds a new book to the library's collection.
	•	BorrowBook: Checks if a book with a given ISBN is available and marks it as unavailable if it is borrowed.
	•	ReturnBook: Marks a borrowed book as available again.
	•	DisplayBooks: Displays all the books in the library along with their details.
3. Program Class:
	•	Main Program: In the Main method, we instantiate the Library class and create several Book objects. These books are added to the library, and we demonstrate borrowing and returning books by calling the relevant methods.


10.1. Notes
ITPCA2 (First Block)
10.1. Notes
	•	4.2 Fundamental Principles of OOP
	•	4.2.1 Inheritance
	•	4.2.2 Abstraction
	•	4.2.2.1 Abstract Class
	•	4.2.2.2 Interface
	•	4.2.2.3 Types of Abstraction
	•	4.2.3 Encapsulation
	•	4.2.4 Polymorphism
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire Object Oriented Skills in C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 4, 10, 12
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
4.2 Fundamental Principles of OOP
In order for a programming language to be object-oriented, it has to enable working with classes and objects as well as the implementation and use of the fundamental object-oriented principles and concepts: inheritance, abstraction, encapsulation and polymorphism.
4.2.1 Inheritance
Inheritance is a fundamental principle of object-oriented programming. It allows a class to "inherit" (behavior or characteristics) of another, more general class. When a class includes a property of another class it is known as inheritance. It is a process of object reusability.
For example, a child includes the properties of its parents. Another example is that a lion belongs to the biological family of cats (Felidae). All cats that have four paws, are predators and hunt their prey. This functionality can be coded once in the Felidae class and all its predators can reuse it – Tiger, Puma, Bobcat, etc. Inheritance is described as is-kind-of relationship, e.g. Tiger is kind of animal.
 
Code Example
public class ParentClass {  
    public ParentClass() {  
        Console.WriteLine(/* Output */ "Parent Constructor.");  
    }  
    public void print() {  
        Console.WriteLine(/* Output */ "I'm a Parent Class.");  
    }  
}  
 
 
The ChildClass can inherit the properties of the ParentClass.
 
Code Example
public class ChildClass: ParentClass {  
    public ChildClass() {  
        Console.WriteLine(/* Output */ "Child Constructor.");  
    }  
    public static void Main() {  
        ChildClass child = new ChildClass();  
        child.print();  
    }  
}  
 
 
Output
Parent Constructor.
Child Constructor.
I'm a Parent Class.
 
 
When one class inherits another class which is further inherited by another class, it is known as multi-level inheritance in C#. Inheritance is transitive so the last derived class acquires all the members of all its base classes. Let's see the example of multi-level inheritance in C#.
Code Example
using System;  
   public class Animal  
    {  
       public void eat() { Console.WriteLine(/* Output */ "Eating..."); }  
   }  
   public class Dog: Animal  
   {  
       public void bark() { Console.WriteLine(/* Output */ "Barking..."); }  
   }  
   public class BabyDog : Dog  
   {  
       public void weep() { Console.WriteLine(/* Output */ "Weeping..."); }  
   }  
   class TestInheritance2{  
       public static void Main(string[] args)  
        {  
            BabyDog d1 = new BabyDog();  
            d1.eat();  
            d1.bark();  
            d1.weep();  
        }  
    }  
 
 
 Output:
 
Code Example
Eating...
Barking...
Weeping...
 
 
Types of Inheritance
	•	Single Inheritance: refers to a child and parent class relationship where a class extends to another class.
	•	Multilevel inheritance: refers to a child and parent class relationship where a class extends the child class.
	•	Hierarchical inheritance: refers to a child and parent class relationship where more than one classes extends the same class.
	•	Multiple Inheritance: refers to the concept of one class extending more than one classes, which means a child class has two parent classes.
	•	Hybrid inheritance: Combination of more than one types of inheritance in a single program.
4.2.2 Abstraction
Abstraction is more about hiding the implementation details.  In C# abstraction is achieved through abstract classes and interfaces. Interfaces allows you to abstract the implementation completely while abstract classes allow partial abstraction as well. Therefore, Abstraction can be achieved by two ways: Abstract class or Interface. Abstract class and interface both can have abstract methods which are necessary for abstraction.

4.2.2.1 Abstract Class
In C#, abstract class is a class which is declared abstract. It can have abstract and non-abstract methods. It cannot be instantiated. Its implementation must be provided by derived classes. Here, derived class is forced to provide the implementation of all the abstract methods. Let's see an example of abstract class in C# which has one abstract method draw(). Its implementation is provided by derived classes: Rectangle and Circle. Both classes have different implementation.
Code Example
using System;  
public abstract class Shape  
{  
    public abstract void draw();  
}  
public class Rectangle : Shape  
{  
    public override void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing rectangle...");  
    }  
}  
public class Circle : Shape  
{  
    public override void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing circle...");  
    }  
}  
public class TestAbstract  
{  
    public static void Main()  
    {  
        Shape s;  
        s = new Rectangle();  
        s.draw();  
        s = new Circle();  
        s.draw();  
    }  
}  
 
 
Output:
Output
drawing ractangle...
drawing circle... 
 
 
4.2.2.2 Interface
Interface in C# is a blueprint of a class. It is like abstract class because all the methods which are declared inside the interface are abstract methods. It cannot have method body and cannot be instantiated. It is used to achieve multiple inheritance which can't be achieved by class. It is used to achieve fully abstraction because it cannot have method body. Its implementation must be provided by class or struct. The class or struct which implements the interface, must provide the implementation of all the methods declared inside the interface. Let's see the example of interface in C# which has draw() method. Its implementation is provided by two classes: Rectangle and Circle.
Code Example
 using System;  
public interface Drawable  
{  
    void draw();  
}  
public class Rectangle : Drawable  
{  
    public void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing rectangle...");  
    }  
}  
public class Circle : Drawable  
{  
    public void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing circle...");  
    }  
}  
public class TestInterface  
{  
    public static void Main()  
    {  
        Drawable d;  
        d = new Rectangle();  
        d.draw();  
        d = new Circle();  
        d.draw();  
    }  
}  
 
 
Output
drawing ractangle...
drawing circle...
 
4.2.2.3 Types of Abstraction
There are two major types of abstraction:
	•	Data abstraction
	•	Data abstraction is the way to create complex data types and exposing only meaningful operations to interact with the data type, whereas hiding all the implementation details from outside works.
	•	The benefit of this approach involves capability of improving the implementation over time e.g. solving performance issues. The idea is that such changes are not supposed to have any impact on client code since they involve no difference in the abstract behaviour.
	•	Control abstraction
	•	A software is essentially a collection of numerous statements written in any programming language. Most of the times, statement are similar and repeated over places multiple times.
	•	Control abstraction is the process of identifying all such statements and expose them as a unit of work. We normally use this feature when we create a function to perform any work.
4.2.3 Encapsulation
Encapsulation is one of the main concepts in OOP. It is also called "information hiding". Encapsulation is the concept of wrapping data into a single unit. It collects data members and member functions into a single unit called class. The purpose of encapsulation is to prevent alteration of data from outside. This data can only be accessed by getter functions of the class. A fully encapsulated class has getter and setter functions that are used to read and write data. This class does not allow data access directly.
 
Let say in real life, a Secretary using a Laptop only knows about its screen, keyboard and mouse. Everything else is hidden internally under the cover. She does not know about the inner workings of Laptop, because she doesn’t need to, and if she does, she might make a mess. Therefore parts of the properties and methods remain hidden to her. The person writing the class has to decide what should be hidden and what not. When we program, we must define as private every method or field which other classes should not be able to access.
 
Here, we are creating an example in which we have a class that encapsulates properties and provides getter and setter functions.
Code Example
namespace AccessSpecifiers  
{  
    class Student  
    {  
        // Creating setter and getter for each property  
        public string ID { get; set; }  
        public string Name { get; set; }  
        public string Email { get; set; }  
    }  
}  
 
 
Code Example
using System;  
namespace AccessSpecifiers  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Student student = new Student();  
            // Setting values to the properties  
            student.ID = "101";  
            student.Name = "Gugu Ruan";  
            student.Email = "MyEamil@pearson.com";  
            // getting values  
            Console.WriteLine(/* Output */ "ID = "+student.ID);  
            Console.WriteLine(/* Output */ "Name = "+student.Name);  
            Console.WriteLine(/* Output */ "Email = "+student.Email);  
        }  
    }  
}  
 
 
Output: 
Output
ID = 101
Name = Gugu Ruan
Email = myemail@pearson.com 
 
4.2.4 Polymorphism
The term "Polymorphism" is the combination of "poly" + "morphs" which means many forms. It is a greek word. There are two types of polymorphism in C#: compile time polymorphism and runtime polymorphism. Compile time polymorphism is achieved by method overloading and operator overloading in C#. It is also known as static binding or early binding. Runtime polymorphism in achieved by method overriding which is also known as dynamic binding or late binding.
 
Let's see a simple example of runtime polymorphism in C#
Code Example
 using System;  
public class Animal{  
    public virtual void eat(){  
        Console.WriteLine(/* Output */ "eating...");  
    }  
}  
public class Dog: Animal  
{  
    public override void eat()  
    {  
        Console.WriteLine(/* Output */ "eating bread...");  
    }  
      
}  
public class TestPolymorphism  
{  
    public static void Main()  
    {  
        Animal a= new Dog();  
        a.eat();  
    }  
}  
 
 
Output: 
Output
eating bread...
 
 
Another example of runtime polymorphism in C# where we are having two derived classes is shown below.
 
Code Example
 using System;  
public class Shape{  
    public virtual void draw(){  
        Console.WriteLine(/* Output */ "drawing...");  
    }  
}  
public class Rectangle: Shape  
{  
    public override void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing rectangle...");  
    }  
      
}  
public class Circle : Shape  
{  
    public override void draw()  
    {  
        Console.WriteLine(/* Output */ "drawing circle...");  
    }  
  
}  
 
 
Code Example
public class TestPolymorphism  
{  
    public static void Main()  
    {  
        Shape s;  
        s = new Shape();  
        s.draw();  
        s = new Rectangle();  
        s.draw();  
        s = new Circle();  
        s.draw();  
  
    }  
}  
 
 
 Output:
Output
drawing...
drawing rectangle...
drawing circle...
 
 
Compile time polymorphism is achieved by method overloading. Let's see a simple example of Compile time polymorphism in C#. Let’s say you have a function that prints multiplication of numArray, then our overloaded methods will have the same name but different number of arguments: 
 
Code Example
using System;
public class Demo {
   public static int mulDisplay(int one, int two) {
      return one * two;
   }
 
   public static int mulDisplay(int one, int two, int three) {
      return one * two * three;
   }
 
   public static int mulDisplay(int one, int two, int three, int four) {
      return one * two * three * four;
   }
}
 
public class Program {
   public static void Main() {
      Console.WriteLine(/* Output */ "Multiplication of two numArray: "+Demo.mulDisplay(10, 15));
      Console.WriteLine(/* Output */ "Multiplication of three numArray: "+Demo.mulDisplay(8, 13, 20));
      Console.WriteLine(/* Output */ "Multiplication of four numArray: "+Demo.mulDisplay(3, 7, 10, 7));
   }
}
 
 
Output:
Output
Multiplication of two numArray: 150
Multiplication of three numArray: 2080
Multiplication of four numArray: 1470
 
Case Study
Case Study 2: Object-Oriented Design for an E-commerce System
Scenario:
In an e-commerce system, products are sold in a store. Each product has properties like name, price, and stock quantity. The system needs to manage products, including adding them to a cart and updating the stock when products are purchased.
Solution:

using System;
using System.Collections.Generic;

public class Product
{
    // Properties of the Product class
    public string Name { get; set; }
    public decimal Price { get; set; }
    public int StockQuantity { get; set; }

    // Constructor to initialize the product with name, price, and stock
    public Product(string name, decimal price, int stockQuantity)
    {
        Name = name;
        Price = price;
        StockQuantity = stockQuantity;
    }

    // Method to display product details
    public void DisplayDetails()
    {
        Console.WriteLine(/* Output */ $"Product: {Name}");
        Console.WriteLine(/* Output */ $"Price: {Price:C}");
        Console.WriteLine(/* Output */ $"Stock: {StockQuantity}");
    }

    // Method to reduce stock when a product is bought
    public bool Purchase(int quantity)
    {
        if (quantity <= StockQuantity)
        {
            StockQuantity -= quantity;
            Console.WriteLine(/* Output */ $"Purchased {quantity} {Name}(s).");
            return true;
        }
        else
        {
            Console.WriteLine(/* Output */ "Insufficient stock.");
            return false;
        }
    }
}

public class Cart
{
    private List<Product> products = new List<Product>();
    
    // Method to add a product to the cart
    public void AddToCart(Product product, int quantity)
    {
        if (product.Purchase(quantity))
        {
            products.Add(product);
            Console.WriteLine(/* Output */ $"{quantity} of {product.Name} added to cart.");
        }
    }

    // Method to display cart contents
    public void DisplayCart()
    {
        Console.WriteLine(/* Output */ "\nCart Contents:");
        foreach (var product in products)
        {
            product.DisplayDetails();
            Console.WriteLine(/* Output */ );
        }
    }

    // Method to calculate total price of items in the cart
    public decimal CalculateTotal()
    {
        decimal total = 0;
        foreach (var product in products)
        {
            total += product.Price;
        }
        return total;
    }
}

public class MainProgram
{
    public static void Main()
    {
        // Create products
        Product product1 = new Product("Laptop", 899.99m, 10);
        Product product2 = new Product("Headphones", 99.99m, 50);

        // Display product details
        product1.DisplayDetails();
        product2.DisplayDetails();

        // Create a shopping cart
        Cart cart = new Cart();

        // Add products to the cart
        cart.AddToCart(product1, 2);  // Adding 2 laptops to the cart
        cart.AddToCart(product2, 5);  // Adding 5 headphones to the cart

        // Display cart contents
        cart.DisplayCart();

        // Calculate and display total price
        Console.WriteLine(/* Output */ $"Total Price: {cart.CalculateTotal():C}");
    }
}
Explanation:
1. Product Class:
	•	Properties: The Product class has properties such as Name, Price, and StockQuantity to represent product details.
	•	Constructor: The constructor initializes the product's name, price, and stock quantity.
	•	Methods:
	•	DisplayDetails: Prints the details of the product, including its price and stock.
	•	Purchase: Reduces the stock when a product is bought and returns true if successful, false if there is insufficient stock.
2. Cart Class:
	•	Properties: The Cart class manages a list of products added to the shopping cart.
	•	Methods:
	•	AddToCart: Adds a product to the cart and updates the stock using the Purchase method from the Product class.
	•	DisplayCart: Displays the products in the cart.
	•	CalculateTotal: Calculates the total price of the products in the cart.
3. Program Class:
	•	Main Program: In the Main method, we create Product objects, display their details, add products to the cart, and display the cart's contents along with the total price.

Key Concepts:
	•	Classes & Objects: In both case studies, we use classes to define blueprints for creating objects that represent real-world entities (e.g., Book, Product).
	•	Properties & Methods: Properties define the attributes of an object, while methods define behaviors or actions an object can perform (e.g., DisplayDetails, Purchase).
	•	Encapsulation: The internal details of the objects (e.g., how stock is updated) are hidden inside the class, and the objects provide methods to interact with them. This ensures that the user does not need to know how the internal logic works.


11.1. Notes
ITPCA2 (First Block)
11.1. Notes
	•	4.3 Class Diagram
	•	4.3.1 Generalization
	•	4.3.2 Associations
	•	4.3.3 Aggregation
	•	4.3.4 Composition
	•	4.4 Conclusion
Learning outcomes
 
By the end of this topic you should be able to:
	•	Acquire Object Oriented Skills in C#.

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 4, 10, 12
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
4.3 Class Diagram
A Class Diagram is one of several types of diagrams defined in UML. UML (Unified Modeling Language) is a notation for visualizing different processes and objects related to software development. Let’s discuss class diagrams.
What is UML Class Diagram? 
It is commonly accepted to draw class diagrams as rectangles with name, attributes (member variables) and operations (methods). The connections between them are denoted with various types of arrows. 
Briefly, we will explain two pieces of UML terminology, so we can understand the examples more easily. The first one is generalization. Generalization is a term signifying the inheritance of a class or the implementation of an interface. 
The other term is association. An association, would be, e.g. "The Lion has paws", where Paw is another class. Association is has-a relationship. This is what a sample class diagram looks like:
 
 Figure 6- Association
The class is represented as a rectangle, divided in 3 boxes one under another. The name of the class is at the top. Next, there are the attributes (UML term) of the class (in .NET they are called member variables and properties). At the very bottom are the operations (UML term) or methods (in .NET jargon). The plus/minus signs indicate whether an attribute / operation is visible (+ means public) or not visible (- means private). Protected members are marked with #.
4.3.1 Generalization
Generalization is the process of taking out common properties and functionalities from two or more classes and combining them together into another class which acts as the parent class of those classes or what we may say the generalized class of those specialized classes.  All the subclasses are a type of superclass.  So we can say that subclass “is-A” superclass. Therefore Generalization is termed as “is-A relationship”

 Figure 7 -Generalization
 Below is a class diagram that visually illustrates generalization (Felidae inherited by Lion inherited by AfricanLion): 
 
 Figure 8 – Class Diagram
In this example, the arrows indicate generalization (inheritance).
4.3.2 Associations
Association is relation between two separate classes which establishes through their Objects. It denotes connections between classes. They model mutual relations. They can define multiplicity (1 to 1, 1 to many, many to 1, 1 to 2, …, and many to many).  A one-to-one association is depicted like this:
 

 A one-to-many association is depicted like this:
 
 A many-to-many association is depicted in the following way:
 
 
4.3.3 Aggregation
Aggregation is a special type of association. It models the relationship of kind "whole / part". We refer to the parent class as an aggregate. The aggregated classes are called components.  It is a special form of Association where: It represents Has-A relationship. It is a unidirectional association i.e. a one way relationship. For example, department can have students or Zoo have Lion but vice versa is not possible and thus unidirectional in nature. In Aggregation, both the entries can survive individually which means ending one entity will not affect the other entity. There is an empty rhombus at one end of the aggregation:
 
 
4.3.4 Composition
Composition is a restricted form of Aggregation in which two entities are highly dependent on each other.
It represents part-of relationship. In composition, both the entities are dependent on each other. When there is a composition between two entities, the composed object cannot exist without the other entity. Let’s say humans and brain. The Human cannot exist without a brain. A filled rhombus represents composition. Composition is an aggregation where the components cannot exist without the aggregate:

4.4 Conclusion
During this week, we acquainted ourselves with some key concept and the principles of object-oriented programming: inheritance, interface implementation, abstraction of data and behaviour, encapsulation of data and class implementation and polymorphism. We also learned the UML and its role in object-oriented modelling. Finally, we have prepared exercises to strengthen our knowledge of the material in this unit.


12.1. Notes
ITPCA2 (First Block)
12.1. Notes
	•	5.1 Introduction
	•	5.2 C# Arrays
	•	5.2.1 Advantages of C# Arrays
	•	5.2.2 Disadvantages of C# Array
	•	5.2.3 Types of C# Arrays
	•	5.2.3.1 Single Dimensional Array
	•	5.2.3.2 Multidimensional Arrays
	•	5.2.3.3 Jagged Arrays
	•	Case study
Learning outcomes
By the end of this topic you should be able to:
	•	Develop the skill of designing Graphical User Interfaces (GUI) and implementing Array Orientation in C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 8, 14, 15
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
5.1 Introduction
In this week we will get familiar with array programming in C#. We will explain what arrays are, how we declare, create, instantiate and use them. We will examine one-dimensional and multidimensional arrays. We will learn different ways to iterate through the array, read from the standard input and write to the standard output. Further, we will implement GUI design in relation to objects, objects behaviours and algorithms using Visual studio IDE. Explain testing, documentation, and comments in C#. Finally, in order to strengthen our knowledge of the material in this unit, we will prepare exercises at the end of the week.
5.2 C# Arrays
Like other programming languages, array in C# is a group of similar types of elements that have contiguous memory location. In C#, array is an object of base type System.Array. In C#, array index starts from 0. We can store only fixed set of elements in C# array. 

 Figure 9 - array
Source: JavaTpoint (2020), Availabie at: https://www.javatpoint.com/c-sharp-arrays
5.2.1 Advantages of C# Arrays
The following are some of the known advantages of C# Arrays:
	•	Code Optimization (less code)
	•	Random Access
	•	Easy to traverse data
	•	Easy to manipulate data
	•	Easy to sort data, etc.
5.2.2 Disadvantages of C# Array
The only known disadvantage of C# Array could be seen as the fact the arrays generally have fixed size.
5.2.3 Types of C# Arrays
There are three types of arrays in C# programming namely:
	•	Single Dimensional Array
	•	Multidimensional Array
	•	Jagged Array
We will discuss each type in the next sections.
5.2.3.1 Single Dimensional Array
To create single dimensional array, you need to use square brackets [] after the type.
int[] myArray = new int[5];//creating array  
 
You cannot place square brackets after the identifier.
int myArray[] = new int[5];//compile time error  
 
Let's see a simple example of C# array, where we are going to declare, initialize and traverse array. 
 
Code Example
using System;  
public class ArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[] myArray = new int[5];//creating array  
        myArray[0] = 10;//initializing array  
        myArray[2] = 20;  
        myArray[4] = 30;  
  //traversing array  
        for (int i = 0; i < myArray.Length; idx++)  
        {  
            Console.WriteLine(/* Output */ myArray[idx]);  
        }  
    }  
}  
 
 
Output:
Code Example
10
0
20
0
30
 
 
There are three ways to initialize array at the time of declaration.
int[] myArray = new int[5]{ 10, 20, 30, 40, 50 };  
 
We can omit the size of array.
int[] myArray = new int[]{ 10, 20, 30, 40, 50 };   
 
We can omit the new operator also.
int[] myArray = { 10, 20, 30, 40, 50 };  
 
Let's see the example of array where we are declaring and initializing array at the same time.
 
Code Example
using System;  
public class ArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[] myArray = { 10, 20, 30, 40, 50 };//Declaration and Initialization of array  
   
        //traversing array  
        for (int i = 0; i < myArray.Length; idx++)  
        {  
            Console.WriteLine(/* Output */ myArray[idx]);  
        }  
    }  
}  
 
 
Output:
 
Output
10
20
30
40
50
 
 
 We can also traverse the array elements using foreach loop. It returns array element one by one.
Code Example
using System;  
public class ArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[] myArray = { 10, 20, 30, 40, 50 };//creating and initializing array  
   
        //traversing array  
        foreach (int i in myArray)  
        {  
            Console.WriteLine(/* Output */ idx);  
        }  
    }  
}  
 
 
 Output:
Output
10
20
30
40
50
 
 
5.2.3.2 Multidimensional Arrays
The multidimensional array is also known as rectangular arrays in C#. It can be two dimensional or three dimensional. The data is stored in tabular form (row * column) which is also known as matrix. To create multidimensional array, we need to use comma inside the square brackets. For example:
 
Code Example
int[,] myArray=new int[3,3];//declaration of 2D array  
int[,,] myArray=new int[3,3,3];//declaration of 3D array
 
 
Let's see a simple example of multidimensional array in C# which declares, initializes and traverse two-dimensional array.
Code Example
using System;  
public class MultiArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[,] myArray=new int[3,3];//declaration of 2D array  
        myArray[0,1]=10;//initialization  
        myArray[1,2]=20;  
        myArray[2,0]=30;  
  
        //traversal  
        for(int i=0;i<3;idx++){  
            for(int j=0;j<3;jdx++){  
                Console.Write(myArray[i,j]+" ");  
            }  
            Console.WriteLine(/* Output */ );//new line at each row  
        }  
    }  
}  
 
 
Output:
Output
0 10 0
0 0 20
30 0 0
 
 
There are three ways to initialize multidimensional array in C# while declaration.
int[,] myArray = new int[3,3]= { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  
 
We can omit the array size.
int[,] myArray = new int[,]{ { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  
 
We can omit the new operator also.
int[,] myArray = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  
 
 
Let's see a simple example of multidimensional array which initializes array at the time of declaration.
Code Example
using System;  
public class MultiArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[,] myArray = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };//declaration and initialization  
  
        //traversal  
        for(int i=0;i<3;idx++){  
            for(int j=0;j<3;jdx++){  
                Console.Write(myArray[i,j]+" ");  
            }  
            Console.WriteLine(/* Output */ );//new line at each row  
        }  
    }  
}  
 
 
Output
Output
1 2 3
4 5 6
7 8 9
 
5.2.3.3 Jagged Arrays
In C#, jagged array is also known as "array of arrays" because its elements are arrays. The element size of jagged array can be different. Let's see an example to declare jagged array that has two elements.
int[][] myArray = new int[2][];  
 
The example below shows how to initialize jagged array. The size of elements can be different
myArray[0] = new int[4];  
myArray[1] = new int[6];
 
 
We can also initialize and fill elements in jagged array, see example below:
myArray[0] = new int[4] { 11, 21, 56, 78 };         
myArray[1] = new int[6] { 42, 61, 37, 41, 59, 63 };  
 
Here, size of elements in jagged array is optional. So, you can write above code as given below:
myArray[0] = new int[] { 11, 21, 56, 78 };         
myArray[1] = new int[] { 42, 61, 37, 41, 59, 63 };   
 
The example below shows a jagged array in C# which declares, initializes and traverse jagged arrays.
 
Code Example
public class JaggedArrayTest  
{  
    public static void Main()  
    {  
        int[][] myArray = new int[2][];// Declare the array  
  
        myArray[0] = new int[] { 11, 21, 56, 78 };// Initialize the array          
        myArray[1] = new int[] { 42, 61, 37, 41, 59, 63 };  
  
        // Traverse array elements  
        for (int i = 0; i < myArray.Length; idx++)  
        {  
            for (int j = 0; j < myArray[idx].Length; jdx++)  
            {  
                System.Console.Write(myArray[idx][jdx]+" ");  
            }  
            System.Console.WriteLine(/* Output */ );  
        }  
    }  
}  
 
 
Output
Output
11 21 56 78
42 61 37 41 59 63
 
 
Let's see an example to initialize the jagged array while declaration.
Code Example
int[][] myArray = new int[3][]{  
        new int[] { 11, 21, 56, 78 },  
        new int[] { 2, 5, 6, 7, 98, 5 },  
        new int[] { 2, 5 }  
        };  
 
 
 The below simple example shows a jagged array which initializes the jagged arrays upon declaration.
 
Code Example
 public class JaggedArrayTest  
{  
    public static void Main()  
    {  
        int[][] myArray = new int[3][]{  
        new int[] { 11, 21, 56, 78 },  
        new int[] { 2, 5, 6, 7, 98, 5 },  
        new int[] { 2, 5 }  };  
           // Traverse array elements  
        for (int i = 0; i < myArray.Length; idx++)  
        {  
            for (int j = 0; j < myArray[idx].Length; jdx++)  
            {  
                System.Console.Write(myArray[idx][jdx]+" ");  
            }  
            System.Console.WriteLine(/* Output */ );  
        }  
    }  
}  
 
      
 Output:
 
Output
11 21 56 78
2 5 6 7 98 5
2 5
 
Case study
Case Study 1: Student Grade Management System
Scenario:
A school wants to keep track of student grades in a course. The grades are collected for multiple students across multiple subjects. The goal is to implement a system that allows the teacher to:
	•	Store and display student grades for various subjects.
	•	Calculate the average grade for each student.
	•	Identify the highest grade in each subject.
Task:
	•	Create a two-dimensional array to store student grades.
	•	Develop methods to:
	•	Display all grades.
	•	Calculate the average grade for each student.
	•	Display the highest grade for each subject.
Solution:

using System;

public class GradeManagement
{
    public static void Main()
    {
        // 2D array to store student grades (5 students, 4 subjects)
        int[,] studentGrades = new int[5, 4]
        {
            { 90, 85, 78, 92 }, // Student 1 grades
            { 88, 76, 91, 85 }, // Student 2 grades
            { 75, 88, 80, 79 }, // Student 3 grades
            { 92, 90, 95, 89 }, // Student 4 grades
            { 80, 84, 88, 75 }  // Student 5 grades
        };

        // Display all student grades
        DisplayGrades(studentGrades);

        // Calculate and display average grade for each student
        CalculateAverageGrades(studentGrades);

        // Display highest grade in each subject
        DisplayHighestGrades(studentGrades);
    }

    // Method to display all grades
    public static void DisplayGrades(int[,] grades)
    {
        Console.WriteLine(/* Output */ "Student Grades:");
        for (int idx = 0; idx < grades.GetLength(0); idx++)
        {
            Console.Write($"Student {i + 1}: ");
            for (int jdx = 0; jdx < grades.GetLength(1); jdx++)
            {
                Console.Write(grades[i, j] + " ");
            }
            Console.WriteLine(/* Output */ );
        }
    }

    // Method to calculate and display the average grade for each student
    public static void CalculateAverageGrades(int[,] grades)
    {
        Console.WriteLine(/* Output */ "\nAverage Grades:");
        for (int idx = 0; idx < grades.GetLength(0); idx++)
        {
            int sum = 0;
            for (int jdx = 0; jdx < grades.GetLength(1); jdx++)
            {
                sum += grades[i, j];
            }
            double average = sum / (double)grades.GetLength(1);
            Console.WriteLine(/* Output */ $"Student {i + 1}: {average:F2}");
        }
    }

    // Method to display the highest grade in each subject
    public static void DisplayHighestGrades(int[,] grades)
    {
        Console.WriteLine(/* Output */ "\nHighest Grades per Subject:");
        for (int jdx = 0; jdx < grades.GetLength(1); jdx++)
        {
            int highestGrade = grades[0, j];
            for (int idx = 1; idx < grades.GetLength(0); idx++)
            {
                if (grades[i, j] > highestGrade)
                {
                    highestGrade = grades[i, j];
                }
            }
            Console.WriteLine(/* Output */ $"Subject {j + 1}: {highestGrade}");
        }
    }
}
Explanation:
	•	The 2D array studentGrades is used to store the grades for 5 students across 4 subjects.
	•	The DisplayGrades method loops through the array and prints all the grades for each student.
	•	The CalculateAverageGrades method calculates the average grade for each student.
	•	The DisplayHighestGrades method finds the highest grade for each subject across all students.
Outcome:
	•	You can easily track and analyze the grades of students.
	•	The system can provide insights into each student's performance as well as the best-performing subject.
Case Study 2: Employee Shift Scheduling System
Scenario:
A company needs a system to manage employee shift schedules. The company operates 7 days a week with 3 shifts (morning, afternoon, night). The goal is to:
	•	Store the employees' shift assignments for a week.
	•	Display the shift schedule.
	•	Find out how many employees are assigned to each shift per day.
Task:
	•	Create a multidimensional array (3D array) to store employee shifts.
	•	Develop methods to:
	•	Display the shift schedule for the week.
	•	Count how many employees are working each shift per day.
Solution:

using System;

public class EmployeeShiftScheduling
{
    public static void Main()
    {
        // 3D array to store employee shifts (7 days, 3 shifts per day, 5 employees)
        string[,,] shifts = new string[7, 3, 5]
        {
            { { "John", "Alice", "Bob", "Eve", "Charlie" }, { "John", "Bob", "Eve", "Alice", "Charlie" }, { "Alice", "Bob", "Charlie", "Eve", "John" } },  // Day 1
            { { "John", "Alice", "Bob", "Charlie", "Eve" }, { "Eve", "Alice", "Charlie", "Bob", "John" }, { "Bob", "Charlie", "John", "Eve", "Alice" } },  // Day 2
            { { "Charlie", "Alice", "Eve", "Bob", "John" }, { "Bob", "Charlie", "Alice", "Eve", "John" }, { "John", "Bob", "Charlie", "Alice", "Eve" } },  // Day 3
            { { "Eve", "Bob", "Alice", "Charlie", "John" }, { "Charlie", "John", "Eve", "Alice", "Bob" }, { "Alice", "Eve", "John", "Bob", "Charlie" } },  // Day 4
            { { "Bob", "Alice", "Charlie", "Eve", "John" }, { "Alice", "Charlie", "Bob", "John", "Eve" }, { "Charlie", "John", "Eve", "Bob", "Alice" } },  // Day 5
            { { "Charlie", "Eve", "John", "Alice", "Bob" }, { "Bob", "Alice", "Eve", "Charlie", "John" }, { "Alice", "John", "Charlie", "Bob", "Eve" } },  // Day 6
            { { "Eve", "Charlie", "Bob", "Alice", "John" }, { "Charlie", "Eve", "Alice", "Bob", "John" }, { "John", "Alice", "Bob", "Charlie", "Eve" } }   // Day 7
        };

        // Display the shift schedule for the week
        DisplayShiftSchedule(shifts);

        // Count and display how many employees are working each shift per day
        CountEmployeesPerShift(shifts);
    }

    // Method to display the shift schedule
    public static void DisplayShiftSchedule(string[,,] shifts)
    {
        Console.WriteLine(/* Output */ "Employee Shift Schedule for the Week:");

        for (int day = 0; day < shifts.GetLength(0); day++)
        {
            Console.WriteLine(/* Output */ $"Day {day + 1}:");
            for (int shift = 0; shift < shifts.GetLength(1); shift++)
            {
                Console.Write($"Shift {shift + 1}: ");
                for (int emp = 0; emp < shifts.GetLength(2); emp++)
                {
                    Console.Write(shifts[day, shift, emp] + " ");
                }
                Console.WriteLine(/* Output */ );
            }
            Console.WriteLine(/* Output */ );
        }
    }

    // Method to count how many employees are working each shift per day
    public static void CountEmployeesPerShift(string[,,] shifts)
    {
        Console.WriteLine(/* Output */ "Number of Employees Working Each Shift Per Day:");
        
        for (int day = 0; day < shifts.GetLength(0); day++)
        {
            Console.WriteLine(/* Output */ $"Day {day + 1}:");
            for (int shift = 0; shift < shifts.GetLength(1); shift++)
            {
                int employeeCount = shifts.GetLength(2);
                Console.WriteLine(/* Output */ $"Shift {shift + 1}: {employeeCount} employees");
            }
            Console.WriteLine(/* Output */ );
        }
    }
}
Explanation:
	•	The 3D array shifts stores the employee assignments for 7 days, 3 shifts per day, and 5 employees per shift.
	•	The DisplayShiftSchedule method prints out the schedule, showing which employees are assigned to which shifts on each day.
	•	The CountEmployeesPerShift method calculates how many employees are working each shift per day (since it's always 5 in this case, but this can be modified as needed).
Outcome:
	•	This system efficiently manages employee shift assignments, ensuring there is no overlap, and makes it easy to monitor shift distribution.


14.1. Notes
ITPCA2 (First Block)
14.1. Notes
	•	6.1 Introduction
	•	6.2 Database Operations in C#
	•	6.2.1 Database Creation in C#
	•	6.2.2 Connect to the Database with C#
	•	6.2.3 Accessing Data in the Database
	•	6.2.4 Insert into the Database with C#
	•	6.2.5 Update a Record in the Database with C#
	•	6.2.6 Delete a Record from the Database with C#
	•	6.3 Conclusion
Learning outcomes
By the end of this topic you should be able to:
	•	Develop the ability to write database applications in C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapter 22
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
6.1 Introduction
In this week, you learn how to perform basic database operations using system.data.SqlClient namespace in C#. You will also learn the basic database operations such as INSERT, UPDATE, SELECT and DELETE. Although the target database system is SQL Server Database, the same techniques can be applied to other database systems because the query syntax used is standard SQL that is generally supported by all relational database systems. We will also learn file handling operations in C#. We will explain what a File Stream, the two classes of file stream and how they work. At the end we will strengthen our knowledge of the material in this week with some exercises.
6.2 Database Operations in C#
A database is an organized collection of data, generally stored and accessed electronically from a computer system. Where databases are more complex they are often developed using formal design and modelling techniques. In this part we are concerned with the four basic database operation in C# such as INSERT, UPDATE, SELECT, and DELETE. Firstly we consider how to create a database and connect to the database with our C# code.
6.2.1 Database Creation in C#
To create a dataset in C#, let us under the format first.
 
Syntax:
 
Code Example
create database <database name>;
 
 
The database name in the angular brackets will be provided by the user. Then Open Microsoft SQL Server Management Studio and write the below script to create a database and table in it.
Code Example
create database Demodb;
 
use Demodb;
 
CREATE TABLE demo(
    articleID varchar(30) NOT NULL PRIMARY KEY,
    articleName varchar(30) NOT NULL,
);
 
insert into demo values(1, 'C#');
insert into demo values(2, 'C++');
 
 
After executing the above script the table named demo is created and it contains the following data as shown in below:
Output
articleID articleName
1          C#
2          C++
 
6.2.2 Connect to the Database with C#
After the data base creation, you need to connect your C# to the database. To work with a database, the first of all you required a connection. The connection to a database normally consists of the following parameters. Database name or Data Source: The database name to which the connection needs to be set up and connection can be made or you can say only work with one database at a time. Credentials: The username and password which needs to be used to establish a connection to the database. Optional Parameters: For each database type, you can specify optional parameters to provide more information on how .NET should connect to the database to handle the data.
 
The example below is to connect the database to C#
Code Example
// C# code to connect the database 
using System; 
using System.Data.SqlClient; 
namespace Database_Operation { 
class DBConn { 
    // Main Method 
    static void Main() 
    { 
        Connect(); 
        Console.ReadKey(); 
    } 
    static void Connect() 
    { 
        string constr; 
 
        // for the connection to 
        // sql server database 
        SqlConnection conn; 
// Data Source is the name of the 
        // server on which the database is stored. 
        // The Initial Catalog is used to specify 
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
 
        conn = new SqlConnection(constr); 
 
        // to open the connection 
        conn.Open(); 
 
        Console.WriteLine(/* Output */ "Connection Open!"); 
    
        // to close the connection 
        conn.Close(); 
    } 
} 
}
 
 
Output:
Output
Connection Open!
 
6.2.3 Accessing Data in the Database
To access data in the database, we use the SQL select statement and SqlDataReader for accessing the data in C#. This will enable us to retrieve some or all the data in the database depending on we use it. The C# code below demonstrate how we can retrieve all the data from the table demo in the database demodb.
Code Example
// C# code to demonstrate how 
// to use select statement 
using System; 
using System.Data.SqlClient; 
 
namespace Database_Operation { 
 
class SelectStatement{ 
 
    // Main Method 
    static void Main() 
    { 
        Read(); 
        Console.ReadKey(); 
    } 
 
    static void Read() 
    { 
        string constr; 
// for the connection to 
        // sql server database 
        SqlConnection conn; 
 
        // Data Source is the name of the 
        // server on which the database is stored. 
        // The Initial Catalog is used to specify 
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
 
        conn = new SqlConnection(constr); 
 
        // to open the connection 
        conn.Open(); 
 
        // use to perform read and write 
        // operations in the database 
        SqlCommand cmd; 
 
        // use to read a row in 
        // table one by one 
        SqlDataReader dreader; 
 
        // to sore SQL command and 
        // the output of SQL command 
        string sql, output = ""; 
 
        // use to fetch rwos from demo table 
        sql = "Select articleID, articleName from demo"; 
// to execute the sql statement 
        cmd = new SqlCommand(sql, conn); 
 
        // fetch all the rows 
        // from the demo table 
        dreader = cmd.ExecuteReader(); 
 
               // for one by one reading row 
        while (dreader.Read()) { 
            output = output + dreader.GetValue(0) + " - " + 
                                dreader.GetValue(1) + "\n"; 
        } 
 
        // to display the output 
        Console.Write(output); 
 
        // to close all the objects 
        dreader.Close(); 
        cmd.Dispose(); 
        conn.Close(); 
    } 
} 
}
 
 
 Output:
Output
1 - C#
2 - C++
     
6.2.4 Insert into the Database with C#
To insert data into the database table, we use the SQL insert statement in C#. The C# code below demonstrate how we can insert data to the table demo in the database demodb.
 
Code Example
// C# code for how to use Insert Statement 
using System; 
using System.Data.SqlClient; 
 
namespace Database_Operation { 
    
class InsertStatement { 
    
    // Main Method 
    static void Main() 
    { 
        Insert(); 
        Console.ReadKey(); 
    } 
 
    static void Insert() 
    { 
        string constr; 
 
        // for the connection to 
        // sql server database 
        SqlConnection conn; 
// Data Source is the name of the 
        // server on which the database is stored. 
        // The Initial Catalog is used to specify
          
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
 
conn = new SqlConnection(constr); 
 
        // to open the connection 
        conn.Open(); 
 
        // use to perform read and write 
        // operations in the database 
        SqlCommand cmd; 
        
        // data adapter object is use to 
        // insert, update or delete commands 
        SqlDataAdapter adap = new SqlDataAdapter(); 
        
        string sql = ""; 
 
// use the defined sql statement 
        // against our database 
        sql = "insert into demo values(3, 'Python')"; 
        
        // use to execute the sql command so we 
        // are passing query and connection object 
        cmd = new SqlCommand(sql, conn);    
        
// associate the insert SQL 
        // command to adapter object 
        adap.InsertCommand = new SqlCommand(sql, conn); 
        
        // use to execute the DML statement against 
        // our database
adap.InsertCommand.ExecuteNonQuery(); 
        
        // closing all the objects 
        cmd.Dispose(); 
        conn.Close(); 
 
         
    } 
} 
}   
    
 
Output:
 
Output
articleID articleName
1          C#
2          C++
3          Python
6.2.5 Update a Record in the Database with C#
In order to update a record in the database table, we use the SQL update statement in C#. The C# code below demonstrate how we can update a record in the table demo in the database demodb 
 
Code Example
// C# code for how to use Update Statement 
using System; 
using System.Data.SqlClient; 
   
namespace Database_Operation { 
      
class UpdateStatement { 
      
    // Main Method 
    static void Main() 
    { 
        Update(); 
        Console.ReadKey(); 
    }  
   static void Update() 
    { 
       string constr; 
    
        // for the connection to  
        // sql server database 
        SqlConnection conn;  
    
        // Data Source is the name of the  
        // server on which the database is stored. 
        // The Initial Catalog is used to specify 
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
    
        conn = new SqlConnection(constr); 
    
        // to open the connection 
        conn.Open();  
    
        // use to perform read and write 
        // operations in the database 
        SqlCommand cmd;  
           
        // data adapter object is use to  
        // insert, update or delete commands 
        SqlDataAdapter adap = new SqlDataAdapter();  
           
        string sql = ""; 
          
        // use the define sql  
        // statement against our database 
        sql = "update demo set articleName='django' where articleID=3";  
    
        // use to execute the sql command so we  
        // are passing query and connection object 
        cmd = new SqlCommand(sql, conn);  
          
        // associate the insert SQL 
        // command to adapter object 
        adap.InsertCommand = new SqlCommand(sql, conn);  
          
        // use to execute the DML statement against  
        // our database  
        adap.InsertCommand.ExecuteNonQuery();  
          
        // closing all the objects 
        cmd.Dispose(); 
        conn.Close(); 
    } 
} 
}   
   
 
Output:
Output
articleID articleName
1          C#
2          C++
3          django
 
6.2.6 Delete a Record from the Database with C#
In order to delete a record from the database table, we use the SQL delete statement in C#. The C# code below demonstrate how we can delete a record from the table demo in the database demodb. 
 
Code Example
// C# code for how to use Delete Statement 
using System; 
using System.Data.SqlClient; 
 
namespace Database_Operation { 
    
class DeleteStatement { 
    
    // Main Method 
    static void Main() 
    { 
        Delete(); 
        Console.ReadKey(); 
    } 
 
    static void Delete() 
    { 
    string constr; 
    
        // for the connection to 
        // sql server database 
        SqlConnection conn; 
// Data Source is the name of the 
        // server on which the database is stored. 
// The Initial Catalog is used to specify 
        // the name of the database 
        // The UserID and Password are the credentials 
        // required to connect to the database. 
        constr = @"Data Source=DESKTOP-GP8F496;Initial Catalog=Demodb;User ID=sa;Password=24518300"; 
    
        conn = new SqlConnection(constr); 
    
        // to open the connection 
        conn.Open(); 
    
        // use to perform read and write 
        // operations in the database 
        SqlCommand cmd; 
        
        // data adapter object is use to 
        // insert, update or delete commands 
        SqlDataAdapter adap = new SqlDataAdapter();
string sql = ""; 
          
        // use the define SQL statement  
        // against our database 
        sql = "delete from demo where articleID=3";  
          
        // use to execute the sql command so we  
        // are passing query and connection object 
        cmd = new SqlCommand(sql, conn);  
          
        // associate the insert SQL  
        // command to adapter object 
        adap.InsertCommand = new SqlCommand(sql, conn);  
          
        // use to execute the DML statement 
        // against our database 
        adap.InsertCommand.ExecuteNonQuery();  
          
        // closing all the objects 
        cmd.Dispose(); 
        conn.Close(); 
    } 
} 
}
 
 
Output
articleID articleName
1          C#
	•	          C++
 
6.3 Conclusion
In this week we learnt about database operations in C#. You learnt database creation, how to connect to a SQL Server database. You also learnt how to perform CRUD operations on a database from within a C# program.
Case Study
Case Study 1: Employee Management System
In this case study, we will create an Employee Management System that allows users to:
	•	Add new employee records.
	•	View all employees.
	•	Update employee details.
	•	Delete employee records.

Scenario:
The company needs an application to manage employees' information such as their name, department, and salary. The system should allow administrators to:
	•	Add a new employee to the database.
	•	View the list of all employees.
	•	Edit existing employee information.
	•	Remove an employee from the database.

Database Schema:
The database will have a table named Employees with the following columns:
	•	EmployeeID (Primary Key)
	•	Name (Employee's name)
	•	Department (Employee's department)
	•	Salary (Employee's salary)

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY IDENTITY,
    Name NVARCHAR(100),
    Department NVARCHAR(100),
    Salary DECIMAL(18, 2)
);

C# Code for CRUD Operations:
1. Create New Employee:

using System;
using System.Data;
using System.Data.SqlClient;

public class EmployeeManagement
{
    private string connectionString = "your_connection_string_here";

    // Create operation: Add new employee to the database
    public void AddEmployee(string name, string department, decimal salary)
    {
        using (SqlConnection conn = new SqlConnection(connectionString))
        {
            conn.Open();
            string query = "INSERT INTO Employees (Name, Department, Salary) VALUES (@Name, @Department, @Salary)";
            using (SqlCommand cmd = new SqlCommand(query, conn))
            {
                cmd.Parameters.AddWithValue("@Name", name);
                cmd.Parameters.AddWithValue("@Department", department);
                cmd.Parameters.AddWithValue("@Salary", salary);
                cmd.ExecuteNonQuery();
            }
        }
    }
}

2. Read All Employees:

public void GetAllEmployees()
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "SELECT * FROM Employees";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            SqlDataReader reader = cmd.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(/* Output */ $"ID: {reader["EmployeeID"]}, Name: {reader["Name"]}, Department: {reader["Department"]}, Salary: {reader["Salary"]}");
            }
        }
    }
}

3. Update Employee Information:

public void UpdateEmployee(int employeeId, string name, string department, decimal salary)
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "UPDATE Employees SET Name = @Name, Department = @Department, Salary = @Salary WHERE EmployeeID = @EmployeeID";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@Name", name);
            cmd.Parameters.AddWithValue("@Department", department);
            cmd.Parameters.AddWithValue("@Salary", salary);
            cmd.Parameters.AddWithValue("@EmployeeID", employeeId);
            cmd.ExecuteNonQuery();
        }
    }
}

4. Delete Employee Record:

public void DeleteEmployee(int employeeId)
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "DELETE FROM Employees WHERE EmployeeID = @EmployeeID";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@EmployeeID", employeeId);
            cmd.ExecuteNonQuery();
        }
    }
}

Usage Example:

class MainProgram
{
    static void Main(string[] args)
    {
        EmployeeManagement empMgmt = new EmployeeManagement();

        // Add a new employee
        empMgmt.AddEmployee("John Doe", "IT", 50000);

        // View all employees
        empMgmt.GetAllEmployees();

        // Update an employee
        empMgmt.UpdateEmployee(1, "John Doe", "HR", 55000);

        // Delete an employee
        empMgmt.DeleteEmployee(1);

        Console.WriteLine(/* Output */ "Operations completed successfully!");
    }
}

Case Study 2: Product Inventory Management System
In this case study, we will create a Product Inventory Management System that allows users to:
	•	Add new products.
	•	View all products.
	•	Update product details.
	•	Remove products from the inventory.

Scenario:
The company needs an application to manage products in their inventory. Each product has:
	•	A unique product ID.
	•	A name.
	•	A description.
	•	A price.
	•	A quantity available in the inventory.

Database Schema:
The database will have a table named Products with the following columns:
	•	ProductID (Primary Key)
	•	ProductName (Name of the product)
	•	Description (Description of the product)
	•	Price (Price of the product)
	•	Quantity (Quantity of the product in stock)

CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY,
    ProductName NVARCHAR(100),
    Description NVARCHAR(200),
    Price DECIMAL(18, 2),
    Quantity INT
);

C# Code for CRUD Operations:
1. Create New Product:

public class ProductInventory
{
    private string connectionString = "your_connection_string_here";

    // Create operation: Add a new product to the inventory
    public void AddProduct(string productName, string description, decimal price, int quantity)
    {
        using (SqlConnection conn = new SqlConnection(connectionString))
        {
            conn.Open();
            string query = "INSERT INTO Products (ProductName, Description, Price, Quantity) VALUES (@ProductName, @Description, @Price, @Quantity)";
            using (SqlCommand cmd = new SqlCommand(query, conn))
            {
                cmd.Parameters.AddWithValue("@ProductName", productName);
                cmd.Parameters.AddWithValue("@Description", description);
                cmd.Parameters.AddWithValue("@Price", price);
                cmd.Parameters.AddWithValue("@Quantity", quantity);
                cmd.ExecuteNonQuery();
            }
        }
    }
}

2. Read All Products:

public void GetAllProducts()
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "SELECT * FROM Products";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            SqlDataReader reader = cmd.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(/* Output */ $"ID: {reader["ProductID"]}, Name: {reader["ProductName"]}, Price: {reader["Price"]}, Quantity: {reader["Quantity"]}");
            }
        }
    }
}

3. Update Product Information:

public void UpdateProduct(int productId, string productName, string description, decimal price, int quantity)
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "UPDATE Products SET ProductName = @ProductName, Description = @Description, Price = @Price, Quantity = @Quantity WHERE ProductID = @ProductID";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@ProductName", productName);
            cmd.Parameters.AddWithValue("@Description", description);
            cmd.Parameters.AddWithValue("@Price", price);
            cmd.Parameters.AddWithValue("@Quantity", quantity);
            cmd.Parameters.AddWithValue("@ProductID", productId);
            cmd.ExecuteNonQuery();
        }
    }
}

4. Delete Product Record:

public void DeleteProduct(int productId)
{
    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        string query = "DELETE FROM Products WHERE ProductID = @ProductID";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@ProductID", productId);
            cmd.ExecuteNonQuery();
        }
    }
}

Usage Example:

class MainProgram
{
    static void Main(string[] args)
    {
        ProductInventory productInventory = new ProductInventory();

        // Add a new product
        productInventory.AddProduct("Laptop", "A high-performance laptop", 1200.50m, 100);

        // View all products
        productInventory.GetAllProducts();

        // Update a product
        productInventory.UpdateProduct(1, "Laptop", "A top-end laptop", 1250.00m, 80);

        // Delete a product
        productInventory.DeleteProduct(1);

        Console.WriteLine(/* Output */ "Operations completed successfully!");
    }
}


15.1. Notes
ITPCA2 (First Block)
15.1. Notes
	•	7.1 File Handling
	•	7.1.1 StreamWriter Class
	•	7.1.2 StreamReader Class
	•	7.2 Conclusion
Learning outcomes
By the end of this topic you should be able to:
	•	Develop the ability to write database applications in C#

Prescribed Reading
Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 Chapters 17
   
Not signed in? Click here and then refresh this page.
Need help? Contact Support
Please note: You will only be able to access the book on Kortext if you have purchased it with your vossie.net account via the Eduvos eBookstore.
7.1 File Handling
In programming, a file is used to store the data. The term File Handling refers to the various operations like creating the file, reading from the file, writing to the file, appending the file, etc. There are two basic operation which is mostly used in file handling, they are: reading and writing of the file. The file becomes stream when we open the file for writing and reading. A stream is a sequence of bytes which is used for communication. In C#, System.IO namespace contains classes which handle input and output streams and provide information about file and directory structure. There are two major stream classes that are used for most of the operations in file handling. These classes are StreamWriter class and StreamReader class.
7.1.1 StreamWriter Class
The StreamWriter class implements TextWriter for writing character to stream in a particular format. The class contains the following method which are mostly used.
 
Method
Description
Close()
Closes the current StreamWriter object and stream associate with it.
Flush()
Clears all the data from the buffer and write it in the stream associate with it.
Write()
Write data to the stream. It has different overloads for different data types to write in stream.
WriteLine()
It is same as Write() but it adds the newline character at the end of the data.
 
Example:
Code Example
// C# program to write user input 
// to a file using StreamWriter Class 
using System; 
using System.IO; 
 
namespace GeeksforGeeks { 
    
class GFG { 
    
    class WriteToFile { 
        
        public void Data() 
        { 
            // This will create a file named sample.txt 
            // at the specified location 
            StreamWriter sw = new StreamWriter("C://Test.txt"); 
            
            // To write on the console screen 
            Console.WriteLine(/* Output */ "Enter the Text that you want to write on File"); 
            
            // To read the input from the user 
            string str = Console.ReadLine(); 
            
            // To write a line in buffer 
            sw.WriteLine(str); 
            
            // To write in output stream 
            sw.Flush(); 
            
            // To close the stream 
            sw.Close(); 
        } 
    } 
    
    // Main Method 
    static void Main(string[] args) 
    { 
        WriteToFile wr = new WriteToFile(); 
        wr.Data(); 
        Console.ReadKey(); 
    } 
} 
}
 
 
The C# example above will create a text file called Test.txt on the C: drive.  
 
Output: 
Output
You will find the file at the specified location having the content you entered.
 
7.1.2 StreamReader Class
The StreamReader class implements TextReader for reading character from the stream in a particular format. The class contains the following method which are mostly used.
Method
Description
Close()
Closes the current StreamReader object and stream associate with it.
Peek()
Returns the next available character but does not consume it.
Read()
Reads the next character in input stream and increment characters position by one in the stream
ReadLine()
Reads a line from the input stream and return the data in form of string
Seek()
It is use to read/write at the specific location from a file
 
Example:
Code Example
// C# program to read from a file 
// using StreamReader Class 
using System; 
using System.IO; 
 
namespace GeeksforGeeks { 
    
class GFG { 
    
    class ReadFile { 
        
        public void DataReading() 
        { 
            // Taking a new input stream i.e. 
            // geeksforgeeks.txt and opens it 
            StreamReader sr = new StreamReader("C://Test.txt"); 
            
            Console.WriteLine(/* Output */ "Content of the File"); 
            
            // This is used to specify from where 
            // to start reading input stream 
            sr.BaseStream.Seek(0, SeekOrigin.Begin); 
            
            // To read line from input stream 
            string str = sr.ReadLine(); 
            // To read the whole file line by line 
            while (str != null) 
            { 
                Console.WriteLine(/* Output */ str); 
                str = sr.ReadLine(); 
            } 
            Console.ReadLine(); 
            
            // to close the stream 
            sr.Close(); 
        } 
    }
// Main Method 
    static void Main(string[] args) 
    { 
        ReadFile wr = new ReadFile(); 
        wr.DataReading(); 
    } 
} 
}
 
             
Output
Output
You will find the context of the file at the specified location having the content you entered.
 
7.2 Conclusion
In this week we learnt about file handling, specifically the two classes for reading and writing textfiles. These are the StreamReader and StreamWriter classes. Examples were provided to show how to implement these classes.
Case Study
Case Study 1: Personal Notes Application
Scenario:
A user wants to manage personal notes by storing, reading, updating, and deleting notes in a simple file-based application. Each note is stored in a separate text file in a folder named Notes, with the file names representing the titles of the notes. The application should allow the user to:
	•	Create a new note by providing a title and content.
	•	View a list of all existing notes (file names).
	•	Read the content of a selected note.
	•	Delete a selected note.

Directory Structure:
All notes are stored in a folder called Notes (which should be created beforehand).

│
├── Note1.txt
├── Note2.txt
├── Note3.txt
...
C# Code for File Operations:
1. Create New Note:

using System;
using System.IO;

public class FileManager
{
    private string notesDirectory = @"C:\Notes\"; // Path to the Notes folder

    // Create operation: Add a new note
    public void CreateNote(string title, string content)
    {
        string filePath = Path.Combine(notesDirectory, title + ".txt");

        if (!File.Exists(filePath)) // Ensure the file doesn't already exist
        {
            File.WriteAllText(filePath, content);
            Console.WriteLine(/* Output */ "Note created successfully.");
        }
        else
        {
            Console.WriteLine(/* Output */ "A note with this title already exists.");
        }
    }
}

2. View All Notes:

public void ViewAllNotes()
{
    if (Directory.Exists(notesDirectory))
    {
        string[] noteFiles = Directory.GetFiles(notesDirectory, "*.txt");

        if (noteFiles.Length > 0)
        {
            Console.WriteLine(/* Output */ "Available notes:");
            foreach (var note in noteFiles)
            {
                string noteTitle = Path.GetFileNameWithoutExtension(note);
                Console.WriteLine(/* Output */ noteTitle);
            }
        }
        else
        {
            Console.WriteLine(/* Output */ "No notes available.");
        }
    }
    else
    {
        Console.WriteLine(/* Output */ "Notes directory not found.");
    }
}

3. Read Note Content:

public void ReadNoteContent(string title)
{
    string filePath = Path.Combine(notesDirectory, title + ".txt");

    if (File.Exists(filePath))
    {
        string content = File.ReadAllText(filePath);
        Console.WriteLine(/* Output */ $"Content of {title}:");
        Console.WriteLine(/* Output */ content);
    }
    else
    {
        Console.WriteLine(/* Output */ "Note not found.");
    }
}

4. Delete Note:

public void DeleteNote(string title)
{
    string filePath = Path.Combine(notesDirectory, title + ".txt");

    if (File.Exists(filePath))
    {
        File.Delete(filePath);
        Console.WriteLine(/* Output */ "Note deleted successfully.");
    }
    else
    {
        Console.WriteLine(/* Output */ "Note not found.");
    }
}

Usage Example:
class MainProgram
{
    static void Main(string[] args)
    {
        FileManager fileManager = new FileManager();

        // Create a new note
        fileManager.CreateNote("FirstNote", "This is the content of the first note.");

        // View all notes
        fileManager.ViewAllNotes();

        // Read a note's content
        fileManager.ReadNoteContent("FirstNote");

        // Delete a note
        fileManager.DeleteNote("FirstNote");

        Console.WriteLine(/* Output */ "Operations completed successfully.");
    }
}

Case Study 2: Student Report Management System
Scenario:
The school wants to manage student reports stored in text files. Each student has a report file named with their ID (e.g., 12345.txt for a student with ID 12345). The system should allow administrators to:
	•	Add a new report for a student.
	•	View all student reports.
	•	Update a student report.
	•	Delete a student's report.

Directory Structure:
The reports are stored in a folder called StudentReports.

StudentReports
│
├── 12345.txt
├── 67890.txt
├── 11223.txt
...
C# Code for File Operations:
1. Create New Report:

public class ReportManager
{
    private string reportsDirectory = @"C:\StudentReports\"; // Path to the Reports folder

    // Create operation: Add a new student report
    public void CreateReport(string studentId, string content)
    {
        string filePath = Path.Combine(reportsDirectory, studentId + ".txt");

        if (!File.Exists(filePath)) // Check if the report already exists
        {
            File.WriteAllText(filePath, content);
            Console.WriteLine(/* Output */ "Report created successfully.");
        }
        else
        {
            Console.WriteLine(/* Output */ "A report for this student already exists.");
        }
    }
}

2. View All Reports:

public void ViewAllReports()
{
    if (Directory.Exists(reportsDirectory))
    {
        string[] reportFiles = Directory.GetFiles(reportsDirectory, "*.txt");

        if (reportFiles.Length > 0)
        {
            Console.WriteLine(/* Output */ "Available student reports:");
            foreach (var report in reportFiles)
            {
                string studentId = Path.GetFileNameWithoutExtension(report);
                Console.WriteLine(/* Output */ studentId);
            }
        }
        else
        {
            Console.WriteLine(/* Output */ "No reports available.");
        }
    }
    else
    {
        Console.WriteLine(/* Output */ "Reports directory not found.");
    }
}

3. Read Report Content:

public void ReadReportContent(string studentId)
{
    string filePath = Path.Combine(reportsDirectory, studentId + ".txt");

    if (File.Exists(filePath))
    {
        string content = File.ReadAllText(filePath);
        Console.WriteLine(/* Output */ $"Report for student {studentId}:");
        Console.WriteLine(/* Output */ content);
    }
    else
    {
        Console.WriteLine(/* Output */ "Report not found.");
    }
}

4. Update Report:

public void UpdateReport(string studentId, string newContent)
{
    string filePath = Path.Combine(reportsDirectory, studentId + ".txt");

    if (File.Exists(filePath))
    {
        File.WriteAllText(filePath, newContent);
        Console.WriteLine(/* Output */ "Report updated successfully.");
    }
    else
    {
        Console.WriteLine(/* Output */ "Report not found.");
    }
}

5. Delete Report:

public void DeleteReport(string studentId)
{
    string filePath = Path.Combine(reportsDirectory, studentId + ".txt");

    if (File.Exists(filePath))
    {
        File.Delete(filePath);
        Console.WriteLine(/* Output */ "Report deleted successfully.");
    }
    else
    {
        Console.WriteLine(/* Output */ "Report not found.");
    }
}

Usage Example:

class MainProgram
{
    static void Main(string[] args)
    {
        ReportManager reportManager = new ReportManager();

        // Create a new student report
        reportManager.CreateReport("12345", "Student performance is excellent.");

        // View all student reports
        reportManager.ViewAllReports();

        // Read a student report
        reportManager.ReadReportContent("12345");

        // Update a student report
        reportManager.UpdateReport("12345", "Student performance has improved significantly.");

        // Delete a student report
        reportManager.DeleteReport("12345");

        Console.WriteLine(/* Output */ "Operations completed successfully.");
    }
}


1.1. Notes
ITPCA2 (Second Block)
1.1. Notes
	•	2. Collaborative Project
	•	3. Introduction to LINQ
	•	3.1. Application of LINQ
	•	3.2. The shared System.Linq namespace
	•	4. LINQ Standard Query operators
	•	4.1. The OrderBy() method.
	•	4.2. The Any() method.
	•	4.3. Case Studies
	•	4.4. WEEKLY ACTIVITY
