---
title: Azure Content Moderator - Video moderation | Microsoft Docs
description: Use machine-assisted video moderation and human review tools to moderate inappropriate content
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/20/2018
ms.author: sajagtap
ms.openlocfilehash: d9c01d4c2590535a4106e8e4ee79a12bdc60d956
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870317"
---
# <a name="video-moderation"></a><span data-ttu-id="5b11c-103">Video moderation</span><span class="sxs-lookup"><span data-stu-id="5b11c-103">Video moderation</span></span>

<span data-ttu-id="5b11c-104">Use Content Moderator’s machine-assisted [video moderation](video-moderation-api.md) and [human review tool](Review-Tool-User-Guide/human-in-the-loop.md) to moderate videos and transcripts for adult (explicit) and racy (suggestive) content to get the best results for your business.</span><span class="sxs-lookup"><span data-stu-id="5b11c-104">Use Content Moderator’s machine-assisted [video moderation](video-moderation-api.md) and [human review tool](Review-Tool-User-Guide/human-in-the-loop.md) to moderate videos and transcripts for adult (explicit) and racy (suggestive) content to get the best results for your business.</span></span>

## <a name="video-trained-classifier-preview"></a><span data-ttu-id="5b11c-105">Video-trained classifier (preview)</span><span class="sxs-lookup"><span data-stu-id="5b11c-105">Video-trained classifier (preview)</span></span>

<span data-ttu-id="5b11c-106">Machine-assisted video classification is either achieved with image trained models or video trained models.</span><span class="sxs-lookup"><span data-stu-id="5b11c-106">Machine-assisted video classification is either achieved with image trained models or video trained models.</span></span> <span data-ttu-id="5b11c-107">Unlike image-trained video classifiers, Microsoft's adult and racy video classifier is trained with videos.</span><span class="sxs-lookup"><span data-stu-id="5b11c-107">Unlike image-trained video classifiers, Microsoft's adult and racy video classifier is trained with videos.</span></span> <span data-ttu-id="5b11c-108">This method results in better match quality.</span><span class="sxs-lookup"><span data-stu-id="5b11c-108">This method results in better match quality.</span></span>

## <a name="shot-detection"></a><span data-ttu-id="5b11c-109">Shot detection</span><span class="sxs-lookup"><span data-stu-id="5b11c-109">Shot detection</span></span>

<span data-ttu-id="5b11c-110">When outputting the classification details, additional video intelligence helps with more flexibility in analyzing videos.</span><span class="sxs-lookup"><span data-stu-id="5b11c-110">When outputting the classification details, additional video intelligence helps with more flexibility in analyzing videos.</span></span> <span data-ttu-id="5b11c-111">Instead of outputting just the frames, Microsoft's video moderation service provides shot-level information too.</span><span class="sxs-lookup"><span data-stu-id="5b11c-111">Instead of outputting just the frames, Microsoft's video moderation service provides shot-level information too.</span></span> <span data-ttu-id="5b11c-112">You now have the option to analyze your videos at the shot level and the frame level.</span><span class="sxs-lookup"><span data-stu-id="5b11c-112">You now have the option to analyze your videos at the shot level and the frame level.</span></span>
 
## <a name="key-frame-detection"></a><span data-ttu-id="5b11c-113">Key frame detection</span><span class="sxs-lookup"><span data-stu-id="5b11c-113">Key frame detection</span></span>

<span data-ttu-id="5b11c-114">Instead of outputting frames at regular intervals, the video moderation service identifies and outputs only potentially complete (good) frames.</span><span class="sxs-lookup"><span data-stu-id="5b11c-114">Instead of outputting frames at regular intervals, the video moderation service identifies and outputs only potentially complete (good) frames.</span></span> <span data-ttu-id="5b11c-115">The feature allows efficient frame generation for frame-level adult and racy analysis.</span><span class="sxs-lookup"><span data-stu-id="5b11c-115">The feature allows efficient frame generation for frame-level adult and racy analysis.</span></span>

<span data-ttu-id="5b11c-116">The following extract shows a partial response with potential shots, key frames, and adult and racy scores:</span><span class="sxs-lookup"><span data-stu-id="5b11c-116">The following extract shows a partial response with potential shots, key frames, and adult and racy scores:</span></span>

    "fragments": [
    {
      "start": 0,
      "duration": 18000
    },
    {
      "start": 18000,
      "duration": 3600,
      "interval": 3600,
      "events": [
        [
          {
            "reviewRecommended": false,
            "adultScore": 0.00001,
            "racyScore": 0.03077,
            "index": 5,
            "timestamp": 18000,
            "shotIndex": 0
          }
        ]
      ]
    },
    {
      "start": 18386372,
      "duration": 119149,
      "interval": 119149,
      "events": [
        [
          {
            "reviewRecommended": true,
            "adultScore": 0.00000,
            "racyScore": 0.91902,
            "index": 5085,
            "timestamp": 18386372,
            "shotIndex": 62
          }
        ]
      ]


## <a name="visualization-for-human-reviews"></a><span data-ttu-id="5b11c-117">Visualization for human reviews</span><span class="sxs-lookup"><span data-stu-id="5b11c-117">Visualization for human reviews</span></span>

<span data-ttu-id="5b11c-118">For more nuanced cases, businesses need a human review solution for rendering the video, its frames, and machine-assigned tags.</span><span class="sxs-lookup"><span data-stu-id="5b11c-118">For more nuanced cases, businesses need a human review solution for rendering the video, its frames, and machine-assigned tags.</span></span> <span data-ttu-id="5b11c-119">The human moderators reviewing videos and frames get a complete view of the insights, change tags, and submit their decisions.</span><span class="sxs-lookup"><span data-stu-id="5b11c-119">The human moderators reviewing videos and frames get a complete view of the insights, change tags, and submit their decisions.</span></span>

![video review tool default view](images/video-review-default-view.png)

## <a name="player-view-for-video-level-review"></a><span data-ttu-id="5b11c-121">Player view for video-level review</span><span class="sxs-lookup"><span data-stu-id="5b11c-121">Player view for video-level review</span></span>

<span data-ttu-id="5b11c-122">Video-level binary decisions are made possible with a video player view that shows potential adult and racy frames.</span><span class="sxs-lookup"><span data-stu-id="5b11c-122">Video-level binary decisions are made possible with a video player view that shows potential adult and racy frames.</span></span> <span data-ttu-id="5b11c-123">The human reviewers navigate the video with various speed options to examine the scenes.</span><span class="sxs-lookup"><span data-stu-id="5b11c-123">The human reviewers navigate the video with various speed options to examine the scenes.</span></span> <span data-ttu-id="5b11c-124">They confirm their decisions by toggling the tags.</span><span class="sxs-lookup"><span data-stu-id="5b11c-124">They confirm their decisions by toggling the tags.</span></span>

![video review tool player view](images/video-review-player-view.PNG)

## <a name="frames-view-for-detailed-reviews"></a><span data-ttu-id="5b11c-126">Frames view for detailed reviews</span><span class="sxs-lookup"><span data-stu-id="5b11c-126">Frames view for detailed reviews</span></span>

<span data-ttu-id="5b11c-127">A detailed video review for frame-by-frame analysis is made possible with a frame-based view.</span><span class="sxs-lookup"><span data-stu-id="5b11c-127">A detailed video review for frame-by-frame analysis is made possible with a frame-based view.</span></span> <span data-ttu-id="5b11c-128">The human reviewers review and select one or more frames and toggle tags to confirm their decisions.</span><span class="sxs-lookup"><span data-stu-id="5b11c-128">The human reviewers review and select one or more frames and toggle tags to confirm their decisions.</span></span> <span data-ttu-id="5b11c-129">An optional next step is redaction of the offensive frames or content.</span><span class="sxs-lookup"><span data-stu-id="5b11c-129">An optional next step is redaction of the offensive frames or content.</span></span>

![video review tool frames view](images/video-review-frames-view-apply-tags.PNG)

## <a name="transcript-moderation"></a><span data-ttu-id="5b11c-131">Transcript moderation</span><span class="sxs-lookup"><span data-stu-id="5b11c-131">Transcript moderation</span></span>

<span data-ttu-id="5b11c-132">Videos typically have voice over that needs moderation as well for offensive speech.</span><span class="sxs-lookup"><span data-stu-id="5b11c-132">Videos typically have voice over that needs moderation as well for offensive speech.</span></span> <span data-ttu-id="5b11c-133">You use the Azure Media Indexer service to convert speech to text and use Content Moderator's review API to submit the transcript for text moderation within the review tool.</span><span class="sxs-lookup"><span data-stu-id="5b11c-133">You use the Azure Media Indexer service to convert speech to text and use Content Moderator's review API to submit the transcript for text moderation within the review tool.</span></span>

![video review tool transcript view](images/video-review-transcript-view.png)

## <a name="next-steps"></a><span data-ttu-id="5b11c-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b11c-135">Next steps</span></span>

<span data-ttu-id="5b11c-136">Get started with the [video moderation quickstart](video-moderation-api.md).</span><span class="sxs-lookup"><span data-stu-id="5b11c-136">Get started with the [video moderation quickstart](video-moderation-api.md).</span></span> 

<span data-ttu-id="5b11c-137">Learn how to generate [video reviews](video-reviews-quickstart-dotnet.md) for your human reviewers from your moderated output.</span><span class="sxs-lookup"><span data-stu-id="5b11c-137">Learn how to generate [video reviews](video-reviews-quickstart-dotnet.md) for your human reviewers from your moderated output.</span></span>

<span data-ttu-id="5b11c-138">Add [video transcript reviews](video-transcript-reviews-quickstart-dotnet.md) to your video reviews.</span><span class="sxs-lookup"><span data-stu-id="5b11c-138">Add [video transcript reviews](video-transcript-reviews-quickstart-dotnet.md) to your video reviews.</span></span>

<span data-ttu-id="5b11c-139">Check out the detailed tutorial on how to develop a [complete video moderation solution](video-transcript-moderation-review-tutorial-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5b11c-139">Check out the detailed tutorial on how to develop a [complete video moderation solution](video-transcript-moderation-review-tutorial-dotnet.md).</span></span> 
