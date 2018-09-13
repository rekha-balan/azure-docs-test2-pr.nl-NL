---
title: How to encode an Azure asset by using Media Encoder Standard | Microsoft Docs
description: Learn how to use Media Encoder Standard to encode media content on Azure Media Services. Code samples use REST API.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2017
ms.author: juliako
ms.openlocfilehash: 78087bbb43d12af65bfbde93f54e2f29309ac093
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968318"
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="9c7e8-104">How to encode an asset by using Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9c7e8-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portal](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="9c7e8-108">Overview</span><span class="sxs-lookup"><span data-stu-id="9c7e8-108">Overview</span></span>
<span data-ttu-id="9c7e8-109">To deliver digital video over the Internet, you must compress the media.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="9c7e8-110">Digital video files are large and may be too large to deliver over the Internet, or for your customers’ devices to display properly.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-110">Digital video files are large and may be too large to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="9c7e8-111">Encoding is the process of compressing video and audio so your customers can view your media.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="9c7e8-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="9c7e8-113">You create encoding jobs to convert media files from one encoding to another.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="9c7e8-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="9c7e8-115">You can also use an encoder provided by a Media Services partner.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="9c7e8-116">Third-party encoders are available through the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="9c7e8-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="9c7e8-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="9c7e8-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="9c7e8-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span><span class="sxs-lookup"><span data-stu-id="9c7e8-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="9c7e8-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="9c7e8-122">Use OData batch processing.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-122">Use OData batch processing.</span></span>

<span data-ttu-id="9c7e8-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="9c7e8-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="9c7e8-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="9c7e8-126">Considerations</span><span class="sxs-lookup"><span data-stu-id="9c7e8-126">Considerations</span></span>

<span data-ttu-id="9c7e8-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="9c7e8-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="9c7e8-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span></span> <span data-ttu-id="9c7e8-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="9c7e8-131">Connect to Media Services</span><span class="sxs-lookup"><span data-stu-id="9c7e8-131">Connect to Media Services</span></span>

<span data-ttu-id="9c7e8-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="9c7e8-133">Create a job with a single encoding task</span><span class="sxs-lookup"><span data-stu-id="9c7e8-133">Create a job with a single encoding task</span></span>
> [!NOTE]
> When you're working with the Media Services REST API, the following considerations apply:
>
> When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).
>
> When using JSON and specifying to use the **__metadata** keyword in the request (for example, to reference a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.
>
>

<span data-ttu-id="9c7e8-138">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-138">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="9c7e8-139">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-139">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="9c7e8-140">Request:</span><span class="sxs-lookup"><span data-stu-id="9c7e8-140">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.17
        Authorization: Bearer <ENCODED JWT TOKEN> 
        x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
        Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="9c7e8-141">Response:</span><span class="sxs-lookup"><span data-stu-id="9c7e8-141">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="9c7e8-142">Set the output asset's name</span><span class="sxs-lookup"><span data-stu-id="9c7e8-142">Set the output asset's name</span></span>
<span data-ttu-id="9c7e8-143">The following example shows how to set the assetName attribute:</span><span class="sxs-lookup"><span data-stu-id="9c7e8-143">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="9c7e8-144">Considerations</span><span class="sxs-lookup"><span data-stu-id="9c7e8-144">Considerations</span></span>
* <span data-ttu-id="9c7e8-145">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-145">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="9c7e8-146">The task article contains the XML Schema Definition for the XML.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-146">The task article contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="9c7e8-147">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-147">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="9c7e8-148">A task can have multiple output assets.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-148">A task can have multiple output assets.</span></span> <span data-ttu-id="9c7e8-149">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-149">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="9c7e8-150">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-150">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="9c7e8-151">Tasks must not form a cycle.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-151">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="9c7e8-152">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-152">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="9c7e8-153">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-153">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="9c7e8-154">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata: uri" name-value pair.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-154">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata: uri" name-value pair.</span></span>
* <span data-ttu-id="9c7e8-155">InputMediaAssets maps to one or more assets that you created in Media Services.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-155">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="9c7e8-156">OutputMediaAssets are created by the system.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-156">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="9c7e8-157">They don't reference an existing asset.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-157">They don't reference an existing asset.</span></span>
* <span data-ttu-id="9c7e8-158">OutputMediaAssets can be named by using the assetName attribute.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-158">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="9c7e8-159">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-159">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="9c7e8-160">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span><span class="sxs-lookup"><span data-stu-id="9c7e8-160">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="9c7e8-161">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span><span class="sxs-lookup"><span data-stu-id="9c7e8-161">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="9c7e8-162">Create a job with chained tasks</span><span class="sxs-lookup"><span data-stu-id="9c7e8-162">Create a job with chained tasks</span></span>
<span data-ttu-id="9c7e8-163">In many application scenarios, developers want to create a series of processing tasks.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-163">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="9c7e8-164">In Media Services, you can create a series of chained tasks.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-164">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="9c7e8-165">Each task performs different processing steps and can use different media processors.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-165">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="9c7e8-166">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-166">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="9c7e8-167">However, the tasks performed in a job are not required to be in a sequence.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-167">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="9c7e8-168">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-168">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> There is currently a limit of 30 tasks per job. If you need to chain more than 30 tasks, create more than one job to contain the tasks.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.17
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="9c7e8-171">Considerations</span><span class="sxs-lookup"><span data-stu-id="9c7e8-171">Considerations</span></span>
<span data-ttu-id="9c7e8-172">To enable task chaining:</span><span class="sxs-lookup"><span data-stu-id="9c7e8-172">To enable task chaining:</span></span>

* <span data-ttu-id="9c7e8-173">A job must have at least two tasks.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-173">A job must have at least two tasks.</span></span>
* <span data-ttu-id="9c7e8-174">There must be at least one task whose input is the output of another task in the job.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-174">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="9c7e8-175">Use OData batch processing</span><span class="sxs-lookup"><span data-stu-id="9c7e8-175">Use OData batch processing</span></span>
<span data-ttu-id="9c7e8-176">The following example shows how to use OData batch processing to create a job and tasks.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-176">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="9c7e8-177">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-177">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="9c7e8-178">Create a job by using a JobTemplate</span><span class="sxs-lookup"><span data-stu-id="9c7e8-178">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="9c7e8-179">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-179">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="9c7e8-180">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-180">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="9c7e8-181">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-181">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="9c7e8-182">However, other MediaProcessors can be used as well.</span><span class="sxs-lookup"><span data-stu-id="9c7e8-182">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.17
    Authorization: Bearer <ENCODED JWT TOKEN> 
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body. The content identification scheme must follow the scheme described in Identify Azure Media Services Entities. Also, JobTemplates cannot be updated. Instead, you must create a new one with your updated changes.
>
>

<span data-ttu-id="9c7e8-187">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="9c7e8-187">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="9c7e8-188">The following example shows how to create a job that references a JobTemplate Id:</span><span class="sxs-lookup"><span data-stu-id="9c7e8-188">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.17
    Authorization: Bearer <ENCODED JWT TOKEN> 
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="9c7e8-189">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="9c7e8-189">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


## <a name="advanced-encoding-features-to-explore"></a><span data-ttu-id="9c7e8-190">Advanced Encoding Features to explore</span><span class="sxs-lookup"><span data-stu-id="9c7e8-190">Advanced Encoding Features to explore</span></span>
* [<span data-ttu-id="9c7e8-191">How to generate thumbnails</span><span class="sxs-lookup"><span data-stu-id="9c7e8-191">How to generate thumbnails</span></span>](media-services-dotnet-generate-thumbnail-with-mes.md)
* [<span data-ttu-id="9c7e8-192">Generating thumbnails during encoding</span><span class="sxs-lookup"><span data-stu-id="9c7e8-192">Generating thumbnails during encoding</span></span>](media-services-dotnet-generate-thumbnail-with-mes.md#example-of-generating-a-thumbnail-while-encoding)
* [<span data-ttu-id="9c7e8-193">Crop videos during encoding</span><span class="sxs-lookup"><span data-stu-id="9c7e8-193">Crop videos during encoding</span></span>](media-services-crop-video.md)
* [<span data-ttu-id="9c7e8-194">Customizing encoding presets</span><span class="sxs-lookup"><span data-stu-id="9c7e8-194">Customizing encoding presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="9c7e8-195">Overlay or watermark a video with an image</span><span class="sxs-lookup"><span data-stu-id="9c7e8-195">Overlay or watermark a video with an image</span></span>](media-services-advanced-encoding-with-mes.md#overlay)

## <a name="media-services-learning-paths"></a><span data-ttu-id="9c7e8-196">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="9c7e8-196">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9c7e8-197">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="9c7e8-197">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="9c7e8-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c7e8-198">Next steps</span></span>
<span data-ttu-id="9c7e8-199">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="9c7e8-199">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9c7e8-200">See also</span><span class="sxs-lookup"><span data-stu-id="9c7e8-200">See also</span></span>
[<span data-ttu-id="9c7e8-201">Get Media Processors</span><span class="sxs-lookup"><span data-stu-id="9c7e8-201">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
