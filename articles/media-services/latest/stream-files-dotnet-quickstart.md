---
title: Stream video files with Azure Media Services - .NET | Microsoft Docs
description: Follow the steps of this quickstart to create a new Azure Media Services account, encode a file, and stream it to Azure Media Player.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
keywords: azure media services, stream
ms.service: media-services
ms.workload: media
ms.topic: quickstart
ms.custom: mvc
ms.date: 04/08/2018
ms.author: juliako
ms.openlocfilehash: 48f85311f38d7e4ab1414dfc22c111b92163740e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856992"
---
# <a name="quickstart-stream-video-files---net"></a><span data-ttu-id="b4c74-104">Quickstart: Stream video files - .NET</span><span class="sxs-lookup"><span data-stu-id="b4c74-104">Quickstart: Stream video files - .NET</span></span>

> [!NOTE]
> <span data-ttu-id="b4c74-105">The latest version of Azure Media Services is in Preview and may be referred to as v3.</span><span class="sxs-lookup"><span data-stu-id="b4c74-105">The latest version of Azure Media Services is in Preview and may be referred to as v3.</span></span> <span data-ttu-id="b4c74-106">To start using v3 APIs, you should create a new Media Services account, as described in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="b4c74-106">To start using v3 APIs, you should create a new Media Services account, as described in this quickstart.</span></span> 

<span data-ttu-id="b4c74-107">This quickstart shows you how easy it is to start streaming videos on a wide variety of browsers and devices using Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b4c74-107">This quickstart shows you how easy it is to start streaming videos on a wide variety of browsers and devices using Azure Media Services.</span></span> <span data-ttu-id="b4c74-108">The sample in this topic encodes content that you make accessible via a HTTPS URL.</span><span class="sxs-lookup"><span data-stu-id="b4c74-108">The sample in this topic encodes content that you make accessible via a HTTPS URL.</span></span> 

<span data-ttu-id="b4c74-109">By the end of the quickstart you will be able to stream a video.</span><span class="sxs-lookup"><span data-stu-id="b4c74-109">By the end of the quickstart you will be able to stream a video.</span></span>  

![Play the video](./media/stream-files-dotnet-quickstart/final-video.png)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="b4c74-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4c74-111">Prerequisites</span></span>

<span data-ttu-id="b4c74-112">If you do not have Visual Studio installed, you can get [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="b4c74-112">If you do not have Visual Studio installed, you can get [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="b4c74-113">Download the sample</span><span class="sxs-lookup"><span data-stu-id="b4c74-113">Download the sample</span></span>

<span data-ttu-id="b4c74-114">Clone a GitHub repository that contains the streaming .NET sample to your machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="b4c74-114">Clone a GitHub repository that contains the streaming .NET sample to your machine using the following command:</span></span>  

 ```bash
 git clone http://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts.git
 ```

<span data-ttu-id="b4c74-115">The sample is located in the [EncodeAndStreamFiles](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/tree/master/AMSV3Quickstarts/EncodeAndStreamFiles) folder.</span><span class="sxs-lookup"><span data-stu-id="b4c74-115">The sample is located in the [EncodeAndStreamFiles](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/tree/master/AMSV3Quickstarts/EncodeAndStreamFiles) folder.</span></span>

<span data-ttu-id="b4c74-116">The sample performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="b4c74-116">The sample performs the following actions:</span></span>

1. <span data-ttu-id="b4c74-117">Creates a Transform (first, checks if the specified Transform exists).</span><span class="sxs-lookup"><span data-stu-id="b4c74-117">Creates a Transform (first, checks if the specified Transform exists).</span></span> 
2. <span data-ttu-id="b4c74-118">Creates an output Asset that is used as the encoding Job's output.</span><span class="sxs-lookup"><span data-stu-id="b4c74-118">Creates an output Asset that is used as the encoding Job's output.</span></span>
3. <span data-ttu-id="b4c74-119">Creates the Job's input that is based on an HTTPS URL.</span><span class="sxs-lookup"><span data-stu-id="b4c74-119">Creates the Job's input that is based on an HTTPS URL.</span></span>
4. <span data-ttu-id="b4c74-120">Submits the encoding Job using the input and output that was created earlier.</span><span class="sxs-lookup"><span data-stu-id="b4c74-120">Submits the encoding Job using the input and output that was created earlier.</span></span>
5. <span data-ttu-id="b4c74-121">Checks the Job's status.</span><span class="sxs-lookup"><span data-stu-id="b4c74-121">Checks the Job's status.</span></span>
6. <span data-ttu-id="b4c74-122">Creates a StreamingLocator.</span><span class="sxs-lookup"><span data-stu-id="b4c74-122">Creates a StreamingLocator.</span></span>
7. <span data-ttu-id="b4c74-123">Builds streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="b4c74-123">Builds streaming URLs.</span></span>

<span data-ttu-id="b4c74-124">For explanations about what each function in the sample does, examine the code and look at the comments in [this source file](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="b4c74-124">For explanations about what each function in the sample does, examine the code and look at the comments in [this source file](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="b4c74-125">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="b4c74-125">Log in to Azure</span></span>

<span data-ttu-id="b4c74-126">Log in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4c74-126">Log in to the [Azure portal](http://portal.azure.com).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]

[!INCLUDE [media-services-v3-cli-access-api-include](../../../includes/media-services-v3-cli-access-api-include.md)]

## <a name="run-the-sample-app"></a><span data-ttu-id="b4c74-127">Run the sample app</span><span class="sxs-lookup"><span data-stu-id="b4c74-127">Run the sample app</span></span>

<span data-ttu-id="b4c74-128">When you run the app, URLs that can be used to playback the video using different protocols are displayed.</span><span class="sxs-lookup"><span data-stu-id="b4c74-128">When you run the app, URLs that can be used to playback the video using different protocols are displayed.</span></span> 

1. <span data-ttu-id="b4c74-129">Press Ctrl+F5 to run the *EncodeAndStreamFiles* application.</span><span class="sxs-lookup"><span data-stu-id="b4c74-129">Press Ctrl+F5 to run the *EncodeAndStreamFiles* application.</span></span>
2. <span data-ttu-id="b4c74-130">Choose the Apple's **HLS** protocol (ends with *manifest(format=m3u8-aapl)*) and copy the streaming URL from the console.</span><span class="sxs-lookup"><span data-stu-id="b4c74-130">Choose the Apple's **HLS** protocol (ends with *manifest(format=m3u8-aapl)*) and copy the streaming URL from the console.</span></span>

![Output](./media/stream-files-tutorial-with-api/output.png)

<span data-ttu-id="b4c74-132">In the sample's [source code](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs), you can see how the URL is built.</span><span class="sxs-lookup"><span data-stu-id="b4c74-132">In the sample's [source code](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs), you can see how the URL is built.</span></span> <span data-ttu-id="b4c74-133">To build it, you need to concatenate the streaming endpoint's host name and the streaming locator path.</span><span class="sxs-lookup"><span data-stu-id="b4c74-133">To build it, you need to concatenate the streaming endpoint's host name and the streaming locator path.</span></span>  

## <a name="test-with-azure-media-player"></a><span data-ttu-id="b4c74-134">Test with Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="b4c74-134">Test with Azure Media Player</span></span>

<span data-ttu-id="b4c74-135">To test the stream, this article uses Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="b4c74-135">To test the stream, this article uses Azure Media Player.</span></span> 

> [!NOTE]
> <span data-ttu-id="b4c74-136">If a player is hosted on an https site, make sure to update the URL to "https".</span><span class="sxs-lookup"><span data-stu-id="b4c74-136">If a player is hosted on an https site, make sure to update the URL to "https".</span></span>

1. <span data-ttu-id="b4c74-137">Open a web browser and navigate to [https://aka.ms/azuremediaplayer/](https://aka.ms/azuremediaplayer/).</span><span class="sxs-lookup"><span data-stu-id="b4c74-137">Open a web browser and navigate to [https://aka.ms/azuremediaplayer/](https://aka.ms/azuremediaplayer/).</span></span>
2. <span data-ttu-id="b4c74-138">In the **URL:** box, paste one of the streaming URL values you got when you ran the application.</span><span class="sxs-lookup"><span data-stu-id="b4c74-138">In the **URL:** box, paste one of the streaming URL values you got when you ran the application.</span></span> 
3. <span data-ttu-id="b4c74-139">Press **Update Player**.</span><span class="sxs-lookup"><span data-stu-id="b4c74-139">Press **Update Player**.</span></span>

<span data-ttu-id="b4c74-140">Azure Media Player can be used for testing but should not be used in a production environment.</span><span class="sxs-lookup"><span data-stu-id="b4c74-140">Azure Media Player can be used for testing but should not be used in a production environment.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="b4c74-141">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b4c74-141">Clean up resources</span></span>

<span data-ttu-id="b4c74-142">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this Quickstart, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="b4c74-142">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this Quickstart, delete the resource group.</span></span> <span data-ttu-id="b4c74-143">You can use the **CloudShell** tool.</span><span class="sxs-lookup"><span data-stu-id="b4c74-143">You can use the **CloudShell** tool.</span></span>

<span data-ttu-id="b4c74-144">In the **CloudShell**, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="b4c74-144">In the **CloudShell**, execute the following command:</span></span>

```azurecli-interactive
az group delete --name amsResourceGroup
```

## <a name="examine-the-code"></a><span data-ttu-id="b4c74-145">Examine the code</span><span class="sxs-lookup"><span data-stu-id="b4c74-145">Examine the code</span></span>

<span data-ttu-id="b4c74-146">For explanations about what each function in the sample does, examine the code and look at the comments in [this source file](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="b4c74-146">For explanations about what each function in the sample does, examine the code and look at the comments in [this source file](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs).</span></span>

<span data-ttu-id="b4c74-147">The [upload, encode, and stream files](stream-files-tutorial-with-api.md) tutorial gives you a more advanced streaming example with detailed explanations.</span><span class="sxs-lookup"><span data-stu-id="b4c74-147">The [upload, encode, and stream files](stream-files-tutorial-with-api.md) tutorial gives you a more advanced streaming example with detailed explanations.</span></span> 

## <a name="multithreading"></a><span data-ttu-id="b4c74-148">Multithreading</span><span class="sxs-lookup"><span data-stu-id="b4c74-148">Multithreading</span></span>

<span data-ttu-id="b4c74-149">The Azure Media Services v3 SDKs are not thread-safe.</span><span class="sxs-lookup"><span data-stu-id="b4c74-149">The Azure Media Services v3 SDKs are not thread-safe.</span></span> <span data-ttu-id="b4c74-150">When working with multi-threaded application, you should generate a new  AzureMediaServicesClient object per thread.</span><span class="sxs-lookup"><span data-stu-id="b4c74-150">When working with multi-threaded application, you should generate a new  AzureMediaServicesClient object per thread.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4c74-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4c74-151">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4c74-152">Tutorial: upload, encode, and stream files</span><span class="sxs-lookup"><span data-stu-id="b4c74-152">Tutorial: upload, encode, and stream files</span></span>](stream-files-tutorial-with-api.md)
