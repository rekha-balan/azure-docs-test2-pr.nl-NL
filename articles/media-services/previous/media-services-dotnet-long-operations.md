---
title: Polling Long-Running Operations | Microsoft Docs
description: This topic shows how to poll long-running operations.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: fa456a2d0bb427af80d67a0b971fe8bd41bb7868
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966864"
---
# <a name="delivering-live-streaming-with-azure-media-services"></a>Delivering Live Streaming with Azure Media Services

## <a name="overview"></a>Overview

Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel). These operations are long-running.

The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals). For example, when you call channel.Start(), the method returns after the channel is started. You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”. These methods (especially the Async version) are recommended for rich client applications and/or stateful services.

There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually. A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser. The browser could then ask the web service to get the operation status based on the ID. The Media Services .NET SDK provides APIs that are useful for this scenario. These APIs are called “non-polling methods”.
The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation). Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation. The Send*OperationName*OperationAsync methods return **Task<IOperation>**.

Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.

To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class. Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.

## <a name="create-and-configure-a-visual-studio-project"></a>Create and configure a Visual Studio project

Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Example

The following example defines a class called **ChannelOperations**. This class definition could be a starting point for your web service class definition. For simplicity, the following examples use the non-async versions of methods.

The example also shows how the client might use this class.

### <a name="channeloperations-class-definition"></a>ChannelOperations class definition

```csharp
using Microsoft.WindowsAzure.MediaServices.Client;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Net;

/// <summary> 
/// The ChannelOperations class only implements 
/// the Channel’s creation operation. 
/// </summary> 
public class ChannelOperations
{
    // Read values from the App.config file.
    private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AMSAADTenantDomain"];
    private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
    private static readonly string _AMSClientId =
        ConfigurationManager.AppSettings["AMSClientId"];
    private static readonly string _AMSClientSecret =
        ConfigurationManager.AppSettings["AMSClientSecret"];

    // Field for service context.
    private static CloudMediaContext _context = null;

    public ChannelOperations()
    {
        AzureAdTokenCredentials tokenCredentials = 
            new AzureAdTokenCredentials(_AADTenantDomain,
                new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                AzureEnvironments.AzureCloudEnvironment);

        var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

        _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    }

    /// <summary>  
    /// Initiates the creation of a new channel.  
    /// </summary>  
    /// <param name="channelName">Name to be given to the new channel</param>  
    /// <returns>  
    /// Operation Id for the long running operation being executed by Media Services. 
    /// Use this operation Id to poll for the channel creation status. 
    /// </returns> 
    public string StartChannelCreation(string channelName)
    {
        var operation = _context.Channels.SendCreateOperation(
            new ChannelCreationOptions
            {
                Name = channelName,
                Input = CreateChannelInput(),
                Preview = CreateChannelPreview(),
                Output = CreateChannelOutput()
            });

        return operation.Id;
    }

    /// <summary> 
    /// Checks if the operation has been completed. 
    /// If the operation succeeded, the created channel Id is returned in the out parameter.
    /// </summary> 
    /// <param name="operationId">The operation Id.</param> 
    /// <param name="channel">
    /// If the operation succeeded, 
    /// the created channel Id is returned in the out parameter.</param>
    /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
    public bool IsCompleted(string operationId, out string channelId)
    {
        IOperation operation = _context.Operations.GetOperation(operationId);
        bool completed = false;

        channelId = null;

        switch (operation.State)
        {
            case OperationState.Failed:
                // Handle the failure. 
                // For example, throw an exception. 
                // Use the following information in the exception: operationId, operation.ErrorMessage.
                break;
            case OperationState.Succeeded:
                completed = true;
                channelId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                break;
        }
        return completed;
    }

    private static ChannelInput CreateChannelInput()
    {
        return new ChannelInput
        {
            StreamingProtocol = StreamingProtocol.RTMP,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                    {
                        new IPRange
                        {
                            Name = "TestChannelInput001",
                            Address = IPAddress.Parse("0.0.0.0"),
                            SubnetPrefixLength = 0
                        }
                    }
            }
        };
    }

    private static ChannelPreview CreateChannelPreview()
    {
        return new ChannelPreview
        {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                    {
                        new IPRange
                        {
                            Name = "TestChannelPreview001",
                            Address = IPAddress.Parse("0.0.0.0"),
                            SubnetPrefixLength = 0
                        }
                    }
            }
        };
    }

    private static ChannelOutput CreateChannelOutput()
    {
        return new ChannelOutput
        {
            Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
        };
    }
}
```

### <a name="the-client-code"></a>The client code

```csharp
ChannelOperations channelOperations = new ChannelOperations();
string opId = channelOperations.StartChannelCreation("MyChannel001");

string channelId = null;
bool isCompleted = false;

while (isCompleted == false)
{
    System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
    isCompleted = channelOperations.IsCompleted(opId, out channelId);
}

// If we got here, we should have the newly created channel id.
Console.WriteLine(channelId);
```

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

