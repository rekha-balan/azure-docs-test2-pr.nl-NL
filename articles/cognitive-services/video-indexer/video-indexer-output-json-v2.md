---
title: Examine the Azure Video Indexer output produced by v2 API | Microsoft Docs
description: This topic examines the Video Indexer output produced by v2 API.
services: cognitive services
documentationcenter: ''
author: juliako
manager: cfowler
ms.service: cognitive-services
ms.topic: article
ms.date: 07/25/2018
ms.author: juliako
ms.openlocfilehash: 43cc02417fad8a2fa46bd309235951393cd55b8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965869"
---
# <a name="examine-the-video-indexer-output-produced-by-v2-api"></a><span data-ttu-id="fb6c9-103">Examine the Video Indexer output produced by v2 API</span><span class="sxs-lookup"><span data-stu-id="fb6c9-103">Examine the Video Indexer output produced by v2 API</span></span>

> [!Note]
> <span data-ttu-id="fb6c9-104">The Video Indexer V1 API was deprecated on August 1st, 2018.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-104">The Video Indexer V1 API was deprecated on August 1st, 2018.</span></span> <span data-ttu-id="fb6c9-105">You should now use the Video Indexer v2 API.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-105">You should now use the Video Indexer v2 API.</span></span> <br/><span data-ttu-id="fb6c9-106">To develop with Video Indexer v2 APIs, please refer to the instructions found [here](https://api-portal.videoindexer.ai/).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-106">To develop with Video Indexer v2 APIs, please refer to the instructions found [here](https://api-portal.videoindexer.ai/).</span></span> 

<span data-ttu-id="fb6c9-107">When you call the **Get Video Index** API and the response status is OK, you get a detailed JSON output as the response content.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-107">When you call the **Get Video Index** API and the response status is OK, you get a detailed JSON output as the response content.</span></span> <span data-ttu-id="fb6c9-108">The JSON content contains details of the specified video insights.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-108">The JSON content contains details of the specified video insights.</span></span> <span data-ttu-id="fb6c9-109">The insights include dimensions like: transcripts, ocrs, faces, topics, blocks, etc. The dimensions have instances of time ranges that show when each dimension appeared in the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-109">The insights include dimensions like: transcripts, ocrs, faces, topics, blocks, etc. The dimensions have instances of time ranges that show when each dimension appeared in the video.</span></span>  

<span data-ttu-id="fb6c9-110">You can also visually examine the video's summarized insights by pressing the **Play** button on the video in the Video Indexer portal.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-110">You can also visually examine the video's summarized insights by pressing the **Play** button on the video in the Video Indexer portal.</span></span> <span data-ttu-id="fb6c9-111">For more information, see [View and edit video insights](video-indexer-view-edit.md).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-111">For more information, see [View and edit video insights](video-indexer-view-edit.md).</span></span>

![Insights](./media/video-indexer-output-json/video-indexer-summarized-insights.png)

<span data-ttu-id="fb6c9-113">This article examines the JSON content returned by the  **Get Video Index** API.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-113">This article examines the JSON content returned by the  **Get Video Index** API.</span></span> 

> [!NOTE]
> <span data-ttu-id="fb6c9-114">Expiration of all the access tokens in Video Indexer is one hour.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-114">Expiration of all the access tokens in Video Indexer is one hour.</span></span>


## <a name="root-elements"></a><span data-ttu-id="fb6c9-115">Root elements</span><span class="sxs-lookup"><span data-stu-id="fb6c9-115">Root elements</span></span>

|<span data-ttu-id="fb6c9-116">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-116">Name</span></span>|<span data-ttu-id="fb6c9-117">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-117">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-118">accountId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-118">accountId</span></span>|<span data-ttu-id="fb6c9-119">The playlist's VI account ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-119">The playlist's VI account ID.</span></span>|
|<span data-ttu-id="fb6c9-120">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-120">id</span></span>|<span data-ttu-id="fb6c9-121">The playlist's ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-121">The playlist's ID.</span></span>|
|<span data-ttu-id="fb6c9-122">name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-122">name</span></span>|<span data-ttu-id="fb6c9-123">The playlist's name.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-123">The playlist's name.</span></span>|
|<span data-ttu-id="fb6c9-124">description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-124">description</span></span>|<span data-ttu-id="fb6c9-125">The playlist's description.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-125">The playlist's description.</span></span>|
|<span data-ttu-id="fb6c9-126">userName</span><span class="sxs-lookup"><span data-stu-id="fb6c9-126">userName</span></span>|<span data-ttu-id="fb6c9-127">The name of the user who created the playlist.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-127">The name of the user who created the playlist.</span></span>|
|<span data-ttu-id="fb6c9-128">created</span><span class="sxs-lookup"><span data-stu-id="fb6c9-128">created</span></span>|<span data-ttu-id="fb6c9-129">The playlist's creation time.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-129">The playlist's creation time.</span></span>|
|<span data-ttu-id="fb6c9-130">privacyMode</span><span class="sxs-lookup"><span data-stu-id="fb6c9-130">privacyMode</span></span>|<span data-ttu-id="fb6c9-131">The playlist’s privacy mode (Private/Public).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-131">The playlist’s privacy mode (Private/Public).</span></span>|
|<span data-ttu-id="fb6c9-132">state</span><span class="sxs-lookup"><span data-stu-id="fb6c9-132">state</span></span>|<span data-ttu-id="fb6c9-133">The playlist’s (uploaded, processing, processed, failed, quarantined).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-133">The playlist’s (uploaded, processing, processed, failed, quarantined).</span></span>|
|<span data-ttu-id="fb6c9-134">isOwned</span><span class="sxs-lookup"><span data-stu-id="fb6c9-134">isOwned</span></span>|<span data-ttu-id="fb6c9-135">Indicates whether the playlist was created by the current user.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-135">Indicates whether the playlist was created by the current user.</span></span>|
|<span data-ttu-id="fb6c9-136">isEditable</span><span class="sxs-lookup"><span data-stu-id="fb6c9-136">isEditable</span></span>|<span data-ttu-id="fb6c9-137">Indicates whether the current user is authorized to edit the playlist.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-137">Indicates whether the current user is authorized to edit the playlist.</span></span>|
|<span data-ttu-id="fb6c9-138">isBase</span><span class="sxs-lookup"><span data-stu-id="fb6c9-138">isBase</span></span>|<span data-ttu-id="fb6c9-139">Indicates whether the playlist is a base playlist (a video) or a playlist made of other videos (derived).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-139">Indicates whether the playlist is a base playlist (a video) or a playlist made of other videos (derived).</span></span>|
|<span data-ttu-id="fb6c9-140">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="fb6c9-140">durationInSeconds</span></span>|<span data-ttu-id="fb6c9-141">The total duration of the playlist.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-141">The total duration of the playlist.</span></span>|
|<span data-ttu-id="fb6c9-142">summarizedInsights</span><span class="sxs-lookup"><span data-stu-id="fb6c9-142">summarizedInsights</span></span>|<span data-ttu-id="fb6c9-143">Contains one [summarizedInsights](#summarizedinsights).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-143">Contains one [summarizedInsights](#summarizedinsights).</span></span>
|<span data-ttu-id="fb6c9-144">videos</span><span class="sxs-lookup"><span data-stu-id="fb6c9-144">videos</span></span>|<span data-ttu-id="fb6c9-145">A list of [videos](#videos) constructing the playlist.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-145">A list of [videos](#videos) constructing the playlist.</span></span><br/><span data-ttu-id="fb6c9-146">If this playlist of constructed of time ranges of other videos (derived), the videos in this list will contain only data from the included time ranges.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-146">If this playlist of constructed of time ranges of other videos (derived), the videos in this list will contain only data from the included time ranges.</span></span>|

```json
{
  "accountId": "bca61527-1221-bca6-1527-a90000002000",
  "id": "abc3454321",
  "name": "My first video",
  "description": "I am trying VI",
  "userName": "Some name",
  "created": "2018/2/2 18:00:00.000",
  "privacyMode": "Private",
  "state": "Processed",
  "isOwned": true,
  "isEditable": false,
  "isBase": false,
  "durationInSeconds": 120, 
  "summarizedInsights" : { . . . }
  "videos": [{ . . . }]
}
```

## <a name="summarizedinsights"></a><span data-ttu-id="fb6c9-147">summarizedInsights</span><span class="sxs-lookup"><span data-stu-id="fb6c9-147">summarizedInsights</span></span>

<span data-ttu-id="fb6c9-148">This section shows the summary of the insights.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-148">This section shows the summary of the insights.</span></span>

|<span data-ttu-id="fb6c9-149">Attribute</span><span class="sxs-lookup"><span data-stu-id="fb6c9-149">Attribute</span></span> | <span data-ttu-id="fb6c9-150">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-150">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-151">name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-151">name</span></span>|<span data-ttu-id="fb6c9-152">The name of the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-152">The name of the video.</span></span> <span data-ttu-id="fb6c9-153">For example, Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-153">For example, Azure Monitor.</span></span>|
|<span data-ttu-id="fb6c9-154">shortId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-154">shortId</span></span>|<span data-ttu-id="fb6c9-155">The ID of the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-155">The ID of the video.</span></span> <span data-ttu-id="fb6c9-156">For example, 63c6d532ff.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-156">For example, 63c6d532ff.</span></span>|
|<span data-ttu-id="fb6c9-157">privacyMode</span><span class="sxs-lookup"><span data-stu-id="fb6c9-157">privacyMode</span></span>|<span data-ttu-id="fb6c9-158">Your breakdown can have one of the following modes: **Private**, **Public**.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-158">Your breakdown can have one of the following modes: **Private**, **Public**.</span></span> <span data-ttu-id="fb6c9-159">**Public** - the video is visible to everyone in your account and anyone that has a link to the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-159">**Public** - the video is visible to everyone in your account and anyone that has a link to the video.</span></span> <span data-ttu-id="fb6c9-160">**Private** - the video is visible to everyone in your account.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-160">**Private** - the video is visible to everyone in your account.</span></span>|
|<span data-ttu-id="fb6c9-161">duration</span><span class="sxs-lookup"><span data-stu-id="fb6c9-161">duration</span></span>|<span data-ttu-id="fb6c9-162">Contains one duration that describes the time an insight occurred.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-162">Contains one duration that describes the time an insight occurred.</span></span> <span data-ttu-id="fb6c9-163">Duration is in seconds.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-163">Duration is in seconds.</span></span>|
|<span data-ttu-id="fb6c9-164">thumbnailVideoId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-164">thumbnailVideoId</span></span>|<span data-ttu-id="fb6c9-165">The ID of the video from which the thumbnail was taken.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-165">The ID of the video from which the thumbnail was taken.</span></span>
|<span data-ttu-id="fb6c9-166">thumbnailId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-166">thumbnailId</span></span>|<span data-ttu-id="fb6c9-167">The video's thumbnail ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-167">The video's thumbnail ID.</span></span> <span data-ttu-id="fb6c9-168">To get the actual thumbnail call Get-Thumbnail (https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-thumbnail) and pass it thumbnailVideoId and  thumbnailId.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-168">To get the actual thumbnail call Get-Thumbnail (https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-thumbnail) and pass it thumbnailVideoId and  thumbnailId.</span></span>|
|<span data-ttu-id="fb6c9-169">faces</span><span class="sxs-lookup"><span data-stu-id="fb6c9-169">faces</span></span>|<span data-ttu-id="fb6c9-170">May contain zero or more faces.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-170">May contain zero or more faces.</span></span> <span data-ttu-id="fb6c9-171">For more detailed information, see [faces](#faces).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-171">For more detailed information, see [faces](#faces).</span></span>|
|<span data-ttu-id="fb6c9-172">keywords</span><span class="sxs-lookup"><span data-stu-id="fb6c9-172">keywords</span></span>|<span data-ttu-id="fb6c9-173">May contain zero or more keywords.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-173">May contain zero or more keywords.</span></span> <span data-ttu-id="fb6c9-174">For more detailed information, see [keywords](#keywords).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-174">For more detailed information, see [keywords](#keywords).</span></span>|
|<span data-ttu-id="fb6c9-175">sentiments</span><span class="sxs-lookup"><span data-stu-id="fb6c9-175">sentiments</span></span>|<span data-ttu-id="fb6c9-176">May contain zero or more sentiments.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-176">May contain zero or more sentiments.</span></span> <span data-ttu-id="fb6c9-177">For more detailed information, see [sentiments](#sentiments).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-177">For more detailed information, see [sentiments](#sentiments).</span></span>|
|<span data-ttu-id="fb6c9-178">audioEffects</span><span class="sxs-lookup"><span data-stu-id="fb6c9-178">audioEffects</span></span>| <span data-ttu-id="fb6c9-179">May contain zero or more audioEffects.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-179">May contain zero or more audioEffects.</span></span> <span data-ttu-id="fb6c9-180">For more detailed information, see [audioEffects](#audioeffects).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-180">For more detailed information, see [audioEffects](#audioeffects).</span></span>|
|<span data-ttu-id="fb6c9-181">labels</span><span class="sxs-lookup"><span data-stu-id="fb6c9-181">labels</span></span>| <span data-ttu-id="fb6c9-182">May contain zero or more labels.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-182">May contain zero or more labels.</span></span> <span data-ttu-id="fb6c9-183">For detailed more information, see [labels](#labels).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-183">For detailed more information, see [labels](#labels).</span></span>|
|<span data-ttu-id="fb6c9-184">brands</span><span class="sxs-lookup"><span data-stu-id="fb6c9-184">brands</span></span>| <span data-ttu-id="fb6c9-185">May contain zero or more brands.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-185">May contain zero or more brands.</span></span> <span data-ttu-id="fb6c9-186">For more detailed information, see [brands](#brands).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-186">For more detailed information, see [brands](#brands).</span></span>|
|<span data-ttu-id="fb6c9-187">statistics</span><span class="sxs-lookup"><span data-stu-id="fb6c9-187">statistics</span></span> | <span data-ttu-id="fb6c9-188">For more detailed information, see [statistics](#statistics).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-188">For more detailed information, see [statistics](#statistics).</span></span>|

## <a name="videos"></a><span data-ttu-id="fb6c9-189">videos</span><span class="sxs-lookup"><span data-stu-id="fb6c9-189">videos</span></span>

|<span data-ttu-id="fb6c9-190">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-190">Name</span></span>|<span data-ttu-id="fb6c9-191">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-191">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-192">accountId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-192">accountId</span></span>|<span data-ttu-id="fb6c9-193">The video's VI account ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-193">The video's VI account ID.</span></span>|
|<span data-ttu-id="fb6c9-194">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-194">id</span></span>|<span data-ttu-id="fb6c9-195">The video's ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-195">The video's ID.</span></span>|
|<span data-ttu-id="fb6c9-196">name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-196">name</span></span>|<span data-ttu-id="fb6c9-197">The video's name.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-197">The video's name.</span></span>
|<span data-ttu-id="fb6c9-198">state</span><span class="sxs-lookup"><span data-stu-id="fb6c9-198">state</span></span>|<span data-ttu-id="fb6c9-199">The video’s state (uploaded, processing, processed, failed, quarantined).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-199">The video’s state (uploaded, processing, processed, failed, quarantined).</span></span>|
|<span data-ttu-id="fb6c9-200">processingProgress</span><span class="sxs-lookup"><span data-stu-id="fb6c9-200">processingProgress</span></span>|<span data-ttu-id="fb6c9-201">The processing progress during processing (for example, 20%).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-201">The processing progress during processing (for example, 20%).</span></span>|
|<span data-ttu-id="fb6c9-202">failureCode</span><span class="sxs-lookup"><span data-stu-id="fb6c9-202">failureCode</span></span>|<span data-ttu-id="fb6c9-203">The failure code if failed to process (for example, 'UnsupportedFileType').</span><span class="sxs-lookup"><span data-stu-id="fb6c9-203">The failure code if failed to process (for example, 'UnsupportedFileType').</span></span>|
|<span data-ttu-id="fb6c9-204">failureMessage</span><span class="sxs-lookup"><span data-stu-id="fb6c9-204">failureMessage</span></span>|<span data-ttu-id="fb6c9-205">The failure message if failed to process.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-205">The failure message if failed to process.</span></span>|
|<span data-ttu-id="fb6c9-206">externalId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-206">externalId</span></span>|<span data-ttu-id="fb6c9-207">The video's external ID (if specified by the user).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-207">The video's external ID (if specified by the user).</span></span>|
|<span data-ttu-id="fb6c9-208">externalUrl</span><span class="sxs-lookup"><span data-stu-id="fb6c9-208">externalUrl</span></span>|<span data-ttu-id="fb6c9-209">The video's external url (if specified by the user).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-209">The video's external url (if specified by the user).</span></span>|
|<span data-ttu-id="fb6c9-210">metadata</span><span class="sxs-lookup"><span data-stu-id="fb6c9-210">metadata</span></span>|<span data-ttu-id="fb6c9-211">The video's external metadata (if specified by the user).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-211">The video's external metadata (if specified by the user).</span></span>|
|<span data-ttu-id="fb6c9-212">isAdult</span><span class="sxs-lookup"><span data-stu-id="fb6c9-212">isAdult</span></span>|<span data-ttu-id="fb6c9-213">Indicates whether the video was manually reviewed and identified as an adult video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-213">Indicates whether the video was manually reviewed and identified as an adult video.</span></span>|
|<span data-ttu-id="fb6c9-214">insights</span><span class="sxs-lookup"><span data-stu-id="fb6c9-214">insights</span></span>|<span data-ttu-id="fb6c9-215">The insights object.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-215">The insights object.</span></span> <span data-ttu-id="fb6c9-216">For more information, see [insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-216">For more information, see [insights](#insights).</span></span>|
|<span data-ttu-id="fb6c9-217">thumbnailId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-217">thumbnailId</span></span>|<span data-ttu-id="fb6c9-218">The video's thumbnail ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-218">The video's thumbnail ID.</span></span> <span data-ttu-id="fb6c9-219">To get the actual thumbnail call Get-Thumbnail (https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-thumbnail) and pass it the video ID and thumbnailId.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-219">To get the actual thumbnail call Get-Thumbnail (https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-thumbnail) and pass it the video ID and thumbnailId.</span></span>|
|<span data-ttu-id="fb6c9-220">publishedUrl</span><span class="sxs-lookup"><span data-stu-id="fb6c9-220">publishedUrl</span></span>|<span data-ttu-id="fb6c9-221">A url to stream the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-221">A url to stream the video.</span></span>|
|<span data-ttu-id="fb6c9-222">publishedUrlProxy</span><span class="sxs-lookup"><span data-stu-id="fb6c9-222">publishedUrlProxy</span></span>|<span data-ttu-id="fb6c9-223">A url to stream the video from (for Apple devices).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-223">A url to stream the video from (for Apple devices).</span></span>|
|<span data-ttu-id="fb6c9-224">viewToken</span><span class="sxs-lookup"><span data-stu-id="fb6c9-224">viewToken</span></span>|<span data-ttu-id="fb6c9-225">A short lived view token for streaming the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-225">A short lived view token for streaming the video.</span></span>|
|<span data-ttu-id="fb6c9-226">sourceLanguage</span><span class="sxs-lookup"><span data-stu-id="fb6c9-226">sourceLanguage</span></span>|<span data-ttu-id="fb6c9-227">The video's source language.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-227">The video's source language.</span></span>|
|<span data-ttu-id="fb6c9-228">language</span><span class="sxs-lookup"><span data-stu-id="fb6c9-228">language</span></span>|<span data-ttu-id="fb6c9-229">The video's actual language (translation).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-229">The video's actual language (translation).</span></span>|
|<span data-ttu-id="fb6c9-230">indexingPreset</span><span class="sxs-lookup"><span data-stu-id="fb6c9-230">indexingPreset</span></span>|<span data-ttu-id="fb6c9-231">The preset used to index the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-231">The preset used to index the video.</span></span>|
|<span data-ttu-id="fb6c9-232">streamingPreset</span><span class="sxs-lookup"><span data-stu-id="fb6c9-232">streamingPreset</span></span>|<span data-ttu-id="fb6c9-233">The preset used to publish the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-233">The preset used to publish the video.</span></span>|
|<span data-ttu-id="fb6c9-234">linguisticModelId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-234">linguisticModelId</span></span>|<span data-ttu-id="fb6c9-235">The CRIS model used to transcribe the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-235">The CRIS model used to transcribe the video.</span></span>|
|<span data-ttu-id="fb6c9-236">statistics</span><span class="sxs-lookup"><span data-stu-id="fb6c9-236">statistics</span></span> | <span data-ttu-id="fb6c9-237">For more information, see [statistics](#statistics).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-237">For more information, see [statistics](#statistics).</span></span>|

```json
{
    "videos": [{
        "accountId": "2cbbed36-1972-4506-9bc7-55367912df2d",
        "id": "142a356aa6",
        "state": "Processed",
        "privacyMode": "Private",
        "processingProgress": "100%",
        "failureCode": "General",
        "failureMessage": "",
        "externalId": null,
        "externalUrl": null,
        "metadata": null,
        "insights": {. . . },
        "thumbnailId": "89d7192c-1dab-4377-9872-473eac723845",
        "publishedUrl": "https://videvmediaservices.streaming.mediaservices.windows.net:443/d88a652d-334b-4a66-a294-3826402100cd/Xamarine.ism/manifest",
        "publishedProxyUrl": null,
        "viewToken": "Bearer=<token>",
        "sourceLanguage": "En-US",
        "language": "En-US",
        "indexingPreset": "Default",
        "linguisticModelId": "00000000-0000-0000-0000-000000000000"
    }],
}
```
### <a name="insights"></a><span data-ttu-id="fb6c9-238">insights</span><span class="sxs-lookup"><span data-stu-id="fb6c9-238">insights</span></span>

<span data-ttu-id="fb6c9-239">The insights are a set of dimensions (for example, transcript lines, faces, brands, etc.), where each dimension is a list of unique elements (for example, face1, face2, face3), and each element has its own metadata and a list of its instances (which are time ranges with additional optional metadata).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-239">The insights are a set of dimensions (for example, transcript lines, faces, brands, etc.), where each dimension is a list of unique elements (for example, face1, face2, face3), and each element has its own metadata and a list of its instances (which are time ranges with additional optional metadata).</span></span>

<span data-ttu-id="fb6c9-240">A face might  have an ID, a name, a thumbnail, other metadata, and a list of its temporal instances (for example: 00:00:05 – 00:00:10, 00:01:00 - 00:02:30 and 00:41:21 – 00:41:49.) Each temporal instance can have additional metadata.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-240">A face might  have an ID, a name, a thumbnail, other metadata, and a list of its temporal instances (for example: 00:00:05 – 00:00:10, 00:01:00 - 00:02:30 and 00:41:21 – 00:41:49.) Each temporal instance can have additional metadata.</span></span> <span data-ttu-id="fb6c9-241">For example, the face’s rectangle coordinates (20,230,60,60).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-241">For example, the face’s rectangle coordinates (20,230,60,60).</span></span>

|<span data-ttu-id="fb6c9-242">Version</span><span class="sxs-lookup"><span data-stu-id="fb6c9-242">Version</span></span>|<span data-ttu-id="fb6c9-243">The code version</span><span class="sxs-lookup"><span data-stu-id="fb6c9-243">The code version</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-244">sourceLanguage</span><span class="sxs-lookup"><span data-stu-id="fb6c9-244">sourceLanguage</span></span>|<span data-ttu-id="fb6c9-245">The video's source language (assuming one master language).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-245">The video's source language (assuming one master language).</span></span> <span data-ttu-id="fb6c9-246">In the form of a [BCP-47](https://tools.ietf.org/html/bcp47) string.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-246">In the form of a [BCP-47](https://tools.ietf.org/html/bcp47) string.</span></span>|
|<span data-ttu-id="fb6c9-247">language</span><span class="sxs-lookup"><span data-stu-id="fb6c9-247">language</span></span>|<span data-ttu-id="fb6c9-248">The insights language (translated from the source language).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-248">The insights language (translated from the source language).</span></span> <span data-ttu-id="fb6c9-249">In the form of a [BCP-47](https://tools.ietf.org/html/bcp47) string.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-249">In the form of a [BCP-47](https://tools.ietf.org/html/bcp47) string.</span></span>|
|<span data-ttu-id="fb6c9-250">transcript</span><span class="sxs-lookup"><span data-stu-id="fb6c9-250">transcript</span></span>|<span data-ttu-id="fb6c9-251">The [transcript](#transcript) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-251">The [transcript](#transcript) dimension.</span></span>|
|<span data-ttu-id="fb6c9-252">ocr</span><span class="sxs-lookup"><span data-stu-id="fb6c9-252">ocr</span></span>|<span data-ttu-id="fb6c9-253">The [ocr](#ocr) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-253">The [ocr](#ocr) dimension.</span></span>|
|<span data-ttu-id="fb6c9-254">keywords</span><span class="sxs-lookup"><span data-stu-id="fb6c9-254">keywords</span></span>|<span data-ttu-id="fb6c9-255">The [keywords](#keywords) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-255">The [keywords](#keywords) dimension.</span></span>|
|<span data-ttu-id="fb6c9-256">blocks</span><span class="sxs-lookup"><span data-stu-id="fb6c9-256">blocks</span></span>|<span data-ttu-id="fb6c9-257">May contain one or more [blocks](#blocks)</span><span class="sxs-lookup"><span data-stu-id="fb6c9-257">May contain one or more [blocks](#blocks)</span></span>|
|<span data-ttu-id="fb6c9-258">faces</span><span class="sxs-lookup"><span data-stu-id="fb6c9-258">faces</span></span>|<span data-ttu-id="fb6c9-259">The [faces](#faces) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-259">The [faces](#faces) dimension.</span></span>|
|<span data-ttu-id="fb6c9-260">labels</span><span class="sxs-lookup"><span data-stu-id="fb6c9-260">labels</span></span>|<span data-ttu-id="fb6c9-261">The [labels](#labels) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-261">The [labels](#labels) dimension.</span></span>|
|<span data-ttu-id="fb6c9-262">shots</span><span class="sxs-lookup"><span data-stu-id="fb6c9-262">shots</span></span>|<span data-ttu-id="fb6c9-263">The [shots](#shots) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-263">The [shots](#shots) dimension.</span></span>|
|<span data-ttu-id="fb6c9-264">brands</span><span class="sxs-lookup"><span data-stu-id="fb6c9-264">brands</span></span>|<span data-ttu-id="fb6c9-265">The [brands](#brands) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-265">The [brands](#brands) dimension.</span></span>|
|<span data-ttu-id="fb6c9-266">audioEffects</span><span class="sxs-lookup"><span data-stu-id="fb6c9-266">audioEffects</span></span>|<span data-ttu-id="fb6c9-267">The [audioEffects](#audioEffects) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-267">The [audioEffects](#audioEffects) dimension.</span></span>|
|<span data-ttu-id="fb6c9-268">sentiments</span><span class="sxs-lookup"><span data-stu-id="fb6c9-268">sentiments</span></span>|<span data-ttu-id="fb6c9-269">The [sentiments](#sentiments) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-269">The [sentiments](#sentiments) dimension.</span></span>|
|<span data-ttu-id="fb6c9-270">visualContentModeration</span><span class="sxs-lookup"><span data-stu-id="fb6c9-270">visualContentModeration</span></span>|<span data-ttu-id="fb6c9-271">The [visualContentModeration](#visualcontentmoderation) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-271">The [visualContentModeration](#visualcontentmoderation) dimension.</span></span>|
|<span data-ttu-id="fb6c9-272">textualConentModeration</span><span class="sxs-lookup"><span data-stu-id="fb6c9-272">textualConentModeration</span></span>|<span data-ttu-id="fb6c9-273">The [textualConentModeration](#textualconentmoderation) dimension.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-273">The [textualConentModeration](#textualconentmoderation) dimension.</span></span>|

<span data-ttu-id="fb6c9-274">Example:</span><span class="sxs-lookup"><span data-stu-id="fb6c9-274">Example:</span></span>

```json
{
  "version": "0.9.0.0",
  "sourceLanguage": "en-US",
  "language": "es-ES",
  "transcript": ...,
  "ocr": ...,
  "keywords": ...,
  "faces": ...,
  "labels": ...,
  "shots": ...,
  "brands": ...,
  "audioEffects": ...,
  "sentiments": ...,
  "visualContentModeration": ...,
  "textualConentModeration": ...
}
```

#### <a name="blocks"></a><span data-ttu-id="fb6c9-275">blocks</span><span class="sxs-lookup"><span data-stu-id="fb6c9-275">blocks</span></span>

<span data-ttu-id="fb6c9-276">Attribute</span><span class="sxs-lookup"><span data-stu-id="fb6c9-276">Attribute</span></span> | <span data-ttu-id="fb6c9-277">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-277">Description</span></span>
---|---
<span data-ttu-id="fb6c9-278">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-278">id</span></span>|<span data-ttu-id="fb6c9-279">ID of the block.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-279">ID of the block.</span></span>|
<span data-ttu-id="fb6c9-280">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-280">instances</span></span>|<span data-ttu-id="fb6c9-281">A list of time ranges of this block.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-281">A list of time ranges of this block.</span></span>|

#### <a name="transcript"></a><span data-ttu-id="fb6c9-282">transcript</span><span class="sxs-lookup"><span data-stu-id="fb6c9-282">transcript</span></span>

|<span data-ttu-id="fb6c9-283">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-283">Name</span></span>|<span data-ttu-id="fb6c9-284">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-284">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-285">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-285">id</span></span>|<span data-ttu-id="fb6c9-286">The line ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-286">The line ID.</span></span>|
|<span data-ttu-id="fb6c9-287">text</span><span class="sxs-lookup"><span data-stu-id="fb6c9-287">text</span></span>|<span data-ttu-id="fb6c9-288">The transcript itself.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-288">The transcript itself.</span></span>|
|<span data-ttu-id="fb6c9-289">language</span><span class="sxs-lookup"><span data-stu-id="fb6c9-289">language</span></span>|<span data-ttu-id="fb6c9-290">The transcript language.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-290">The transcript language.</span></span> <span data-ttu-id="fb6c9-291">Intended to support transcript where each line can have a different language.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-291">Intended to support transcript where each line can have a different language.</span></span>|
|<span data-ttu-id="fb6c9-292">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-292">instances</span></span>|<span data-ttu-id="fb6c9-293">A list of time ranges where this line appeared.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-293">A list of time ranges where this line appeared.</span></span> <span data-ttu-id="fb6c9-294">If the instance is transcript, it will have only 1 instance.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-294">If the instance is transcript, it will have only 1 instance.</span></span>|

<span data-ttu-id="fb6c9-295">Example:</span><span class="sxs-lookup"><span data-stu-id="fb6c9-295">Example:</span></span>

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

#### <a name="ocr"></a><span data-ttu-id="fb6c9-296">ocr</span><span class="sxs-lookup"><span data-stu-id="fb6c9-296">ocr</span></span>

|<span data-ttu-id="fb6c9-297">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-297">Name</span></span>|<span data-ttu-id="fb6c9-298">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-298">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-299">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-299">id</span></span>|<span data-ttu-id="fb6c9-300">The OCR line ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-300">The OCR line ID.</span></span>|
|<span data-ttu-id="fb6c9-301">text</span><span class="sxs-lookup"><span data-stu-id="fb6c9-301">text</span></span>|<span data-ttu-id="fb6c9-302">The OCR text.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-302">The OCR text.</span></span>|
|<span data-ttu-id="fb6c9-303">confidence</span><span class="sxs-lookup"><span data-stu-id="fb6c9-303">confidence</span></span>|<span data-ttu-id="fb6c9-304">The recognition confidence.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-304">The recognition confidence.</span></span>|
|<span data-ttu-id="fb6c9-305">language</span><span class="sxs-lookup"><span data-stu-id="fb6c9-305">language</span></span>|<span data-ttu-id="fb6c9-306">The OCR language.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-306">The OCR language.</span></span>|
|<span data-ttu-id="fb6c9-307">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-307">instances</span></span>|<span data-ttu-id="fb6c9-308">A list of time ranges where this OCR appeared (the same OCR can appear multiple times).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-308">A list of time ranges where this OCR appeared (the same OCR can appear multiple times).</span></span>|

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

#### <a name="keywords"></a><span data-ttu-id="fb6c9-309">keywords</span><span class="sxs-lookup"><span data-stu-id="fb6c9-309">keywords</span></span>

|<span data-ttu-id="fb6c9-310">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-310">Name</span></span>|<span data-ttu-id="fb6c9-311">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-311">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-312">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-312">id</span></span>|<span data-ttu-id="fb6c9-313">The keyword ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-313">The keyword ID.</span></span>|
|<span data-ttu-id="fb6c9-314">text</span><span class="sxs-lookup"><span data-stu-id="fb6c9-314">text</span></span>|<span data-ttu-id="fb6c9-315">The keyword text.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-315">The keyword text.</span></span>|
|<span data-ttu-id="fb6c9-316">confidence</span><span class="sxs-lookup"><span data-stu-id="fb6c9-316">confidence</span></span>|<span data-ttu-id="fb6c9-317">The keyword's recognition confidence.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-317">The keyword's recognition confidence.</span></span>|
|<span data-ttu-id="fb6c9-318">language</span><span class="sxs-lookup"><span data-stu-id="fb6c9-318">language</span></span>|<span data-ttu-id="fb6c9-319">The keyword language (when translated).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-319">The keyword language (when translated).</span></span>|
|<span data-ttu-id="fb6c9-320">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-320">instances</span></span>|<span data-ttu-id="fb6c9-321">A list of time ranges where this keyword appeared (a keyword can appear multiple times).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-321">A list of time ranges where this keyword appeared (a keyword can appear multiple times).</span></span>|

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

#### <a name="faces"></a><span data-ttu-id="fb6c9-322">faces</span><span class="sxs-lookup"><span data-stu-id="fb6c9-322">faces</span></span>

|<span data-ttu-id="fb6c9-323">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-323">Name</span></span>|<span data-ttu-id="fb6c9-324">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-324">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-325">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-325">id</span></span>|<span data-ttu-id="fb6c9-326">The face ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-326">The face ID.</span></span>|
|<span data-ttu-id="fb6c9-327">name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-327">name</span></span>|<span data-ttu-id="fb6c9-328">The face name.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-328">The face name.</span></span> <span data-ttu-id="fb6c9-329">It can be ‘Unknown #0’, an identified celebrity or a customer trained person.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-329">It can be ‘Unknown #0’, an identified celebrity or a customer trained person.</span></span>|
|<span data-ttu-id="fb6c9-330">confidence</span><span class="sxs-lookup"><span data-stu-id="fb6c9-330">confidence</span></span>|<span data-ttu-id="fb6c9-331">The face identification confidence.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-331">The face identification confidence.</span></span>|
|<span data-ttu-id="fb6c9-332">description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-332">description</span></span>|<span data-ttu-id="fb6c9-333">A description of the celebrity.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-333">A description of the celebrity.</span></span> |
|<span data-ttu-id="fb6c9-334">thumbnalId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-334">thumbnalId</span></span>|<span data-ttu-id="fb6c9-335">The ID of the thumbnail of that face.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-335">The ID of the thumbnail of that face.</span></span>|
|<span data-ttu-id="fb6c9-336">knownPersonId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-336">knownPersonId</span></span>|<span data-ttu-id="fb6c9-337">If it is a known person, its internal ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-337">If it is a known person, its internal ID.</span></span>|
|<span data-ttu-id="fb6c9-338">referenceId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-338">referenceId</span></span>|<span data-ttu-id="fb6c9-339">If it is a Bing celebrity, its Bing ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-339">If it is a Bing celebrity, its Bing ID.</span></span>|
|<span data-ttu-id="fb6c9-340">referenceType</span><span class="sxs-lookup"><span data-stu-id="fb6c9-340">referenceType</span></span>|<span data-ttu-id="fb6c9-341">Currently just Bing.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-341">Currently just Bing.</span></span>|
|<span data-ttu-id="fb6c9-342">title</span><span class="sxs-lookup"><span data-stu-id="fb6c9-342">title</span></span>|<span data-ttu-id="fb6c9-343">If it is a celebrity, its title (for example "Microsoft's CEO").</span><span class="sxs-lookup"><span data-stu-id="fb6c9-343">If it is a celebrity, its title (for example "Microsoft's CEO").</span></span>|
|<span data-ttu-id="fb6c9-344">imageUrl</span><span class="sxs-lookup"><span data-stu-id="fb6c9-344">imageUrl</span></span>|<span data-ttu-id="fb6c9-345">If it is a celebrity, its image url.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-345">If it is a celebrity, its image url.</span></span>|
|<span data-ttu-id="fb6c9-346">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-346">instances</span></span>|<span data-ttu-id="fb6c9-347">These are instances of where the face appeared in the given time range.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-347">These are instances of where the face appeared in the given time range.</span></span> <span data-ttu-id="fb6c9-348">Each instance also has a thumbnailsId.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-348">Each instance also has a thumbnailsId.</span></span> |

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

#### <a name="labels"></a><span data-ttu-id="fb6c9-349">labels</span><span class="sxs-lookup"><span data-stu-id="fb6c9-349">labels</span></span>

|<span data-ttu-id="fb6c9-350">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-350">Name</span></span>|<span data-ttu-id="fb6c9-351">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-351">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-352">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-352">id</span></span>|<span data-ttu-id="fb6c9-353">The label ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-353">The label ID.</span></span>|
|<span data-ttu-id="fb6c9-354">name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-354">name</span></span>|<span data-ttu-id="fb6c9-355">The label name (for example, 'Computer', 'TV').</span><span class="sxs-lookup"><span data-stu-id="fb6c9-355">The label name (for example, 'Computer', 'TV').</span></span>|
|<span data-ttu-id="fb6c9-356">language</span><span class="sxs-lookup"><span data-stu-id="fb6c9-356">language</span></span>|<span data-ttu-id="fb6c9-357">The label name language (when translated).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-357">The label name language (when translated).</span></span> <span data-ttu-id="fb6c9-358">BCP-47</span><span class="sxs-lookup"><span data-stu-id="fb6c9-358">BCP-47</span></span>|
|<span data-ttu-id="fb6c9-359">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-359">instances</span></span>|<span data-ttu-id="fb6c9-360">A list of time ranges where this label appeared (a label can appear multiple times).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-360">A list of time ranges where this label appeared (a label can appear multiple times).</span></span> <span data-ttu-id="fb6c9-361">Each instance has a confidence field.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-361">Each instance has a confidence field.</span></span> |


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

#### <a name="shots"></a><span data-ttu-id="fb6c9-362">shots</span><span class="sxs-lookup"><span data-stu-id="fb6c9-362">shots</span></span>

|<span data-ttu-id="fb6c9-363">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-363">Name</span></span>|<span data-ttu-id="fb6c9-364">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-364">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-365">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-365">id</span></span>|<span data-ttu-id="fb6c9-366">The shot ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-366">The shot ID.</span></span>|
|<span data-ttu-id="fb6c9-367">keyFrames</span><span class="sxs-lookup"><span data-stu-id="fb6c9-367">keyFrames</span></span>|<span data-ttu-id="fb6c9-368">A list of key frames within the shot (each has an ID and a list of instances time ranges).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-368">A list of key frames within the shot (each has an ID and a list of instances time ranges).</span></span> <span data-ttu-id="fb6c9-369">Key frames instances have a thumbnailId field with the keyFrame’s thumbnail ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-369">Key frames instances have a thumbnailId field with the keyFrame’s thumbnail ID.</span></span>|
|<span data-ttu-id="fb6c9-370">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-370">instances</span></span>|<span data-ttu-id="fb6c9-371">A list of time ranges of this shot (shots have only 1 instance).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-371">A list of time ranges of this shot (shots have only 1 instance).</span></span>|

```json
"Shots": [
    {
      "id": 0,
      "keyFrames": [
        {
          "id": 0,
          "instances": [
            {
          "thumbnailId": "00000000-0000-0000-0000-000000000000",
              "start": "00: 00: 00.1670000",
              "end": "00: 00: 00.2000000"
            }
          ]
        }
      ],
      "instances": [
        {
       "thumbnailId": "00000000-0000-0000-0000-000000000000",   
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
          "thumbnailId": "00000000-0000-0000-0000-000000000000",        
              "start": "00: 00: 05.2670000",
              "end": "00: 00: 05.3000000"
            }
          ]
        }
      ],
      "instances": [
        {
      "thumbnailId": "00000000-0000-0000-0000-000000000000",
          "start": "00: 00: 05.2670000",
          "end": "00: 00: 10.3000000"
        }
      ]
    }
  ]
```

#### <a name="brands"></a><span data-ttu-id="fb6c9-372">brands</span><span class="sxs-lookup"><span data-stu-id="fb6c9-372">brands</span></span>

<span data-ttu-id="fb6c9-373">Business and product brand names detected in the speech to text transcript and/or Video OCR.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-373">Business and product brand names detected in the speech to text transcript and/or Video OCR.</span></span> <span data-ttu-id="fb6c9-374">This does not include visual recognition of brands or logo detection.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-374">This does not include visual recognition of brands or logo detection.</span></span>

|<span data-ttu-id="fb6c9-375">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-375">Name</span></span>|<span data-ttu-id="fb6c9-376">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-376">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-377">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-377">id</span></span>|<span data-ttu-id="fb6c9-378">The brand ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-378">The brand ID.</span></span>|
|<span data-ttu-id="fb6c9-379">name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-379">name</span></span>|<span data-ttu-id="fb6c9-380">The brands name.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-380">The brands name.</span></span>|
|<span data-ttu-id="fb6c9-381">referenceId</span><span class="sxs-lookup"><span data-stu-id="fb6c9-381">referenceId</span></span> | <span data-ttu-id="fb6c9-382">The suffix of the brand wikipedia url.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-382">The suffix of the brand wikipedia url.</span></span> <span data-ttu-id="fb6c9-383">For example, "Target_Corporation” is the suffix of [https://en.wikipedia.org/wiki/Target_Corporation](https://en.wikipedia.org/wiki/Target_Corporation).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-383">For example, "Target_Corporation” is the suffix of [https://en.wikipedia.org/wiki/Target_Corporation](https://en.wikipedia.org/wiki/Target_Corporation).</span></span>
|<span data-ttu-id="fb6c9-384">referenceUrl</span><span class="sxs-lookup"><span data-stu-id="fb6c9-384">referenceUrl</span></span> | <span data-ttu-id="fb6c9-385">The brand’s Wikipedia url, if exists.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-385">The brand’s Wikipedia url, if exists.</span></span> <span data-ttu-id="fb6c9-386">For example, [https://en.wikipedia.org/wiki/Target_Corporation](https://en.wikipedia.org/wiki/Target_Corporation).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-386">For example, [https://en.wikipedia.org/wiki/Target_Corporation](https://en.wikipedia.org/wiki/Target_Corporation).</span></span>
|<span data-ttu-id="fb6c9-387">description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-387">description</span></span>|<span data-ttu-id="fb6c9-388">The brands description.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-388">The brands description.</span></span>|
|<span data-ttu-id="fb6c9-389">tags</span><span class="sxs-lookup"><span data-stu-id="fb6c9-389">tags</span></span>|<span data-ttu-id="fb6c9-390">A list of predefined tags that were associated with this brand.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-390">A list of predefined tags that were associated with this brand.</span></span>|
|<span data-ttu-id="fb6c9-391">confidence</span><span class="sxs-lookup"><span data-stu-id="fb6c9-391">confidence</span></span>|<span data-ttu-id="fb6c9-392">The confidence value of the Video Indexer brand detector (0-1).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-392">The confidence value of the Video Indexer brand detector (0-1).</span></span>|
|<span data-ttu-id="fb6c9-393">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-393">instances</span></span>|<span data-ttu-id="fb6c9-394">A list of time ranges of this brand.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-394">A list of time ranges of this brand.</span></span> <span data-ttu-id="fb6c9-395">Each instance has a brandType, which indicates whether this brand appeared in the transcript or in OCR.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-395">Each instance has a brandType, which indicates whether this brand appeared in the transcript or in OCR.</span></span>|

```json
"brands": [
{
    "id": 0,
    "name": "MicrosoftExcel",
    "referenceId": "Microsoft_Excel",
    "referenceUrl": "http: //en.wikipedia.org/wiki/Microsoft_Excel",
    "referenceType": "Wiki",
    "description": "Microsoft Excel is a sprea..",
    "tags": [],
    "confidence": 0.975,
    "instances": [
    {
        "brandType": "Transcript",
        "start": "00: 00: 31.3000000",
        "end": "00: 00: 39.0600000"
    }
    ]
},
{
    "id": 1,
    "name": "Microsoft",
    "referenceId": "Microsoft",
    "referenceUrl": "http: //en.wikipedia.org/wiki/Microsoft",
    "description": "Microsoft Corporation is...",
    "tags": [
    "competitors",
    "technology"
    ],
    "confidence": 1.0,
    "instances": [
    {
        "brandType": "Transcript",
        "start": "00: 01: 44",
        "end": "00: 01: 45.3670000"
    },
    {
        "brandType": "Ocr",
        "start": "00: 01: 54",
        "end": "00: 02: 45.3670000"
    }
    ]
}
]
```

#### <a name="statistics"></a><span data-ttu-id="fb6c9-396">statistics</span><span class="sxs-lookup"><span data-stu-id="fb6c9-396">statistics</span></span>

|<span data-ttu-id="fb6c9-397">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-397">Name</span></span>|<span data-ttu-id="fb6c9-398">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-398">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-399">CorrespondenceCount</span><span class="sxs-lookup"><span data-stu-id="fb6c9-399">CorrespondenceCount</span></span>|<span data-ttu-id="fb6c9-400">Number of correspondences in the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-400">Number of correspondences in the video.</span></span>|
|<span data-ttu-id="fb6c9-401">WordCount</span><span class="sxs-lookup"><span data-stu-id="fb6c9-401">WordCount</span></span>|<span data-ttu-id="fb6c9-402">The number of words per speaker.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-402">The number of words per speaker.</span></span>|
|<span data-ttu-id="fb6c9-403">SpeakerNumberOfFragments</span><span class="sxs-lookup"><span data-stu-id="fb6c9-403">SpeakerNumberOfFragments</span></span>|<span data-ttu-id="fb6c9-404">The amount of fragments the speaker has in a video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-404">The amount of fragments the speaker has in a video.</span></span>|
|<span data-ttu-id="fb6c9-405">SpeakerLongestMonolog</span><span class="sxs-lookup"><span data-stu-id="fb6c9-405">SpeakerLongestMonolog</span></span>|<span data-ttu-id="fb6c9-406">The speaker's longest monolog.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-406">The speaker's longest monolog.</span></span> <span data-ttu-id="fb6c9-407">If the speaker has silences inside the monolog it is included.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-407">If the speaker has silences inside the monolog it is included.</span></span> <span data-ttu-id="fb6c9-408">Silence at the beginning and the end of the monolog is removed.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-408">Silence at the beginning and the end of the monolog is removed.</span></span>| 
|<span data-ttu-id="fb6c9-409">SpeakerTalkToListenRatio</span><span class="sxs-lookup"><span data-stu-id="fb6c9-409">SpeakerTalkToListenRatio</span></span>|<span data-ttu-id="fb6c9-410">The calculation is based on the time spent on the speaker's monolog (without the silence in between) divided by the total time of the video.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-410">The calculation is based on the time spent on the speaker's monolog (without the silence in between) divided by the total time of the video.</span></span> <span data-ttu-id="fb6c9-411">The time is rounded to the third decimal point.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-411">The time is rounded to the third decimal point.</span></span>|

#### <a name="audioeffects"></a><span data-ttu-id="fb6c9-412">audioEffects</span><span class="sxs-lookup"><span data-stu-id="fb6c9-412">audioEffects</span></span>

|<span data-ttu-id="fb6c9-413">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-413">Name</span></span>|<span data-ttu-id="fb6c9-414">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-414">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-415">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-415">id</span></span>|<span data-ttu-id="fb6c9-416">The audio effect ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-416">The audio effect ID.</span></span>|
|<span data-ttu-id="fb6c9-417">type</span><span class="sxs-lookup"><span data-stu-id="fb6c9-417">type</span></span>|<span data-ttu-id="fb6c9-418">The audio effect type (for example, Clapping, Speech, Silence).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-418">The audio effect type (for example, Clapping, Speech, Silence).</span></span>|
|<span data-ttu-id="fb6c9-419">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-419">instances</span></span>|<span data-ttu-id="fb6c9-420">A list of time ranges where this audio effect appeared.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-420">A list of time ranges where this audio effect appeared.</span></span>|

```json
"audioEffects": [
{
    "id": 0,
    "type": "Clapping",
    "instances": [
    {
        "start": "00:00:00",
        "end": "00:00:03"
    },
    {
        "start": "00:01:13",
        "end": "00:01:21"
    }
    ]
}
]
```

#### <a name="sentiments"></a><span data-ttu-id="fb6c9-421">sentiments</span><span class="sxs-lookup"><span data-stu-id="fb6c9-421">sentiments</span></span>

<span data-ttu-id="fb6c9-422">Sentiments are aggregated by their sentimentType field (Positive/Neutral/Negative).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-422">Sentiments are aggregated by their sentimentType field (Positive/Neutral/Negative).</span></span> <span data-ttu-id="fb6c9-423">For example, 0-0.1, 0.1-0.2.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-423">For example, 0-0.1, 0.1-0.2.</span></span>

|<span data-ttu-id="fb6c9-424">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-424">Name</span></span>|<span data-ttu-id="fb6c9-425">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-425">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-426">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-426">id</span></span>|<span data-ttu-id="fb6c9-427">The sentiment ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-427">The sentiment ID.</span></span>|
|<span data-ttu-id="fb6c9-428">averageScore</span><span class="sxs-lookup"><span data-stu-id="fb6c9-428">averageScore</span></span> |<span data-ttu-id="fb6c9-429">The average of all scores of all instances of that sentiment type - Positive/Neutral/Negative</span><span class="sxs-lookup"><span data-stu-id="fb6c9-429">The average of all scores of all instances of that sentiment type - Positive/Neutral/Negative</span></span>|
|<span data-ttu-id="fb6c9-430">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-430">instances</span></span>|<span data-ttu-id="fb6c9-431">A list of time ranges where this sentiment appeared.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-431">A list of time ranges where this sentiment appeared.</span></span>|
|<span data-ttu-id="fb6c9-432">sentimentType</span><span class="sxs-lookup"><span data-stu-id="fb6c9-432">sentimentType</span></span> |<span data-ttu-id="fb6c9-433">The type can be 'Positive', 'Neutral', or 'Negative'.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-433">The type can be 'Positive', 'Neutral', or 'Negative'.</span></span>|

```json
"sentiments": [
{
    "id": 0,
    "averageScore": 0.87,
    "sentimentType": "Positive",
    "instances": [
    {
        "start": "00:00:23",
        "end": "00:00:41"
    }
    ]
}, {
    "id": 1,
    "averageScore": 0.11,
    "sentimentType": "Positive",
    "instances": [
    {
        "start": "00:00:13",
        "end": "00:00:21"
    }
    ]
}
]
```

#### <a name="visualcontentmoderation"></a><span data-ttu-id="fb6c9-434">visualContentModeration</span><span class="sxs-lookup"><span data-stu-id="fb6c9-434">visualContentModeration</span></span>

<span data-ttu-id="fb6c9-435">The visualContentModeration block contains time ranges which Video Indexer found to potentially have adult content.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-435">The visualContentModeration block contains time ranges which Video Indexer found to potentially have adult content.</span></span> <span data-ttu-id="fb6c9-436">If visualContentModeration is empty, there is no adult content that was identified.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-436">If visualContentModeration is empty, there is no adult content that was identified.</span></span>

<span data-ttu-id="fb6c9-437">Videos that are found to contain adult or racy content might be available for private view only.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-437">Videos that are found to contain adult or racy content might be available for private view only.</span></span> <span data-ttu-id="fb6c9-438">Users have the option to submit a request for a human review of the content, in which case the IsAdult attribute will contain the result of the human review.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-438">Users have the option to submit a request for a human review of the content, in which case the IsAdult attribute will contain the result of the human review.</span></span>

|<span data-ttu-id="fb6c9-439">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-439">Name</span></span>|<span data-ttu-id="fb6c9-440">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-440">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-441">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-441">id</span></span>|<span data-ttu-id="fb6c9-442">The visual content moderation ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-442">The visual content moderation ID.</span></span>|
|<span data-ttu-id="fb6c9-443">adultScore</span><span class="sxs-lookup"><span data-stu-id="fb6c9-443">adultScore</span></span>|<span data-ttu-id="fb6c9-444">The adult score (from content moderator).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-444">The adult score (from content moderator).</span></span>|
|<span data-ttu-id="fb6c9-445">racyScore</span><span class="sxs-lookup"><span data-stu-id="fb6c9-445">racyScore</span></span>|<span data-ttu-id="fb6c9-446">The racy score (from content moderation).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-446">The racy score (from content moderation).</span></span>|
|<span data-ttu-id="fb6c9-447">instances</span><span class="sxs-lookup"><span data-stu-id="fb6c9-447">instances</span></span>|<span data-ttu-id="fb6c9-448">A list of time ranges where this visual content moderation appeared.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-448">A list of time ranges where this visual content moderation appeared.</span></span>|

```json
"VisualContentModeration": [
{
    "id": 0,
    "adultScore": 0.00069,
    "racyScore": 0.91129,
    "instances": [
    {
        "start": "00:00:25.4840000",
        "end": "00:00:25.5260000"
    }
    ]
},
{
    "id": 1,
    "adultScore": 0.99231,
    "racyScore": 0.99912,
    "instances": [
    {
        "start": "00:00:35.5360000",
        "end": "00:00:35.5780000"
    }
    ]
}
] 
```

#### <a name="textualconentmoderation"></a><span data-ttu-id="fb6c9-449">textualConentModeration</span><span class="sxs-lookup"><span data-stu-id="fb6c9-449">textualConentModeration</span></span> 

|<span data-ttu-id="fb6c9-450">Name</span><span class="sxs-lookup"><span data-stu-id="fb6c9-450">Name</span></span>|<span data-ttu-id="fb6c9-451">Description</span><span class="sxs-lookup"><span data-stu-id="fb6c9-451">Description</span></span>|
|---|---|
|<span data-ttu-id="fb6c9-452">id</span><span class="sxs-lookup"><span data-stu-id="fb6c9-452">id</span></span>|<span data-ttu-id="fb6c9-453">The textual content moderation ID.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-453">The textual content moderation ID.</span></span>|
|<span data-ttu-id="fb6c9-454">bannedWordsCount</span><span class="sxs-lookup"><span data-stu-id="fb6c9-454">bannedWordsCount</span></span> |<span data-ttu-id="fb6c9-455">The number of banned words.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-455">The number of banned words.</span></span>|
|<span data-ttu-id="fb6c9-456">bannedWordsRatio</span><span class="sxs-lookup"><span data-stu-id="fb6c9-456">bannedWordsRatio</span></span> |<span data-ttu-id="fb6c9-457">The ratio from total number of words.</span><span class="sxs-lookup"><span data-stu-id="fb6c9-457">The ratio from total number of words.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="fb6c9-458">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb6c9-458">Next steps</span></span>

[<span data-ttu-id="fb6c9-459">Video Indexer API</span><span class="sxs-lookup"><span data-stu-id="fb6c9-459">Video Indexer API</span></span>](https://api-portal.videoindexer.ai)

<span data-ttu-id="fb6c9-460">For information about how to embed widgets in your application, see [Embed Video Indexer widgets into your applications](video-indexer-embed-widgets.md).</span><span class="sxs-lookup"><span data-stu-id="fb6c9-460">For information about how to embed widgets in your application, see [Embed Video Indexer widgets into your applications](video-indexer-embed-widgets.md).</span></span> 

