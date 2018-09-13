---
title: Analyze videos with Azure Media Services | Microsoft Docs
description: Follow the steps of this tutorial to analyze videos using Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: tutorial
ms.custom: mvc
ms.date: 06/28/2018
ms.author: juliako
ms.openlocfilehash: 314ffce8a9f8dde62cac670099afbc2223df37e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864837"
---
# <a name="tutorial-analyze-videos-with-azure-media-services"></a><span data-ttu-id="a8479-103">Tutorial: Analyze videos with Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="a8479-103">Tutorial: Analyze videos with Azure Media Services</span></span> 

<span data-ttu-id="a8479-104">This tutorial shows you how to analyze videos with Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="a8479-104">This tutorial shows you how to analyze videos with Azure Media Services.</span></span> <span data-ttu-id="a8479-105">There are many scenarios in which you might want to gain deep insights into recorded videos or audio content.</span><span class="sxs-lookup"><span data-stu-id="a8479-105">There are many scenarios in which you might want to gain deep insights into recorded videos or audio content.</span></span> <span data-ttu-id="a8479-106">For example, to achieve higher customer satisfaction, organizations can run speech-to-text processing to convert customer support recordings into a searchable catalog, with indexes and dashboards.</span><span class="sxs-lookup"><span data-stu-id="a8479-106">For example, to achieve higher customer satisfaction, organizations can run speech-to-text processing to convert customer support recordings into a searchable catalog, with indexes and dashboards.</span></span> <span data-ttu-id="a8479-107">Then, they can obtain insights into their business such as a list of common complaints, sources of such complaints, etc.</span><span class="sxs-lookup"><span data-stu-id="a8479-107">Then, they can obtain insights into their business such as a list of common complaints, sources of such complaints, etc.</span></span>

<span data-ttu-id="a8479-108">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="a8479-108">This tutorial shows you how to:</span></span>    

> [!div class="checklist"]
> * <span data-ttu-id="a8479-109">Create a Media Services account</span><span class="sxs-lookup"><span data-stu-id="a8479-109">Create a Media Services account</span></span>
> * <span data-ttu-id="a8479-110">Access the Media Services API</span><span class="sxs-lookup"><span data-stu-id="a8479-110">Access the Media Services API</span></span>
> * <span data-ttu-id="a8479-111">Configure the sample app</span><span class="sxs-lookup"><span data-stu-id="a8479-111">Configure the sample app</span></span>
> * <span data-ttu-id="a8479-112">Examine the code that analyzes the specified video</span><span class="sxs-lookup"><span data-stu-id="a8479-112">Examine the code that analyzes the specified video</span></span>
> * <span data-ttu-id="a8479-113">Run the app</span><span class="sxs-lookup"><span data-stu-id="a8479-113">Run the app</span></span>
> * <span data-ttu-id="a8479-114">Examine the output</span><span class="sxs-lookup"><span data-stu-id="a8479-114">Examine the output</span></span>
> * <span data-ttu-id="a8479-115">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a8479-115">Clean up resources</span></span>

> [!Note]
> <span data-ttu-id="a8479-116">Use the Azure portal, as described in [Scaling media processing](../previous/media-services-scale-media-processing-overview.md), to set your Media Services account to 10 S3 Media Reserved Units.</span><span class="sxs-lookup"><span data-stu-id="a8479-116">Use the Azure portal, as described in [Scaling media processing](../previous/media-services-scale-media-processing-overview.md), to set your Media Services account to 10 S3 Media Reserved Units.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="a8479-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8479-117">Prerequisites</span></span>

<span data-ttu-id="a8479-118">If you do not have Visual Studio installed, you can get [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="a8479-118">If you do not have Visual Studio installed, you can get [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="a8479-119">Download the sample</span><span class="sxs-lookup"><span data-stu-id="a8479-119">Download the sample</span></span>

<span data-ttu-id="a8479-120">Clone a GitHub repository that contains the .NET sample to your machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="a8479-120">Clone a GitHub repository that contains the .NET sample to your machine using the following command:</span></span>  

 ```bash
 git clone https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials.git
 ```

<span data-ttu-id="a8479-121">The sample is located in the [AnalyzeVideos](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/master/AMSV3Tutorials/AnalyzeVideos) folder.</span><span class="sxs-lookup"><span data-stu-id="a8479-121">The sample is located in the [AnalyzeVideos](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/master/AMSV3Tutorials/AnalyzeVideos) folder.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]

[!INCLUDE [media-services-v3-cli-access-api-include](../../../includes/media-services-v3-cli-access-api-include.md)]

## <a name="examine-the-code-that-analyzes-the-specified-video"></a><span data-ttu-id="a8479-122">Examine the code that analyzes the specified video</span><span class="sxs-lookup"><span data-stu-id="a8479-122">Examine the code that analyzes the specified video</span></span>

<span data-ttu-id="a8479-123">This section examines functions defined in the [Program.cs](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/AnalyzeVideos/Program.cs) file of the *AnalyzeVideos* project.</span><span class="sxs-lookup"><span data-stu-id="a8479-123">This section examines functions defined in the [Program.cs](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/AnalyzeVideos/Program.cs) file of the *AnalyzeVideos* project.</span></span>

<span data-ttu-id="a8479-124">The sample performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="a8479-124">The sample performs the following actions:</span></span>

1. <span data-ttu-id="a8479-125">Creates a transform and a job that analyzes your video.</span><span class="sxs-lookup"><span data-stu-id="a8479-125">Creates a transform and a job that analyzes your video.</span></span>
2. <span data-ttu-id="a8479-126">Creates an input asset and uploads the video into it.</span><span class="sxs-lookup"><span data-stu-id="a8479-126">Creates an input asset and uploads the video into it.</span></span> <span data-ttu-id="a8479-127">The asset is used as the job's input.</span><span class="sxs-lookup"><span data-stu-id="a8479-127">The asset is used as the job's input.</span></span>
3. <span data-ttu-id="a8479-128">Creates an output asset that stores the job's output.</span><span class="sxs-lookup"><span data-stu-id="a8479-128">Creates an output asset that stores the job's output.</span></span> 
4. <span data-ttu-id="a8479-129">Submits the job.</span><span class="sxs-lookup"><span data-stu-id="a8479-129">Submits the job.</span></span>
5. <span data-ttu-id="a8479-130">Checks the job's status.</span><span class="sxs-lookup"><span data-stu-id="a8479-130">Checks the job's status.</span></span>
6. <span data-ttu-id="a8479-131">Downloads the files that resulted from running the job.</span><span class="sxs-lookup"><span data-stu-id="a8479-131">Downloads the files that resulted from running the job.</span></span> 

### <a name="start-using-media-services-apis-with-net-sdk"></a><span data-ttu-id="a8479-132">Start using Media Services APIs with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a8479-132">Start using Media Services APIs with .NET SDK</span></span>

<span data-ttu-id="a8479-133">To start using Media Services APIs with .NET, you need to create an **AzureMediaServicesClient** object.</span><span class="sxs-lookup"><span data-stu-id="a8479-133">To start using Media Services APIs with .NET, you need to create an **AzureMediaServicesClient** object.</span></span> <span data-ttu-id="a8479-134">To create the object, you need to supply credentials needed for the client to connect to Azure using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8479-134">To create the object, you need to supply credentials needed for the client to connect to Azure using Azure AD.</span></span> <span data-ttu-id="a8479-135">In the code you cloned at the beginning of the article, the **GetCredentialsAsync** function creates the ServiceClientCredentials object based on the credentials supplied in local configuration file.</span><span class="sxs-lookup"><span data-stu-id="a8479-135">In the code you cloned at the beginning of the article, the **GetCredentialsAsync** function creates the ServiceClientCredentials object based on the credentials supplied in local configuration file.</span></span> 

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CreateMediaServicesClient)]

### <a name="create-an-input-asset-and-upload-a-local-file-into-it"></a><span data-ttu-id="a8479-136">Create an input asset and upload a local file into it</span><span class="sxs-lookup"><span data-stu-id="a8479-136">Create an input asset and upload a local file into it</span></span> 

<span data-ttu-id="a8479-137">The **CreateInputAsset** function creates a new input [Asset](https://docs.microsoft.com/rest/api/media/assets) and uploads the specified local video file into it.</span><span class="sxs-lookup"><span data-stu-id="a8479-137">The **CreateInputAsset** function creates a new input [Asset](https://docs.microsoft.com/rest/api/media/assets) and uploads the specified local video file into it.</span></span> <span data-ttu-id="a8479-138">This Asset is used as the input to your encoding Job.</span><span class="sxs-lookup"><span data-stu-id="a8479-138">This Asset is used as the input to your encoding Job.</span></span> <span data-ttu-id="a8479-139">In Media Services v3, the input to a Job can either be an Asset, or it can be content that you make available to your Media Services account via HTTPS URLs.</span><span class="sxs-lookup"><span data-stu-id="a8479-139">In Media Services v3, the input to a Job can either be an Asset, or it can be content that you make available to your Media Services account via HTTPS URLs.</span></span> <span data-ttu-id="a8479-140">If you want to learn how to encode from a HTTPS URL, see [this](job-input-from-http-how-to.md) article.</span><span class="sxs-lookup"><span data-stu-id="a8479-140">If you want to learn how to encode from a HTTPS URL, see [this](job-input-from-http-how-to.md) article.</span></span>  

<span data-ttu-id="a8479-141">In Media Services v3, you use Azure Storage APIs to upload files.</span><span class="sxs-lookup"><span data-stu-id="a8479-141">In Media Services v3, you use Azure Storage APIs to upload files.</span></span> <span data-ttu-id="a8479-142">The following .NET snippet shows how.</span><span class="sxs-lookup"><span data-stu-id="a8479-142">The following .NET snippet shows how.</span></span>

<span data-ttu-id="a8479-143">The following function performs these actions:</span><span class="sxs-lookup"><span data-stu-id="a8479-143">The following function performs these actions:</span></span>

* <span data-ttu-id="a8479-144">Creates an Asset</span><span class="sxs-lookup"><span data-stu-id="a8479-144">Creates an Asset</span></span> 
* <span data-ttu-id="a8479-145">Gets a writable [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) to the Asset’s [container in storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet?tabs=windows#upload-blobs-to-the-container)</span><span class="sxs-lookup"><span data-stu-id="a8479-145">Gets a writable [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) to the Asset’s [container in storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet?tabs=windows#upload-blobs-to-the-container)</span></span>
* <span data-ttu-id="a8479-146">Uploads the file into the container in storage using the SAS URL</span><span class="sxs-lookup"><span data-stu-id="a8479-146">Uploads the file into the container in storage using the SAS URL</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CreateInputAsset)]

### <a name="create-an-output-asset-to-store-the-result-of-the-job"></a><span data-ttu-id="a8479-147">Create an output asset to store the result of the job</span><span class="sxs-lookup"><span data-stu-id="a8479-147">Create an output asset to store the result of the job</span></span> 

<span data-ttu-id="a8479-148">The output [Asset](https://docs.microsoft.com/rest/api/media/assets) stores the result of your job.</span><span class="sxs-lookup"><span data-stu-id="a8479-148">The output [Asset](https://docs.microsoft.com/rest/api/media/assets) stores the result of your job.</span></span> <span data-ttu-id="a8479-149">The project defines the **DownloadResults** function that downloads the results from this output asset into the "output" folder, so you can see what you got.</span><span class="sxs-lookup"><span data-stu-id="a8479-149">The project defines the **DownloadResults** function that downloads the results from this output asset into the "output" folder, so you can see what you got.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CreateOutputAsset)]

### <a name="create-a-transform-and-a-job-that-analyzes-videos"></a><span data-ttu-id="a8479-150">Create a transform and a job that analyzes videos</span><span class="sxs-lookup"><span data-stu-id="a8479-150">Create a transform and a job that analyzes videos</span></span>

<span data-ttu-id="a8479-151">When encoding or processing content in Media Services, it is a common pattern to set up the encoding settings as a recipe.</span><span class="sxs-lookup"><span data-stu-id="a8479-151">When encoding or processing content in Media Services, it is a common pattern to set up the encoding settings as a recipe.</span></span> <span data-ttu-id="a8479-152">You would then submit a **Job** to apply that recipe to a video.</span><span class="sxs-lookup"><span data-stu-id="a8479-152">You would then submit a **Job** to apply that recipe to a video.</span></span> <span data-ttu-id="a8479-153">By submitting new Jobs for each new video, you are applying that recipe to all the videos in your library.</span><span class="sxs-lookup"><span data-stu-id="a8479-153">By submitting new Jobs for each new video, you are applying that recipe to all the videos in your library.</span></span> <span data-ttu-id="a8479-154">A recipe in Media Services is called as a **Transform**.</span><span class="sxs-lookup"><span data-stu-id="a8479-154">A recipe in Media Services is called as a **Transform**.</span></span> <span data-ttu-id="a8479-155">For more information, see [Transforms and jobs](transform-concept.md).</span><span class="sxs-lookup"><span data-stu-id="a8479-155">For more information, see [Transforms and jobs](transform-concept.md).</span></span> <span data-ttu-id="a8479-156">The sample described in this tutorial defines a recipe that analyzes the specified video.</span><span class="sxs-lookup"><span data-stu-id="a8479-156">The sample described in this tutorial defines a recipe that analyzes the specified video.</span></span> 

#### <a name="transform"></a><span data-ttu-id="a8479-157">Transform</span><span class="sxs-lookup"><span data-stu-id="a8479-157">Transform</span></span>

<span data-ttu-id="a8479-158">When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms) instance, you need to specify what you want it to produce as an output.</span><span class="sxs-lookup"><span data-stu-id="a8479-158">When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms) instance, you need to specify what you want it to produce as an output.</span></span> <span data-ttu-id="a8479-159">The required parameter is a **TransformOutput** object, as shown in the code above.</span><span class="sxs-lookup"><span data-stu-id="a8479-159">The required parameter is a **TransformOutput** object, as shown in the code above.</span></span> <span data-ttu-id="a8479-160">Each **TransformOutput** contains a **Preset**.</span><span class="sxs-lookup"><span data-stu-id="a8479-160">Each **TransformOutput** contains a **Preset**.</span></span> <span data-ttu-id="a8479-161">**Preset** describes step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**.</span><span class="sxs-lookup"><span data-stu-id="a8479-161">**Preset** describes step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**.</span></span> <span data-ttu-id="a8479-162">In this example, the **VideoAnalyzerPreset** preset is used and the language ("en-US") is passed to its constructor.</span><span class="sxs-lookup"><span data-stu-id="a8479-162">In this example, the **VideoAnalyzerPreset** preset is used and the language ("en-US") is passed to its constructor.</span></span> <span data-ttu-id="a8479-163">This preset enables you to extract multiple audio and video insights from a video.</span><span class="sxs-lookup"><span data-stu-id="a8479-163">This preset enables you to extract multiple audio and video insights from a video.</span></span> <span data-ttu-id="a8479-164">You can use the **AudioAnalyzerPreset** preset if you need to extract multiple audio insights from a video.</span><span class="sxs-lookup"><span data-stu-id="a8479-164">You can use the **AudioAnalyzerPreset** preset if you need to extract multiple audio insights from a video.</span></span> 

<span data-ttu-id="a8479-165">When creating a **Transform**, you should first check if one already exists using the **Get** method, as shown in the code that follows.</span><span class="sxs-lookup"><span data-stu-id="a8479-165">When creating a **Transform**, you should first check if one already exists using the **Get** method, as shown in the code that follows.</span></span>  <span data-ttu-id="a8479-166">In Media Services v3, **Get** methods on entities return **null** if the entity doesn’t exist (a case-insensitive check on the name).</span><span class="sxs-lookup"><span data-stu-id="a8479-166">In Media Services v3, **Get** methods on entities return **null** if the entity doesn’t exist (a case-insensitive check on the name).</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#EnsureTransformExists)]

#### <a name="job"></a><span data-ttu-id="a8479-167">Job</span><span class="sxs-lookup"><span data-stu-id="a8479-167">Job</span></span>

<span data-ttu-id="a8479-168">As mentioned above, the [Transform](https://docs.microsoft.com/rest/api/media/transforms) object is the recipe and a [Job](https://docs.microsoft.com/rest/api/media/jobs) is the actual request to Media Services to apply that **Transform** to a given input video or audio content.</span><span class="sxs-lookup"><span data-stu-id="a8479-168">As mentioned above, the [Transform](https://docs.microsoft.com/rest/api/media/transforms) object is the recipe and a [Job](https://docs.microsoft.com/rest/api/media/jobs) is the actual request to Media Services to apply that **Transform** to a given input video or audio content.</span></span> <span data-ttu-id="a8479-169">The **Job** specifies information like the location of the input video, and the location for the output.</span><span class="sxs-lookup"><span data-stu-id="a8479-169">The **Job** specifies information like the location of the input video, and the location for the output.</span></span> <span data-ttu-id="a8479-170">You can specify the location of your video using: HTTPS URLs, SAS URLs, or Assets that are in your Media Service account.</span><span class="sxs-lookup"><span data-stu-id="a8479-170">You can specify the location of your video using: HTTPS URLs, SAS URLs, or Assets that are in your Media Service account.</span></span> 

<span data-ttu-id="a8479-171">In this example, the job input is a local video.</span><span class="sxs-lookup"><span data-stu-id="a8479-171">In this example, the job input is a local video.</span></span>  

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#SubmitJob)]

### <a name="wait-for-the-job-to-complete"></a><span data-ttu-id="a8479-172">Wait for the job to complete</span><span class="sxs-lookup"><span data-stu-id="a8479-172">Wait for the job to complete</span></span>

<span data-ttu-id="a8479-173">The job takes some time to complete and when it does you want to be notified.</span><span class="sxs-lookup"><span data-stu-id="a8479-173">The job takes some time to complete and when it does you want to be notified.</span></span> <span data-ttu-id="a8479-174">There are different options to get notified about the [Job](https://docs.microsoft.com/rest/api/media/jobs) completion.</span><span class="sxs-lookup"><span data-stu-id="a8479-174">There are different options to get notified about the [Job](https://docs.microsoft.com/rest/api/media/jobs) completion.</span></span> <span data-ttu-id="a8479-175">The simplest option (that is shown here) is to use polling.</span><span class="sxs-lookup"><span data-stu-id="a8479-175">The simplest option (that is shown here) is to use polling.</span></span> 

<span data-ttu-id="a8479-176">Polling is not a recommended best practice for production applications because of potential latency.</span><span class="sxs-lookup"><span data-stu-id="a8479-176">Polling is not a recommended best practice for production applications because of potential latency.</span></span> <span data-ttu-id="a8479-177">Polling can be throttled if overused on an account.</span><span class="sxs-lookup"><span data-stu-id="a8479-177">Polling can be throttled if overused on an account.</span></span> <span data-ttu-id="a8479-178">Developers should instead use Event Grid.</span><span class="sxs-lookup"><span data-stu-id="a8479-178">Developers should instead use Event Grid.</span></span>

<span data-ttu-id="a8479-179">Event Grid is designed for high availability, consistent performance, and dynamic scale.</span><span class="sxs-lookup"><span data-stu-id="a8479-179">Event Grid is designed for high availability, consistent performance, and dynamic scale.</span></span> <span data-ttu-id="a8479-180">With Event Grid, your apps can listen for and react to events from virtually all Azure services, as well as custom sources.</span><span class="sxs-lookup"><span data-stu-id="a8479-180">With Event Grid, your apps can listen for and react to events from virtually all Azure services, as well as custom sources.</span></span> <span data-ttu-id="a8479-181">Simple, HTTP-based reactive event handling helps you build efficient solutions through intelligent filtering and routing of events.</span><span class="sxs-lookup"><span data-stu-id="a8479-181">Simple, HTTP-based reactive event handling helps you build efficient solutions through intelligent filtering and routing of events.</span></span> <span data-ttu-id="a8479-182">See [Route events to a custom web endpoint](job-state-events-cli-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a8479-182">See [Route events to a custom web endpoint](job-state-events-cli-how-to.md).</span></span>

<span data-ttu-id="a8479-183">The **Job** usually goes through the following states: **Scheduled**, **Queued**, **Processing**, **Finished** (the final state).</span><span class="sxs-lookup"><span data-stu-id="a8479-183">The **Job** usually goes through the following states: **Scheduled**, **Queued**, **Processing**, **Finished** (the final state).</span></span> <span data-ttu-id="a8479-184">If the job has encountered an error, you get the **Error** state.</span><span class="sxs-lookup"><span data-stu-id="a8479-184">If the job has encountered an error, you get the **Error** state.</span></span> <span data-ttu-id="a8479-185">If the job is in the process of being canceled, you get **Canceling** and **Canceled** when it is done.</span><span class="sxs-lookup"><span data-stu-id="a8479-185">If the job is in the process of being canceled, you get **Canceling** and **Canceled** when it is done.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#WaitForJobToFinish)]

### <a name="download-the-result-of-the-job"></a><span data-ttu-id="a8479-186">Download the result of the job</span><span class="sxs-lookup"><span data-stu-id="a8479-186">Download the result of the job</span></span>

<span data-ttu-id="a8479-187">The following function downloads the results from the output [Asset](https://docs.microsoft.com/rest/api/media/assets) into the "output" folder, so you can examine the results of the job.</span><span class="sxs-lookup"><span data-stu-id="a8479-187">The following function downloads the results from the output [Asset](https://docs.microsoft.com/rest/api/media/assets) into the "output" folder, so you can examine the results of the job.</span></span> 

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#DownloadResults)]

### <a name="clean-up-resource-in-your-media-services-account"></a><span data-ttu-id="a8479-188">Clean up resource in your Media Services account</span><span class="sxs-lookup"><span data-stu-id="a8479-188">Clean up resource in your Media Services account</span></span>

<span data-ttu-id="a8479-189">Generally, you should clean up everything except objects that you are planning to reuse (typically, you will reuse Transforms and  persist StreamingLocators).</span><span class="sxs-lookup"><span data-stu-id="a8479-189">Generally, you should clean up everything except objects that you are planning to reuse (typically, you will reuse Transforms and  persist StreamingLocators).</span></span> <span data-ttu-id="a8479-190">If you want for your account to be clean after experimenting, you should delete the resources that you do not plan to reuse.</span><span class="sxs-lookup"><span data-stu-id="a8479-190">If you want for your account to be clean after experimenting, you should delete the resources that you do not plan to reuse.</span></span> <span data-ttu-id="a8479-191">For example, the following code deletes Jobs.</span><span class="sxs-lookup"><span data-stu-id="a8479-191">For example, the following code deletes Jobs.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CleanUp)]

## <a name="run-the-sample-app"></a><span data-ttu-id="a8479-192">Run the sample app</span><span class="sxs-lookup"><span data-stu-id="a8479-192">Run the sample app</span></span>

<span data-ttu-id="a8479-193">Press Ctrl+F5 to run the *AnalyzeVideos* application.</span><span class="sxs-lookup"><span data-stu-id="a8479-193">Press Ctrl+F5 to run the *AnalyzeVideos* application.</span></span>

<span data-ttu-id="a8479-194">When we run the program, the job produces thumbnails for each face that it finds in the video.</span><span class="sxs-lookup"><span data-stu-id="a8479-194">When we run the program, the job produces thumbnails for each face that it finds in the video.</span></span> <span data-ttu-id="a8479-195">It also produces the insights.json file.</span><span class="sxs-lookup"><span data-stu-id="a8479-195">It also produces the insights.json file.</span></span>

## <a name="examine-the-output"></a><span data-ttu-id="a8479-196">Examine the output</span><span class="sxs-lookup"><span data-stu-id="a8479-196">Examine the output</span></span>

<span data-ttu-id="a8479-197">The output file of analyzing videos is called insights.json.</span><span class="sxs-lookup"><span data-stu-id="a8479-197">The output file of analyzing videos is called insights.json.</span></span> <span data-ttu-id="a8479-198">This file contains insights about your video.</span><span class="sxs-lookup"><span data-stu-id="a8479-198">This file contains insights about your video.</span></span> <span data-ttu-id="a8479-199">You can find description of  elements found in the json file in the [Media intelligence](intelligence-concept.md) article.</span><span class="sxs-lookup"><span data-stu-id="a8479-199">You can find description of  elements found in the json file in the [Media intelligence](intelligence-concept.md) article.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a8479-200">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a8479-200">Clean up resources</span></span>

<span data-ttu-id="a8479-201">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier.</span><span class="sxs-lookup"><span data-stu-id="a8479-201">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier.</span></span> <span data-ttu-id="a8479-202">You can use the **CloudShell** tool.</span><span class="sxs-lookup"><span data-stu-id="a8479-202">You can use the **CloudShell** tool.</span></span>

<span data-ttu-id="a8479-203">In the **CloudShell**, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="a8479-203">In the **CloudShell**, execute the following command:</span></span>

```azurecli-interactive
az group delete --name amsResourceGroup
```

## <a name="multithreading"></a><span data-ttu-id="a8479-204">Multithreading</span><span class="sxs-lookup"><span data-stu-id="a8479-204">Multithreading</span></span>

<span data-ttu-id="a8479-205">The Azure Media Services v3 SDKs are not thread-safe.</span><span class="sxs-lookup"><span data-stu-id="a8479-205">The Azure Media Services v3 SDKs are not thread-safe.</span></span> <span data-ttu-id="a8479-206">When working with multi-threaded application, you should generate a new  AzureMediaServicesClient object per thread.</span><span class="sxs-lookup"><span data-stu-id="a8479-206">When working with multi-threaded application, you should generate a new  AzureMediaServicesClient object per thread.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8479-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8479-207">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8479-208">Tutorial: upload, encode, and stream files</span><span class="sxs-lookup"><span data-stu-id="a8479-208">Tutorial: upload, encode, and stream files</span></span>](stream-files-tutorial-with-api.md)
