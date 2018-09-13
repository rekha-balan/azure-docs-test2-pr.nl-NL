### <a name="create-a-console-application"></a><span data-ttu-id="250e5-101">Create a console application</span><span class="sxs-lookup"><span data-stu-id="250e5-101">Create a console application</span></span>
* <span data-ttu-id="250e5-102">Launch Visual Studio and create a new Console application.</span><span class="sxs-lookup"><span data-stu-id="250e5-102">Launch Visual Studio and create a new Console application.</span></span>

### <a name="add-the-relay-nuget-package"></a><span data-ttu-id="250e5-103">Add the Relay NuGet package</span><span class="sxs-lookup"><span data-stu-id="250e5-103">Add the Relay NuGet package</span></span>
1. <span data-ttu-id="250e5-104">Right-click the newly created project and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="250e5-104">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="250e5-105">Click the **Browse** tab, then search for "Microsoft.Azure.Relay" and select the **Microsoft Azure Relay** item.</span><span class="sxs-lookup"><span data-stu-id="250e5-105">Click the **Browse** tab, then search for "Microsoft.Azure.Relay" and select the **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="250e5-106">Click **Install** to complete the installation, then close this dialog box.</span><span class="sxs-lookup"><span data-stu-id="250e5-106">Click **Install** to complete the installation, then close this dialog box.</span></span>

### <a name="write-some-code-to-receive-messages"></a><span data-ttu-id="250e5-107">Write some code to receive messages</span><span class="sxs-lookup"><span data-stu-id="250e5-107">Write some code to receive messages</span></span>
1. <span data-ttu-id="250e5-108">Replace the existing `using` statements at the top of the Program.cs file with the following statements:</span><span class="sxs-lookup"><span data-stu-id="250e5-108">Replace the existing `using` statements at the top of the Program.cs file with the following statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="250e5-109">Add constants to the `Program` class for the Hybrid Connection connection details.</span><span class="sxs-lookup"><span data-stu-id="250e5-109">Add constants to the `Program` class for the Hybrid Connection connection details.</span></span> <span data-ttu-id="250e5-110">Replace the placeholders in brackets with the proper values that were obtained when creating the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="250e5-110">Replace the placeholders in brackets with the proper values that were obtained when creating the Hybrid Connection.</span></span> <span data-ttu-id="250e5-111">Be sure to use the fully qualified namespace name:</span><span class="sxs-lookup"><span data-stu-id="250e5-111">Be sure to use the fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="250e5-112">Add the following new method called `ProcessMessagesOnConnection` to the `Program` class:</span><span class="sxs-lookup"><span data-stu-id="250e5-112">Add the following new method called `ProcessMessagesOnConnection` to the `Program` class:</span></span>
   
    ```csharp
    // Method is used to initiate connection
    private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
    {
        Console.WriteLine("New session");
   
        // The connection is a fully bidrectional stream. 
        // We put a stream reader and a stream writer over it 
        // which allows us to read UTF-8 text that comes from 
        // the sender and to write text replies back.
        var reader = new StreamReader(relayConnection);
        var writer = new StreamWriter(relayConnection) { AutoFlush = true };
        while (!cts.IsCancellationRequested)
        {
            try
            {
                // Read a line of input until a newline is encountered
                var line = await reader.ReadLineAsync();
   
                if (string.IsNullOrEmpty(line))
                {
                    // If there's no input data, we will signal that 
                    // we will no longer send data on this connection
                    // and then break out of the processing loop.
                    await relayConnection.ShutdownAsync(cts.Token);
                    break;
                }
   
                // Output the line on the console
                Console.WriteLine(line);
   
                // Write the line back to the client, prepending "Echo:"
                await writer.WriteLineAsync($"Echo: {line}");
            }
            catch (IOException)
            {
                // Catch an IO exception that is likely caused because
                // the client disconnected.
                Console.WriteLine("Client closed connection");
                break;
            }
        }
   
        Console.WriteLine("End session");
   
        // Closing the connection
        await relayConnection.CloseAsync(cts.Token);
    }
    ```
4. <span data-ttu-id="250e5-113">Add another new method called `RunAsync` to the `Program` class, as follows:</span><span class="sxs-lookup"><span data-stu-id="250e5-113">Add another new method called `RunAsync` to the `Program` class, as follows:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        var cts = new CancellationTokenSource();
   
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Subscribe to the status events
        listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
        listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
        listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
        // Opening the listener will establish the control channel to
        // the Azure Relay service. The control channel will be continuously 
        // maintained and reestablished when connectivity is disrupted.
        await listener.OpenAsync(cts.Token);
        Console.WriteLine("Server listening");
   
        // Providing callback for cancellation token that will close the listener.
        cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
        // Start a new thread that will continuously read the console.
        new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
        // Accept the next available, pending connection request. 
        // Shutting down the listener will allow a clean exit with 
        // this method returning null
        while (true)
        {
            var relayConnection = await listener.AcceptConnectionAsync();
            if (relayConnection == null)
            {
                break;
            }
   
            ProcessMessagesOnConnection(relayConnection, cts);
        }
   
        // Close the listener after we exit the processing loop
        await listener.CloseAsync(cts.Token);
    }
    ```
5. <span data-ttu-id="250e5-114">Add the following line of code to the `Main` method in the `Program` class.</span><span class="sxs-lookup"><span data-stu-id="250e5-114">Add the following line of code to the `Main` method in the `Program` class.</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="250e5-115">Here is what your Program.cs should look like:</span><span class="sxs-lookup"><span data-stu-id="250e5-115">Here is what your Program.cs should look like:</span></span>
   
    ```csharp
    namespace Server
    {
        using System;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.Relay;
   
        public class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            public static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                var cts = new CancellationTokenSource();
   
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Subscribe to the status events
                listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
                listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
                listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
                // Opening the listener will establish the control channel to
                // the Azure Relay service. The control channel will be continuously 
                // maintained and reestablished when connectivity is disrupted.
                await listener.OpenAsync(cts.Token);
                Console.WriteLine("Server listening");
   
                // Providing callback for cancellation token that will close the listener.
                cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
                // Start a new thread that will continuously read the console.
                new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
                // Accept the next available, pending connection request. 
                // Shutting down the listener will allow a clean exit with 
                // this method returning null
                while (true)
                {
                    var relayConnection = await listener.AcceptConnectionAsync();
                    if (relayConnection == null)
                    {
                        break;
                    }
   
                    ProcessMessagesOnConnection(relayConnection, cts);
                }
   
                // Close the listener after we exit the processing loop
                await listener.CloseAsync(cts.Token);
            }
   
            private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
            {
                Console.WriteLine("New session");
   
                // The connection is a fully bidrectional stream. 
                // We put a stream reader and a stream writer over it 
                // which allows us to read UTF-8 text that comes from 
                // the sender and to write text replies back.
                var reader = new StreamReader(relayConnection);
                var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                while (!cts.IsCancellationRequested)
                {
                    try
                    {
                        // Read a line of input until a newline is encountered
                        var line = await reader.ReadLineAsync();
   
                        if (string.IsNullOrEmpty(line))
                        {
                            // If there's no input data, we will signal that 
                            // we will no longer send data on this connection
                            // and then break out of the processing loop.
                            await relayConnection.ShutdownAsync(cts.Token);
                            break;
                        }
   
                        // Output the line on the console
                        Console.WriteLine(line);
   
                        // Write the line back to the client, prepending "Echo:"
                        await writer.WriteLineAsync($"Echo: {line}");
                    }
                    catch (IOException)
                    {
                        // Catch an IO exception that is likely caused because
                        // the client disconnected.
                        Console.WriteLine("Client closed connection");
                        break;
                    }
                }
   
                Console.WriteLine("End session");
   
                // Closing the connection
                await relayConnection.CloseAsync(cts.Token);
            }
        }
    }
    ```

