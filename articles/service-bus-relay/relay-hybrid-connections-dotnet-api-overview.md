---
title: Overview of the Azure Relay .NET Standard APIs | Microsoft Docs
description: Relay .NET Standard API overview
services: service-bus-relay
documentationcenter: na
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: jotaub
ms.openlocfilehash: d1756dee37771941caae781682b342986c7ecbc9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563577"
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="6d3cb-103">Azure Relay Hybrid Connections .NET Standard API overview</span><span class="sxs-lookup"><span data-stu-id="6d3cb-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>
<span data-ttu-id="6d3cb-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="6d3cb-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="6d3cb-105">Relay Connection String Builder</span><span class="sxs-lookup"><span data-stu-id="6d3cb-105">Relay Connection String Builder</span></span>
<span data-ttu-id="6d3cb-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class will format connection strings that are specific to Relay Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class will format connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="6d3cb-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="6d3cb-108">See the following for an example.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-108">See the following for an example.</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of the Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

<span data-ttu-id="6d3cb-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="6d3cb-110">This will enable you to verify that the connection string is in a valid format, and the constructor will throw an `ArgumentException` if any of the parameters are invalid.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-110">This will enable you to verify that the connection string is in a valid format, and the constructor will throw an `ArgumentException` if any of the parameters are invalid.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
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

## <a name="hybrid-connection-stream"></a><span data-ttu-id="6d3cb-111">Hybrid Connection Stream</span><span class="sxs-lookup"><span data-stu-id="6d3cb-111">Hybrid Connection Stream</span></span>
<span data-ttu-id="6d3cb-112">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="6d3cb-112">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="6d3cb-113">Getting a Hybrid Connection Stream</span><span class="sxs-lookup"><span data-stu-id="6d3cb-113">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="6d3cb-114">Listener</span><span class="sxs-lookup"><span data-stu-id="6d3cb-114">Listener</span></span>
<span data-ttu-id="6d3cb-115">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` as follows:</span><span class="sxs-lookup"><span data-stu-id="6d3cb-115">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="6d3cb-116">Client</span><span class="sxs-lookup"><span data-stu-id="6d3cb-116">Client</span></span>
<span data-ttu-id="6d3cb-117">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` as follows:</span><span class="sxs-lookup"><span data-stu-id="6d3cb-117">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="6d3cb-118">Receiving data</span><span class="sxs-lookup"><span data-stu-id="6d3cb-118">Receiving data</span></span>
<span data-ttu-id="6d3cb-119">The [HybridConnectionStream][HCStream] class allows for two way communication.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-119">The [HybridConnectionStream][HCStream] class allows for two way communication.</span></span> <span data-ttu-id="6d3cb-120">In most use cases, you will want to continuously receive from the stream.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-120">In most use cases, you will want to continuously receive from the stream.</span></span> <span data-ttu-id="6d3cb-121">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx), which enables easier parsing of the data.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-121">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx), which enables easier parsing of the data.</span></span> <span data-ttu-id="6d3cb-122">For example, you can read data as text, rather than as `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-122">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="6d3cb-123">The following code reads individual lines of text from the stream until a cancellation is requested.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-123">The following code reads individual lines of text from the stream until a cancellation is requested.</span></span>

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

### <a name="sending-data"></a><span data-ttu-id="6d3cb-124">Sending data</span><span class="sxs-lookup"><span data-stu-id="6d3cb-124">Sending data</span></span>
<span data-ttu-id="6d3cb-125">Once you have a connection established, you can send a message to the Relay endpoint.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-125">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="6d3cb-126">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-126">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="6d3cb-127">The following example shows how to do this:</span><span class="sxs-lookup"><span data-stu-id="6d3cb-127">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="6d3cb-128">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span><span class="sxs-lookup"><span data-stu-id="6d3cb-128">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="6d3cb-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d3cb-129">Next steps</span></span>
<span data-ttu-id="6d3cb-130">To learn more about Azure Relay, visit these links:</span><span class="sxs-lookup"><span data-stu-id="6d3cb-130">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="6d3cb-131">Microsoft.Azure.Relay reference</span><span class="sxs-lookup"><span data-stu-id="6d3cb-131">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="6d3cb-132">What is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="6d3cb-132">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="6d3cb-133">Available Relay APIs</span><span class="sxs-lookup"><span data-stu-id="6d3cb-133">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener