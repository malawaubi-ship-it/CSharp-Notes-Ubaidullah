# Module 18: Networking in C#

## Learning Outcomes

By the end of this module you should be able to:
- Explain the role of TCP and UDP in network communication.
- Implement a basic TCP client and server in C#.
- Make HTTP requests using `HttpClient`.

---

## Networking Fundamentals

| Concept | Description |
|---------|-------------|
| **IP Address** | Unique identifier for a device on a network |
| **Port** | A number that identifies a specific service on a device |
| **TCP** | Connection-oriented, reliable, ordered delivery |
| **UDP** | Connectionless, fast, no delivery guarantee |
| **HTTP/HTTPS** | Application-layer protocol for web communication |
| **Socket** | An endpoint for sending and receiving data |

---

## TCP Client and Server

TCP is used when data integrity is critical. A connection must be established before data is exchanged.

### TCP Server

```csharp
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;

public static void StartTcpServer(int port)
{
    TcpListener server = new TcpListener(IPAddress.Any, port);
    server.Start();
    Console.WriteLine($"Server listening on port {port}");

    TcpClient client = server.AcceptTcpClient(); // blocks until a client connects
    Console.WriteLine("Client connected.");

    NetworkStream stream = client.GetStream();
    byte[] buffer = new byte[1024];
    int bytesRead  = stream.Read(buffer, 0, buffer.Length);
    string message = Encoding.UTF8.GetString(buffer, 0, bytesRead);
    Console.WriteLine($"Received: {message}");

    // Echo the message back
    byte[] response = Encoding.UTF8.GetBytes($"Echo: {message}");
    stream.Write(response, 0, response.Length);

    client.Close();
    server.Stop();
}
```

### TCP Client

```csharp
using System;
using System.Net.Sockets;
using System.Text;

public static void TcpClientExample(string host, int port, string message)
{
    TcpClient client = new TcpClient(host, port);
    NetworkStream stream = client.GetStream();

    // Send message
    byte[] data = Encoding.UTF8.GetBytes(message);
    stream.Write(data, 0, data.Length);

    // Receive response
    byte[] buffer    = new byte[1024];
    int bytesRead    = stream.Read(buffer, 0, buffer.Length);
    string response  = Encoding.UTF8.GetString(buffer, 0, bytesRead);
    Console.WriteLine($"Server responded: {response}");

    client.Close();
}
```

---

## UDP Communication

UDP is used when speed is more important than guaranteed delivery — e.g. live video streaming, online gaming.

```csharp
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;

// UDP Sender
public static void UdpSend(string host, int port, string message)
{
    UdpClient sender       = new UdpClient();
    byte[] data            = Encoding.UTF8.GetBytes(message);
    IPEndPoint destination = new IPEndPoint(IPAddress.Parse(host), port);

    sender.Send(data, data.Length, destination);
    Console.WriteLine($"Sent UDP packet: {message}");
    sender.Close();
}

// UDP Receiver
public static void UdpReceive(int port)
{
    UdpClient receiver   = new UdpClient(port);
    IPEndPoint anySource = new IPEndPoint(IPAddress.Any, 0);

    Console.WriteLine($"Listening for UDP on port {port}...");
    byte[] data   = receiver.Receive(ref anySource);
    string message = Encoding.UTF8.GetString(data);
    Console.WriteLine($"Received from {anySource}: {message}");
    receiver.Close();
}
```

---

## HTTP Requests with HttpClient

For web APIs and web services, use `HttpClient` — the modern HTTP client in .NET.

```csharp
using System;
using System.Net.Http;
using System.Text;
using System.Text.Json;
using System.Threading.Tasks;

public class ApiClient
{
    private readonly HttpClient client = new HttpClient();

    // GET request
    public async Task<string> GetAsync(string url)
    {
        HttpResponseMessage response = await client.GetAsync(url);
        response.EnsureSuccessStatusCode();
        return await response.Content.ReadAsStringAsync();
    }

    // POST request with JSON body
    public async Task<string> PostAsync(string url, object payload)
    {
        string json    = JsonSerializer.Serialize(payload);
        var    content = new StringContent(json, Encoding.UTF8, "application/json");

        HttpResponseMessage response = await client.PostAsync(url, content);
        response.EnsureSuccessStatusCode();
        return await response.Content.ReadAsStringAsync();
    }
}

// Usage
public static async Task Main()
{
    ApiClient api    = new ApiClient();
    string    result = await api.GetAsync("https://api.example.com/data");
    Console.WriteLine(result);
}
```

---

## Summary

| Protocol | Layer | Use Case | Reliable? |
|----------|-------|----------|-----------|
| TCP | Transport | File transfer, messaging, HTTP | Yes |
| UDP | Transport | Streaming, gaming, DNS | No |
| HTTP/HTTPS | Application | Web APIs, web browsing | Yes (via TCP) |

C# provides `System.Net.Sockets` for low-level TCP and UDP communication,
and `System.Net.Http.HttpClient` for high-level HTTP communication.
Always prefer `async/await` to avoid blocking the calling thread on network operations.

Reference: Microsoft Docs. "System.Net.Sockets Namespace." docs.microsoft.com
