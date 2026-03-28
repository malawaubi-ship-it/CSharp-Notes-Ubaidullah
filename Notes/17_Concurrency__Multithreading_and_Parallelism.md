# Module 17: Concurrency in C# - Multithreading and Parallelism

## 1. Learning outcomes

By the end of this lesson, you should be able to:
	-	Develop the ability to implement concurrency and parallelism in C#

Paul Deitel and Harvey Deitel. 2016. Visual C# How to Program. Sofia, Prentice Hall, ISBN: 9781292153469 
Chapter 9 & 21




## 2. Concurrency in C# - Multithreading and Parallelism
Overview:
Concurrency and parallelism are essential concepts for building efficient, high-performance applications in C#. Concurrency refers to the ability of a system to manage multiple tasks at once, while parallelism involves executing multiple tasks simultaneously on multiple processors or cores. In this week’s notes, we will explore methods for creating threads and implementing multithreading in C#.

Examine Different Methods to Create Threads in C#
Introduction to Threads:
In C#, threads are used for executing tasks concurrently, which can improve the performance of applications, especially in I/O-bound and CPU-bound operations. The .NET framework provides several ways to create and manage threads. Understanding these methods is crucial for building responsive and efficient applications.
## 1. Using the Thread Class:
The Thread class in C# is part of the System.Threading namespace and is one of the most direct ways to create and manage threads. You can create a new thread by providing a ThreadStart delegate, which points to the method that the thread will execute.
## 2. Using the Task Class (Recommended):
The Task class, introduced in .NET Framework 4.0, provides a more modern and flexible approach to working with threads. The Task class is part of the System.Threading.Tasks namespace and makes it easier to handle asynchronous operations and parallel tasks.
## 3. Using the ThreadPool:
The ThreadPool class provides a pool of worker threads that can be used to perform tasks without the need to manually create and manage individual threads. It is efficient for short-lived tasks, reducing the overhead of creating and destroying threads.

## 1. Example Using the Thread Class:
using System;
using System.Threading;
 
class ThreadExample
{
    // Method to be executed by the thread
    static void PrintNumbers()
    {
        for (int idx = 1; idx <= 5; idx++)
        {
            Console.WriteLine( $"Number {i}");
            Thread.Sleep(1000);  // Simulate some work by sleeping for 1 second
        }
    }
 
    static void Main()
    {
        // Create a new thread to execute the PrintNumbers method
        Thread thread = new Thread(new ThreadStart(PrintNumbers));
        thread.Start();  // Start the thread
 
        // Continue with the main thread
        Console.WriteLine( "Main thread is doing some work...");
        thread.Join();  // Wait for the created thread to finish
    }
}
Output:
Main thread is doing some work...
Number 1
Number 2
Number 3
Number 4
Number 5
Explanation:
	-	A new thread is created using the Thread class and starts executing the PrintNumbers method.
	-	The Join method is used to wait for the newly created thread to finish before continuing the main thread.

## 2. Example Using the Task Class:
using System;
using System.Threading.Tasks;
 
class TaskExample
{
    // Method to be executed by the task
    static void PrintNumbers()
    {
        for (int idx = 1; idx <= 5; idx++)
        {
            Console.WriteLine( $"Number {i}");
            Task.Delay(1000).Wait();  // Simulate some work by delaying for 1 second
        }
    }
 
    static void Main()
    {
        // Create a new task to execute the PrintNumbers method
        Task task = new Task(PrintNumbers);
        task.Start();  // Start the task
 
        // Continue with the main thread
        Console.WriteLine( "Main thread is doing some work...");
        task.Wait();  // Wait for the task to finish
    }
}
Output:
Main thread is doing some work...
Number 1
Number 2
Number 3
Number 4
Number 5
Explanation:
	-	A task is created and executed with the Task class.
	-	Task.Delay is used to simulate work, and the Wait method ensures that the main thread waits for the task to complete before continuing.

## 3. Example Using the ThreadPool:
using System;
using System.Threading;
 
class ThreadPoolExample
{
    // Method to be executed by the thread pool worker
    static void PrintNumbers(object state)
    {
        for (int idx = 1; idx <= 5; idx++)
        {
            Console.WriteLine( $"Number {i}");
            Thread.Sleep(1000);  // Simulate some work by sleeping for 1 second
        }
    }
 
    static void Main()
    {
        // Queue the work item to the thread pool
        ThreadPool.QueueUserWorkItem(PrintNumbers);
 
        // Continue with the main thread
        Console.WriteLine( "Main thread is doing some work...");
        Thread.Sleep(6000);  // Sleep for enough time to allow the thread pool to finish its work
    }
}
Output:
Main thread is doing some work...
Number 1
Number 2
Number 3
Number 4
Number 5
Explanation:
	-	The ThreadPool.QueueUserWorkItem method is used to queue a method to be executed by a worker thread from the thread pool.
	-	The main thread sleeps for a sufficient amount of time to ensure that the worker thread completes its task.

## 3. Implementing Multithreading in C#
Introduction to Multithreading:
Multithreading allows multiple tasks to run concurrently, which can significantly improve the performance of an application, especially when dealing with CPU-intensive operations. In C#, multithreading can be implemented using the Thread class, the Task class, and the ThreadPool.
Example: Running Multiple Tasks in Parallel
In this example, we will use multiple threads to calculate the sum of numArray in different ranges concurrently, and then combine the results:

using System;
using System.Threading;
using System.Threading.Tasks;
 
class MultithreadingExample
{
    static void CalculateSum(int start, int end, int threadNumber)
    {
        int sum = 0;
        for (int idx = start; idx <= end; idx++)
        {
            sum += i;
        }
        Console.WriteLine( $"Thread {threadNumber}: Sum = {sum}");
    }
 
    static void Main()
    {
        // Define ranges for each thread to calculate the sum
        Task task1 = Task.Run(() => CalculateSum(1, 1000, 1));  // Thread 1
        Task task2 = Task.Run(() => CalculateSum(1001, 2000, 2));  // Thread 2
        Task task3 = Task.Run(() => CalculateSum(2001, 3000, 3));  // Thread 3
 
        // Wait for all tasks to complete
        Task.WhenAll(task1, task2, task3).Wait();
    }
}
Output:
Thread 1: Sum = 500500
Thread 2: Sum = 1501500
Thread 3: Sum = 4501500
Explanation:
	-	Three tasks are created using Task.Run to calculate the sum of different ranges of numArray in parallel.
	-	The results are printed concurrently, and the main thread waits for all tasks to finish using Task.WhenAll.

Key Points:
	-	Thread Class: Provides low-level control over thread creation and execution. Best for simple tasks, but more complex handling is needed for synchronization.
	-	Task Class: A higher-level abstraction that simplifies multithreading and integrates with asynchronous programming.
	-	ThreadPool: Ideal for short-lived tasks to avoid overhead of creating and destroying threads manually.
	-	Multithreading Benefits: Multithreading can improve the responsiveness and performance of applications by utilizing multiple processors or cores.
	-	Synchronization: When using multithreading, it's essential to ensure proper synchronization (e.g., using locks or other synchronization techniques) to avoid race conditions.


## 4. Case Study 1: Asynchronous File Downloading
Case Study 1: Asynchronous File Downloading
Problem:
You are developing a file downloader that needs to download multiple files from the internet concurrently. This will improve the download speed and prevent the application from freezing while waiting for downloads to complete. You need to implement a solution using multithreading or tasks to handle the download process.
Solution:
We will use the Task class to download files concurrently. Each file will be downloaded in a separate task to improve performance and responsiveness.
using System;
using System.Net.Http;
using System.Threading.Tasks;
 
class FileDownloader
{
    // Method to simulate downloading a file
    static async Task DownloadFileAsync(string url, string filename)
    {
        using (HttpClient client = new HttpClient())
        {
            Console.WriteLine( $"Starting download for {filename} from {url}");
            var content = await client.GetStringAsync(url);  // Simulate downloading content
            Console.WriteLine( $"Downloaded {filename} successfully.");
        }
    }
 
    static async Task Main(string[] args)
    {
        string[] fileUrls = {
            "https://example.com/file1",
            "https://example.com/file2",
            "https://example.com/file3"
        };
        string[] filenames = { "file1", "file2", "file3" };
 
        // Start downloading files concurrently using tasks
        Task[] downloadTasks = new Task[fileUrls.Length];
 
        for (int idx = 0; idx < fileUrls.Length; idx++)
        {
            int index = i;
            downloadTasks[idx] = DownloadFileAsync(fileUrls[index], filenames[index]);
        }
 
        // Wait for all downloads to complete
        await Task.WhenAll(downloadTasks);
        Console.WriteLine( "All files downloaded successfully.");
    }
}
Explanation:
	-	The DownloadFileAsync method is asynchronous and uses HttpClient to simulate downloading a file.
	-	We start three concurrent tasks to download the files using Task.WhenAll, ensuring all downloads happen in parallel.
	-	The async and await keywords help us manage asynchronous operations efficiently.
Outcome:
Starting download for file1 from https://example.com/file1
Starting download for file2 from https://example.com/file2
Starting download for file3 from https://example.com/file3
Downloaded file1 successfully.
Downloaded file2 successfully.
Downloaded file3 successfully.
All files downloaded successfully.


## 5. Case Study 2: Parallel Processing of Large Data Set
Case Study 2: Parallel Processing of Large Data Set
Problem:
You need to process a large dataset of numArray and perform some intensive computation on each number (e.g., squaring the numArray). The dataset is too large to process in a single thread, and you want to speed up the process using parallelism.
Solution:
We can use the Parallel.For method to process the dataset concurrently in multiple threads.
using System;
using System.Linq;
using System.Threading.Tasks;
 
class ParallelProcessingExample
{
    static void ProcessData(int number)
    {
        // Simulate a time-consuming computation
        double result = Math.Pow(number, 2);  // Square the number
        Console.WriteLine( $"Processed number: {number}, Result: {result}");
    }
 
    static void Main()
    {
        // Simulate a large dataset of numArray from 1 to 100
        int[] numArray = Enumerable.Range(1, 100).ToArray();
 
        // Use Parallel.For to process the dataset concurrently
        Parallel.For(0, numArray.Length, i =>
        {
            ProcessData(numArray[idx]);
        });
 
        Console.WriteLine( "All data processed.");
    }
}
Explanation:
	-	We use Parallel.For to process each element of the array in parallel. This splits the work across multiple threads and speeds up the computation.
	-	Each number is squared in the ProcessData method, and the result is printed.
Outcome:
Processed number: 1, Result: 1
Processed number: 2, Result: 4
Processed number: 3, Result: 9
...
Processed number: 100, Result: 10000
All data processed.



## 6. Case Study 3: Parallel Data Aggregation
Case Study 3: Parallel Data Aggregation
Problem:
You are given a collection of numArray, and you need to compute the sum of all the numArray in the collection. However, the dataset is very large, and you want to leverage parallelism to compute the sum more quickly.
Solution:
Use Parallel.Aggregate or Parallel.For to aggregate the sum concurrently.
using System;
using System.Linq;
using System.Threading.Tasks;
 
class ParallelAggregationExample
{
    static void Main()
    {
        // Generate a large dataset of numArray
        int[] numArray = Enumerable.Range(1, 1000000).ToArray();
 
        // Use Parallel LINQ (PLINQ) for parallel aggregation
        int totalSum = numArray.AsParallel().Sum();
 
        Console.WriteLine( $"The total sum is: {totalSum}");
    }
}
Explanation:
	-	We use PLINQ (AsParallel()) to perform the summation in parallel, which automatically splits the work across multiple threads.
	-	The Sum() method computes the sum of the entire dataset efficiently using parallelism.
Outcome:
The total sum is: 500000500000



## 7. Case Study 4: Thread Safety in Bank Account Operations
Case Study 4: Thread Safety in Bank Account Operations
Problem:
You are building a bank account system where multiple users can access and update the account balance concurrently. You need to ensure thread safety when depositing or withdrawing money from the account.
Solution:
We will use locking to ensure that only one thread can access the critical section of the code (the account balance) at a time. This is achieved using lock in C#.
using System;
using System.Threading;
 
class BankAccount
{
    private decimal balance;
    private readonly object balanceLock = new object();  // Lock object for thread safety
 
    public BankAccount(decimal initialBalance)
    {
        balance = initialBalance;
    }
 
    public void Deposit(decimal amount)
    {
        lock (balanceLock)  // Lock to ensure thread safety
        {
            balance += amount;
            Console.WriteLine( $"Deposited {amount:C}. New balance: {balance:C}");
        }
    }
 
    public void Withdraw(decimal amount)
    {
        lock (balanceLock)  // Lock to ensure thread safety
        {
            if (balance >= amount)
            {
                balance -= amount;
                Console.WriteLine( $"Withdrew {amount:C}. New balance: {balance:C}");
            }
            else
            {
                Console.WriteLine( $"Insufficient funds to withdraw {amount:C}. Balance: {balance:C}");
            }
        }
    }
 
    public decimal Balance => balance;
}
 
class BankAccountExample
{
    static void Main()
    {
        BankAccount account = new BankAccount(1000m);
 
        // Create tasks for depositing and withdrawing concurrently
        Task[] tasks = new Task[4];
 
        tasks[0] = Task.Run(() => account.Deposit(500m));
        tasks[1] = Task.Run(() => account.Withdraw(200m));
        tasks[2] = Task.Run(() => account.Deposit(1000m));
        tasks[3] = Task.Run(() => account.Withdraw(300m));
 
        // Wait for all tasks to complete
        Task.WhenAll(tasks).Wait();
 
        Console.WriteLine( $"Final account balance: {account.Balance:C}");
    }
}
Explanation:
	-	The BankAccount class has methods for depositing and withdrawing money. We use lock to ensure that only one thread can access the critical section (the balance) at a time.
	-	Multiple tasks are created to simulate concurrent deposits and withdrawals on the same bank account.
Outcome:
Deposited $500.00. New balance: $1500.00
Withdrew $200.00. New balance: $1300.00
Deposited $1000.00. New balance: $2300.00
Withdrew $300.00. New balance: $2000.00
Final account balance: $2,000.00
Note:
	-	The locking mechanism ensures thread safety and prevents race conditions in concurrent operations.

Conclusion:
These case studies demonstrate practical applications of multithreading and parallelism in C#:
	-	File downloading: Concurrent downloading of multiple files using tasks.
	-	Parallel processing: Efficiently processing a large dataset of numArray using Parallel.For.
	-	Parallel aggregation: Summing a large collection of numArray using PLINQ for parallelism.
	-	Thread safety: Ensuring safe concurrent access to shared resources (bank account) using locks.


## 8. Case Study 5: Thread Safety in Bank Account Operations with Random Values
Case Study 5: Thread Safety in Bank Account Operations with Random Values
Problem:
You are building a bank account system where multiple users can access and update the account balance concurrently. You need to ensure thread safety when depositing or withdrawing money from the account. Instead of using static values for deposits and withdrawals, you'll generate random values to simulate real-world financial transactions.
Solution:
We will use the Random class in C# to generate random deposit and withdrawal amounts. We'll also ensure thread safety using the lock keyword to prevent race conditions when accessing or modifying the account balance.
using System;
using System.Threading;
using System.Threading.Tasks;
 
class BankAccount
{
    private decimal balance;
    private readonly object balanceLock = new object();  // Lock object for thread safety
    private Random random = new Random();
 
    public BankAccount(decimal initialBalance)
    {
        balance = initialBalance;
    }
 
    public void Deposit()
    {
        lock (balanceLock)  // Lock to ensure thread safety
        {
            decimal amount = random.Next(100, 1000);  // Random deposit amount between 100 and 1000
            balance += amount;
            Console.WriteLine( $"Deposited {amount:C}. New balance: {balance:C}");
        }
    }
 
    public void Withdraw()
    {
        lock (balanceLock)  // Lock to ensure thread safety
        {
            decimal amount = random.Next(50, 500);  // Random withdrawal amount between 50 and 500
            if (balance >= amount)
            {
                balance -= amount;
                Console.WriteLine( $"Withdrew {amount:C}. New balance: {balance:C}");
            }
            else
            {
                Console.WriteLine( $"Insufficient funds to withdraw {amount:C}. Balance: {balance:C}");
            }
        }
    }
 
    public decimal Balance => balance;
}
 
class BankAccountExample
{
    static void Main()
    {
        BankAccount account = new BankAccount(1000m);  // Initial balance of $1000
 
        // Create tasks for depositing and withdrawing concurrently
        Task[] tasks = new Task[6];
 
        // Random deposits and withdrawals
        tasks[0] = Task.Run(() => account.Deposit());
        tasks[1] = Task.Run(() => account.Withdraw());
        tasks[2] = Task.Run(() => account.Deposit());
        tasks[3] = Task.Run(() => account.Withdraw());
        tasks[4] = Task.Run(() => account.Deposit());
        tasks[5] = Task.Run(() => account.Withdraw());
 
        // Wait for all tasks to complete
        Task.WhenAll(tasks).Wait();
 
        Console.WriteLine( $"Final account balance: {account.Balance:C}");
    }
}
Explanation:
	-	The Deposit and Withdraw methods generate random amounts using the Random class. The Deposit method generates a random amount between 100 and 1000, while the Withdraw method generates a random amount between 50 and 500.
	-	The lock statement ensures that only one thread can access or modify the balance at a time, preventing race conditions.
	-	The account starts with an initial balance of 1000, and multiple tasks perform random deposit and withdrawal operations concurrently.
Outcome:
Deposited $578.94. New balance: $1578.94
Withdrew $163.34. New balance: $1415.60
Deposited $721.17. New balance: $2136.77
Withdrew $228.60. New balance: $1908.17
Deposited $459.42. New balance: $2367.59
Withdrew $315.63. New balance: $2051.96
Final account balance: $2,051.96
Explanation of Outcome:
	-	Each task randomly deposits or withdraws an amount from the account, and the final account balance reflects the combined results of all operations.
	-	Thread safety is maintained by using lock to prevent simultaneous access to the balance during deposit or withdrawal.



## 9. Concept Overview
Concept Overview
Multithreading
	-	Runs multiple threads concurrently.
	-	Each horse is on a separate thread, and all threads run independently.
Parallelism (with Parallel class or Tasks)
	-	Utilizes multiple cores for better performance.
	-	Automatically manages thread usage under the hood.

Scenario: Horse Race Simulation
You want to simulate a race with multiple horses starting at the same time and racing to the finish line independently.

Multithreading Version (Using Threads)
using System;
using System.Threading;

class HorseRace
{
    static void Main()
    {
        Console.WriteLine( " Horse Race Started!\n");

        for (int idx = 1; idx <= 5; idx++)
        {
            int horseNumber = i;
            Thread thread = new Thread(() => RunHorse(horseNumber));
            thread.Start();
        }

        Console.WriteLine( "\nAll horses are running concurrently!\n");
    }

    static void RunHorse(int horseNumber)
    {
        Random rand = new Random(Guid.NewGuid().GetHashCode());
        int distance = 0;

        while (distance < 100)
        {
            Thread.Sleep(rand.Next(100, 300));  // Simulate running
            distance += rand.Next(5, 15);       // Advance
            Console.WriteLine( $" Horse {horseNumber} at {distance}m");
        }

        Console.WriteLine( $" Horse {horseNumber} has finished!");
    }
}
Sample Output:
Horse Race Started!

All horses are running concurrently!

Horse 1 at 10m
Horse 2 at 9m
Horse 3 at 8m
...
Horse 3 has finished!
Horse 1 has finished!
...

Parallel Version (Using Parallel.For)

using System;
using System.Threading;
using System.Threading.Tasks;

class HorseRaceParallel
{
    static void Main()
    {
        Console.WriteLine( " Parallel Horse Race Started!\n");

        Parallel.For(1, 6, (idx) =>
        {
            RunHorse(idx);
        });

        Console.WriteLine( "\nAll horses have finished!");
    }

    static void RunHorse(int horseNumber)
    {
        Random rand = new Random(Guid.NewGuid().GetHashCode());
        int distance = 0;

        while (distance < 100)
        {
            Thread.Sleep(rand.Next(100, 300));
            distance += rand.Next(5, 15);
            Console.WriteLine( $" Horse {horseNumber} at {distance}m");
        }

        Console.WriteLine( $" Horse {horseNumber} has finished!");
    }
}

Summary of Key Concepts:
Feature
Threading
Parallel.For
Manual Thread Control
 Yes
 Managed automatically
Better for...
Fine-grained control (start, pause, stop)
CPU-bound tasks (parallel computation)
Syntax Simplicity
Moderate (manual)
Easy (auto-managed)
Performance
Scales well but requires tuning
Auto-balances across cores


## 10. Video


## 11. Scenario 1: Concurrency in Processing Orders in an E-Commerce System
Scenario 1: Concurrency in Processing Orders in an E-Commerce System
Problem:
In an e-commerce system, multiple customers can place orders concurrently, and each order needs to be processed for payment, inventory check, and shipment. The order processing involves multiple steps: verifying the order details, checking the inventory, deducting the stock, charging the payment, and generating an invoice. Each order should be processed independently, but due to concurrency, there are potential issues, such as double-charging or overselling stock.
The goal is to use concurrency to process orders efficiently and ensure that critical sections of the code, such as inventory updates and payment processing, are handled safely in a multi-threaded environment.
Solution:
To solve this problem, we will use multithreading with locking to ensure thread safety in the critical sections of the order processing pipeline. We will also use Task Parallel Library (TPL) to handle multiple orders concurrently.
using System;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
 
class OrderProcessor
{
    private readonly object inventoryLock = new object();  // Lock object for inventory operations
    private int stock = 100;  // Initial stock
    private decimal totalRevenue = 0;  // Total revenue from orders
 
    public void ProcessOrder(int orderId, decimal orderAmount, int orderQuantity)
    {
        lock (inventoryLock)  // Lock to ensure thread safety during stock updates
        {
            Console.WriteLine( $"Order {orderId} - Processing started.");
            if (stock >= orderQuantity)
            {
                // Deduct the stock
                stock -= orderQuantity;
                totalRevenue += orderAmount;
 
                // Simulate payment processing
                Thread.Sleep(500);  // Simulating a delay for payment processing
                Console.WriteLine( $"Order {orderId} - Payment processed. Revenue updated.");
 
                // Simulate shipment generation
                Thread.Sleep(500);  // Simulating a delay for shipment processing
                Console.WriteLine( $"Order {orderId} - Shipment generated.");
            }
            else
            {
                Console.WriteLine( $"Order {orderId} - Insufficient stock. Order cannot be processed.");
            }
        }
    }
 
    public void DisplayStockAndRevenue()
    {
        Console.WriteLine( $"Remaining stock: {stock}");
        Console.WriteLine( $"Total Revenue: {totalRevenue:C}");
    }
}
 
class MainProgram
{
    static async Task Main()
    {
        OrderProcessor processor = new OrderProcessor();
 
        // Simulate 5 concurrent orders
        List<Task> tasks = new List<Task>
        {
            Task.Run(() => processor.ProcessOrder(1, 100.00m, 3)),
            Task.Run(() => processor.ProcessOrder(2, 50.00m, 1)),
            Task.Run(() => processor.ProcessOrder(3, 200.00m, 5)),
            Task.Run(() => processor.ProcessOrder(4, 80.00m, 2)),
            Task.Run(() => processor.ProcessOrder(5, 120.00m, 4))
        };
 
        // Wait for all orders to be processed
        await Task.WhenAll(tasks);
 
        // Display the remaining stock and total revenue after processing
        processor.DisplayStockAndRevenue();
    }
}
Explanation:
	-	Concurrency: The Task.Run method is used to run each order processing task concurrently. Each task processes an order in a separate thread.
	-	Thread Safety: The lock (inventoryLock) ensures that only one thread can update the stock or total revenue at a time, preventing race conditions.
	-	Order Processing Steps: For each order, we simulate a stock check, deduct stock if sufficient, process payment, and generate shipment details. All critical sections (stock update and revenue update) are synchronized using the lock statement.
Outcome:
Order 1 - Processing started.
Order 2 - Processing started.
Order 3 - Processing started.
Order 4 - Processing started.
Order 5 - Processing started.
Order 2 - Payment processed. Revenue updated.
Order 2 - Shipment generated.
Order 1 - Payment processed. Revenue updated.
Order 1 - Shipment generated.
Order 5 - Insufficient stock. Order cannot be processed.
Order 4 - Payment processed. Revenue updated.
Order 4 - Shipment generated.
Order 3 - Insufficient stock. Order cannot be processed.
Remaining stock: 88
Total Revenue: $330.00
Explanation of Outcome:
	-	Orders are processed concurrently, but only one order is allowed to update the stock at a time due to the lock. As a result, the system avoids overselling.
	-	Orders with insufficient stock are rejected, and the stock and revenue are correctly updated.


## 12. References
	-	Microsoft Learn. (n.d.). Threading in C#.
https://learn.microsoft.com/en-us/dotnet/standard/threading/
Accessed April 2025.
	-	Microsoft Learn. (n.d.). Parallel Programming in .NET.
https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/
Accessed April 2025.
	-	C# Corner. (n.d.). Multithreading in C# with Examples.
https://www.c-sharpcorner.com/UploadFile/1e050f/multithreading-in-C-Sharp/
Accessed April 2025.


	-	2. C# Networking Concepts
	-	3. Implement C# Remote Objects (Remote Method Invocation - RMI)
	-	4. Example 1
	-	5. Example 2
	-	6. Reference Videos
	-	7. Scenario Question:
