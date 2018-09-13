---
title: Polling Long-Running Operations | Microsoft Docs
description: This topic shows how to poll long-running operations.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: cb7d28c7b556b12fe5441813acc4d8d91e301de4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662384"
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="039ee-103">Delivering Live Streaming with Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="039ee-103">Delivering Live Streaming with Azure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="039ee-104">Overview</span><span class="sxs-lookup"><span data-stu-id="039ee-104">Overview</span></span>
<span data-ttu-id="039ee-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span><span class="sxs-lookup"><span data-stu-id="039ee-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="039ee-106">These operations are long-running.</span><span class="sxs-lookup"><span data-stu-id="039ee-106">These operations are long-running.</span></span>

<span data-ttu-id="039ee-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span><span class="sxs-lookup"><span data-stu-id="039ee-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="039ee-108">For example, when you call channel.Start(), the method returns after the channel is started.</span><span class="sxs-lookup"><span data-stu-id="039ee-108">For example, when you call channel.Start(), the method returns after the channel is started.</span></span> <span data-ttu-id="039ee-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="039ee-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="039ee-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span><span class="sxs-lookup"><span data-stu-id="039ee-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span></span> <span data-ttu-id="039ee-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span><span class="sxs-lookup"><span data-stu-id="039ee-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="039ee-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span><span class="sxs-lookup"><span data-stu-id="039ee-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span></span> <span data-ttu-id="039ee-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span><span class="sxs-lookup"><span data-stu-id="039ee-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span></span> <span data-ttu-id="039ee-114">The browser could then ask the web service to get the operation status based on the ID.</span><span class="sxs-lookup"><span data-stu-id="039ee-114">The browser could then ask the web service to get the operation status based on the ID.</span></span> <span data-ttu-id="039ee-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span><span class="sxs-lookup"><span data-stu-id="039ee-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="039ee-116">These APIs are called “non-polling methods”.</span><span class="sxs-lookup"><span data-stu-id="039ee-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="039ee-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="039ee-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="039ee-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span><span class="sxs-lookup"><span data-stu-id="039ee-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span></span> <span data-ttu-id="039ee-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="039ee-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="039ee-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span><span class="sxs-lookup"><span data-stu-id="039ee-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="039ee-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span><span class="sxs-lookup"><span data-stu-id="039ee-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span></span> <span data-ttu-id="039ee-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="039ee-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="example"></a><span data-ttu-id="039ee-123">Example</span><span class="sxs-lookup"><span data-stu-id="039ee-123">Example</span></span>
<span data-ttu-id="039ee-124">The following example defines a class called **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="039ee-124">The following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="039ee-125">This class definition could be a starting point for your web service class definition.</span><span class="sxs-lookup"><span data-stu-id="039ee-125">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="039ee-126">For simplicity, the following examples use the non-async versions of methods.</span><span class="sxs-lookup"><span data-stu-id="039ee-126">For simplicity, the following examples use the non-async versions of methods.</span></span>

<span data-ttu-id="039ee-127">The example also shows how the client might use this class.</span><span class="sxs-lookup"><span data-stu-id="039ee-127">The example also shows how the client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="039ee-128">ChannelOperations class definition</span><span class="sxs-lookup"><span data-stu-id="039ee-128">ChannelOperations class definition</span></span>
    /// <summary> 
    /// The ChannelOperations class only implements 
    /// the Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from the App.config file.
        private static readonly string _mediaServicesAccountName =
            ConfigurationManager.AppSettings["MediaServicesAccountName"];
        private static readonly string _mediaServicesAccountKey =
            ConfigurationManager.AppSettings["MediaServicesAccountKey"];

        // Field for service context.
        private static CloudMediaContext _context = null;
        private static MediaServicesCredentials _cachedCredentials = null;

        public ChannelOperations()
        {
                _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName,
                    _mediaServicesAccountKey);

                _context = new CloudMediaContext(_cachedCredentials);    }

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

### <a name="the-client-code"></a><span data-ttu-id="039ee-129">The client code</span><span class="sxs-lookup"><span data-stu-id="039ee-129">The client code</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="039ee-130">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="039ee-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="039ee-131">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="039ee-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

