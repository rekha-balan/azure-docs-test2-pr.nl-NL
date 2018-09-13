---
title: Stream live with Azure Media Services v3 using .NET Core | Microsoft Docs
description: This tutorial walks you through the steps of streaming live with Media Services v3 using .NET Core.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 06/06/2018
ms.author: juliako
ms.openlocfilehash: 82ef04993b597778c808d649032603a0f3672e4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857559"
---
# <a name="stream-live-with-azure-media-services-v3-using-net-core"></a><span data-ttu-id="e1546-103">Stream live with Azure Media Services v3 using .NET Core</span><span class="sxs-lookup"><span data-stu-id="e1546-103">Stream live with Azure Media Services v3 using .NET Core</span></span>

<span data-ttu-id="e1546-104">In Media Services, [LiveEvents](https://docs.microsoft.com/rest/api/media/liveevents) are responsible for processing live streaming content.</span><span class="sxs-lookup"><span data-stu-id="e1546-104">In Media Services, [LiveEvents](https://docs.microsoft.com/rest/api/media/liveevents) are responsible for processing live streaming content.</span></span> <span data-ttu-id="e1546-105">A LiveEvent provides an input endpoint (ingest URL) that you then provide to a live encoder.</span><span class="sxs-lookup"><span data-stu-id="e1546-105">A LiveEvent provides an input endpoint (ingest URL) that you then provide to a live encoder.</span></span> <span data-ttu-id="e1546-106">The LiveEvent receives live input streams from the live encoder and makes it available for streaming through one or more [StreamingEndpoints](https://docs.microsoft.com/rest/api/media/streamingendpoints).</span><span class="sxs-lookup"><span data-stu-id="e1546-106">The LiveEvent receives live input streams from the live encoder and makes it available for streaming through one or more [StreamingEndpoints](https://docs.microsoft.com/rest/api/media/streamingendpoints).</span></span> <span data-ttu-id="e1546-107">LiveEvents also provide a preview endpoint (preview URL) that you use to preview and validate your stream before further processing and delivery.</span><span class="sxs-lookup"><span data-stu-id="e1546-107">LiveEvents also provide a preview endpoint (preview URL) that you use to preview and validate your stream before further processing and delivery.</span></span> <span data-ttu-id="e1546-108">This tutorial shows how to use .NET Core to create a **pass-through** type of a live event.</span><span class="sxs-lookup"><span data-stu-id="e1546-108">This tutorial shows how to use .NET Core to create a **pass-through** type of a live event.</span></span> 

> [!NOTE]
> <span data-ttu-id="e1546-109">Make sure to review [Live streaming with Media Services v3](live-streaming-overview.md) before proceeding.</span><span class="sxs-lookup"><span data-stu-id="e1546-109">Make sure to review [Live streaming with Media Services v3](live-streaming-overview.md) before proceeding.</span></span> 

<span data-ttu-id="e1546-110">The tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="e1546-110">The tutorial shows you how to:</span></span>    

> [!div class="checklist"]
> * <span data-ttu-id="e1546-111">Create a Media Services account</span><span class="sxs-lookup"><span data-stu-id="e1546-111">Create a Media Services account</span></span>
> * <span data-ttu-id="e1546-112">Access the Media Services API</span><span class="sxs-lookup"><span data-stu-id="e1546-112">Access the Media Services API</span></span>
> * <span data-ttu-id="e1546-113">Configure the sample app</span><span class="sxs-lookup"><span data-stu-id="e1546-113">Configure the sample app</span></span>
> * <span data-ttu-id="e1546-114">Examine the code that performs live streaming</span><span class="sxs-lookup"><span data-stu-id="e1546-114">Examine the code that performs live streaming</span></span>
> * <span data-ttu-id="e1546-115">Watch the event with [Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/index.html) at http://ampdemo.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="e1546-115">Watch the event with [Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/index.html) at http://ampdemo.azureedge.net</span></span>
> * <span data-ttu-id="e1546-116">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e1546-116">Clean up resources</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="e1546-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e1546-117">Prerequisites</span></span>

<span data-ttu-id="e1546-118">The following are required to complete the tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1546-118">The following are required to complete the tutorial.</span></span>

* <span data-ttu-id="e1546-119">Install Visual Studio Code or Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e1546-119">Install Visual Studio Code or Visual Studio</span></span>
* <span data-ttu-id="e1546-120">A camera or a device (like laptop) that is used to broadcast an event.</span><span class="sxs-lookup"><span data-stu-id="e1546-120">A camera or a device (like laptop) that is used to broadcast an event.</span></span>
* <span data-ttu-id="e1546-121">An on-premises live encoder that converts signals from the camera to streams that are sent to the Media Services live streaming service.</span><span class="sxs-lookup"><span data-stu-id="e1546-121">An on-premises live encoder that converts signals from the camera to streams that are sent to the Media Services live streaming service.</span></span> <span data-ttu-id="e1546-122">The stream has to be in **RTMP** or **Smooth Streaming** format.</span><span class="sxs-lookup"><span data-stu-id="e1546-122">The stream has to be in **RTMP** or **Smooth Streaming** format.</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="e1546-123">Download the sample</span><span class="sxs-lookup"><span data-stu-id="e1546-123">Download the sample</span></span>

<span data-ttu-id="e1546-124">Clone a GitHub repository that contains the streaming .NET sample to your machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="e1546-124">Clone a GitHub repository that contains the streaming .NET sample to your machine using the following command:</span></span>  

 ```bash
 git clone https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials.git
 ```

<span data-ttu-id="e1546-125">The live streaming sample is located in the [Live](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials/tree/master/NETCore/Live/MediaV3LiveApp) folder.</span><span class="sxs-lookup"><span data-stu-id="e1546-125">The live streaming sample is located in the [Live](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials/tree/master/NETCore/Live/MediaV3LiveApp) folder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1546-126">This sample uses unique suffix for each resource.</span><span class="sxs-lookup"><span data-stu-id="e1546-126">This sample uses unique suffix for each resource.</span></span> <span data-ttu-id="e1546-127">If you cancel the debugging or terminate the app without running it through, you will end up with multiple LiveEvents in your account.</span><span class="sxs-lookup"><span data-stu-id="e1546-127">If you cancel the debugging or terminate the app without running it through, you will end up with multiple LiveEvents in your account.</span></span> <br/>
> <span data-ttu-id="e1546-128">Make sure to stop the running LiveEvents.</span><span class="sxs-lookup"><span data-stu-id="e1546-128">Make sure to stop the running LiveEvents.</span></span> <span data-ttu-id="e1546-129">Otherwise, you will be **billed**!</span><span class="sxs-lookup"><span data-stu-id="e1546-129">Otherwise, you will be **billed**!</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]

[!INCLUDE [media-services-v3-cli-access-api-include](../../../includes/media-services-v3-cli-access-api-include.md)]

## <a name="examine-the-code-that-performs-live-streaming"></a><span data-ttu-id="e1546-130">Examine the code that performs live streaming</span><span class="sxs-lookup"><span data-stu-id="e1546-130">Examine the code that performs live streaming</span></span>

<span data-ttu-id="e1546-131">This section examines functions defined in the [Program.cs](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials/blob/master/NETCore/Live/MediaV3LiveApp/Program.cs) file of the *MediaV3LiveApp* project.</span><span class="sxs-lookup"><span data-stu-id="e1546-131">This section examines functions defined in the [Program.cs](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials/blob/master/NETCore/Live/MediaV3LiveApp/Program.cs) file of the *MediaV3LiveApp* project.</span></span>

<span data-ttu-id="e1546-132">The sample creates a unique suffix for each resource so that we don't have name collisions if you run the sample multiple times without cleaning up.</span><span class="sxs-lookup"><span data-stu-id="e1546-132">The sample creates a unique suffix for each resource so that we don't have name collisions if you run the sample multiple times without cleaning up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1546-133">This sample uses unique suffix for each resource.</span><span class="sxs-lookup"><span data-stu-id="e1546-133">This sample uses unique suffix for each resource.</span></span> <span data-ttu-id="e1546-134">If you cancel the debugging or terminate the app without running it through, you will end up with multiple LiveEvents in your account.</span><span class="sxs-lookup"><span data-stu-id="e1546-134">If you cancel the debugging or terminate the app without running it through, you will end up with multiple LiveEvents in your account.</span></span> <br/>
> <span data-ttu-id="e1546-135">Make sure to stop the running LiveEvents.</span><span class="sxs-lookup"><span data-stu-id="e1546-135">Make sure to stop the running LiveEvents.</span></span> <span data-ttu-id="e1546-136">Otherwise, you will be **billed**!</span><span class="sxs-lookup"><span data-stu-id="e1546-136">Otherwise, you will be **billed**!</span></span>
 
### <a name="start-using-media-services-apis-with-net-sdk"></a><span data-ttu-id="e1546-137">Start using Media Services APIs with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e1546-137">Start using Media Services APIs with .NET SDK</span></span>

<span data-ttu-id="e1546-138">To start using Media Services APIs with .NET, you need to create an **AzureMediaServicesClient** object.</span><span class="sxs-lookup"><span data-stu-id="e1546-138">To start using Media Services APIs with .NET, you need to create an **AzureMediaServicesClient** object.</span></span> <span data-ttu-id="e1546-139">To create the object, you need to supply credentials needed for the client to connect to Azure using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1546-139">To create the object, you need to supply credentials needed for the client to connect to Azure using Azure AD.</span></span> <span data-ttu-id="e1546-140">In the code you cloned at the beginning of the article, the **GetCredentialsAsync** function creates the ServiceClientCredentials object based on the credentials supplied in local configuration file.</span><span class="sxs-lookup"><span data-stu-id="e1546-140">In the code you cloned at the beginning of the article, the **GetCredentialsAsync** function creates the ServiceClientCredentials object based on the credentials supplied in local configuration file.</span></span>  

```csharp
private static async Task<IAzureMediaServicesClient> CreateMediaServicesClientAsync(ConfigWrapper config)
{
    var credentials = await GetCredentialsAsync(config);

    return new AzureMediaServicesClient(config.ArmEndpoint, credentials)
    {
        SubscriptionId = config.SubscriptionId,
    };
}
```

### <a name="create-a-live-event"></a><span data-ttu-id="e1546-141">Create a live event</span><span class="sxs-lookup"><span data-stu-id="e1546-141">Create a live event</span></span>

<span data-ttu-id="e1546-142">This section shows how to create a **pass-through** type of LiveEvent (LiveEventEncodingType set to None).</span><span class="sxs-lookup"><span data-stu-id="e1546-142">This section shows how to create a **pass-through** type of LiveEvent (LiveEventEncodingType set to None).</span></span> <span data-ttu-id="e1546-143">If you want to create a LiveEvent that is enabled for live encoding set LiveEventEncodingType to Basic.</span><span class="sxs-lookup"><span data-stu-id="e1546-143">If you want to create a LiveEvent that is enabled for live encoding set LiveEventEncodingType to Basic.</span></span> 

<span data-ttu-id="e1546-144">Some other things that you might want to specify when creating the live event are:</span><span class="sxs-lookup"><span data-stu-id="e1546-144">Some other things that you might want to specify when creating the live event are:</span></span>

* <span data-ttu-id="e1546-145">Media Services location</span><span class="sxs-lookup"><span data-stu-id="e1546-145">Media Services location</span></span> 
* <span data-ttu-id="e1546-146">The streaming protocol for the Live Event (currently, the RTMP and Smooth Streaming protocols are supported)</span><span class="sxs-lookup"><span data-stu-id="e1546-146">The streaming protocol for the Live Event (currently, the RTMP and Smooth Streaming protocols are supported)</span></span>
       
    <span data-ttu-id="e1546-147">You cannot change the protocol option while the LiveEvent or its associated LiveOutputs are running.</span><span class="sxs-lookup"><span data-stu-id="e1546-147">You cannot change the protocol option while the LiveEvent or its associated LiveOutputs are running.</span></span> <span data-ttu-id="e1546-148">If you require different protocols, you should create separate LiveEvent for each streaming protocol.</span><span class="sxs-lookup"><span data-stu-id="e1546-148">If you require different protocols, you should create separate LiveEvent for each streaming protocol.</span></span>  
* <span data-ttu-id="e1546-149">IP restrictions on the ingest and preview.</span><span class="sxs-lookup"><span data-stu-id="e1546-149">IP restrictions on the ingest and preview.</span></span> <span data-ttu-id="e1546-150">You can define the IP addresses that are allowed to ingest a video to this LiveEvent.</span><span class="sxs-lookup"><span data-stu-id="e1546-150">You can define the IP addresses that are allowed to ingest a video to this LiveEvent.</span></span> <span data-ttu-id="e1546-151">Allowed IP addresses can be specified as either a single IP address (for example '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using an IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.252.0)').</span><span class="sxs-lookup"><span data-stu-id="e1546-151">Allowed IP addresses can be specified as either a single IP address (for example '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using an IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.252.0)').</span></span>
    
    <span data-ttu-id="e1546-152">If no IP addresses are specified and there is no rule definition, then no IP address will be allowed.</span><span class="sxs-lookup"><span data-stu-id="e1546-152">If no IP addresses are specified and there is no rule definition, then no IP address will be allowed.</span></span> <span data-ttu-id="e1546-153">To allow any IP address, create a rule and set 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="e1546-153">To allow any IP address, create a rule and set 0.0.0.0/0.</span></span>

<span data-ttu-id="e1546-154">When creating the event, you can specify to auto start it.</span><span class="sxs-lookup"><span data-stu-id="e1546-154">When creating the event, you can specify to auto start it.</span></span> 

```csharp
Console.WriteLine($"Creating a live event named {liveEventName}");
Console.WriteLine();

LiveEventPreview liveEventPreview = new LiveEventPreview
{
    AccessControl = new LiveEventPreviewAccessControl(
        ip: new IPAccessControl(
            allow: new IPRange[]
            {
                new IPRange (
                    name: "AllowAll",
                    address: "0.0.0.0",
                    subnetPrefixLength: 0
                )
            }
        )
    )
};

// This can sometimes take awhile. Be patient.
LiveEvent liveEvent = new LiveEvent(
    location: mediaService.Location, 
    description:"Sample LiveEvent for testing",
    vanityUrl:false,
    encoding: new LiveEventEncoding(
                // Set this to Basic to enable a transcoding LiveEvent, and None to enable a pass-through LiveEvent
                encodingType:LiveEventEncodingType.None, 
                presetName:null
            ),
    input: new LiveEventInput(LiveEventInputProtocol.RTMP), 
    preview: liveEventPreview,
    streamOptions: new List<StreamOptionsFlag?>()
    {
        // Set this to Default or Low Latency.
        // Low latency reduces the amount of buffering Media Services does.
        // Low latency can also reduce the stability of the live stream. 
        StreamOptionsFlag.Default
    }
);

Console.WriteLine($"Creating the LiveEvent, be patient this can take time...");
liveEvent = client.LiveEvents.Create(config.ResourceGroup, config.AccountName, liveEventName, liveEvent, autoStart:true);
```

### <a name="get-ingest-urls"></a><span data-ttu-id="e1546-155">Get ingest URLs</span><span class="sxs-lookup"><span data-stu-id="e1546-155">Get ingest URLs</span></span>

<span data-ttu-id="e1546-156">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span><span class="sxs-lookup"><span data-stu-id="e1546-156">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="e1546-157">The encoder uses these URLs to input a live stream.</span><span class="sxs-lookup"><span data-stu-id="e1546-157">The encoder uses these URLs to input a live stream.</span></span>


```csharp
// Get the input endpoint to configure the on-premises encoder with
string ingestUrl = liveEvent.Input.Endpoints.First().Url;
Console.WriteLine($"The ingest url to configure the on-premises encoder with is:");
Console.WriteLine($"\t{ingestUrl}");
Console.WriteLine();
```

### <a name="get-the-preview-url"></a><span data-ttu-id="e1546-158">Get the preview URL</span><span class="sxs-lookup"><span data-stu-id="e1546-158">Get the preview URL</span></span>

<span data-ttu-id="e1546-159">Use the previewEndpoint to preview and verify that the input from the encoder is actually being received.</span><span class="sxs-lookup"><span data-stu-id="e1546-159">Use the previewEndpoint to preview and verify that the input from the encoder is actually being received.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1546-160">Make sure that the video is flowing to the Preview URL before continuing!</span><span class="sxs-lookup"><span data-stu-id="e1546-160">Make sure that the video is flowing to the Preview URL before continuing!</span></span>

```sharp
string previewEndpoint = liveEvent.Preview.Endpoints.First().Url;
Console.WriteLine($"The preview url is:");
Console.WriteLine($"\t{previewEndpoint}");
Console.WriteLine();

Console.WriteLine($"Open the live preview in your browser and use the Azure Media Player to monitor the preview playback:");
Console.WriteLine($"\thttps://ampdemo.azureedge.net/?url={previewEndpoint}");
Console.WriteLine();
```

### <a name="create-and-manage-liveevents-and-liveoutputs"></a><span data-ttu-id="e1546-161">Create and manage LiveEvents and LiveOutputs</span><span class="sxs-lookup"><span data-stu-id="e1546-161">Create and manage LiveEvents and LiveOutputs</span></span>

<span data-ttu-id="e1546-162">Once you have the stream flowing into the LiveEvent, you can begin the streaming event by creating an Asset, LiveOutput, and StreamingLocator.</span><span class="sxs-lookup"><span data-stu-id="e1546-162">Once you have the stream flowing into the LiveEvent, you can begin the streaming event by creating an Asset, LiveOutput, and StreamingLocator.</span></span> <span data-ttu-id="e1546-163">This will archive the stream and make it available to viewers through the StreamingEndpoint.</span><span class="sxs-lookup"><span data-stu-id="e1546-163">This will archive the stream and make it available to viewers through the StreamingEndpoint.</span></span> 

#### <a name="create-an-asset"></a><span data-ttu-id="e1546-164">Create an Asset</span><span class="sxs-lookup"><span data-stu-id="e1546-164">Create an Asset</span></span>

<span data-ttu-id="e1546-165">Create an Asset for the LiveOutput to use.</span><span class="sxs-lookup"><span data-stu-id="e1546-165">Create an Asset for the LiveOutput to use.</span></span>

```csharp
string assetName = "archiveAsset" + uniqueness;
Console.WriteLine($"Creating an asset named {assetName}");
Console.WriteLine();
Asset asset = client.Assets.CreateOrUpdate(config.ResourceGroup, config.AccountName, assetName, new Asset());
```

#### <a name="create-a-liveoutput"></a><span data-ttu-id="e1546-166">Create a LiveOutput</span><span class="sxs-lookup"><span data-stu-id="e1546-166">Create a LiveOutput</span></span>

```csharp
string manifestName = "output";
string liveOutputName = "liveOutput" + uniqueness;
Console.WriteLine($"Creating a live output named {liveOutputName}");
Console.WriteLine();

LiveOutput liveOutput = new LiveOutput(assetName: asset.Name, manifestName: manifestName, archiveWindowLength: TimeSpan.FromMinutes(10));
liveOutput = client.LiveOutputs.Create(config.ResourceGroup, config.AccountName, liveEventName, liveOutputName, liveOutput);
```

#### <a name="create-a-streaminglocator"></a><span data-ttu-id="e1546-167">Create a StreamingLocator</span><span class="sxs-lookup"><span data-stu-id="e1546-167">Create a StreamingLocator</span></span>

> [!NOTE]
> <span data-ttu-id="e1546-168">When your Media Services account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="e1546-168">When your Media Services account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="e1546-169">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="e1546-169">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 


```csharp
StreamingLocator locator = new StreamingLocator(assetName: assetName, streamingPolicyName: PredefinedStreamingPolicy.ClearStreamingOnly);
locator = client.StreamingLocators.Create(config.ResourceGroup, config.AccountName, streamingLocatorName, locator);

// Get the default Streaming Endpoint on the account
StreamingEndpoint streamingEndpoint = client.StreamingEndpoints.Get(config.ResourceGroup, config.AccountName, "default");

// If it's not running, Start it. 
if (streamingEndpoint.ResourceState != StreamingEndpointResourceState.Running)
{
    Console.WriteLine("Streaming Endpoint was Stopped, restarting now..");
    client.StreamingEndpoints.Start(config.ResourceGroup, config.AccountName, "default");
}

// Get the url to stream the output
ListPathsResponse paths = await client.StreamingLocators.ListPathsAsync(resourceGroupName, accountName, locatorName);

foreach (StreamingPath path in paths.StreamingPaths)
{
    UriBuilder uriBuilder = new UriBuilder();
    uriBuilder.Scheme = "https";
    uriBuilder.Host = streamingEndpoint.HostName;

    uriBuilder.Path = path.Paths[0];
    // Get the URL from the uriBuilder: uriBuilder.ToString()
}
```

### <a name="cleaning-up-resources-in-your-media-services-account"></a><span data-ttu-id="e1546-170">Cleaning up resources in your Media Services account</span><span class="sxs-lookup"><span data-stu-id="e1546-170">Cleaning up resources in your Media Services account</span></span>

<span data-ttu-id="e1546-171">If you are done streaming events and want to clean up the resources provisioned earlier, follow the following procedure.</span><span class="sxs-lookup"><span data-stu-id="e1546-171">If you are done streaming events and want to clean up the resources provisioned earlier, follow the following procedure.</span></span>

* <span data-ttu-id="e1546-172">Stop pushing the stream from the encoder.</span><span class="sxs-lookup"><span data-stu-id="e1546-172">Stop pushing the stream from the encoder.</span></span>
* <span data-ttu-id="e1546-173">Stop the LiveEvent.</span><span class="sxs-lookup"><span data-stu-id="e1546-173">Stop the LiveEvent.</span></span> <span data-ttu-id="e1546-174">Once the LiveEvent is stopped, it will not incur any charges.</span><span class="sxs-lookup"><span data-stu-id="e1546-174">Once the LiveEvent is stopped, it will not incur any charges.</span></span> <span data-ttu-id="e1546-175">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span><span class="sxs-lookup"><span data-stu-id="e1546-175">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="e1546-176">You can stop your StreamingEndpoint, unless you want to continue to provide the archive of your live event as an on-demand stream.</span><span class="sxs-lookup"><span data-stu-id="e1546-176">You can stop your StreamingEndpoint, unless you want to continue to provide the archive of your live event as an on-demand stream.</span></span> <span data-ttu-id="e1546-177">If the LiveEvent is in stopped state, it will not incur any charges.</span><span class="sxs-lookup"><span data-stu-id="e1546-177">If the LiveEvent is in stopped state, it will not incur any charges.</span></span>

```csharp
private static void CleanupLiveEventAndOutput(IAzureMediaServicesClient client, string resourceGroup, string accountName, string liveEventName, string liveOutputName)
{
    // Delete the LiveOutput
    client.LiveOutputs.Delete(resourceGroup, accountName, liveEventName, liveOutputName);

    // Stop and delete the LiveEvent
    client.LiveEvents.Stop(resourceGroup, accountName, liveEventName);
    client.LiveEvents.Delete(resourceGroup, accountName, liveEventName);
}

private static void CleanupLocatorAssetAndStreamingEndpoint(IAzureMediaServicesClient client, string resourceGroup, string accountName, string streamingLocatorName, string assetName)
{
    // Delete the Streaming Locator
    client.StreamingLocators.Delete(resourceGroup, accountName, streamingLocatorName);

    // Delete the Archive Asset
    client.Assets.Delete(resourceGroup, accountName, assetName);
}

private static void CleanupAccount(IAzureMediaServicesClient client, string resourceGroup, string accountName)
{
    try{
        Console.WriteLine("Cleaning up the resources used, stopping the LiveEvent. This can take a few minutes to complete.");
        Console.WriteLine();

        var events = client.LiveEvents.List(resourceGroup, accountName);
        
        foreach (LiveEvent l in events)
        {
            if (l.Name == liveEventName){
                var outputs = client.LiveOutputs.List(resourceGroup, accountName, l.Name);

                foreach (LiveOutput o in outputs)
                {
                    client.LiveOutputs.Delete(resourceGroup, accountName, l.Name, o.Name);
                    Console.WriteLine($"LiveOutput: {o.Name} deleted from LiveEvent {l.Name}. The archived Asset and Streaming URLs are still retained for on-demand viewing.");
                }

                if (l.ResourceState == LiveEventResourceState.Running){
                    client.LiveEvents.Stop(resourceGroup, accountName, l.Name);
                    Console.WriteLine($"LiveEvent: {l.Name} Stopped.");
                    client.LiveEvents.Delete(resourceGroup, accountName, l.Name);
                    Console.WriteLine($"LiveEvent: {l.Name} Deleted.");
                    Console.WriteLine();
                }
            }
        }
    } 
    catch(ApiErrorException e)
    {
        Console.WriteLine("Hit ApiErrorException");
        Console.WriteLine($"\tCode: {e.Body.Error.Code}");
        Console.WriteLine($"\tCode: {e.Body.Error.Message}");
        Console.WriteLine();

    }
}
```        

## <a name="watch-the-event"></a><span data-ttu-id="e1546-178">Watch the event</span><span class="sxs-lookup"><span data-stu-id="e1546-178">Watch the event</span></span>

<span data-ttu-id="e1546-179">To watch the event, copy the streaming URL that you got when you ran code described in [Create a StreamingLocator](#create-a-streaminglocator) and use a player of your choice.</span><span class="sxs-lookup"><span data-stu-id="e1546-179">To watch the event, copy the streaming URL that you got when you ran code described in [Create a StreamingLocator](#create-a-streaminglocator) and use a player of your choice.</span></span> <span data-ttu-id="e1546-180">You can use [Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/index.html) to test your stream at http://ampdemo.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="e1546-180">You can use [Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/index.html) to test your stream at http://ampdemo.azureedge.net.</span></span> 

<span data-ttu-id="e1546-181">Live event automatically converts events to on-demand content when stopped.</span><span class="sxs-lookup"><span data-stu-id="e1546-181">Live event automatically converts events to on-demand content when stopped.</span></span> <span data-ttu-id="e1546-182">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span><span class="sxs-lookup"><span data-stu-id="e1546-182">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="e1546-183">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span><span class="sxs-lookup"><span data-stu-id="e1546-183">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="e1546-184">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e1546-184">Clean up resources</span></span>

<span data-ttu-id="e1546-185">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier.</span><span class="sxs-lookup"><span data-stu-id="e1546-185">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier.</span></span> <span data-ttu-id="e1546-186">You can use the **CloudShell** tool.</span><span class="sxs-lookup"><span data-stu-id="e1546-186">You can use the **CloudShell** tool.</span></span>

<span data-ttu-id="e1546-187">In the **CloudShell**, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="e1546-187">In the **CloudShell**, execute the following command:</span></span>

```azurecli-interactive
az group delete --name amsResourceGroup
```

> [!IMPORTANT]
> <span data-ttu-id="e1546-188">Leaving the LiveEvent running incurs billing costs.</span><span class="sxs-lookup"><span data-stu-id="e1546-188">Leaving the LiveEvent running incurs billing costs.</span></span> <span data-ttu-id="e1546-189">Be aware, if the project/program crashes or is closed out for any reason, it could leave the LiveEvent running in a billing state.</span><span class="sxs-lookup"><span data-stu-id="e1546-189">Be aware, if the project/program crashes or is closed out for any reason, it could leave the LiveEvent running in a billing state.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1546-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1546-190">Next steps</span></span>

[<span data-ttu-id="e1546-191">Stream files</span><span class="sxs-lookup"><span data-stu-id="e1546-191">Stream files</span></span>](stream-files-tutorial-with-api.md)

