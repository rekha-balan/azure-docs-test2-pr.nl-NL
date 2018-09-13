---
title: include file
description: include file
services: service-bus-relay
author: clemensv
ms.service: service-bus-relay
ms.topic: include
ms.date: 05/02/2018
ms.author: clemensv
ms.custom: include file
ms.openlocfilehash: 2784102cdc778188f0874a15e3ff02e4cc2e3eb8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857266"
---
### <a name="create-a-console-application"></a><span data-ttu-id="b1572-103">Create a console application</span><span class="sxs-lookup"><span data-stu-id="b1572-103">Create a console application</span></span>

<span data-ttu-id="b1572-104">In Visual Studio, create a new **Console App (.NET Framework)** project.</span><span class="sxs-lookup"><span data-stu-id="b1572-104">In Visual Studio, create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-the-relay-nuget-package"></a><span data-ttu-id="b1572-105">Add the Relay NuGet package</span><span class="sxs-lookup"><span data-stu-id="b1572-105">Add the Relay NuGet package</span></span>

1. <span data-ttu-id="b1572-106">Right-click the newly created project, and then select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="b1572-106">Right-click the newly created project, and then select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="b1572-107">Select **Browse**, and then search for **Microsoft.Azure.Relay**.</span><span class="sxs-lookup"><span data-stu-id="b1572-107">Select **Browse**, and then search for **Microsoft.Azure.Relay**.</span></span> <span data-ttu-id="b1572-108">In the search results, select  **Microsoft Azure Relay**.</span><span class="sxs-lookup"><span data-stu-id="b1572-108">In the search results, select  **Microsoft Azure Relay**.</span></span> 
3. <span data-ttu-id="b1572-109">Select **Install** to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="b1572-109">Select **Install** to complete the installation.</span></span> <span data-ttu-id="b1572-110">Close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="b1572-110">Close the dialog box.</span></span>

### <a name="write-code-to-receive-messages"></a><span data-ttu-id="b1572-111">Write code to receive messages</span><span class="sxs-lookup"><span data-stu-id="b1572-111">Write code to receive messages</span></span>

1. <span data-ttu-id="b1572-112">At the top of the Program.cs file, replace the existing `using` statements with the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="b1572-112">At the top of the Program.cs file, replace the existing `using` statements with the following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="b1572-113">Add constants to the `Program` class for the hybrid connection details.</span><span class="sxs-lookup"><span data-stu-id="b1572-113">Add constants to the `Program` class for the hybrid connection details.</span></span> <span data-ttu-id="b1572-114">Replace the placeholders in brackets with the values that you obtained when you created the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="b1572-114">Replace the placeholders in brackets with the values that you obtained when you created the hybrid connection.</span></span> <span data-ttu-id="b1572-115">Be sure to use the fully qualified namespace name.</span><span class="sxs-lookup"><span data-stu-id="b1572-115">Be sure to use the fully qualified namespace name.</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```

3. <span data-ttu-id="b1572-116">Add the `RunAsync` method to the `Program` class:</span><span class="sxs-lookup"><span data-stu-id="b1572-116">Add the `RunAsync` method to the `Program` class:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        var cts = new CancellationTokenSource();
   
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Subscribe to the status events.
        listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
        listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
        listener.Online += (o, e) => { Console.WriteLine("Online"); };

        // Provide an HTTP request handler
        listener.RequestHandler = (context) =>
        {
            // Do something with context.Request.Url, HttpMethod, Headers, InputStream...
            context.Response.StatusCode = HttpStatusCode.OK;
            context.Response.StatusDescription = "OK, This is pretty neat";
            using (var sw = new StreamWriter(context.Response.OutputStream))
            {
                sw.WriteLine("hello!");
            }
            
            // The context MUST be closed here
            context.Response.Close();
        };
            
        // Opening the listener establishes the control channel to
        // the Azure Relay service. The control channel is continuously 
        // maintained, and is reestablished when connectivity is disrupted.
        await listener.OpenAsync();
        Console.WriteLine("Server listening");
    
        // Start a new thread that will continuously read the console.
        await Console.In.ReadLineAsync();
        
        // Close the listener after you exit the processing loop.
        await listener.CloseAsync();
    }
    ```
5. <span data-ttu-id="b1572-117">Add the following line of code to the `Main` method in the `Program` class:</span><span class="sxs-lookup"><span data-stu-id="b1572-117">Add the following line of code to the `Main` method in the `Program` class:</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="b1572-118">The completed Program.cs file should look like this:</span><span class="sxs-lookup"><span data-stu-id="b1572-118">The completed Program.cs file should look like this:</span></span>
   
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
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
           
                // Subscribe to the status events.
                listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
                listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
                listener.Online += (o, e) => { Console.WriteLine("Online"); };
        
                // Provide an HTTP request handler
                listener.RequestHandler = (context) =>
                {
                    // Do something with context.Request.Url, HttpMethod, Headers, InputStream...
                    context.Response.StatusCode = HttpStatusCode.OK;
                    context.Response.StatusDescription = "OK";
                    using (var sw = new StreamWriter(context.Response.OutputStream))
                    {
                        sw.WriteLine("hello!");
                    }
                    
                    // The context MUST be closed here
                    context.Response.Close();
                };
           
                // Opening the listener establishes the control channel to
                // the Azure Relay service. The control channel is continuously 
                // maintained, and is reestablished when connectivity is disrupted.
                await listener.OpenAsync();
                Console.WriteLine("Server listening");
           
                // Start a new thread that will continuously read the console.
                await Console.In.ReadLineAsync();
               
                // Close the listener after you exit the processing loop.
                await listener.CloseAsync();
            }
        }
    }
    ```

