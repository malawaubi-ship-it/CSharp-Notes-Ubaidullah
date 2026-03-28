# Module 6: Activity

## 1. Learning outcomes
 
By the end of this topic you should be able to:
	-	Acquire the skill to interpret data structures and algorithms.
	-	Implement data structures in C#.
	-	Develop the skill to select a suitable data structure/algorithm and effectively justify your decision

Jamro, M., (2018). C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd




## 2. Activity
	-	Describe the difference between a queue and a stack.
	-	Describe the difference between a queue and a priority queue.
	-	Describe the difference between a list and an array list. Which one is better and why?
## 3. Practice Activities
Case Study 1: Hospital Emergency Room Patient Management
Problem Statement:
In a hospital emergency room, patients are treated based on the severity of their condition. The priority levels are:
	-	Critical (Priority 1) – Life-threatening cases
	-	Serious (Priority 2) – Requires immediate medical attention
	-	Stable (Priority 3) – Can wait for treatment
The hospital must process patients in order of priority, ensuring that critical patients receive attention first.

Solution: Implementing a Priority Queue for Patient Management

using System;
using System.Collections.Generic;

class HospitalQueue {
    private PriorityQueue<string, int> patientQueue = new PriorityQueue<string, int>();

    public void AddPatient(string name, int priority) {
        patientQueue.Enqueue(name, priority);
        Console.WriteLine( $"Patient Added: {name} (Priority: {priority})");
    }

    public void TreatPatient() {
        if (patientQueue.Count > 0) {
            Console.WriteLine( $"Treating Patient: {patientQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No patients to treat.");
        }
    }
}

// Test Program
class MainProgram {
    static void Main() {
        HospitalQueue hospital = new HospitalQueue();

        hospital.AddPatient("John (Critical)", 1);
        hospital.AddPatient("Alice (Stable)", 3);
        hospital.AddPatient("Bob (Serious)", 2);

        Console.WriteLine( "\nTreating Patients:");
        while (true) {
            hospital.TreatPatient();
            if (hospital.patientQueue.Count == 0) break;
        }
    }
}
Output:
Patient Added: John (Critical) (Priority: 1)
Patient Added: Alice (Stable) (Priority: 3)
Patient Added: Bob (Serious) (Priority: 2)

Treating Patients:
Treating Patient: John (Critical)
Treating Patient: Bob (Serious)
Treating Patient: Alice (Stable)
 Critical patients are treated first, ensuring efficient medical care.

Case Study 2: Job Scheduling in an Operating System
Problem Statement:
An operating system schedules processes based on priority:
	-	Priority 1: System processes
	-	Priority 2: User applications
	-	Priority 3: Background tasks
The OS must process higher-priority jobs first.

Solution: Using a Custom Priority Queue
using System;
using System.Collections.Generic;

class JobScheduler {
    private SortedList<int, Queue<string>> jobQueue = new SortedList<int, Queue<string>>();

    public void AddJob(string jobName, int priority) {
        if (!jobQueue.ContainsKey(priority)) {
            jobQueue[priority] = new Queue<string>();
        }
        jobQueue[priority].Enqueue(jobName);
        Console.WriteLine( $"Job Added: {jobName} (Priority: {priority})");
    }

    public void ExecuteJob() {
        if (jobQueue.Count == 0) {
            Console.WriteLine( "No jobs to execute.");
            return;
        }

        int highestPriority = jobQueue.Keys[0];
        string job = jobQueue[highestPriority].Dequeue();
        Console.WriteLine( $"Executing Job: {job}");

        if (jobQueue[highestPriority].Count == 0) {
            jobQueue.Remove(highestPriority);
        }
    }
}

// Test Program
class MainProgram {
    static void Main() {
        JobScheduler scheduler = new JobScheduler();

        scheduler.AddJob("System Update", 1);
        scheduler.AddJob("User App Execution", 2);
        scheduler.AddJob("Background Sync", 3);

        Console.WriteLine( "\nExecuting Jobs:");
        while (true) {
            scheduler.ExecuteJob();
            if (scheduler.jobQueue.Count == 0) break;
        }
    }
}
Output:
Job Added: System Update (Priority: 1)
Job Added: User App Execution (Priority: 2)
Job Added: Background Sync (Priority: 3)

Executing Jobs:
Executing Job: System Update
Executing Job: User App Execution
Executing Job: Background Sync
 System-critical jobs run before background tasks.

Case Study 3: Parcel Delivery System
Problem Statement:
A courier company prioritizes deliveries based on urgency:
	-	Priority 1: Express deliveries
	-	Priority 2: Standard deliveries
	-	Priority 3: Economy deliveries
The system must ensure express parcels are delivered first.

Solution: Implementing Priority Queue for Delivery
using System;
using System.Collections.Generic;

class ParcelDelivery {
    private PriorityQueue<string, int> deliveryQueue = new PriorityQueue<string, int>();

    public void AddParcel(string parcel, int priority) {
        deliveryQueue.Enqueue(parcel, priority);
        Console.WriteLine( $"Parcel Added: {parcel} (Priority: {priority})");
    }

    public void DeliverParcel() {
        if (deliveryQueue.Count > 0) {
            Console.WriteLine( $"Delivering: {deliveryQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No parcels to deliver.");
        }
    }
}

// Test Program
class MainProgram {
    static void Main() {
        ParcelDelivery deliverySystem = new ParcelDelivery();

        deliverySystem.AddParcel("Express Parcel A", 1);
        deliverySystem.AddParcel("Standard Parcel B", 2);
        deliverySystem.AddParcel("Economy Parcel C", 3);

        Console.WriteLine( "\nDelivering Parcels:");
        while (true) {
            deliverySystem.DeliverParcel();
            if (deliverySystem.deliveryQueue.Count == 0) break;
        }
    }
}
Output:

Parcel Added: Express Parcel A (Priority: 1)
Parcel Added: Standard Parcel B (Priority: 2)
Parcel Added: Economy Parcel C (Priority: 3)

Delivering Parcels:
Delivering: Express Parcel A
Delivering: Standard Parcel B
Delivering: Economy Parcel C
 Urgent parcels are delivered first, ensuring timely service.

Case Study 4: Stock Market Order Processing
Problem Statement:
A stock exchange processes buy/sell orders based on priority:
	-	Priority 1: Market Orders (executed immediately)
	-	Priority 2: Limit Orders (executed at a set price)
	-	Priority 3: Stop Orders (triggered later)
The system ensures real-time order execution.

Solution: Stock Order Processing with Priority Queue

using System;
using System.Collections.Generic;

class StockOrderSystem {
    private PriorityQueue<string, int> orderQueue = new PriorityQueue<string, int>();

    public void PlaceOrder(string order, int priority) {
        orderQueue.Enqueue(order, priority);
        Console.WriteLine( $"Order Placed: {order} (Priority: {priority})");
    }

    public void ProcessOrder() {
        if (orderQueue.Count > 0) {
            Console.WriteLine( $"Processing Order: {orderQueue.Dequeue()}");
        } else {
            Console.WriteLine( "No orders to process.");
        }
    }
}

// Test Program
class MainProgram {
    static void Main() {
        StockOrderSystem stockSystem = new StockOrderSystem();

        stockSystem.PlaceOrder("Market Order: Buy 100 Shares", 1);
        stockSystem.PlaceOrder("Limit Order: Buy at $50", 2);
        stockSystem.PlaceOrder("Stop Order: Sell if Price Falls", 3);

        Console.WriteLine( "\nProcessing Orders:");
        while (true) {
            stockSystem.ProcessOrder();
            if (stockSystem.orderQueue.Count == 0) break;
        }
    }
}
Output:

Order Placed: Market Order: Buy 100 Shares (Priority: 1)
Order Placed: Limit Order: Buy at $50 (Priority: 2)
Order Placed: Stop Order: Sell if Price Falls (Priority: 3)

Processing Orders:
Processing Order: Market Order: Buy 100 Shares
Processing Order: Limit Order: Buy at $50
Processing Order: Stop Order: Sell if Price Falls
 Market orders are executed first for real-time trading.

Conclusion
These four case studies demonstrate how Priority Queues improve efficiency in different real-world applications.


	-	3. Hashing
	-	3.1. Hash Tables
	-	3.2. Dictionaries
	-	3.3. Sorted Dictionaries
	-	3.4. Hash Sets
	-	3.5. Sorted Sets
