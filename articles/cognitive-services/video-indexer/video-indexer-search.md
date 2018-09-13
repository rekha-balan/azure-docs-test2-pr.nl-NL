---
title: Use Azure Video Indexer to find exact moments within videos | Microsoft Docs
description: This topic demonstrates how to find exact moments within videos.
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 07/31/2018
ms.author: juliako
ms.openlocfilehash: 1cffa067d8028adab4dbcc82c529f77d980ce6be
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855673"
---
# <a name="find-exact-moments-within-videos"></a><span data-ttu-id="91732-103">Find exact moments within videos</span><span class="sxs-lookup"><span data-stu-id="91732-103">Find exact moments within videos</span></span>

<span data-ttu-id="91732-104">This topic shows you the search options that enable you to find exact moments within videos.</span><span class="sxs-lookup"><span data-stu-id="91732-104">This topic shows you the search options that enable you to find exact moments within videos.</span></span>

1. <span data-ttu-id="91732-105">Sign in to your [Video Indexer](https://api-portal.videoindexer.ai/) account.</span><span class="sxs-lookup"><span data-stu-id="91732-105">Sign in to your [Video Indexer](https://api-portal.videoindexer.ai/) account.</span></span>
2. <span data-ttu-id="91732-106">Search among all videos in your account.</span><span class="sxs-lookup"><span data-stu-id="91732-106">Search among all videos in your account.</span></span>

    <span data-ttu-id="91732-107">In the following example, we searched for all videos created by Channel9 with Scott Hanselman.</span><span class="sxs-lookup"><span data-stu-id="91732-107">In the following example, we searched for all videos created by Channel9 with Scott Hanselman.</span></span>

    ![Search](./media/video-indexer-search/video-indexer-search01.png)
    
3. <span data-ttu-id="91732-109">Search the summarized insights of the video.</span><span class="sxs-lookup"><span data-stu-id="91732-109">Search the summarized insights of the video.</span></span>

    <span data-ttu-id="91732-110">You can then search within a video by clicking **Play** on the video.</span><span class="sxs-lookup"><span data-stu-id="91732-110">You can then search within a video by clicking **Play** on the video.</span></span> <span data-ttu-id="91732-111">Then, you can search within the video by selecting the **Search** tab. For example, we searched for all the places where the "identity protection" text is used.</span><span class="sxs-lookup"><span data-stu-id="91732-111">Then, you can search within the video by selecting the **Search** tab. For example, we searched for all the places where the "identity protection" text is used.</span></span> 

    ![Search](./media/video-indexer-search/video-indexer-search02.png)

    <span data-ttu-id="91732-113">If you click one of the results, the player brings you to that moment in the video.</span><span class="sxs-lookup"><span data-stu-id="91732-113">If you click one of the results, the player brings you to that moment in the video.</span></span> <span data-ttu-id="91732-114">You can achieve the player/insights view and synchronization in your application.</span><span class="sxs-lookup"><span data-stu-id="91732-114">You can achieve the player/insights view and synchronization in your application.</span></span> <span data-ttu-id="91732-115">For more information, see [Embed Video Indexer widgets into your application](video-indexer-embed-widgets.md).</span><span class="sxs-lookup"><span data-stu-id="91732-115">For more information, see [Embed Video Indexer widgets into your application](video-indexer-embed-widgets.md).</span></span> 

    
4. <span data-ttu-id="91732-116">Search the detailed breakdown of the video.</span><span class="sxs-lookup"><span data-stu-id="91732-116">Search the detailed breakdown of the video.</span></span>

    <span data-ttu-id="91732-117">If you want to create your own breakdown based on the video that you found, press the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="91732-117">If you want to create your own breakdown based on the video that you found, press the **Edit** button.</span></span> <span data-ttu-id="91732-118">This page shows you the full breakdown of a video.</span><span class="sxs-lookup"><span data-stu-id="91732-118">This page shows you the full breakdown of a video.</span></span> <span data-ttu-id="91732-119">You can search within the breakdown to only show the lines you are interested in.</span><span class="sxs-lookup"><span data-stu-id="91732-119">You can search within the breakdown to only show the lines you are interested in.</span></span> <span data-ttu-id="91732-120">For more information, see [View and edit Video Indexer insights](video-indexer-view-edit.md).</span><span class="sxs-lookup"><span data-stu-id="91732-120">For more information, see [View and edit Video Indexer insights](video-indexer-view-edit.md).</span></span>

    <span data-ttu-id="91732-121">In this example, we searched the "identity protection" text.</span><span class="sxs-lookup"><span data-stu-id="91732-121">In this example, we searched the "identity protection" text.</span></span> <span data-ttu-id="91732-122">We also applied additional filters, as shown in the screen below.</span><span class="sxs-lookup"><span data-stu-id="91732-122">We also applied additional filters, as shown in the screen below.</span></span>

    ![Search](./media/video-indexer-search/video-indexer-search03.png)

## <a name="next-steps"></a><span data-ttu-id="91732-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="91732-124">Next steps</span></span> 

<span data-ttu-id="91732-125">Once you find the video you want to work with, you can continue processing the video, as described in one of these topics:</span><span class="sxs-lookup"><span data-stu-id="91732-125">Once you find the video you want to work with, you can continue processing the video, as described in one of these topics:</span></span> 

- [<span data-ttu-id="91732-126">Create new video insights based on existing video</span><span class="sxs-lookup"><span data-stu-id="91732-126">Create new video insights based on existing video</span></span>](video-indexer-create-new.md)
- [<span data-ttu-id="91732-127">Process content with Video Indexer REST API</span><span class="sxs-lookup"><span data-stu-id="91732-127">Process content with Video Indexer REST API</span></span>](video-indexer-use-apis.md)
- [<span data-ttu-id="91732-128">Embed visual widgets in your application</span><span class="sxs-lookup"><span data-stu-id="91732-128">Embed visual widgets in your application</span></span>](video-indexer-embed-widgets.md)

## <a name="see-also"></a><span data-ttu-id="91732-129">See also</span><span class="sxs-lookup"><span data-stu-id="91732-129">See also</span></span>

[<span data-ttu-id="91732-130">Video Indexer overview</span><span class="sxs-lookup"><span data-stu-id="91732-130">Video Indexer overview</span></span>](video-indexer-overview.md)
