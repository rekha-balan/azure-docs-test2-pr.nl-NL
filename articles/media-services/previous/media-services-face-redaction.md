---
title: Redact faces with Azure Media Analytics | Microsoft Docs
description: This topic demonstrates how to redact faces with Azure media analytics.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako;
ms.openlocfilehash: 910cc246aa19e19b109fc660682c6b2dc239cbb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855754"
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="27fe3-103">Redact faces with Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="27fe3-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="27fe3-104">Overview</span><span class="sxs-lookup"><span data-stu-id="27fe3-104">Overview</span></span>
<span data-ttu-id="27fe3-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span><span class="sxs-lookup"><span data-stu-id="27fe3-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="27fe3-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span><span class="sxs-lookup"><span data-stu-id="27fe3-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="27fe3-107">You may want to use the face redaction service in public safety and news media scenarios.</span><span class="sxs-lookup"><span data-stu-id="27fe3-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="27fe3-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="27fe3-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="27fe3-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="27fe3-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="27fe3-110">This article gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="27fe3-110">This article gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="face-redaction-modes"></a><span data-ttu-id="27fe3-111">Face redaction modes</span><span class="sxs-lookup"><span data-stu-id="27fe3-111">Face redaction modes</span></span>
<span data-ttu-id="27fe3-112">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span><span class="sxs-lookup"><span data-stu-id="27fe3-112">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="27fe3-113">The automated redaction process is complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span><span class="sxs-lookup"><span data-stu-id="27fe3-113">The automated redaction process is complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="27fe3-114">In addition to a fully automatic mode, there is a two-pass workflow, which allows the selection/de-selection of found faces via a list of IDs.</span><span class="sxs-lookup"><span data-stu-id="27fe3-114">In addition to a fully automatic mode, there is a two-pass workflow, which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="27fe3-115">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span><span class="sxs-lookup"><span data-stu-id="27fe3-115">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="27fe3-116">This workflow is split into **Analyze** and **Redact** modes.</span><span class="sxs-lookup"><span data-stu-id="27fe3-116">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="27fe3-117">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span><span class="sxs-lookup"><span data-stu-id="27fe3-117">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="27fe3-118">Combined mode</span><span class="sxs-lookup"><span data-stu-id="27fe3-118">Combined mode</span></span>
<span data-ttu-id="27fe3-119">This produces a redacted mp4 automatically without any manual input.</span><span class="sxs-lookup"><span data-stu-id="27fe3-119">This produces a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="27fe3-120">Stage</span><span class="sxs-lookup"><span data-stu-id="27fe3-120">Stage</span></span> | <span data-ttu-id="27fe3-121">File Name</span><span class="sxs-lookup"><span data-stu-id="27fe3-121">File Name</span></span> | <span data-ttu-id="27fe3-122">Notes</span><span class="sxs-lookup"><span data-stu-id="27fe3-122">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="27fe3-123">Input asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-123">Input asset</span></span> |<span data-ttu-id="27fe3-124">foo.bar</span><span class="sxs-lookup"><span data-stu-id="27fe3-124">foo.bar</span></span> |<span data-ttu-id="27fe3-125">Video in WMV, MOV, or MP4 format</span><span class="sxs-lookup"><span data-stu-id="27fe3-125">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="27fe3-126">Input config</span><span class="sxs-lookup"><span data-stu-id="27fe3-126">Input config</span></span> |<span data-ttu-id="27fe3-127">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="27fe3-127">Job configuration preset</span></span> |<span data-ttu-id="27fe3-128">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="27fe3-128">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="27fe3-129">Output asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-129">Output asset</span></span> |<span data-ttu-id="27fe3-130">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="27fe3-130">foo_redacted.mp4</span></span> |<span data-ttu-id="27fe3-131">Video with blurring applied</span><span class="sxs-lookup"><span data-stu-id="27fe3-131">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="27fe3-132">Input example:</span><span class="sxs-lookup"><span data-stu-id="27fe3-132">Input example:</span></span>
[<span data-ttu-id="27fe3-133">view this video</span><span class="sxs-lookup"><span data-stu-id="27fe3-133">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="27fe3-134">Output example:</span><span class="sxs-lookup"><span data-stu-id="27fe3-134">Output example:</span></span>
[<span data-ttu-id="27fe3-135">view this video</span><span class="sxs-lookup"><span data-stu-id="27fe3-135">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="27fe3-136">Analyze mode</span><span class="sxs-lookup"><span data-stu-id="27fe3-136">Analyze mode</span></span>
<span data-ttu-id="27fe3-137">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span><span class="sxs-lookup"><span data-stu-id="27fe3-137">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="27fe3-138">Stage</span><span class="sxs-lookup"><span data-stu-id="27fe3-138">Stage</span></span> | <span data-ttu-id="27fe3-139">File Name</span><span class="sxs-lookup"><span data-stu-id="27fe3-139">File Name</span></span> | <span data-ttu-id="27fe3-140">Notes</span><span class="sxs-lookup"><span data-stu-id="27fe3-140">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="27fe3-141">Input asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-141">Input asset</span></span> |<span data-ttu-id="27fe3-142">foo.bar</span><span class="sxs-lookup"><span data-stu-id="27fe3-142">foo.bar</span></span> |<span data-ttu-id="27fe3-143">Video in WMV, MPV, or MP4 format</span><span class="sxs-lookup"><span data-stu-id="27fe3-143">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="27fe3-144">Input config</span><span class="sxs-lookup"><span data-stu-id="27fe3-144">Input config</span></span> |<span data-ttu-id="27fe3-145">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="27fe3-145">Job configuration preset</span></span> |<span data-ttu-id="27fe3-146">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="27fe3-146">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="27fe3-147">Output asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-147">Output asset</span></span> |<span data-ttu-id="27fe3-148">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="27fe3-148">foo_annotations.json</span></span> |<span data-ttu-id="27fe3-149">Annotation data of face locations in JSON format.</span><span class="sxs-lookup"><span data-stu-id="27fe3-149">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="27fe3-150">This can be edited by the user to modify the blurring bounding boxes.</span><span class="sxs-lookup"><span data-stu-id="27fe3-150">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="27fe3-151">See sample below.</span><span class="sxs-lookup"><span data-stu-id="27fe3-151">See sample below.</span></span> |
| <span data-ttu-id="27fe3-152">Output asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-152">Output asset</span></span> |<span data-ttu-id="27fe3-153">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="27fe3-153">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="27fe3-154">A cropped jpg of each detected face, where the number indicates the labelId of the face</span><span class="sxs-lookup"><span data-stu-id="27fe3-154">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="27fe3-155">Output example:</span><span class="sxs-lookup"><span data-stu-id="27fe3-155">Output example:</span></span>

```json
    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated
```

### <a name="redact-mode"></a><span data-ttu-id="27fe3-156">Redact mode</span><span class="sxs-lookup"><span data-stu-id="27fe3-156">Redact mode</span></span>
<span data-ttu-id="27fe3-157">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span><span class="sxs-lookup"><span data-stu-id="27fe3-157">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="27fe3-158">This includes a list of IDs to blur, the original video, and the annotations JSON.</span><span class="sxs-lookup"><span data-stu-id="27fe3-158">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="27fe3-159">This mode uses the annotations to apply blurring on the input video.</span><span class="sxs-lookup"><span data-stu-id="27fe3-159">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="27fe3-160">The output from the Analyze pass does not include the original video.</span><span class="sxs-lookup"><span data-stu-id="27fe3-160">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="27fe3-161">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span><span class="sxs-lookup"><span data-stu-id="27fe3-161">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="27fe3-162">Stage</span><span class="sxs-lookup"><span data-stu-id="27fe3-162">Stage</span></span> | <span data-ttu-id="27fe3-163">File Name</span><span class="sxs-lookup"><span data-stu-id="27fe3-163">File Name</span></span> | <span data-ttu-id="27fe3-164">Notes</span><span class="sxs-lookup"><span data-stu-id="27fe3-164">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="27fe3-165">Input asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-165">Input asset</span></span> |<span data-ttu-id="27fe3-166">foo.bar</span><span class="sxs-lookup"><span data-stu-id="27fe3-166">foo.bar</span></span> |<span data-ttu-id="27fe3-167">Video in WMV, MPV, or MP4 format.</span><span class="sxs-lookup"><span data-stu-id="27fe3-167">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="27fe3-168">Same video as in step 1.</span><span class="sxs-lookup"><span data-stu-id="27fe3-168">Same video as in step 1.</span></span> |
| <span data-ttu-id="27fe3-169">Input asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-169">Input asset</span></span> |<span data-ttu-id="27fe3-170">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="27fe3-170">foo_annotations.json</span></span> |<span data-ttu-id="27fe3-171">annotations metadata file from phase one, with optional modifications.</span><span class="sxs-lookup"><span data-stu-id="27fe3-171">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="27fe3-172">Input asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-172">Input asset</span></span> |<span data-ttu-id="27fe3-173">foo_IDList.txt (Optional)</span><span class="sxs-lookup"><span data-stu-id="27fe3-173">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="27fe3-174">Optional new line separated list of face IDs to redact.</span><span class="sxs-lookup"><span data-stu-id="27fe3-174">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="27fe3-175">If left blank, this blurs all faces.</span><span class="sxs-lookup"><span data-stu-id="27fe3-175">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="27fe3-176">Input config</span><span class="sxs-lookup"><span data-stu-id="27fe3-176">Input config</span></span> |<span data-ttu-id="27fe3-177">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="27fe3-177">Job configuration preset</span></span> |<span data-ttu-id="27fe3-178">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="27fe3-178">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="27fe3-179">Output asset</span><span class="sxs-lookup"><span data-stu-id="27fe3-179">Output asset</span></span> |<span data-ttu-id="27fe3-180">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="27fe3-180">foo_redacted.mp4</span></span> |<span data-ttu-id="27fe3-181">Video with blurring applied based on annotations</span><span class="sxs-lookup"><span data-stu-id="27fe3-181">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="27fe3-182">Example output</span><span class="sxs-lookup"><span data-stu-id="27fe3-182">Example output</span></span>
<span data-ttu-id="27fe3-183">This is the output from an IDList with one ID selected.</span><span class="sxs-lookup"><span data-stu-id="27fe3-183">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="27fe3-184">view this video</span><span class="sxs-lookup"><span data-stu-id="27fe3-184">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="27fe3-185">Example foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="27fe3-185">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="27fe3-186">Blur types</span><span class="sxs-lookup"><span data-stu-id="27fe3-186">Blur types</span></span>

<span data-ttu-id="27fe3-187">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Box**, and **Black**.</span><span class="sxs-lookup"><span data-stu-id="27fe3-187">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Box**, and **Black**.</span></span> <span data-ttu-id="27fe3-188">By default **Med** is used.</span><span class="sxs-lookup"><span data-stu-id="27fe3-188">By default **Med** is used.</span></span>

<span data-ttu-id="27fe3-189">You can find samples of the blur types below.</span><span class="sxs-lookup"><span data-stu-id="27fe3-189">You can find samples of the blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="27fe3-190">Example JSON:</span><span class="sxs-lookup"><span data-stu-id="27fe3-190">Example JSON:</span></span>

```json
    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}
```

#### <a name="low"></a><span data-ttu-id="27fe3-191">Low</span><span class="sxs-lookup"><span data-stu-id="27fe3-191">Low</span></span>

![Low](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="27fe3-193">Med</span><span class="sxs-lookup"><span data-stu-id="27fe3-193">Med</span></span>

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="27fe3-195">High</span><span class="sxs-lookup"><span data-stu-id="27fe3-195">High</span></span>

![High](./media/media-services-face-redaction/blur3.png)

#### <a name="box"></a><span data-ttu-id="27fe3-197">Box</span><span class="sxs-lookup"><span data-stu-id="27fe3-197">Box</span></span>

![Box](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="27fe3-199">Black</span><span class="sxs-lookup"><span data-stu-id="27fe3-199">Black</span></span>

![Black](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="27fe3-201">Elements of the output JSON file</span><span class="sxs-lookup"><span data-stu-id="27fe3-201">Elements of the output JSON file</span></span>

<span data-ttu-id="27fe3-202">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span><span class="sxs-lookup"><span data-stu-id="27fe3-202">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="27fe3-203">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span><span class="sxs-lookup"><span data-stu-id="27fe3-203">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="27fe3-204">.NET sample code</span><span class="sxs-lookup"><span data-stu-id="27fe3-204">.NET sample code</span></span>

<span data-ttu-id="27fe3-205">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="27fe3-205">The following program shows how to:</span></span>

1. <span data-ttu-id="27fe3-206">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="27fe3-206">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="27fe3-207">Create a job with a face redaction task based on a configuration file that contains the following json preset:</span><span class="sxs-lookup"><span data-stu-id="27fe3-207">Create a job with a face redaction task based on a configuration file that contains the following json preset:</span></span> 

    ```json
            {
                'version':'1.0',
                'options': {
                    'mode':'combined'
                }
            }
    ```

3. <span data-ttu-id="27fe3-208">Download the output JSON files.</span><span class="sxs-lookup"><span data-stu-id="27fe3-208">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="27fe3-209">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="27fe3-209">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="27fe3-210">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="27fe3-210">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="27fe3-211">Example</span><span class="sxs-lookup"><span data-stu-id="27fe3-211">Example</span></span>

```csharp
using System;
using System.Configuration;
using System.IO;
using System.Linq;
using Microsoft.WindowsAzure.MediaServices.Client;
using System.Threading;
using System.Threading.Tasks;

namespace FaceRedaction
{
    class Program
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

        static void Main(string[] args)
        {
            AzureAdTokenCredentials tokenCredentials =
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run the FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference to Azure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, the event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                Console.WriteLine(string.Format("Error: {0}. {1}",
                                error.Code,
                                error.Message));
                return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
                file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

        static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor",
                                       mediaProcessorName));

            return processor;
        }

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine();
                    break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    Console.WriteLine("Please wait...\n");
                    break;
                case JobState.Canceled:
                case JobState.Error:
                    // Cast sender as a job.
                    IJob job = (IJob)sender;
                    // Display or log error details as needed.
                    // LogJobStop(job.Id);
                    break;
                default:
                    break;
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="27fe3-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="27fe3-212">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="27fe3-213">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="27fe3-213">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="27fe3-214">Related links</span><span class="sxs-lookup"><span data-stu-id="27fe3-214">Related links</span></span>
[<span data-ttu-id="27fe3-215">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="27fe3-215">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="27fe3-216">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="27fe3-216">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

