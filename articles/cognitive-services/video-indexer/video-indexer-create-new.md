---
title: Use Azure Video Indexer to create video insights from existing videos | Microsoft Docs
description: This topic shows you how to create and publish video insights based on some other video.
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 07/25/2018
ms.author: juliako
ms.openlocfilehash: 161a47f72a0f8038a515c09f25ec2a8e8a520547
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968499"
---
# <a name="create-highlights-from-existing-videos"></a><span data-ttu-id="4a9d5-103">Create highlights from existing videos</span><span class="sxs-lookup"><span data-stu-id="4a9d5-103">Create highlights from existing videos</span></span>

<span data-ttu-id="4a9d5-104">This topic shows you how to create and publish video insights based on some other video.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-104">This topic shows you how to create and publish video insights based on some other video.</span></span>

1. <span data-ttu-id="4a9d5-105">Sign in to your [Video Indexer](https://api-portal.videoindexer.ai/) account.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-105">Sign in to your [Video Indexer](https://api-portal.videoindexer.ai/) account.</span></span>
2. <span data-ttu-id="4a9d5-106">Find a video from which you want to create your video insights.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-106">Find a video from which you want to create your video insights.</span></span>
3. <span data-ttu-id="4a9d5-107">Press **Play**.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-107">Press **Play**.</span></span>

    <span data-ttu-id="4a9d5-108">The page shows the video's summarized insights.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-108">The page shows the video's summarized insights.</span></span> 

    ![Insights](./media/video-indexer-create-new/video-indexer-summarized-insights.png)

3. <span data-ttu-id="4a9d5-110">Press the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-110">Press the **Edit** button.</span></span>

    <span data-ttu-id="4a9d5-111">This page shows you the full breakdown of a video.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-111">This page shows you the full breakdown of a video.</span></span> <span data-ttu-id="4a9d5-112">The breakdown is broken into blocks.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-112">The breakdown is broken into blocks.</span></span> <span data-ttu-id="4a9d5-113">Blocks are here to make it easier to go through the data.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-113">Blocks are here to make it easier to go through the data.</span></span> <span data-ttu-id="4a9d5-114">For example, block might be broken down based on when speakers change or there is a long pause.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-114">For example, block might be broken down based on when speakers change or there is a long pause.</span></span> <span data-ttu-id="4a9d5-115">You can create your own playlist that contains only lines that you want.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-115">You can create your own playlist that contains only lines that you want.</span></span> <span data-ttu-id="4a9d5-116">To show only specific parts of the source video, you can filter by topics/keywords, sentiments, people, speakers.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-116">To show only specific parts of the source video, you can filter by topics/keywords, sentiments, people, speakers.</span></span> <span data-ttu-id="4a9d5-117">You can choose to only view the video's transcript or OCR.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-117">You can choose to only view the video's transcript or OCR.</span></span>    

    ![Insights](./media/video-indexer-create-new/video-indexer-create-new-playlist.png)

4. <span data-ttu-id="4a9d5-119">Create your playlist.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-119">Create your playlist.</span></span>

    <span data-ttu-id="4a9d5-120">To add or remove lines to/from your playlist, press **+**/**-**.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-120">To add or remove lines to/from your playlist, press **+**/**-**.</span></span>

5. <span data-ttu-id="4a9d5-121">Preview your playlist.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-121">Preview your playlist.</span></span>

    <span data-ttu-id="4a9d5-122">Once you are done creating the playlist, press **Preview**.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-122">Once you are done creating the playlist, press **Preview**.</span></span>
6. <span data-ttu-id="4a9d5-123">Publish the playlist.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-123">Publish the playlist.</span></span>

    <span data-ttu-id="4a9d5-124">After you preview the playlist, you can publish it.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-124">After you preview the playlist, you can publish it.</span></span>

    <span data-ttu-id="4a9d5-125">Once you publish the playlist, it is added to the list of your video insights.</span><span class="sxs-lookup"><span data-stu-id="4a9d5-125">Once you publish the playlist, it is added to the list of your video insights.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4a9d5-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="4a9d5-126">Next steps</span></span> 

<span data-ttu-id="4a9d5-127">Once you create the new playlist, you can continue processing it, as described in one of these topics:</span><span class="sxs-lookup"><span data-stu-id="4a9d5-127">Once you create the new playlist, you can continue processing it, as described in one of these topics:</span></span> 

- [<span data-ttu-id="4a9d5-128">Process content with Video Indexer REST API</span><span class="sxs-lookup"><span data-stu-id="4a9d5-128">Process content with Video Indexer REST API</span></span>](video-indexer-use-apis.md)
- [<span data-ttu-id="4a9d5-129">Embed visual widgets in your application</span><span class="sxs-lookup"><span data-stu-id="4a9d5-129">Embed visual widgets in your application</span></span>](video-indexer-embed-widgets.md)

## <a name="see-also"></a><span data-ttu-id="4a9d5-130">See also</span><span class="sxs-lookup"><span data-stu-id="4a9d5-130">See also</span></span>

[<span data-ttu-id="4a9d5-131">Video Indexer overview</span><span class="sxs-lookup"><span data-stu-id="4a9d5-131">Video Indexer overview</span></span>](video-indexer-overview.md) 
