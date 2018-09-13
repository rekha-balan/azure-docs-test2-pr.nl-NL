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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Azure Relay Hybrid Connections .NET Standard API overview
This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Relay Connection String Builder
The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class will format connection strings that are specific to Relay Hybrid Connections. You can use it to verify the format of a connection string, or to build a connection string from scratch. See the following for an example.

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

You can also pass a connection string directly to the `RelayConnectionStringBuilder` method. This will enable you to verify that the connection string is in a valid format, and the constructor will throw an `ArgumentException` if any of the parameters are invalid.

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

## <a name="hybrid-connection-stream"></a>Hybrid Connection Stream
The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Getting a Hybrid Connection Stream

#### <a name="listener"></a>Listener
Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` as follows:

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Client
Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` as follows:

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Receiving data
The [HybridConnectionStream][HCStream] class allows for two way communication. In most use cases, you will want to continuously receive from the stream. If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx), which enables easier parsing of the data. For example, you can read data as text, rather than as `byte[]`.

The following code reads individual lines of text from the stream until a cancellation is requested.

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

### <a name="sending-data"></a>Sending data
Once you have a connection established, you can send a message to the Relay endpoint. Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`. The following example shows how to do this:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Next steps
To learn more about Azure Relay, visit these links:

* [Microsoft.Azure.Relay reference](/dotnet/api/microsoft.azure.relay)
* [What is Azure Relay?](relay-what-is-it.md)
* [Available Relay APIs](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener