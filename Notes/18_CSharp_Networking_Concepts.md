# Module 18: C# Networking Concepts

## 1. Learning outcomes

By the end of this lesson, you should be able to:
	-	Understand C# networking concepts

Microsoft Official Documentation
## 2. C# Networking Concepts
Overview:
C# provides extensive support for networking through various classes, which enable applications to communicate with each other over networks. This involves both Socket Programming (low-level communication) and Remote Objects (higher-level distributed object communication). The focus of this week is to understand how these two concepts work and how to implement them in C#.

Implement Socket Programming in C#
What is Socket Programming?
Socket programming refers to the use of network sockets for communication between two different systems or processes over a network. A socket is an endpoint for sending or receiving data across a network. In C#, socket programming is used for creating both server-side and client-side applications to exchange data over the network using TCP/IP or UDP protocols.
The System.Net.Sockets namespace in C# provides classes to work with sockets, including Socket, TcpClient, and TcpListener. Socket programming is fundamental for real-time communication and handling client-server models, like chat applications, web servers, or multiplayer games.
Example 1: Simple TCP Server in C#
Here’s a simple TCP server using TcpListener that waits for a client connection, receives a message, and then sends a response.
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class TcpServer
{
    static void Main(string[] args)
    {
        // Define IP address and port for the server
        IPAddress ipAddress = IPAddress.Parse("127.0.0.1"); // Localhost
        int port = 5000;
 
        // Create a TcpListener and start listening for incoming connections
        TcpListener server = new TcpListener(ipAddress, port);
        server.Start();
        Console.WriteLine( "Server is listening...");
 
        // Accept a client connection
        TcpClient client = server.AcceptTcpClient();
        Console.WriteLine( "Client connected.");
 
        // Get the stream to read and write data
        NetworkStream stream = client.GetStream();
        byte[] buffer = new byte[256];
        int bytesRead;
 
        // Read data from the client
        bytesRead = stream.Read(buffer, 0, buffer.Length);
        string messageFromClient = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine( $"Received from client: {messageFromClient}");
 
        // Send a response back to the client
        string response = "Hello from the server!";
        byte[] responseBytes = Encoding.UTF8.GetBytes(response);
        stream.Write(responseBytes, 0, responseBytes.Length);
 
        // Close the connection
        client.Close();
        server.Stop();
    }
}
Explanation of Example 1:
	-	TcpListener listens for incoming TCP connections on a specified IP address and port.
	-	Once a client connects, the server reads the message sent by the client and then sends a response back to the client.
	-	The NetworkStream class allows for bi-directional communication between the client and server.
	-	The server sends and receives data using byte arrays. UTF-8 encoding/decoding is used to convert strings into byte arrays and vice versa.

Example 2: Simple TCP Client in C#
Here’s a simple TCP client that connects to the server from Example 1, sends a message, and waits for the server’s response.
using System;
using System.Net.Sockets;
using System.Text;
 
class TcpClientApp
{
    static void Main(string[] args)
    {
        // Define server IP and port
        string serverAddress = "127.0.0.1"; // Localhost
        int port = 5000;
 
        // Create a TcpClient and connect to the server
        TcpClient client = new TcpClient(serverAddress, port);
        Console.WriteLine( "Connected to server.");
 
        // Get the network stream to send and receive data
        NetworkStream stream = client.GetStream();
 
        // Send a message to the server
        string message = "Hello, Server!";
        byte[] messageBytes = Encoding.UTF8.GetBytes(message);
        stream.Write(messageBytes, 0, messageBytes.Length);
        Console.WriteLine( $"Sent to server: {message}");
 
        // Receive the server's response
        byte[] buffer = new byte[256];
        int bytesRead = stream.Read(buffer, 0, buffer.Length);
        string serverResponse = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine( $"Received from server: {serverResponse}");
 
        // Close the connection
        client.Close();
    }
}
Explanation of Example 2:
	-	The client connects to the server using TcpClient.
	-	The client sends a message to the server using NetworkStream.Write.
	-	After sending the message, the client waits for a response from the server.
	-	The client receives the server's response and prints it on the console.

## 3. Implement C# Remote Objects (Remote Method Invocation - RMI)
Implement C# Remote Objects (Remote Method Invocation - RMI)
What is Remote Objects in C#?
C# provides a way to work with remote objects through Remote Method Invocation (RMI). This allows an application to call methods on objects residing on a remote machine, effectively enabling communication between distributed applications.
In C#, remote objects can be created using .NET Remoting (although it is deprecated in favor of more modern communication mechanisms like WCF and gRPC). However, we will focus on implementing remote objects using Windows Communication Foundation (WCF), which is the recommended approach for building distributed systems in modern C# applications.
Example 1: Simple Remote Object using WCF
Here, we will create a simple WCF service that provides a remote method to say “Hello” to the client.
	-	Step 1: Define the Service Contract
using System.ServiceModel;
 
[ServiceContract]
public interface IHelloService
{
    [OperationContract]
    string SayHello(string name);
}
	-	Step 2: Implement the Service
using System;
 
public class HelloService : IHelloService
{
    public string SayHello(string name)
    {
        return $"Hello, {name}!";
    }
}
	-	Step 3: Host the Service (Service Host)
using System;
using System.ServiceModel;
 
class MainProgram
{
    static void Main()
    {
        // Create and configure the WCF service host
        ServiceHost host = new ServiceHost(typeof(HelloService), new Uri("http://localhost:8000/HelloService"));
        host.AddServiceEndpoint(typeof(IHelloService), new BasicHttpBinding(), "");
        
        // Open the host to begin listening for requests
        host.Open();
        Console.WriteLine( "Service is hosted at http://localhost:8000/HelloService");
 
        // Keep the service running
        Console.ReadLine();
 
        // Close the host when done
        host.Close();
    }
}
	-	Step 4: Client to Call the Remote Service
using System;
using System.ServiceModel;
 
class MainProgram
{
    static void Main()
    {
        // Create a channel factory for the WCF service
        ChannelFactory<IHelloService> factory = new ChannelFactory<IHelloService>(
            new BasicHttpBinding(), new EndpointAddress("http://localhost:8000/HelloService"));
        
        // Get the service proxy
        IHelloService proxy = factory.CreateChannel();
        
        // Call the remote method
        string response = proxy.SayHello("John");
        Console.WriteLine( response);
 
        // Close the proxy
        ((IClientChannel)proxy).Close();
    }
}
Explanation of Example 1:
	-	Service Contract: The IHelloService interface defines the method that the client can call remotely.
	-	Service Implementation: The HelloService class implements the service contract, providing the logic for the remote method (SayHello).
	-	Service Hosting: The WCF service is hosted using ServiceHost, and it listens on a specified URI (in this case, http://localhost:8000/HelloService).
	-	Client: The client uses ChannelFactory to create a proxy that can call the remote method on the service. The client sends a request to the service and gets a response.

Conclusion:
In this week's topic on C# Networking, we covered two essential concepts: Socket Programming and Remote Objects.
	-	Socket Programming allows low-level communication between client and server, providing flexibility for building network applications. The examples demonstrated how to set up a TCP server and client for communication.
	-	Remote Objects in C# using WCF provide a higher-level abstraction for remote method invocation, enabling distributed systems where clients can call methods on remote services. The examples demonstrated how to implement a simple WCF service and client.
Both concepts are critical for building networked applications, and knowing how to implement them in C# is vital for developing real-time, distributed systems.


## 4. Example 1
Example 1: Basic TCP Server and Client Communication in C#
Objective:
Create a basic TCP server that listens for incoming client connections, receives a message, and sends a response back to the client.
Solution:
	-	TCP Server Implementation (Server)
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class TcpServer
{
    static void Main(string[] args)
    {
        // Set up the server's IP address and port
        IPAddress ipAddress = IPAddress.Parse("127.0.0.1");  // Localhost
        int port = 5000;
 
        // Create and start the TCP listener
        TcpListener server = new TcpListener(ipAddress, port);
        server.Start();
        Console.WriteLine( "Server is listening for connections...");
 
        // Accept a client connection
        TcpClient client = server.AcceptTcpClient();
        Console.WriteLine( "Client connected.");
 
        // Get the network stream to read and write data
        NetworkStream stream = client.GetStream();
        byte[] buffer = new byte[256];
        int bytesRead;
 
        // Read the incoming data from the client
        bytesRead = stream.Read(buffer, 0, buffer.Length);
        string messageFromClient = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine( $"Received from client: {messageFromClient}");
 
        // Send a response back to the client
        string response = "Hello from the server!";
        byte[] responseBytes = Encoding.UTF8.GetBytes(response);
        stream.Write(responseBytes, 0, responseBytes.Length);
 
        // Close the connection
        client.Close();
        server.Stop();
    }
}
	-	TCP Client Implementation (Client)
using System;
using System.Net.Sockets;
using System.Text;
 
class TcpClientApp
{
    static void Main(string[] args)
    {
        // Server IP and port to connect to
        string serverAddress = "127.0.0.1";  // Localhost
        int port = 5000;
 
        // Create a TCP client and connect to the server
        TcpClient client = new TcpClient(serverAddress, port);
        Console.WriteLine( "Connected to server.");
 
        // Get the network stream to send and receive data
        NetworkStream stream = client.GetStream();
 
        // Send a message to the server
        string message = "Hello, Server!";
        byte[] messageBytes = Encoding.UTF8.GetBytes(message);
        stream.Write(messageBytes, 0, messageBytes.Length);
        Console.WriteLine( $"Sent to server: {message}");
 
        // Receive the server's response
        byte[] buffer = new byte[256];
        int bytesRead = stream.Read(buffer, 0, buffer.Length);
        string serverResponse = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine( $"Received from server: {serverResponse}");
 
        // Close the connection
        client.Close();
    }
}
Expected Output:
Server Output:
Server is listening for connections...
Client connected.
Received from client: Hello, Server!
Client Output:
Connected to server.
Sent to server: Hello, Server!
Received from server: Hello from the server!


## 5. Example 2
Example 2: Basic UDP Client-Server Communication
Objective:
Create a simple UDP client-server communication where the client sends a message to the server, and the server responds back with an acknowledgment.
Solution:
	-	UDP Server Implementation (Server)
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class UdpServer
{
    static void Main(string[] args)
    {
        // Set up the UDP listener
        int port = 5000;
        UdpClient server = new UdpClient(port);
        Console.WriteLine( "UDP Server is waiting for messages...");
 
        IPEndPoint clientEndPoint = new IPEndPoint(IPAddress.Any, port);
 
        // Receive a message from the client
        byte[] data = server.Receive(ref clientEndPoint);
        string message = Encoding.UTF8.GetString(data);
        Console.WriteLine( $"Received from client: {message}");
 
        // Send a response to the client
        string response = "Message received by server";
        byte[] responseBytes = Encoding.UTF8.GetBytes(response);
        server.Send(responseBytes, responseBytes.Length, clientEndPoint);
 
        server.Close();
    }
}
	-	UDP Client Implementation (Client)
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class UdpClientApp
{
    static void Main(string[] args)
    {
        // Define server IP address and port
        string serverAddress = "127.0.0.1";  // Localhost
        int port = 5000;
 
        // Create a UDP client
        UdpClient client = new UdpClient();
 
        // Send a message to the server
        string message = "Hello, UDP Server!";
        byte[] messageBytes = Encoding.UTF8.GetBytes(message);
        client.Send(messageBytes, messageBytes.Length, serverAddress, port);
        Console.WriteLine( $"Sent to server: {message}");
 
        // Receive the server's response
        IPEndPoint serverEndPoint = new IPEndPoint(IPAddress.Any, port);
        byte[] responseBytes = client.Receive(ref serverEndPoint);
        string response = Encoding.UTF8.GetString(responseBytes);
        Console.WriteLine( $"Received from server: {response}");
 
        client.Close();
    }
}
Expected Output:
Server Output:
UDP Server is waiting for messages...
Received from client: Hello, UDP Server!
Client Output:
Sent to server: Hello, UDP Server!
Received from server: Message received by server

## 6. Reference Videos

Play Video

Play Video

Play Video

Play Video


## 7. Scenario Question:
Scenario Question:
Scenario:
You are developing a C# application for a small business that needs to communicate between two components: an inventory system (server-side) and a sales application (client-side). The sales application needs to request the current inventory of products in real-time, and based on that, it will check whether a product is in stock before proceeding with a sale. The communication between the two systems should be done over a local network using a TCP connection for reliability.
You need to:
	-	Create a TCP server that will listen for requests from the sales application.
	-	Implement a method that responds with the current stock of products based on the product ID requested by the sales application.
	-	The sales application should send the product ID to the server and display whether the product is in stock or not based on the server's response.

Solution:
Step 1: Define the TCP Server (Inventory System)
The server will listen for incoming TCP connections, receive the product ID from the client, and send back the availability of the product.
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
 
class InventoryServer
{
    static void Main(string[] args)
    {
        // Define the IP address and port for the server
        IPAddress ipAddress = IPAddress.Parse("127.0.0.1");  // Localhost
        int port = 5000;
 
        // Create a TcpListener and start listening for incoming connections
        TcpListener server = new TcpListener(ipAddress, port);
        server.Start();
        Console.WriteLine( "Server is listening for connections...");
 
        // Accept a client connection
        TcpClient client = server.AcceptTcpClient();
        Console.WriteLine( "Client connected.");
 
        // Get the network stream to read and write data
        NetworkStream stream = client.GetStream();
        byte[] buffer = new byte[256];
        int bytesRead;
 
        // Read the product ID sent by the client
        bytesRead = stream.Read(buffer, 0, buffer.Length);
        string productIdFromClient = Encoding.UTF8.GetString(buffer, 0, bytesRead);
        Console.WriteLine( $"Received product ID from client: {productIdFromClient}");
 
        // Check the stock of the requested product (simulated data)
        string response = CheckProductStock(productIdFromClient);
 
        // Send the response back to the client
        byte[] responseBytes = Encoding.UTF8.GetBytes(response);
        stream.Write(responseBytes, 0, responseBytes.Length);
 
        // Close the connection
        client.Close();
        server.Stop();
    }
 
    // Simulate checking product stock based on product ID
    static string CheckProductStock(string productId)
    {
        // In a real scenario, this data might come from a database or inventory system
        if (productId == "101") return "Product 101 is in stock!";
        else if (productId == "102") return "Product 102 is out of stock!";
        else return "Product not found.";
    }
}

Step 2: Define the TCP Client (Sales Application)
The client will send a product ID to the server, and based on the server's response, it will display whether the product is in stock.
using System;
using System.Net.Sockets;
using System.Text;
 
class SalesClient
{
    static void Main(string[] args)
    {
        // Define the server IP and port
        string serverAddress = "127.0.0.1";  // Localhost
        int port = 5000;
 
        // Create a TcpClient and connect to the server
        TcpClient client = new TcpClient(serverAddress, port);
        Console.WriteLine( "Connected to server.");
 
        // Get the network stream to send and receive data
        NetworkStream stream = client.GetStream();
 
        // Get the product ID to check
        Console.Write("Enter product ID to check stock: ");
        string productId = Console.ReadLine();
 
        // Send the product ID to the server
        byte[] productIdBytes = Encoding.UTF8.GetBytes(productId);
        stream.Write(productIdBytes, 0, productIdBytes.Length);
        Console.WriteLine( $"Sent product ID: {productId}");
 
        // Receive the response from the server
        byte[] buffer = new byte[256];
        int bytesRead = stream.Read(buffer, 0, buffer.Length);
        string serverResponse = Encoding.UTF8.GetString(buffer, 0, bytesRead);
 
        // Display the server's response
        Console.WriteLine( $"Server response: {serverResponse}");
 
        // Close the connection
        client.Close();
    }
}

Explanation of Solution:
	-	TCP Server (Inventory System):
	-	The server listens for incoming connections on 127.0.0.1 (localhost) and port 5000.
	-	When a connection is accepted from the client, the server reads the product ID sent by the client.
	-	The server checks if the product is in stock by simulating an inventory system (in this case, hardcoded values for product IDs 101 and 102).
	-	The server then sends a response back to the client based on the availability of the product.
	-	TCP Client (Sales Application):
	-	The client connects to the server on 127.0.0.1 and port 5000.
	-	It prompts the user to enter a product ID and sends this ID to the server.
	-	The client then waits for the server’s response and displays whether the product is in stock or not.

Expected Output:
Server Output:
Server is listening for connections...
Client connected.
Received product ID from client: 101
Product 101 is in stock!
Client Output:
Connected to server.
Enter product ID to check stock: 101
Sent product ID: 101
Server response: Product 101 is in stock!


	-	2. XML Processing in C#
	-	3. Build XML Documents Using C#
	-	4. Building XML Using XDocument (LINQ to XML)
	-	5. Example 1: Building XML Using XmlDocument (DOM Approach)
	-	6. Example 2: Building XML Using XmlWriter (Streaming Approach)
	-	7. Example 3: Building XML Using XDocument (LINQ to XML)
	-	8. Scenarios
