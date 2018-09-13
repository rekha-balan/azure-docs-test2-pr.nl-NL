---
title: How to encode an Azure asset by using Media Encoder Standard | Microsoft Docs
description: Learn how to use Media Encoder Standard to encode media content on Azure Media Services. Code samples use REST API.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: 4e56b8d97a650813dcea1fde9d74ddc29154605d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564217"
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="01105-104">How to encode an asset by using Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="01105-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portal](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="01105-108">Overview</span><span class="sxs-lookup"><span data-stu-id="01105-108">Overview</span></span>
<span data-ttu-id="01105-109">To deliver digital video over the Internet, you must compress the media.</span><span class="sxs-lookup"><span data-stu-id="01105-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="01105-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span><span class="sxs-lookup"><span data-stu-id="01105-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="01105-111">Encoding is the process of compressing video and audio so your customers can view your media.</span><span class="sxs-lookup"><span data-stu-id="01105-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="01105-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="01105-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="01105-113">You create encoding jobs to convert media files from one encoding to another.</span><span class="sxs-lookup"><span data-stu-id="01105-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="01105-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="01105-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="01105-115">You can also use an encoder provided by a Media Services partner.</span><span class="sxs-lookup"><span data-stu-id="01105-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="01105-116">Third-party encoders are available through the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="01105-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="01105-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span><span class="sxs-lookup"><span data-stu-id="01105-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="01105-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="01105-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="01105-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span><span class="sxs-lookup"><span data-stu-id="01105-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="01105-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span><span class="sxs-lookup"><span data-stu-id="01105-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="01105-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span><span class="sxs-lookup"><span data-stu-id="01105-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="01105-122">Use OData batch processing.</span><span class="sxs-lookup"><span data-stu-id="01105-122">Use OData batch processing.</span></span>

<span data-ttu-id="01105-123">We recommend that you always encode your mezzanine files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01105-123">We recommend that you always encode your mezzanine files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="01105-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="01105-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="01105-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="01105-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> Before you start referencing media processors, verify that you have the correct media processor ID. For more information, see [Get media processors](media-services-rest-get-media-processor.md).
>
>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="01105-128">Create a job with a single encoding task</span><span class="sxs-lookup"><span data-stu-id="01105-128">Create a job with a single encoding task</span></span>
> [!NOTE]
> When you're working with the Media Services REST API, the following considerations apply:
>
> When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).
>
> After successfully connecting to https://media.windows.net, you will receive a 301 redirect that specifies another Media Services URI. You must make subsequent calls to the new URI as described in [Connecting to Media Services using REST API](media-services-rest-connect-programmatically.md).
>
> When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.
>
>

<span data-ttu-id="01105-135">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span><span class="sxs-lookup"><span data-stu-id="01105-135">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="01105-136">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="01105-136">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="01105-137">Request:</span><span class="sxs-lookup"><span data-stu-id="01105-137">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="01105-138">Response:</span><span class="sxs-lookup"><span data-stu-id="01105-138">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="01105-139">Set the output asset's name</span><span class="sxs-lookup"><span data-stu-id="01105-139">Set the output asset's name</span></span>
<span data-ttu-id="01105-140">The following example shows how to set the assetName attribute:</span><span class="sxs-lookup"><span data-stu-id="01105-140">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="01105-141">Considerations</span><span class="sxs-lookup"><span data-stu-id="01105-141">Considerations</span></span>
* <span data-ttu-id="01105-142">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span><span class="sxs-lookup"><span data-stu-id="01105-142">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="01105-143">The task topic contains the XML Schema Definition for the XML.</span><span class="sxs-lookup"><span data-stu-id="01105-143">The task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="01105-144">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="01105-144">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="01105-145">A task can have multiple output assets.</span><span class="sxs-lookup"><span data-stu-id="01105-145">A task can have multiple output assets.</span></span> <span data-ttu-id="01105-146">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span><span class="sxs-lookup"><span data-stu-id="01105-146">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="01105-147">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span><span class="sxs-lookup"><span data-stu-id="01105-147">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="01105-148">Tasks must not form a cycle.</span><span class="sxs-lookup"><span data-stu-id="01105-148">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="01105-149">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span><span class="sxs-lookup"><span data-stu-id="01105-149">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="01105-150">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span><span class="sxs-lookup"><span data-stu-id="01105-150">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="01105-151">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span><span class="sxs-lookup"><span data-stu-id="01105-151">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="01105-152">InputMediaAssets maps to one or more assets that you created in Media Services.</span><span class="sxs-lookup"><span data-stu-id="01105-152">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="01105-153">OutputMediaAssets are created by the system.</span><span class="sxs-lookup"><span data-stu-id="01105-153">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="01105-154">They don't reference an existing asset.</span><span class="sxs-lookup"><span data-stu-id="01105-154">They don't reference an existing asset.</span></span>
* <span data-ttu-id="01105-155">OutputMediaAssets can be named by using the assetName attribute.</span><span class="sxs-lookup"><span data-stu-id="01105-155">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="01105-156">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span><span class="sxs-lookup"><span data-stu-id="01105-156">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="01105-157">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span><span class="sxs-lookup"><span data-stu-id="01105-157">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="01105-158">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span><span class="sxs-lookup"><span data-stu-id="01105-158">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="01105-159">Create a job with chained tasks</span><span class="sxs-lookup"><span data-stu-id="01105-159">Create a job with chained tasks</span></span>
<span data-ttu-id="01105-160">In many application scenarios, developers want to create a series of processing tasks.</span><span class="sxs-lookup"><span data-stu-id="01105-160">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="01105-161">In Media Services, you can create a series of chained tasks.</span><span class="sxs-lookup"><span data-stu-id="01105-161">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="01105-162">Each task performs different processing steps and can use different media processors.</span><span class="sxs-lookup"><span data-stu-id="01105-162">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="01105-163">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span><span class="sxs-lookup"><span data-stu-id="01105-163">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="01105-164">However, the tasks performed in a job are not required to be in a sequence.</span><span class="sxs-lookup"><span data-stu-id="01105-164">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="01105-165">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span><span class="sxs-lookup"><span data-stu-id="01105-165">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> There is currently a limit of 30 tasks per job. If you need to chain more than 30 tasks, create more than one job to contain the tasks.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
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


### <a name="considerations"></a><span data-ttu-id="01105-168">Considerations</span><span class="sxs-lookup"><span data-stu-id="01105-168">Considerations</span></span>
<span data-ttu-id="01105-169">To enable task chaining:</span><span class="sxs-lookup"><span data-stu-id="01105-169">To enable task chaining:</span></span>

* <span data-ttu-id="01105-170">A job must have at least two tasks.</span><span class="sxs-lookup"><span data-stu-id="01105-170">A job must have at least two tasks.</span></span>
* <span data-ttu-id="01105-171">There must be at least one task whose input is the output of another task in the job.</span><span class="sxs-lookup"><span data-stu-id="01105-171">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="01105-172">Use OData batch processing</span><span class="sxs-lookup"><span data-stu-id="01105-172">Use OData batch processing</span></span>
<span data-ttu-id="01105-173">The following example shows how to use OData batch processing to create a job and tasks.</span><span class="sxs-lookup"><span data-stu-id="01105-173">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="01105-174">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="01105-174">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
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
    Authorization: Bearer <token>
    x-ms-version: 2.11
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
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="01105-175">Create a job by using a JobTemplate</span><span class="sxs-lookup"><span data-stu-id="01105-175">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="01105-176">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span><span class="sxs-lookup"><span data-stu-id="01105-176">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="01105-177">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span><span class="sxs-lookup"><span data-stu-id="01105-177">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="01105-178">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span><span class="sxs-lookup"><span data-stu-id="01105-178">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="01105-179">However, other MediaProcessors can be used as well.</span><span class="sxs-lookup"><span data-stu-id="01105-179">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body. The content identification scheme must follow the scheme described in Identify Azure Media Services Entities. Also, JobTemplates cannot be updated. Instead, you must create a new one with your updated changes.
>
>

<span data-ttu-id="01105-184">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="01105-184">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="01105-185">The following example shows how to create a job that references a JobTemplate Id:</span><span class="sxs-lookup"><span data-stu-id="01105-185">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="01105-186">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="01105-186">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="01105-187">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="01105-187">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="01105-188">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="01105-188">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="01105-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="01105-189">Next steps</span></span>
<span data-ttu-id="01105-190">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="01105-190">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="01105-191">See also</span><span class="sxs-lookup"><span data-stu-id="01105-191">See also</span></span>
[<span data-ttu-id="01105-192">Get Media Processors</span><span class="sxs-lookup"><span data-stu-id="01105-192">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
