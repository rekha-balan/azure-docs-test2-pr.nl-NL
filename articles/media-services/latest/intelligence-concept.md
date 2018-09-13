---
title: Azure media intelligence | Microsoft Docs
description: When using Azure Media Services, you can analyze your audio and video contnet using AudioAnalyzerPreset and VideoAnalyzerPreset.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 04/24/2018
ms.author: juliako
ms.openlocfilehash: c488060b9db0ba482d12eee2394e5149b918950e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966232"
---
# <a name="media-intelligence"></a><span data-ttu-id="aed25-103">Media intelligence</span><span class="sxs-lookup"><span data-stu-id="aed25-103">Media intelligence</span></span>

<span data-ttu-id="aed25-104">Azure Media Services REST v3 API enables you to analyze audio and video content.</span><span class="sxs-lookup"><span data-stu-id="aed25-104">Azure Media Services REST v3 API enables you to analyze audio and video content.</span></span> <span data-ttu-id="aed25-105">To analyze your content, you create a **Transform** and submit a **Job** that uses one of these presets: **AudioAnalyzerPreset** or **VideoAnalyzerPreset**.</span><span class="sxs-lookup"><span data-stu-id="aed25-105">To analyze your content, you create a **Transform** and submit a **Job** that uses one of these presets: **AudioAnalyzerPreset** or **VideoAnalyzerPreset**.</span></span> 

## <a name="audioanalyzerpreset"></a><span data-ttu-id="aed25-106">AudioAnalyzerPreset</span><span class="sxs-lookup"><span data-stu-id="aed25-106">AudioAnalyzerPreset</span></span>

<span data-ttu-id="aed25-107">**AudioAnalyzerPreset** enables you to extract multiple audio insights from an audio or video file.</span><span class="sxs-lookup"><span data-stu-id="aed25-107">**AudioAnalyzerPreset** enables you to extract multiple audio insights from an audio or video file.</span></span> <span data-ttu-id="aed25-108">The output includes a JSON file (with all the insights) and VTT file for the audio transcript.</span><span class="sxs-lookup"><span data-stu-id="aed25-108">The output includes a JSON file (with all the insights) and VTT file for the audio transcript.</span></span> <span data-ttu-id="aed25-109">This preset accepts a property that specifies the language of the input file in the form of a [BCP47](https://tools.ietf.org/html/bcp47) string.</span><span class="sxs-lookup"><span data-stu-id="aed25-109">This preset accepts a property that specifies the language of the input file in the form of a [BCP47](https://tools.ietf.org/html/bcp47) string.</span></span> <span data-ttu-id="aed25-110">The audio insights include:</span><span class="sxs-lookup"><span data-stu-id="aed25-110">The audio insights include:</span></span>

* <span data-ttu-id="aed25-111">Audio transcription – a transcript of the spoken words with timestamps.</span><span class="sxs-lookup"><span data-stu-id="aed25-111">Audio transcription – a transcript of the spoken words with timestamps.</span></span> <span data-ttu-id="aed25-112">Multiple languages are supported</span><span class="sxs-lookup"><span data-stu-id="aed25-112">Multiple languages are supported</span></span>
* <span data-ttu-id="aed25-113">Speaker indexing – a mapping of the speakers and the corresponding spoken words</span><span class="sxs-lookup"><span data-stu-id="aed25-113">Speaker indexing – a mapping of the speakers and the corresponding spoken words</span></span>
* <span data-ttu-id="aed25-114">Speech sentiment analysis – the output of sentiment analysis performed on the audio transcription</span><span class="sxs-lookup"><span data-stu-id="aed25-114">Speech sentiment analysis – the output of sentiment analysis performed on the audio transcription</span></span>
* <span data-ttu-id="aed25-115">Keywords – keywords that are extracted from the audio transcription.</span><span class="sxs-lookup"><span data-stu-id="aed25-115">Keywords – keywords that are extracted from the audio transcription.</span></span>

## <a name="videoanalyzerpreset"></a><span data-ttu-id="aed25-116">VideoAnalyzerPreset</span><span class="sxs-lookup"><span data-stu-id="aed25-116">VideoAnalyzerPreset</span></span>

<span data-ttu-id="aed25-117">**VideoAnalyzerPreset** enables you to extract multiple audio and video insights from a video file.</span><span class="sxs-lookup"><span data-stu-id="aed25-117">**VideoAnalyzerPreset** enables you to extract multiple audio and video insights from a video file.</span></span> <span data-ttu-id="aed25-118">The output includes a JSON file (with all the insights), a VTT file for the video transcript, and a collection of thumbnails.</span><span class="sxs-lookup"><span data-stu-id="aed25-118">The output includes a JSON file (with all the insights), a VTT file for the video transcript, and a collection of thumbnails.</span></span> <span data-ttu-id="aed25-119">This preset also accepts a [BCP47](https://tools.ietf.org/html/bcp47) string (representing the language of the video) as a property.</span><span class="sxs-lookup"><span data-stu-id="aed25-119">This preset also accepts a [BCP47](https://tools.ietf.org/html/bcp47) string (representing the language of the video) as a property.</span></span> <span data-ttu-id="aed25-120">The video insights include all the audio insights mentioned above and the following additional items:</span><span class="sxs-lookup"><span data-stu-id="aed25-120">The video insights include all the audio insights mentioned above and the following additional items:</span></span>

* <span data-ttu-id="aed25-121">Face tracking – the time during which faces are present in the video.</span><span class="sxs-lookup"><span data-stu-id="aed25-121">Face tracking – the time during which faces are present in the video.</span></span> <span data-ttu-id="aed25-122">Each face has a face id and a corresponding collection of thumbnails</span><span class="sxs-lookup"><span data-stu-id="aed25-122">Each face has a face id and a corresponding collection of thumbnails</span></span>
* <span data-ttu-id="aed25-123">Visual text – the text that is detected via optical character recognition.</span><span class="sxs-lookup"><span data-stu-id="aed25-123">Visual text – the text that is detected via optical character recognition.</span></span> <span data-ttu-id="aed25-124">The text is time stamped and also used to extract keywords (in addition to the audio transcript)</span><span class="sxs-lookup"><span data-stu-id="aed25-124">The text is time stamped and also used to extract keywords (in addition to the audio transcript)</span></span>
* <span data-ttu-id="aed25-125">Keyframes – a collection of keyframes that are extracted from the video</span><span class="sxs-lookup"><span data-stu-id="aed25-125">Keyframes – a collection of keyframes that are extracted from the video</span></span>
* <span data-ttu-id="aed25-126">Visual content moderation – the portion of the videos that have been flagged as adult or racy in nature</span><span class="sxs-lookup"><span data-stu-id="aed25-126">Visual content moderation – the portion of the videos that have been flagged as adult or racy in nature</span></span>
* <span data-ttu-id="aed25-127">Annotation – a result of annotating the videos based on a pre-defined object model</span><span class="sxs-lookup"><span data-stu-id="aed25-127">Annotation – a result of annotating the videos based on a pre-defined object model</span></span>

##  <a name="insightsjson-elements"></a><span data-ttu-id="aed25-128">insights.json elements</span><span class="sxs-lookup"><span data-stu-id="aed25-128">insights.json elements</span></span>

<span data-ttu-id="aed25-129">The output includes a JSON file (insights.json) with all the insights that were found in the video or audio.</span><span class="sxs-lookup"><span data-stu-id="aed25-129">The output includes a JSON file (insights.json) with all the insights that were found in the video or audio.</span></span> <span data-ttu-id="aed25-130">The json may contain the following elements:</span><span class="sxs-lookup"><span data-stu-id="aed25-130">The json may contain the following elements:</span></span>

### <a name="transcript"></a><span data-ttu-id="aed25-131">transcript</span><span class="sxs-lookup"><span data-stu-id="aed25-131">transcript</span></span>

|<span data-ttu-id="aed25-132">Name</span><span class="sxs-lookup"><span data-stu-id="aed25-132">Name</span></span>|<span data-ttu-id="aed25-133">Description</span><span class="sxs-lookup"><span data-stu-id="aed25-133">Description</span></span>|
|---|---|
|<span data-ttu-id="aed25-134">id</span><span class="sxs-lookup"><span data-stu-id="aed25-134">id</span></span>|<span data-ttu-id="aed25-135">The line ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-135">The line ID.</span></span>|
|<span data-ttu-id="aed25-136">text</span><span class="sxs-lookup"><span data-stu-id="aed25-136">text</span></span>|<span data-ttu-id="aed25-137">The transcript itself.</span><span class="sxs-lookup"><span data-stu-id="aed25-137">The transcript itself.</span></span>|
|<span data-ttu-id="aed25-138">language</span><span class="sxs-lookup"><span data-stu-id="aed25-138">language</span></span>|<span data-ttu-id="aed25-139">The transcript language.</span><span class="sxs-lookup"><span data-stu-id="aed25-139">The transcript language.</span></span> <span data-ttu-id="aed25-140">Intended to support transcript where each line can have a different language.</span><span class="sxs-lookup"><span data-stu-id="aed25-140">Intended to support transcript where each line can have a different language.</span></span>|
|<span data-ttu-id="aed25-141">instances</span><span class="sxs-lookup"><span data-stu-id="aed25-141">instances</span></span>|<span data-ttu-id="aed25-142">A list of time ranges where this line appeared.</span><span class="sxs-lookup"><span data-stu-id="aed25-142">A list of time ranges where this line appeared.</span></span> <span data-ttu-id="aed25-143">If the instance is a transcript, it will have only 1 instance.</span><span class="sxs-lookup"><span data-stu-id="aed25-143">If the instance is a transcript, it will have only 1 instance.</span></span>|

<span data-ttu-id="aed25-144">Example:</span><span class="sxs-lookup"><span data-stu-id="aed25-144">Example:</span></span>

```json
"transcript": [
{
    "id": 0,
    "text": "Hi I'm Doug from office.",
    "language": "en-US",
    "instances": [
    {
        "start": "00:00:00.5100000",
        "end": "00:00:02.7200000"
    }
    ]
},
{
    "id": 1,
    "text": "I have a guest. It's Michelle.",
    "language": "en-US",
    "instances": [
    {
        "start": "00:00:02.7200000",
        "end": "00:00:03.9600000"
    }
    ]
}
] 
```

### <a name="ocr"></a><span data-ttu-id="aed25-145">ocr</span><span class="sxs-lookup"><span data-stu-id="aed25-145">ocr</span></span>

|<span data-ttu-id="aed25-146">Name</span><span class="sxs-lookup"><span data-stu-id="aed25-146">Name</span></span>|<span data-ttu-id="aed25-147">Description</span><span class="sxs-lookup"><span data-stu-id="aed25-147">Description</span></span>|
|---|---|
|<span data-ttu-id="aed25-148">id</span><span class="sxs-lookup"><span data-stu-id="aed25-148">id</span></span>|<span data-ttu-id="aed25-149">The OCR line ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-149">The OCR line ID.</span></span>|
|<span data-ttu-id="aed25-150">text</span><span class="sxs-lookup"><span data-stu-id="aed25-150">text</span></span>|<span data-ttu-id="aed25-151">The OCR text.</span><span class="sxs-lookup"><span data-stu-id="aed25-151">The OCR text.</span></span>|
|<span data-ttu-id="aed25-152">confidence</span><span class="sxs-lookup"><span data-stu-id="aed25-152">confidence</span></span>|<span data-ttu-id="aed25-153">The recognition confidence.</span><span class="sxs-lookup"><span data-stu-id="aed25-153">The recognition confidence.</span></span>|
|<span data-ttu-id="aed25-154">language</span><span class="sxs-lookup"><span data-stu-id="aed25-154">language</span></span>|<span data-ttu-id="aed25-155">The OCR language.</span><span class="sxs-lookup"><span data-stu-id="aed25-155">The OCR language.</span></span>|
|<span data-ttu-id="aed25-156">instances</span><span class="sxs-lookup"><span data-stu-id="aed25-156">instances</span></span>|<span data-ttu-id="aed25-157">A list of time ranges where this OCR appeared (the same OCR can appear multiple times).</span><span class="sxs-lookup"><span data-stu-id="aed25-157">A list of time ranges where this OCR appeared (the same OCR can appear multiple times).</span></span>|

```json
"ocr": [
    {
      "id": 0,
      "text": "LIVE FROM NEW YORK",
      "confidence": 0.91,
      "language": "en-US",
      "instances": [
        {
          "start": "00:00:26",
          "end": "00:00:52"
        }
      ]
    },
    {
      "id": 1,
      "text": "NOTICIAS EN VIVO",
      "confidence": 0.9,
      "language": "es-ES",
      "instances": [
        {
          "start": "00:00:26",
          "end": "00:00:28"
        },
        {
          "start": "00:00:32",
          "end": "00:00:38"
        }
      ]
    }
  ],
```

### <a name="keywords"></a><span data-ttu-id="aed25-158">keywords</span><span class="sxs-lookup"><span data-stu-id="aed25-158">keywords</span></span>

|<span data-ttu-id="aed25-159">Name</span><span class="sxs-lookup"><span data-stu-id="aed25-159">Name</span></span>|<span data-ttu-id="aed25-160">Description</span><span class="sxs-lookup"><span data-stu-id="aed25-160">Description</span></span>|
|---|---|
|<span data-ttu-id="aed25-161">id</span><span class="sxs-lookup"><span data-stu-id="aed25-161">id</span></span>|<span data-ttu-id="aed25-162">The keyword ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-162">The keyword ID.</span></span>|
|<span data-ttu-id="aed25-163">text</span><span class="sxs-lookup"><span data-stu-id="aed25-163">text</span></span>|<span data-ttu-id="aed25-164">The keyword text.</span><span class="sxs-lookup"><span data-stu-id="aed25-164">The keyword text.</span></span>|
|<span data-ttu-id="aed25-165">confidence</span><span class="sxs-lookup"><span data-stu-id="aed25-165">confidence</span></span>|<span data-ttu-id="aed25-166">The keyword's recognition confidence.</span><span class="sxs-lookup"><span data-stu-id="aed25-166">The keyword's recognition confidence.</span></span>|
|<span data-ttu-id="aed25-167">language</span><span class="sxs-lookup"><span data-stu-id="aed25-167">language</span></span>|<span data-ttu-id="aed25-168">The keyword language (when translated).</span><span class="sxs-lookup"><span data-stu-id="aed25-168">The keyword language (when translated).</span></span>|
|<span data-ttu-id="aed25-169">instances</span><span class="sxs-lookup"><span data-stu-id="aed25-169">instances</span></span>|<span data-ttu-id="aed25-170">A list of time ranges where this keyword appeared (a keyword can appear multiple times).</span><span class="sxs-lookup"><span data-stu-id="aed25-170">A list of time ranges where this keyword appeared (a keyword can appear multiple times).</span></span>|

```json
"keywords": [
{
    "id": 0,
    "text": "office",
    "confidence": 1.6666666666666667,
    "language": "en-US",
    "instances": [
    {
        "start": "00:00:00.5100000",
        "end": "00:00:02.7200000"
    },
    {
        "start": "00:00:03.9600000",
        "end": "00:00:12.2700000"
    }
    ]
},
{
    "id": 1,
    "text": "icons",
    "confidence": 1.4,
    "language": "en-US",
    "instances": [
    {
        "start": "00:00:03.9600000",
        "end": "00:00:12.2700000"
    },
    {
        "start": "00:00:13.9900000",
        "end": "00:00:15.6100000"
    }
    ]
}
] 

```

### <a name="faces"></a><span data-ttu-id="aed25-171">faces</span><span class="sxs-lookup"><span data-stu-id="aed25-171">faces</span></span>

|<span data-ttu-id="aed25-172">Name</span><span class="sxs-lookup"><span data-stu-id="aed25-172">Name</span></span>|<span data-ttu-id="aed25-173">Description</span><span class="sxs-lookup"><span data-stu-id="aed25-173">Description</span></span>|
|---|---|
|<span data-ttu-id="aed25-174">id</span><span class="sxs-lookup"><span data-stu-id="aed25-174">id</span></span>|<span data-ttu-id="aed25-175">The face ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-175">The face ID.</span></span>|
|<span data-ttu-id="aed25-176">name</span><span class="sxs-lookup"><span data-stu-id="aed25-176">name</span></span>|<span data-ttu-id="aed25-177">The face name.</span><span class="sxs-lookup"><span data-stu-id="aed25-177">The face name.</span></span> <span data-ttu-id="aed25-178">It can be ‘Unknown #0’, an identified celebrity or a customer trained person.</span><span class="sxs-lookup"><span data-stu-id="aed25-178">It can be ‘Unknown #0’, an identified celebrity or a customer trained person.</span></span>|
|<span data-ttu-id="aed25-179">confidence</span><span class="sxs-lookup"><span data-stu-id="aed25-179">confidence</span></span>|<span data-ttu-id="aed25-180">The face identification confidence.</span><span class="sxs-lookup"><span data-stu-id="aed25-180">The face identification confidence.</span></span>|
|<span data-ttu-id="aed25-181">description</span><span class="sxs-lookup"><span data-stu-id="aed25-181">description</span></span>|<span data-ttu-id="aed25-182">In case of a celebrity, its description.</span><span class="sxs-lookup"><span data-stu-id="aed25-182">In case of a celebrity, its description.</span></span> |
|<span data-ttu-id="aed25-183">thumbnalId</span><span class="sxs-lookup"><span data-stu-id="aed25-183">thumbnalId</span></span>|<span data-ttu-id="aed25-184">The id of the thumbnail of that face.</span><span class="sxs-lookup"><span data-stu-id="aed25-184">The id of the thumbnail of that face.</span></span>|
|<span data-ttu-id="aed25-185">knownPersonId</span><span class="sxs-lookup"><span data-stu-id="aed25-185">knownPersonId</span></span>|<span data-ttu-id="aed25-186">In case of a known person, its internal ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-186">In case of a known person, its internal ID.</span></span>|
|<span data-ttu-id="aed25-187">referenceId</span><span class="sxs-lookup"><span data-stu-id="aed25-187">referenceId</span></span>|<span data-ttu-id="aed25-188">In case of a Bing celebrity, its Bing ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-188">In case of a Bing celebrity, its Bing ID.</span></span>|
|<span data-ttu-id="aed25-189">referenceType</span><span class="sxs-lookup"><span data-stu-id="aed25-189">referenceType</span></span>|<span data-ttu-id="aed25-190">Currently just Bing.</span><span class="sxs-lookup"><span data-stu-id="aed25-190">Currently just Bing.</span></span>|
|<span data-ttu-id="aed25-191">title</span><span class="sxs-lookup"><span data-stu-id="aed25-191">title</span></span>|<span data-ttu-id="aed25-192">In case of a celebrity, its title (for example "Microsoft's CEO").</span><span class="sxs-lookup"><span data-stu-id="aed25-192">In case of a celebrity, its title (for example "Microsoft's CEO").</span></span>|
|<span data-ttu-id="aed25-193">imageUrl</span><span class="sxs-lookup"><span data-stu-id="aed25-193">imageUrl</span></span>|<span data-ttu-id="aed25-194">In case of a celebrity, its image url.</span><span class="sxs-lookup"><span data-stu-id="aed25-194">In case of a celebrity, its image url.</span></span>|
|<span data-ttu-id="aed25-195">instances</span><span class="sxs-lookup"><span data-stu-id="aed25-195">instances</span></span>|<span data-ttu-id="aed25-196">These are instances of where the face appeared in the given time range.</span><span class="sxs-lookup"><span data-stu-id="aed25-196">These are instances of where the face appeared in the given time range.</span></span> <span data-ttu-id="aed25-197">Each instance also has a thumbnailsId.</span><span class="sxs-lookup"><span data-stu-id="aed25-197">Each instance also has a thumbnailsId.</span></span> |

```json
"faces": [{
    "id": 2002,
    "name": "Xam 007",
    "confidence": 0.93844,
    "description": null,
    "thumbnailId": "00000000-aee4-4be2-a4d5-d01817c07955",
    "knownPersonId": "8340004b-5cf5-4611-9cc4-3b13cca10634",
    "referenceId": null,
    "title": null,
    "imageUrl": null,
    "instances": [{
        "thumbnailsIds": ["00000000-9f68-4bb2-ab27-3b4d9f2d998e",
        "cef03f24-b0c7-4145-94d4-a84f81bb588c"],
        "adjustedStart": "00:00:07.2400000",
        "adjustedEnd": "00:00:45.6780000",
        "start": "00:00:07.2400000",
        "end": "00:00:45.6780000"
    },
    {
        "thumbnailsIds": ["00000000-51e5-4260-91a5-890fa05c68b0"],
        "adjustedStart": "00:10:23.9570000",
        "adjustedEnd": "00:10:39.2390000",
        "start": "00:10:23.9570000",
        "end": "00:10:39.2390000"
    }]
}]
```

### <a name="labels"></a><span data-ttu-id="aed25-198">labels</span><span class="sxs-lookup"><span data-stu-id="aed25-198">labels</span></span>

|<span data-ttu-id="aed25-199">Name</span><span class="sxs-lookup"><span data-stu-id="aed25-199">Name</span></span>|<span data-ttu-id="aed25-200">Description</span><span class="sxs-lookup"><span data-stu-id="aed25-200">Description</span></span>|
|---|---|
|<span data-ttu-id="aed25-201">id</span><span class="sxs-lookup"><span data-stu-id="aed25-201">id</span></span>|<span data-ttu-id="aed25-202">The label ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-202">The label ID.</span></span>|
|<span data-ttu-id="aed25-203">name</span><span class="sxs-lookup"><span data-stu-id="aed25-203">name</span></span>|<span data-ttu-id="aed25-204">The label name (for example, 'Computer', 'TV').</span><span class="sxs-lookup"><span data-stu-id="aed25-204">The label name (for example, 'Computer', 'TV').</span></span>|
|<span data-ttu-id="aed25-205">language</span><span class="sxs-lookup"><span data-stu-id="aed25-205">language</span></span>|<span data-ttu-id="aed25-206">The label name language (when translated).</span><span class="sxs-lookup"><span data-stu-id="aed25-206">The label name language (when translated).</span></span> <span data-ttu-id="aed25-207">BCP-47</span><span class="sxs-lookup"><span data-stu-id="aed25-207">BCP-47</span></span>|
|<span data-ttu-id="aed25-208">instances</span><span class="sxs-lookup"><span data-stu-id="aed25-208">instances</span></span>|<span data-ttu-id="aed25-209">A list of time ranges where this label appeared (a label can appear multiple times).</span><span class="sxs-lookup"><span data-stu-id="aed25-209">A list of time ranges where this label appeared (a label can appear multiple times).</span></span> <span data-ttu-id="aed25-210">Each instance has a confidence field.</span><span class="sxs-lookup"><span data-stu-id="aed25-210">Each instance has a confidence field.</span></span> |


```json
"labels": [
    {
      "id": 0,
      "name": "person",
      "language": "en-US",
      "instances": [
        {
          "confidence": 1.0,
          "start": "00: 00: 00.0000000",
          "end": "00: 00: 25.6000000"
        },
        {
          "confidence": 1.0,
          "start": "00: 01: 33.8670000",
          "end": "00: 01: 39.2000000"
        }
      ]
    },
    {
      "name": "indoor",
      "language": "en-US",
      "id": 1,
      "instances": [
        {
          "confidence": 1.0,
          "start": "00: 00: 06.4000000",
          "end": "00: 00: 07.4670000"
        },
        {
          "confidence": 1.0,
          "start": "00: 00: 09.6000000",
          "end": "00: 00: 10.6670000"
        },
        {
          "confidence": 1.0,
          "start": "00: 00: 11.7330000",
          "end": "00: 00: 20.2670000"
        },
        {
          "confidence": 1.0,
          "start": "00: 00: 21.3330000",
          "end": "00: 00: 25.6000000"
        }
      ]
    }
  ] 
```

### <a name="shots"></a><span data-ttu-id="aed25-211">shots</span><span class="sxs-lookup"><span data-stu-id="aed25-211">shots</span></span>

|<span data-ttu-id="aed25-212">Name</span><span class="sxs-lookup"><span data-stu-id="aed25-212">Name</span></span>|<span data-ttu-id="aed25-213">Description</span><span class="sxs-lookup"><span data-stu-id="aed25-213">Description</span></span>|
|---|---|
|<span data-ttu-id="aed25-214">id</span><span class="sxs-lookup"><span data-stu-id="aed25-214">id</span></span>|<span data-ttu-id="aed25-215">The shot ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-215">The shot ID.</span></span>|
|<span data-ttu-id="aed25-216">keyFrames</span><span class="sxs-lookup"><span data-stu-id="aed25-216">keyFrames</span></span>|<span data-ttu-id="aed25-217">A list of key frames within the shot (each has an ID and a list of instances time ranges).</span><span class="sxs-lookup"><span data-stu-id="aed25-217">A list of key frames within the shot (each has an ID and a list of instances time ranges).</span></span>|
|<span data-ttu-id="aed25-218">instances</span><span class="sxs-lookup"><span data-stu-id="aed25-218">instances</span></span>|<span data-ttu-id="aed25-219">A list of time ranges of this shot (shots have only 1 instance).</span><span class="sxs-lookup"><span data-stu-id="aed25-219">A list of time ranges of this shot (shots have only 1 instance).</span></span>|

```json
"Shots": [
    {
      "id": 0,
      "keyFrames": [
        {
          "id": 0,
          "instances": [
            {
              "start": "00: 00: 00.1670000",
              "end": "00: 00: 00.2000000"
            }
          ]
        }
      ],
      "instances": [
        {
          "start": "00: 00: 00.2000000",
          "end": "00: 00: 05.0330000"
        }
      ]
    },
    {
      "id": 1,
      "keyFrames": [
        {
          "id": 1,
          "instances": [
            {
              "start": "00: 00: 05.2670000",
              "end": "00: 00: 05.3000000"
            }
          ]
        }
      ],
      "instances": [
        {
          "start": "00: 00: 05.2670000",
          "end": "00: 00: 10.3000000"
        }
      ]
    }
  ]
```


### <a name="sentiments"></a><span data-ttu-id="aed25-220">sentiments</span><span class="sxs-lookup"><span data-stu-id="aed25-220">sentiments</span></span>

<span data-ttu-id="aed25-221">Sentiments are aggregated by their sentimentType field (Positive/Neutral/Negative).</span><span class="sxs-lookup"><span data-stu-id="aed25-221">Sentiments are aggregated by their sentimentType field (Positive/Neutral/Negative).</span></span> <span data-ttu-id="aed25-222">For example, 0-0.1, 0.1-0.2.</span><span class="sxs-lookup"><span data-stu-id="aed25-222">For example, 0-0.1, 0.1-0.2.</span></span>

|<span data-ttu-id="aed25-223">Name</span><span class="sxs-lookup"><span data-stu-id="aed25-223">Name</span></span>|<span data-ttu-id="aed25-224">Description</span><span class="sxs-lookup"><span data-stu-id="aed25-224">Description</span></span>|
|---|---|
|<span data-ttu-id="aed25-225">id</span><span class="sxs-lookup"><span data-stu-id="aed25-225">id</span></span>|<span data-ttu-id="aed25-226">The sentiment ID.</span><span class="sxs-lookup"><span data-stu-id="aed25-226">The sentiment ID.</span></span>|
|<span data-ttu-id="aed25-227">averageScore</span><span class="sxs-lookup"><span data-stu-id="aed25-227">averageScore</span></span> |<span data-ttu-id="aed25-228">The average of all scores of all instances of that sentiment type - Positive/Neutral/Negative</span><span class="sxs-lookup"><span data-stu-id="aed25-228">The average of all scores of all instances of that sentiment type - Positive/Neutral/Negative</span></span>|
|<span data-ttu-id="aed25-229">instances</span><span class="sxs-lookup"><span data-stu-id="aed25-229">instances</span></span>|<span data-ttu-id="aed25-230">A list of time ranges where this sentiment appeared.</span><span class="sxs-lookup"><span data-stu-id="aed25-230">A list of time ranges where this sentiment appeared.</span></span>|

```json
"sentiments": [
{
    "id": 0,
    "averageScore": 0.87,
    "instances": [
    {
        "start": "00:00:23",
        "end": "00:00:41"
    }
    ]
}, {
    "id": 1,
    "averageScore": 0.11,
    "instances": [
    {
        "start": "00:00:13",
        "end": "00:00:21"
    }
    ]
}
]
```

## <a name="next-steps"></a><span data-ttu-id="aed25-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="aed25-231">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aed25-232">Tutorial: Analyze videos with Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="aed25-232">Tutorial: Analyze videos with Azure Media Services</span></span>](analyze-videos-tutorial-with-api.md)
