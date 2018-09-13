---
title: Redact faces with Azure Media Analytics | Microsoft Docs
description: This topic demonstrates how to redact faces with Azure media analytics.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/16/2017
ms.author: juliako;
ms.openlocfilehash: 2600c5cec36a8a44a85a62d6672d6ae57343f20c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552596"
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="b3695-103">Redact faces with Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="b3695-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="b3695-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b3695-104">Overview</span></span>
<span data-ttu-id="b3695-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span><span class="sxs-lookup"><span data-stu-id="b3695-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="b3695-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span><span class="sxs-lookup"><span data-stu-id="b3695-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="b3695-107">You may want to use the face redaction service in public safety and news media scenarios.</span><span class="sxs-lookup"><span data-stu-id="b3695-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="b3695-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="b3695-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="b3695-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="b3695-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="b3695-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="b3695-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="b3695-111">The **Azure Media Redactor** MP is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="b3695-111">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="b3695-112">It is available in all public Azure regions as well as US Government and China data centers.</span><span class="sxs-lookup"><span data-stu-id="b3695-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="b3695-113">This preview is currently free of charge.</span><span class="sxs-lookup"><span data-stu-id="b3695-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="b3695-114">Face redaction modes</span><span class="sxs-lookup"><span data-stu-id="b3695-114">Face redaction modes</span></span>
<span data-ttu-id="b3695-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span><span class="sxs-lookup"><span data-stu-id="b3695-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="b3695-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span><span class="sxs-lookup"><span data-stu-id="b3695-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="b3695-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span><span class="sxs-lookup"><span data-stu-id="b3695-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="b3695-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span><span class="sxs-lookup"><span data-stu-id="b3695-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="b3695-119">This workflow is split into **Analyze** and **Redact** modes.</span><span class="sxs-lookup"><span data-stu-id="b3695-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="b3695-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span><span class="sxs-lookup"><span data-stu-id="b3695-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="b3695-121">Combined mode</span><span class="sxs-lookup"><span data-stu-id="b3695-121">Combined mode</span></span>
<span data-ttu-id="b3695-122">This will produce a redacted mp4 automatically without any manual input.</span><span class="sxs-lookup"><span data-stu-id="b3695-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="b3695-123">Stage</span><span class="sxs-lookup"><span data-stu-id="b3695-123">Stage</span></span> | <span data-ttu-id="b3695-124">File Name</span><span class="sxs-lookup"><span data-stu-id="b3695-124">File Name</span></span> | <span data-ttu-id="b3695-125">Notes</span><span class="sxs-lookup"><span data-stu-id="b3695-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3695-126">Input asset</span><span class="sxs-lookup"><span data-stu-id="b3695-126">Input asset</span></span> |<span data-ttu-id="b3695-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="b3695-127">foo.bar</span></span> |<span data-ttu-id="b3695-128">Video in WMV, MOV, or MP4 format</span><span class="sxs-lookup"><span data-stu-id="b3695-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="b3695-129">Input config</span><span class="sxs-lookup"><span data-stu-id="b3695-129">Input config</span></span> |<span data-ttu-id="b3695-130">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="b3695-130">Job configuration preset</span></span> |<span data-ttu-id="b3695-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="b3695-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="b3695-132">Output asset</span><span class="sxs-lookup"><span data-stu-id="b3695-132">Output asset</span></span> |<span data-ttu-id="b3695-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="b3695-133">foo_redacted.mp4</span></span> |<span data-ttu-id="b3695-134">Video with blurring applied</span><span class="sxs-lookup"><span data-stu-id="b3695-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="b3695-135">Input example:</span><span class="sxs-lookup"><span data-stu-id="b3695-135">Input example:</span></span>
[<span data-ttu-id="b3695-136">view this video</span><span class="sxs-lookup"><span data-stu-id="b3695-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="b3695-137">Output example:</span><span class="sxs-lookup"><span data-stu-id="b3695-137">Output example:</span></span>
[<span data-ttu-id="b3695-138">view this video</span><span class="sxs-lookup"><span data-stu-id="b3695-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="b3695-139">Analyze mode</span><span class="sxs-lookup"><span data-stu-id="b3695-139">Analyze mode</span></span>
<span data-ttu-id="b3695-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span><span class="sxs-lookup"><span data-stu-id="b3695-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="b3695-141">Stage</span><span class="sxs-lookup"><span data-stu-id="b3695-141">Stage</span></span> | <span data-ttu-id="b3695-142">File Name</span><span class="sxs-lookup"><span data-stu-id="b3695-142">File Name</span></span> | <span data-ttu-id="b3695-143">Notes</span><span class="sxs-lookup"><span data-stu-id="b3695-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3695-144">Input asset</span><span class="sxs-lookup"><span data-stu-id="b3695-144">Input asset</span></span> |<span data-ttu-id="b3695-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="b3695-145">foo.bar</span></span> |<span data-ttu-id="b3695-146">Video in WMV, MPV, or MP4 format</span><span class="sxs-lookup"><span data-stu-id="b3695-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="b3695-147">Input config</span><span class="sxs-lookup"><span data-stu-id="b3695-147">Input config</span></span> |<span data-ttu-id="b3695-148">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="b3695-148">Job configuration preset</span></span> |<span data-ttu-id="b3695-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="b3695-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="b3695-150">Output asset</span><span class="sxs-lookup"><span data-stu-id="b3695-150">Output asset</span></span> |<span data-ttu-id="b3695-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="b3695-151">foo_annotations.json</span></span> |<span data-ttu-id="b3695-152">Annotation data of face locations in JSON format.</span><span class="sxs-lookup"><span data-stu-id="b3695-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="b3695-153">This can be edited by the user to modify the blurring bounding boxes.</span><span class="sxs-lookup"><span data-stu-id="b3695-153">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="b3695-154">See sample below.</span><span class="sxs-lookup"><span data-stu-id="b3695-154">See sample below.</span></span> |
| <span data-ttu-id="b3695-155">Output asset</span><span class="sxs-lookup"><span data-stu-id="b3695-155">Output asset</span></span> |<span data-ttu-id="b3695-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="b3695-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="b3695-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span><span class="sxs-lookup"><span data-stu-id="b3695-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="b3695-158">Output Example:</span><span class="sxs-lookup"><span data-stu-id="b3695-158">Output Example:</span></span>
    {
      "version": 1,
      "timescale": 50,
      "offset": 0,
      "framerate": 25.0,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 2,
          "interval": 2,
          "events": [
            [  
              {
                "id": 1,
                "x": 0.306415737,
                "y": 0.03199235,
                "width": 0.15357475,
                "height": 0.322126418
              },
              {
                "id": 2,
                "x": 0.5625317,
                "y": 0.0868245438,
                "width": 0.149155334,
                "height": 0.355517566
              }
            ]
          ]
        },

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="b3695-159">Redact Mode</span><span class="sxs-lookup"><span data-stu-id="b3695-159">Redact Mode</span></span>
<span data-ttu-id="b3695-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span><span class="sxs-lookup"><span data-stu-id="b3695-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="b3695-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span><span class="sxs-lookup"><span data-stu-id="b3695-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="b3695-162">This mode uses the annotations to apply blurring on the input video.</span><span class="sxs-lookup"><span data-stu-id="b3695-162">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="b3695-163">The output from the Analyze pass does not include the original video.</span><span class="sxs-lookup"><span data-stu-id="b3695-163">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="b3695-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span><span class="sxs-lookup"><span data-stu-id="b3695-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="b3695-165">Stage</span><span class="sxs-lookup"><span data-stu-id="b3695-165">Stage</span></span> | <span data-ttu-id="b3695-166">File Name</span><span class="sxs-lookup"><span data-stu-id="b3695-166">File Name</span></span> | <span data-ttu-id="b3695-167">Notes</span><span class="sxs-lookup"><span data-stu-id="b3695-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3695-168">Input asset</span><span class="sxs-lookup"><span data-stu-id="b3695-168">Input asset</span></span> |<span data-ttu-id="b3695-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="b3695-169">foo.bar</span></span> |<span data-ttu-id="b3695-170">Video in WMV, MPV, or MP4 format.</span><span class="sxs-lookup"><span data-stu-id="b3695-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="b3695-171">Same video as in step 1.</span><span class="sxs-lookup"><span data-stu-id="b3695-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="b3695-172">Input asset</span><span class="sxs-lookup"><span data-stu-id="b3695-172">Input asset</span></span> |<span data-ttu-id="b3695-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="b3695-173">foo_annotations.json</span></span> |<span data-ttu-id="b3695-174">annotations metadata file from phase one, with optional modifications.</span><span class="sxs-lookup"><span data-stu-id="b3695-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="b3695-175">Input asset</span><span class="sxs-lookup"><span data-stu-id="b3695-175">Input asset</span></span> |<span data-ttu-id="b3695-176">foo_IDList.txt (Optional)</span><span class="sxs-lookup"><span data-stu-id="b3695-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="b3695-177">Optional new line separated list of face IDs to redact.</span><span class="sxs-lookup"><span data-stu-id="b3695-177">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="b3695-178">If left blank, this blurs all faces.</span><span class="sxs-lookup"><span data-stu-id="b3695-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="b3695-179">Input config</span><span class="sxs-lookup"><span data-stu-id="b3695-179">Input config</span></span> |<span data-ttu-id="b3695-180">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="b3695-180">Job configuration preset</span></span> |<span data-ttu-id="b3695-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="b3695-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="b3695-182">Output asset</span><span class="sxs-lookup"><span data-stu-id="b3695-182">Output asset</span></span> |<span data-ttu-id="b3695-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="b3695-183">foo_redacted.mp4</span></span> |<span data-ttu-id="b3695-184">Video with blurring applied based on annotations</span><span class="sxs-lookup"><span data-stu-id="b3695-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="b3695-185">Example Output</span><span class="sxs-lookup"><span data-stu-id="b3695-185">Example Output</span></span>
<span data-ttu-id="b3695-186">This is the output from an IDList with one ID selected.</span><span class="sxs-lookup"><span data-stu-id="b3695-186">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="b3695-187">view this video</span><span class="sxs-lookup"><span data-stu-id="b3695-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="b3695-188">Example foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="b3695-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3
 
## <a name="attribute-descriptions"></a><span data-ttu-id="b3695-189">Attribute descriptions</span><span class="sxs-lookup"><span data-stu-id="b3695-189">Attribute descriptions</span></span>
<span data-ttu-id="b3695-190">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span><span class="sxs-lookup"><span data-stu-id="b3695-190">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="b3695-191">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span><span class="sxs-lookup"><span data-stu-id="b3695-191">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

<span data-ttu-id="b3695-192">The detected and tracked faces are returned with coordinates indicating the location of faces, as well as a face ID number indicating the tracking of that individual.</span><span class="sxs-lookup"><span data-stu-id="b3695-192">The detected and tracked faces are returned with coordinates indicating the location of faces, as well as a face ID number indicating the tracking of that individual.</span></span> <span data-ttu-id="b3695-193">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span><span class="sxs-lookup"><span data-stu-id="b3695-193">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span></span>

<span data-ttu-id="b3695-194">For detailed explanations for the attributes, see [Detect Face and Emotion with Azure Media Analytics](media-services-face-and-emotion-detection.md) topic.</span><span class="sxs-lookup"><span data-stu-id="b3695-194">For detailed explanations for the attributes, see [Detect Face and Emotion with Azure Media Analytics](media-services-face-and-emotion-detection.md) topic.</span></span>

## <a name="sample-code"></a><span data-ttu-id="b3695-195">Sample code</span><span class="sxs-lookup"><span data-stu-id="b3695-195">Sample code</span></span>
<span data-ttu-id="b3695-196">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="b3695-196">The following program shows how to:</span></span>

1. <span data-ttu-id="b3695-197">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="b3695-197">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="b3695-198">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span><span class="sxs-lookup"><span data-stu-id="b3695-198">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="b3695-199">Download the output JSON files.</span><span class="sxs-lookup"><span data-stu-id="b3695-199">Download the output JSON files.</span></span> 
   
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
                private static readonly string _mediaServicesAccountName =
                    ConfigurationManager.AppSettings["MediaServicesAccountName"];
                private static readonly string _mediaServicesAccountKey =
                    ConfigurationManager.AppSettings["MediaServicesAccountKey"];
   
                // Field for service context.
                private static CloudMediaContext _context = null;
                private static MediaServicesCredentials _cachedCredentials = null;
   
                static void Main(string[] args)
                {
   
                    // Create and cache the Media Services credentials in a static class variable.
                    _cachedCredentials = new MediaServicesCredentials(
                                    _mediaServicesAccountName,
                                    _mediaServicesAccountKey);
                    // Used the cached credentials to create CloudMediaContext.
                    _context = new CloudMediaContext(_cachedCredentials);
   
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

## <a name="next-step"></a><span data-ttu-id="b3695-200">Next step</span><span class="sxs-lookup"><span data-stu-id="b3695-200">Next step</span></span>
<span data-ttu-id="b3695-201">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="b3695-201">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b3695-202">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="b3695-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="b3695-203">Related links</span><span class="sxs-lookup"><span data-stu-id="b3695-203">Related links</span></span>
[<span data-ttu-id="b3695-204">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="b3695-204">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="b3695-205">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="b3695-205">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

