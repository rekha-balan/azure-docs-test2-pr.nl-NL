---
title: include file
description: include file
services: service-bus-relay
author: clemensv
ms.service: service-bus-relay
ms.topic: include
ms.date: 08/16/2018
ms.author: clemensv
ms.custom: include file
ms.openlocfilehash: e07d82b8a3aea4f0db0f5a071d78ea360cd611ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856623"
---
### <a name="create-a-console-application"></a><span data-ttu-id="e7abc-103">Create a console application</span><span class="sxs-lookup"><span data-stu-id="e7abc-103">Create a console application</span></span>

<span data-ttu-id="e7abc-104">If you have disabled the "Requires Client Authorization" option when creating the Relay, you can send requests to the Hybrid Connections URL with any browser.</span><span class="sxs-lookup"><span data-stu-id="e7abc-104">If you have disabled the "Requires Client Authorization" option when creating the Relay, you can send requests to the Hybrid Connections URL with any browser.</span></span> <span data-ttu-id="e7abc-105">For accessing protected endpoints, you need to create and pass a token in the `ServiceBusAuthorization` header, which is shown here.</span><span class="sxs-lookup"><span data-stu-id="e7abc-105">For accessing protected endpoints, you need to create and pass a token in the `ServiceBusAuthorization` header, which is shown here.</span></span>

<span data-ttu-id="e7abc-106">In Visual Studio, create a new **Console App (.NET Framework)** project.</span><span class="sxs-lookup"><span data-stu-id="e7abc-106">In Visual Studio, create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-the-relay-nuget-package"></a><span data-ttu-id="e7abc-107">Add the Relay NuGet package</span><span class="sxs-lookup"><span data-stu-id="e7abc-107">Add the Relay NuGet package</span></span>

1. <span data-ttu-id="e7abc-108">Right-click the newly created project, and then select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="e7abc-108">Right-click the newly created project, and then select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="e7abc-109">Select **Browse**, and then search for **Microsoft.Azure.Relay**.</span><span class="sxs-lookup"><span data-stu-id="e7abc-109">Select **Browse**, and then search for **Microsoft.Azure.Relay**.</span></span> <span data-ttu-id="e7abc-110">In the search results, select **Microsoft Azure Relay**.</span><span class="sxs-lookup"><span data-stu-id="e7abc-110">In the search results, select **Microsoft Azure Relay**.</span></span> 
3. <span data-ttu-id="e7abc-111">Select **Install** to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="e7abc-111">Select **Install** to complete the installation.</span></span> <span data-ttu-id="e7abc-112">Close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="e7abc-112">Close the dialog box.</span></span>

### <a name="write-code-to-send-requests"></a><span data-ttu-id="e7abc-113">Write code to send requests</span><span class="sxs-lookup"><span data-stu-id="e7abc-113">Write code to send requests</span></span>

1. <span data-ttu-id="e7abc-114">At the top of the Program.cs file, replace the existing `using` statements with the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="e7abc-114">At the top of the Program.cs file, replace the existing `using` statements with the following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Net.Http;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="e7abc-115">Add constants to the `Program` class for the hybrid connection details.</span><span class="sxs-lookup"><span data-stu-id="e7abc-115">Add constants to the `Program` class for the hybrid connection details.</span></span> <span data-ttu-id="e7abc-116">Replace the placeholders in brackets with the values that you obtained when you created the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="e7abc-116">Replace the placeholders in brackets with the values that you obtained when you created the hybrid connection.</span></span> <span data-ttu-id="e7abc-117">Be sure to use the fully qualified namespace name.</span><span class="sxs-lookup"><span data-stu-id="e7abc-117">Be sure to use the fully qualified namespace name.</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="e7abc-118">Add the following method to the `Program` class:</span><span class="sxs-lookup"><span data-stu-id="e7abc-118">Add the following method to the `Program` class:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                KeyName, Key);
        var uri = new Uri(string.Format("https://{0}/{1}", RelayNamespace, ConnectionName));
        var token = (await tokenProvider.GetTokenAsync(uri.AbsoluteUri, TimeSpan.FromHours(1))).TokenString;
        var client = new HttpClient();
        var request = new HttpRequestMessage()
        {
            RequestUri = uri,
            Method = HttpMethod.Get,
        };
        request.Headers.Add("ServiceBusAuthorization", token);
        var response = await client.SendAsync(request);
        Console.WriteLine(await response.Content.ReadAsStringAsync());        Console.ReadLine();
    }
    ```
4. <span data-ttu-id="e7abc-119">Add the following line of code to the `Main` method in the `Program` class.</span><span class="sxs-lookup"><span data-stu-id="e7abc-119">Add the following line of code to the `Main` method in the `Program` class.</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="e7abc-120">The Program.cs should look like this:</span><span class="sxs-lookup"><span data-stu-id="e7abc-120">The Program.cs should look like this:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
   
    namespace Client
    {
        class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
               var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                KeyName, Key);
                var uri = new Uri(string.Format("https://{0}/{1}", RelayNamespace, ConnectionName));
                var token = (await tokenProvider.GetTokenAsync(uri.AbsoluteUri, TimeSpan.FromHours(1))).TokenString;
                var client = new HttpClient();
                var request = new HttpRequestMessage()
                {
                    RequestUri = uri,
                    Method = HttpMethod.Get,
                };
                request.Headers.Add("ServiceBusAuthorization", token);
                var response = await client.SendAsync(request);
                Console.WriteLine(await response.Content.ReadAsStringAsync());
            }
        }
    }
    ```

