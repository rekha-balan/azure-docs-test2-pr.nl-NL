---
title: Overview of Azure Relay .NET Standard APIs | Microsoft Docs
description: Azure Relay .NET Standard API overview
services: service-bus-relay
documentationcenter: na
author: spelluru
manager: timlt
editor: ''
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2018
ms.author: spelluru
ms.openlocfilehash: a6a1706c8d1e849fd1bb4309c46063dd3f9439c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824231"
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="b6e65-103">Azure Relay Hybrid Connections .NET Standard API overview</span><span class="sxs-lookup"><span data-stu-id="b6e65-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="b6e65-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="b6e65-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder-class"></a><span data-ttu-id="b6e65-105">Relay Connection String Builder class</span><span class="sxs-lookup"><span data-stu-id="b6e65-105">Relay Connection String Builder class</span></span>

<span data-ttu-id="b6e65-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="b6e65-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="b6e65-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span><span class="sxs-lookup"><span data-stu-id="b6e65-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="b6e65-108">See the following code for an example:</span><span class="sxs-lookup"><span data-stu-id="b6e65-108">See the following code for an example:</span></span>

```csharp
var endpoint = "[Relay namespace]";
var entityPath = "[Name of the Hybrid Connection]";
var sharedAccessKeyName = "[SAS key name]";
var sharedAccessKey = "[SAS key value]";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

<span data-ttu-id="b6e65-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span><span class="sxs-lookup"><span data-stu-id="b6e65-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="b6e65-110">This operation enables you to verify that the connection string is in a valid format.</span><span class="sxs-lookup"><span data-stu-id="b6e65-110">This operation enables you to verify that the connection string is in a valid format.</span></span> <span data-ttu-id="b6e65-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="b6e65-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "[RelayConnectionString]";
// Declare the connectionStringBuilder so that it can be used outside of the loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create the connectionStringBuilder using the supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="b6e65-112">Hybrid connection stream</span><span class="sxs-lookup"><span data-stu-id="b6e65-112">Hybrid connection stream</span></span>

<span data-ttu-id="b6e65-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="b6e65-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="b6e65-114">Getting a Hybrid connection stream</span><span class="sxs-lookup"><span data-stu-id="b6e65-114">Getting a Hybrid connection stream</span></span>

#### <a name="listener"></a><span data-ttu-id="b6e65-115">Listener</span><span class="sxs-lookup"><span data-stu-id="b6e65-115">Listener</span></span>

<span data-ttu-id="b6e65-116">Using a [HybridConnectionListener][HCListener] object, you can obtain a `HybridConnectionStream` object as follows:</span><span class="sxs-lookup"><span data-stu-id="b6e65-116">Using a [HybridConnectionListener][HCListener] object, you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="b6e65-117">Client</span><span class="sxs-lookup"><span data-stu-id="b6e65-117">Client</span></span>

<span data-ttu-id="b6e65-118">Using a [HybridConnectionClient][HCClient] object, you can obtain a `HybridConnectionStream` object as follows:</span><span class="sxs-lookup"><span data-stu-id="b6e65-118">Using a [HybridConnectionClient][HCClient] object, you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="b6e65-119">Receiving data</span><span class="sxs-lookup"><span data-stu-id="b6e65-119">Receiving data</span></span>

<span data-ttu-id="b6e65-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span><span class="sxs-lookup"><span data-stu-id="b6e65-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="b6e65-121">In most cases, you continuously receive from the stream.</span><span class="sxs-lookup"><span data-stu-id="b6e65-121">In most cases, you continuously receive from the stream.</span></span> <span data-ttu-id="b6e65-122">If you are reading text from the stream, you might also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span><span class="sxs-lookup"><span data-stu-id="b6e65-122">If you are reading text from the stream, you might also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span></span> <span data-ttu-id="b6e65-123">For example, you can read data as text, rather than as `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="b6e65-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="b6e65-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span><span class="sxs-lookup"><span data-stu-id="b6e65-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel the while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from the 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of the processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="b6e65-125">Sending data</span><span class="sxs-lookup"><span data-stu-id="b6e65-125">Sending data</span></span>

<span data-ttu-id="b6e65-126">Once you have a connection established, you can send a message to the Relay endpoint.</span><span class="sxs-lookup"><span data-stu-id="b6e65-126">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="b6e65-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="b6e65-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="b6e65-128">The following example shows how to do this:</span><span class="sxs-lookup"><span data-stu-id="b6e65-128">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="b6e65-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span><span class="sxs-lookup"><span data-stu-id="b6e65-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="b6e65-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6e65-130">Next steps</span></span>

<span data-ttu-id="b6e65-131">To learn more about Azure Relay, visit these links:</span><span class="sxs-lookup"><span data-stu-id="b6e65-131">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="b6e65-132">Microsoft.Azure.Relay reference</span><span class="sxs-lookup"><span data-stu-id="b6e65-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="b6e65-133">What is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="b6e65-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="b6e65-134">Available Relay APIs</span><span class="sxs-lookup"><span data-stu-id="b6e65-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener