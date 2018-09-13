---
title: Upload, encode, and stream using Azure Media Services | Microsoft Docs
description: Follow the steps of this tutorial to upload a file, and encode the video, and stream your content with Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: tutorial
ms.custom: mvc
ms.date: 05/30/2018
ms.author: juliako
ms.openlocfilehash: 0216a95a5209f5545b34e446904b3215950c6fbc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856617"
---
# <a name="tutorial-upload-encode-and-stream-videos-using-apis"></a><span data-ttu-id="38416-103">Tutorial: Upload, encode, and stream videos using APIs</span><span class="sxs-lookup"><span data-stu-id="38416-103">Tutorial: Upload, encode, and stream videos using APIs</span></span>

<span data-ttu-id="38416-104">Media Services enables you to encode your media files into formats that can be played on a wide variety of browsers and devices.</span><span class="sxs-lookup"><span data-stu-id="38416-104">Media Services enables you to encode your media files into formats that can be played on a wide variety of browsers and devices.</span></span> <span data-ttu-id="38416-105">For example, you might want to stream your content in Apple's HLS or MPEG DASH formats.</span><span class="sxs-lookup"><span data-stu-id="38416-105">For example, you might want to stream your content in Apple's HLS or MPEG DASH formats.</span></span> <span data-ttu-id="38416-106">Before streaming, you should encode your high-quality digital media file.</span><span class="sxs-lookup"><span data-stu-id="38416-106">Before streaming, you should encode your high-quality digital media file.</span></span> <span data-ttu-id="38416-107">For encoding guidance, see [Encoding concept](encoding-concept.md).</span><span class="sxs-lookup"><span data-stu-id="38416-107">For encoding guidance, see [Encoding concept](encoding-concept.md).</span></span> <span data-ttu-id="38416-108">This tutorial uploads a local video file and encodes the uploaded file.</span><span class="sxs-lookup"><span data-stu-id="38416-108">This tutorial uploads a local video file and encodes the uploaded file.</span></span> <span data-ttu-id="38416-109">You can also encode content that you make accessible via a HTTPS URL.</span><span class="sxs-lookup"><span data-stu-id="38416-109">You can also encode content that you make accessible via a HTTPS URL.</span></span> <span data-ttu-id="38416-110">For more information, see [Create a job input from an HTTP(s) URL](job-input-from-http-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="38416-110">For more information, see [Create a job input from an HTTP(s) URL](job-input-from-http-how-to.md).</span></span>

![Play the video](./media/stream-files-tutorial-with-api/final-video.png)

<span data-ttu-id="38416-112">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="38416-112">This tutorial shows you how to:</span></span>    

> [!div class="checklist"]
> * <span data-ttu-id="38416-113">Create a Media Services account</span><span class="sxs-lookup"><span data-stu-id="38416-113">Create a Media Services account</span></span>
> * <span data-ttu-id="38416-114">Access the Media Services API</span><span class="sxs-lookup"><span data-stu-id="38416-114">Access the Media Services API</span></span>
> * <span data-ttu-id="38416-115">Configure the sample app</span><span class="sxs-lookup"><span data-stu-id="38416-115">Configure the sample app</span></span>
> * <span data-ttu-id="38416-116">Examine the code that uploads, encodes, and streams</span><span class="sxs-lookup"><span data-stu-id="38416-116">Examine the code that uploads, encodes, and streams</span></span>
> * <span data-ttu-id="38416-117">Run the app</span><span class="sxs-lookup"><span data-stu-id="38416-117">Run the app</span></span>
> * <span data-ttu-id="38416-118">Test the streaming URL</span><span class="sxs-lookup"><span data-stu-id="38416-118">Test the streaming URL</span></span>
> * <span data-ttu-id="38416-119">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="38416-119">Clean up resources</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="38416-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="38416-120">Prerequisites</span></span>

<span data-ttu-id="38416-121">If you do not have Visual Studio installed, you can get [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="38416-121">If you do not have Visual Studio installed, you can get [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="38416-122">Download the sample</span><span class="sxs-lookup"><span data-stu-id="38416-122">Download the sample</span></span>

<span data-ttu-id="38416-123">Clone a GitHub repository that contains the streaming .NET sample to your machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="38416-123">Clone a GitHub repository that contains the streaming .NET sample to your machine using the following command:</span></span>  

 ```bash
 git clone https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials.git
 ```

<span data-ttu-id="38416-124">The sample is located in the [UploadEncodeAndStreamFiles](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/master/AMSV3Tutorials/UploadEncodeAndStreamFiles) folder.</span><span class="sxs-lookup"><span data-stu-id="38416-124">The sample is located in the [UploadEncodeAndStreamFiles](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/master/AMSV3Tutorials/UploadEncodeAndStreamFiles) folder.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]

[!INCLUDE [media-services-v3-cli-access-api-include](../../../includes/media-services-v3-cli-access-api-include.md)]

## <a name="examine-the-code-that-uploads-encodes-and-streams"></a><span data-ttu-id="38416-125">Examine the code that uploads, encodes, and streams</span><span class="sxs-lookup"><span data-stu-id="38416-125">Examine the code that uploads, encodes, and streams</span></span>

<span data-ttu-id="38416-126">This section examines functions defined in the [Program.cs](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs) file of the *UploadEncodeAndStreamFiles* project.</span><span class="sxs-lookup"><span data-stu-id="38416-126">This section examines functions defined in the [Program.cs](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs) file of the *UploadEncodeAndStreamFiles* project.</span></span>

<span data-ttu-id="38416-127">The sample performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="38416-127">The sample performs the following actions:</span></span>

1. <span data-ttu-id="38416-128">Creates a new Transform (first, checks if the specified Transform exists).</span><span class="sxs-lookup"><span data-stu-id="38416-128">Creates a new Transform (first, checks if the specified Transform exists).</span></span> 
2. <span data-ttu-id="38416-129">Creates an output Asset that is used as the encoding Job's output.</span><span class="sxs-lookup"><span data-stu-id="38416-129">Creates an output Asset that is used as the encoding Job's output.</span></span>
3. <span data-ttu-id="38416-130">Create an input Asset and uploads the specified local video file into it.</span><span class="sxs-lookup"><span data-stu-id="38416-130">Create an input Asset and uploads the specified local video file into it.</span></span> <span data-ttu-id="38416-131">The Asset is used as the Job's input.</span><span class="sxs-lookup"><span data-stu-id="38416-131">The Asset is used as the Job's input.</span></span> 
4. <span data-ttu-id="38416-132">Submits the encoding Job using the input and output that was created.</span><span class="sxs-lookup"><span data-stu-id="38416-132">Submits the encoding Job using the input and output that was created.</span></span>
5. <span data-ttu-id="38416-133">Checks the Job's status.</span><span class="sxs-lookup"><span data-stu-id="38416-133">Checks the Job's status.</span></span>
6. <span data-ttu-id="38416-134">Creates a StreamingLocator.</span><span class="sxs-lookup"><span data-stu-id="38416-134">Creates a StreamingLocator.</span></span>
7. <span data-ttu-id="38416-135">Builds streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="38416-135">Builds streaming URLs.</span></span>

### <a name="start-using-media-services-apis-with-net-sdk"></a><span data-ttu-id="38416-136">Start using Media Services APIs with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="38416-136">Start using Media Services APIs with .NET SDK</span></span>

<span data-ttu-id="38416-137">To start using Media Services APIs with .NET, you need to create an **AzureMediaServicesClient** object.</span><span class="sxs-lookup"><span data-stu-id="38416-137">To start using Media Services APIs with .NET, you need to create an **AzureMediaServicesClient** object.</span></span> <span data-ttu-id="38416-138">To create the object, you need to supply credentials needed for the client to connect to Azure using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38416-138">To create the object, you need to supply credentials needed for the client to connect to Azure using Azure AD.</span></span> <span data-ttu-id="38416-139">In the code you cloned at the beginning of the article, the **GetCredentialsAsync** function creates the ServiceClientCredentials object based on the credentials supplied in local configuration file.</span><span class="sxs-lookup"><span data-stu-id="38416-139">In the code you cloned at the beginning of the article, the **GetCredentialsAsync** function creates the ServiceClientCredentials object based on the credentials supplied in local configuration file.</span></span> 

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#CreateMediaServicesClient)]

### <a name="create-an-input-asset-and-upload-a-local-file-into-it"></a><span data-ttu-id="38416-140">Create an input asset and upload a local file into it</span><span class="sxs-lookup"><span data-stu-id="38416-140">Create an input asset and upload a local file into it</span></span> 

<span data-ttu-id="38416-141">The **CreateInputAsset** function creates a new input [Asset](https://docs.microsoft.com/rest/api/media/assets) and uploads the specified local video file into it.</span><span class="sxs-lookup"><span data-stu-id="38416-141">The **CreateInputAsset** function creates a new input [Asset](https://docs.microsoft.com/rest/api/media/assets) and uploads the specified local video file into it.</span></span> <span data-ttu-id="38416-142">This Asset is used as the input to your encoding Job.</span><span class="sxs-lookup"><span data-stu-id="38416-142">This Asset is used as the input to your encoding Job.</span></span> <span data-ttu-id="38416-143">In Media Services v3, the input to a Job can either be an Asset, or it can be content that you make available to your Media Services account via HTTPS URLs.</span><span class="sxs-lookup"><span data-stu-id="38416-143">In Media Services v3, the input to a Job can either be an Asset, or it can be content that you make available to your Media Services account via HTTPS URLs.</span></span> <span data-ttu-id="38416-144">If you want to learn how to encode from a HTTPS URL, see [this](job-input-from-http-how-to.md) article.</span><span class="sxs-lookup"><span data-stu-id="38416-144">If you want to learn how to encode from a HTTPS URL, see [this](job-input-from-http-how-to.md) article.</span></span>  

<span data-ttu-id="38416-145">In Media Services v3, you use Azure Storage APIs to upload files.</span><span class="sxs-lookup"><span data-stu-id="38416-145">In Media Services v3, you use Azure Storage APIs to upload files.</span></span> <span data-ttu-id="38416-146">The following .NET snippet shows how.</span><span class="sxs-lookup"><span data-stu-id="38416-146">The following .NET snippet shows how.</span></span>

<span data-ttu-id="38416-147">The following function performs these actions:</span><span class="sxs-lookup"><span data-stu-id="38416-147">The following function performs these actions:</span></span>

* <span data-ttu-id="38416-148">Creates an Asset</span><span class="sxs-lookup"><span data-stu-id="38416-148">Creates an Asset</span></span> 
* <span data-ttu-id="38416-149">Gets a writable [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) to the Asset’s [container in storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet?tabs=windows#upload-blobs-to-the-container)</span><span class="sxs-lookup"><span data-stu-id="38416-149">Gets a writable [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) to the Asset’s [container in storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet?tabs=windows#upload-blobs-to-the-container)</span></span>
* <span data-ttu-id="38416-150">Uploads the file into the container in storage using the SAS URL</span><span class="sxs-lookup"><span data-stu-id="38416-150">Uploads the file into the container in storage using the SAS URL</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#CreateInputAsset)]

### <a name="create-an-output-asset-to-store-the-result-of-a-job"></a><span data-ttu-id="38416-151">Create an output asset to store the result of a job</span><span class="sxs-lookup"><span data-stu-id="38416-151">Create an output asset to store the result of a job</span></span> 

<span data-ttu-id="38416-152">The output [Asset](https://docs.microsoft.com/rest/api/media/assets) stores the result of your encoding job.</span><span class="sxs-lookup"><span data-stu-id="38416-152">The output [Asset](https://docs.microsoft.com/rest/api/media/assets) stores the result of your encoding job.</span></span> <span data-ttu-id="38416-153">The project defines the **DownloadResults** function that downloads the results from this output asset into the "output" folder, so you can see what you got.</span><span class="sxs-lookup"><span data-stu-id="38416-153">The project defines the **DownloadResults** function that downloads the results from this output asset into the "output" folder, so you can see what you got.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#CreateOutputAsset)]

### <a name="create-a-transform-and-a-job-that-encodes-the-uploaded-file"></a><span data-ttu-id="38416-154">Create a Transform and a Job that encodes the uploaded file</span><span class="sxs-lookup"><span data-stu-id="38416-154">Create a Transform and a Job that encodes the uploaded file</span></span>
<span data-ttu-id="38416-155">When encoding or processing content in Media Services, it is a common pattern to set up the encoding settings as a recipe.</span><span class="sxs-lookup"><span data-stu-id="38416-155">When encoding or processing content in Media Services, it is a common pattern to set up the encoding settings as a recipe.</span></span> <span data-ttu-id="38416-156">You would then submit a **Job** to apply that recipe to a video.</span><span class="sxs-lookup"><span data-stu-id="38416-156">You would then submit a **Job** to apply that recipe to a video.</span></span> <span data-ttu-id="38416-157">By submitting new Jobs for each new video, you are applying that recipe to all the videos in your library.</span><span class="sxs-lookup"><span data-stu-id="38416-157">By submitting new Jobs for each new video, you are applying that recipe to all the videos in your library.</span></span> <span data-ttu-id="38416-158">A recipe in Media Services is called as a **Transform**.</span><span class="sxs-lookup"><span data-stu-id="38416-158">A recipe in Media Services is called as a **Transform**.</span></span> <span data-ttu-id="38416-159">For more information, see [Transforms and jobs](transform-concept.md).</span><span class="sxs-lookup"><span data-stu-id="38416-159">For more information, see [Transforms and jobs](transform-concept.md).</span></span> <span data-ttu-id="38416-160">The sample described in this tutorial defines a recipe that encodes the video in order to stream it to a variety of iOS and Android devices.</span><span class="sxs-lookup"><span data-stu-id="38416-160">The sample described in this tutorial defines a recipe that encodes the video in order to stream it to a variety of iOS and Android devices.</span></span> 

#### <a name="transform"></a><span data-ttu-id="38416-161">Transform</span><span class="sxs-lookup"><span data-stu-id="38416-161">Transform</span></span>

<span data-ttu-id="38416-162">When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms) instance, you need to specify what you want it to produce as an output.</span><span class="sxs-lookup"><span data-stu-id="38416-162">When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms) instance, you need to specify what you want it to produce as an output.</span></span> <span data-ttu-id="38416-163">The required parameter is a **TransformOutput** object, as shown in the code below.</span><span class="sxs-lookup"><span data-stu-id="38416-163">The required parameter is a **TransformOutput** object, as shown in the code below.</span></span> <span data-ttu-id="38416-164">Each **TransformOutput** contains a **Preset**.</span><span class="sxs-lookup"><span data-stu-id="38416-164">Each **TransformOutput** contains a **Preset**.</span></span> <span data-ttu-id="38416-165">**Preset** describes the step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**.</span><span class="sxs-lookup"><span data-stu-id="38416-165">**Preset** describes the step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**.</span></span> <span data-ttu-id="38416-166">The sample described in this article uses a built-in Preset called **AdaptiveStreaming**.</span><span class="sxs-lookup"><span data-stu-id="38416-166">The sample described in this article uses a built-in Preset called **AdaptiveStreaming**.</span></span> <span data-ttu-id="38416-167">The Preset encodes the input video into an auto-generated bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate, and produces ISO MP4 files with H.264 video and AAC audio corresponding to each bitrate-resolution pair.</span><span class="sxs-lookup"><span data-stu-id="38416-167">The Preset encodes the input video into an auto-generated bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate, and produces ISO MP4 files with H.264 video and AAC audio corresponding to each bitrate-resolution pair.</span></span> <span data-ttu-id="38416-168">For information about this Preset, see [auto-generating bitrate ladder](autogen-bitrate-ladder.md).</span><span class="sxs-lookup"><span data-stu-id="38416-168">For information about this Preset, see [auto-generating bitrate ladder](autogen-bitrate-ladder.md).</span></span>

<span data-ttu-id="38416-169">You can use a built-in EncoderNamedPreset or use custom presets.</span><span class="sxs-lookup"><span data-stu-id="38416-169">You can use a built-in EncoderNamedPreset or use custom presets.</span></span> <span data-ttu-id="38416-170">For more information, see [How to customize encoder presets](customize-encoder-presets-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="38416-170">For more information, see [How to customize encoder presets](customize-encoder-presets-how-to.md).</span></span>

<span data-ttu-id="38416-171">When creating a [Transform](https://docs.microsoft.com/rest/api/media/transforms), you should first check if one already exists using the **Get** method, as shown in the code that follows.</span><span class="sxs-lookup"><span data-stu-id="38416-171">When creating a [Transform](https://docs.microsoft.com/rest/api/media/transforms), you should first check if one already exists using the **Get** method, as shown in the code that follows.</span></span>  <span data-ttu-id="38416-172">In Media Services v3, **Get** methods on entities return **null** if the entity doesn’t exist (a case-insensitive check on the name).</span><span class="sxs-lookup"><span data-stu-id="38416-172">In Media Services v3, **Get** methods on entities return **null** if the entity doesn’t exist (a case-insensitive check on the name).</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#EnsureTransformExists)]

#### <a name="job"></a><span data-ttu-id="38416-173">Job</span><span class="sxs-lookup"><span data-stu-id="38416-173">Job</span></span>

<span data-ttu-id="38416-174">As mentioned above, the [Transform](https://docs.microsoft.com/rest/api/media/transforms) object is the recipe and a [Job](https://docs.microsoft.com/rest/api/media/jobs) is the actual request to Media Services to apply that **Transform** to a given input video or audio content.</span><span class="sxs-lookup"><span data-stu-id="38416-174">As mentioned above, the [Transform](https://docs.microsoft.com/rest/api/media/transforms) object is the recipe and a [Job](https://docs.microsoft.com/rest/api/media/jobs) is the actual request to Media Services to apply that **Transform** to a given input video or audio content.</span></span> <span data-ttu-id="38416-175">The **Job** specifies information like the location of the input video, and the location for the output.</span><span class="sxs-lookup"><span data-stu-id="38416-175">The **Job** specifies information like the location of the input video, and the location for the output.</span></span>

<span data-ttu-id="38416-176">In this example, the input video has been uploaded from your local machine.</span><span class="sxs-lookup"><span data-stu-id="38416-176">In this example, the input video has been uploaded from your local machine.</span></span> <span data-ttu-id="38416-177">If you want to learn how to encode from a HTTPS URL, see [this](job-input-from-http-how-to.md) article.</span><span class="sxs-lookup"><span data-stu-id="38416-177">If you want to learn how to encode from a HTTPS URL, see [this](job-input-from-http-how-to.md) article.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#SubmitJob)]

### <a name="wait-for-the-job-to-complete"></a><span data-ttu-id="38416-178">Wait for the Job to complete</span><span class="sxs-lookup"><span data-stu-id="38416-178">Wait for the Job to complete</span></span>

<span data-ttu-id="38416-179">The job takes some time to complete and when it does you want to be notified.</span><span class="sxs-lookup"><span data-stu-id="38416-179">The job takes some time to complete and when it does you want to be notified.</span></span> <span data-ttu-id="38416-180">The code sample below shows how to poll the service for the status of the [Job](https://docs.microsoft.com/rest/api/media/jobs).</span><span class="sxs-lookup"><span data-stu-id="38416-180">The code sample below shows how to poll the service for the status of the [Job](https://docs.microsoft.com/rest/api/media/jobs).</span></span> <span data-ttu-id="38416-181">Polling is not a recommended best practice for production applications because of potential latency.</span><span class="sxs-lookup"><span data-stu-id="38416-181">Polling is not a recommended best practice for production applications because of potential latency.</span></span> <span data-ttu-id="38416-182">Polling can be throttled if overused on an account.</span><span class="sxs-lookup"><span data-stu-id="38416-182">Polling can be throttled if overused on an account.</span></span> <span data-ttu-id="38416-183">Developers should instead use Event Grid.</span><span class="sxs-lookup"><span data-stu-id="38416-183">Developers should instead use Event Grid.</span></span>

<span data-ttu-id="38416-184">Event Grid is designed for high availability, consistent performance, and dynamic scale.</span><span class="sxs-lookup"><span data-stu-id="38416-184">Event Grid is designed for high availability, consistent performance, and dynamic scale.</span></span> <span data-ttu-id="38416-185">With Event Grid, your apps can listen for and react to events from virtually all Azure services, as well as custom sources.</span><span class="sxs-lookup"><span data-stu-id="38416-185">With Event Grid, your apps can listen for and react to events from virtually all Azure services, as well as custom sources.</span></span> <span data-ttu-id="38416-186">Simple, HTTP-based reactive event handling helps you build efficient solutions through intelligent filtering and routing of events.</span><span class="sxs-lookup"><span data-stu-id="38416-186">Simple, HTTP-based reactive event handling helps you build efficient solutions through intelligent filtering and routing of events.</span></span>  <span data-ttu-id="38416-187">See [Route events to a custom web endpoint](job-state-events-cli-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="38416-187">See [Route events to a custom web endpoint](job-state-events-cli-how-to.md).</span></span>

<span data-ttu-id="38416-188">The **Job** usually goes through the following states: **Scheduled**, **Queued**, **Processing**, **Finished** (the final state).</span><span class="sxs-lookup"><span data-stu-id="38416-188">The **Job** usually goes through the following states: **Scheduled**, **Queued**, **Processing**, **Finished** (the final state).</span></span> <span data-ttu-id="38416-189">If the job has encountered an error, you get the **Error** state.</span><span class="sxs-lookup"><span data-stu-id="38416-189">If the job has encountered an error, you get the **Error** state.</span></span> <span data-ttu-id="38416-190">If the job is in the process of being canceled, you get **Canceling** and **Canceled** when it is done.</span><span class="sxs-lookup"><span data-stu-id="38416-190">If the job is in the process of being canceled, you get **Canceling** and **Canceled** when it is done.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#WaitForJobToFinish)]

### <a name="get-a-streaminglocator"></a><span data-ttu-id="38416-191">Get a StreamingLocator</span><span class="sxs-lookup"><span data-stu-id="38416-191">Get a StreamingLocator</span></span>

<span data-ttu-id="38416-192">After the encoding is complete, the next step is to make the video in the output Asset available to clients for playback.</span><span class="sxs-lookup"><span data-stu-id="38416-192">After the encoding is complete, the next step is to make the video in the output Asset available to clients for playback.</span></span> <span data-ttu-id="38416-193">You can accomplish this in two steps: first, create a [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators), and second, build the streaming URLs that clients can use.</span><span class="sxs-lookup"><span data-stu-id="38416-193">You can accomplish this in two steps: first, create a [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators), and second, build the streaming URLs that clients can use.</span></span> 

<span data-ttu-id="38416-194">The process of creating a **StreamingLocator** is called publishing.</span><span class="sxs-lookup"><span data-stu-id="38416-194">The process of creating a **StreamingLocator** is called publishing.</span></span> <span data-ttu-id="38416-195">By default, the **StreamingLocator** is valid immediately after you make the API calls, and lasts until it is deleted, unless you configure the optional start and end times.</span><span class="sxs-lookup"><span data-stu-id="38416-195">By default, the **StreamingLocator** is valid immediately after you make the API calls, and lasts until it is deleted, unless you configure the optional start and end times.</span></span> 

<span data-ttu-id="38416-196">When creating a [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators), you will need to specify the desired **StreamingPolicyName**.</span><span class="sxs-lookup"><span data-stu-id="38416-196">When creating a [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators), you will need to specify the desired **StreamingPolicyName**.</span></span> <span data-ttu-id="38416-197">In this example, you will be streaming in-the-clear (or non-encrypted content) so the predefined clear streaming policy (**PredefinedStreamingPolicy.ClearStreamingOnly**) is used.</span><span class="sxs-lookup"><span data-stu-id="38416-197">In this example, you will be streaming in-the-clear (or non-encrypted content) so the predefined clear streaming policy (**PredefinedStreamingPolicy.ClearStreamingOnly**) is used.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38416-198">When using a custom [StreamingPolicy](https://docs.microsoft.com/rest/api/media/streamingpolicies), you should design a limited set of such policies for your Media Service account, and re-use them for your StreamingLocators whenever the same encryption options and protocols are needed.</span><span class="sxs-lookup"><span data-stu-id="38416-198">When using a custom [StreamingPolicy](https://docs.microsoft.com/rest/api/media/streamingpolicies), you should design a limited set of such policies for your Media Service account, and re-use them for your StreamingLocators whenever the same encryption options and protocols are needed.</span></span> <span data-ttu-id="38416-199">Your Media Service account has a quota for the number of StreamingPolicy entries.</span><span class="sxs-lookup"><span data-stu-id="38416-199">Your Media Service account has a quota for the number of StreamingPolicy entries.</span></span> <span data-ttu-id="38416-200">You should not be creating a new StreamingPolicy for each StreamingLocator.</span><span class="sxs-lookup"><span data-stu-id="38416-200">You should not be creating a new StreamingPolicy for each StreamingLocator.</span></span>

<span data-ttu-id="38416-201">The following code assumes that you are calling the function with a unique locatorName.</span><span class="sxs-lookup"><span data-stu-id="38416-201">The following code assumes that you are calling the function with a unique locatorName.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#CreateStreamingLocator)]

<span data-ttu-id="38416-202">While the sample in this topic discusses streaming, you can use the same call to create a StreamingLocator for delivering video via progressive download.</span><span class="sxs-lookup"><span data-stu-id="38416-202">While the sample in this topic discusses streaming, you can use the same call to create a StreamingLocator for delivering video via progressive download.</span></span>

### <a name="get-streaming-urls"></a><span data-ttu-id="38416-203">Get streaming URLs</span><span class="sxs-lookup"><span data-stu-id="38416-203">Get streaming URLs</span></span>

<span data-ttu-id="38416-204">Now that the [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators) has been created, you can get the streaming URLs, as shown in **GetStreamingURLs**.</span><span class="sxs-lookup"><span data-stu-id="38416-204">Now that the [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators) has been created, you can get the streaming URLs, as shown in **GetStreamingURLs**.</span></span> <span data-ttu-id="38416-205">To build a URL, you need to concatenate the [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/streamingendpoints) host name and the **StreamingLocator** path.</span><span class="sxs-lookup"><span data-stu-id="38416-205">To build a URL, you need to concatenate the [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/streamingendpoints) host name and the **StreamingLocator** path.</span></span> <span data-ttu-id="38416-206">In this sample, the *default* **StreamingEndpoint** is used.</span><span class="sxs-lookup"><span data-stu-id="38416-206">In this sample, the *default* **StreamingEndpoint** is used.</span></span> <span data-ttu-id="38416-207">When you first create a Media Service account, this *default* **StreamingEndpoint** will be in a stopped state, so you need to call **Start**.</span><span class="sxs-lookup"><span data-stu-id="38416-207">When you first create a Media Service account, this *default* **StreamingEndpoint** will be in a stopped state, so you need to call **Start**.</span></span>

> [!NOTE]
> <span data-ttu-id="38416-208">In this method, you  need the locatorName that was used when creating the **StreamingLocator** for the output Asset.</span><span class="sxs-lookup"><span data-stu-id="38416-208">In this method, you  need the locatorName that was used when creating the **StreamingLocator** for the output Asset.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#GetStreamingURLs)]

### <a name="clean-up-resources-in-your-media-services-account"></a><span data-ttu-id="38416-209">Clean up resources in your Media Services account</span><span class="sxs-lookup"><span data-stu-id="38416-209">Clean up resources in your Media Services account</span></span>

<span data-ttu-id="38416-210">Generally, you should clean up everything except objects that you are planning to reuse (typically, you will reuse Transforms, and you will persist StreamingLocators, etc.).</span><span class="sxs-lookup"><span data-stu-id="38416-210">Generally, you should clean up everything except objects that you are planning to reuse (typically, you will reuse Transforms, and you will persist StreamingLocators, etc.).</span></span> <span data-ttu-id="38416-211">If you want for your account to be clean after experimenting, you should delete the resources that you do not plan to reuse.</span><span class="sxs-lookup"><span data-stu-id="38416-211">If you want for your account to be clean after experimenting, you should delete the resources that you do not plan to reuse.</span></span>  <span data-ttu-id="38416-212">For example, the following code deletes Jobs.</span><span class="sxs-lookup"><span data-stu-id="38416-212">For example, the following code deletes Jobs.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#CleanUp)]

## <a name="run-the-sample-app"></a><span data-ttu-id="38416-213">Run the sample app</span><span class="sxs-lookup"><span data-stu-id="38416-213">Run the sample app</span></span>

1. <span data-ttu-id="38416-214">Press Ctrl+F5 to run the *EncodeAndStreamFiles* application.</span><span class="sxs-lookup"><span data-stu-id="38416-214">Press Ctrl+F5 to run the *EncodeAndStreamFiles* application.</span></span>
2. <span data-ttu-id="38416-215">Copy one of the streaming URLs from the console.</span><span class="sxs-lookup"><span data-stu-id="38416-215">Copy one of the streaming URLs from the console.</span></span>

<span data-ttu-id="38416-216">This example displays URLs that can be used to play back the video using different protocols:</span><span class="sxs-lookup"><span data-stu-id="38416-216">This example displays URLs that can be used to play back the video using different protocols:</span></span>

![Output](./media/stream-files-tutorial-with-api/output.png)

## <a name="test-the-streaming-url"></a><span data-ttu-id="38416-218">Test the streaming URL</span><span class="sxs-lookup"><span data-stu-id="38416-218">Test the streaming URL</span></span>

<span data-ttu-id="38416-219">To test the stream, this article uses Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="38416-219">To test the stream, this article uses Azure Media Player.</span></span> 

> [!NOTE]
> <span data-ttu-id="38416-220">If a player is hosted on an https site, make sure to update the URL to "https".</span><span class="sxs-lookup"><span data-stu-id="38416-220">If a player is hosted on an https site, make sure to update the URL to "https".</span></span>

1. <span data-ttu-id="38416-221">Open a web browser and navigate to [https://aka.ms/azuremediaplayer/](https://aka.ms/azuremediaplayer/).</span><span class="sxs-lookup"><span data-stu-id="38416-221">Open a web browser and navigate to [https://aka.ms/azuremediaplayer/](https://aka.ms/azuremediaplayer/).</span></span>
2. <span data-ttu-id="38416-222">In the **URL:** box, paste one of the streaming URL values you got when you ran the application.</span><span class="sxs-lookup"><span data-stu-id="38416-222">In the **URL:** box, paste one of the streaming URL values you got when you ran the application.</span></span> 
3. <span data-ttu-id="38416-223">Press **Update Player**.</span><span class="sxs-lookup"><span data-stu-id="38416-223">Press **Update Player**.</span></span>

<span data-ttu-id="38416-224">Azure Media Player can be used for testing but should not be used in a production environment.</span><span class="sxs-lookup"><span data-stu-id="38416-224">Azure Media Player can be used for testing but should not be used in a production environment.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="38416-225">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="38416-225">Clean up resources</span></span>

<span data-ttu-id="38416-226">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier.</span><span class="sxs-lookup"><span data-stu-id="38416-226">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier.</span></span> <span data-ttu-id="38416-227">You can use the **CloudShell** tool.</span><span class="sxs-lookup"><span data-stu-id="38416-227">You can use the **CloudShell** tool.</span></span>

<span data-ttu-id="38416-228">In the **CloudShell**, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="38416-228">In the **CloudShell**, execute the following command:</span></span>

```azurecli-interactive
az group delete --name amsResourceGroup
```

## <a name="multithreading"></a><span data-ttu-id="38416-229">Multithreading</span><span class="sxs-lookup"><span data-stu-id="38416-229">Multithreading</span></span>

<span data-ttu-id="38416-230">The Azure Media Services v3 SDKs are not thread-safe.</span><span class="sxs-lookup"><span data-stu-id="38416-230">The Azure Media Services v3 SDKs are not thread-safe.</span></span> <span data-ttu-id="38416-231">When developing a multi-threaded application, you should generate and use a new  AzureMediaServicesClient object per thread.</span><span class="sxs-lookup"><span data-stu-id="38416-231">When developing a multi-threaded application, you should generate and use a new  AzureMediaServicesClient object per thread.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38416-232">Next steps</span><span class="sxs-lookup"><span data-stu-id="38416-232">Next steps</span></span>

<span data-ttu-id="38416-233">Now that you know how to upload, encode, and stream your video, see the following article:</span><span class="sxs-lookup"><span data-stu-id="38416-233">Now that you know how to upload, encode, and stream your video, see the following article:</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="38416-234">Analyze videos</span><span class="sxs-lookup"><span data-stu-id="38416-234">Analyze videos</span></span>](analyze-videos-tutorial-with-api.md)
