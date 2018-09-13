---
title: View and edit Azure Video Indexer insights | Microsoft Docs
description: This topic demonstrates how to view and edit Video Indexer insights.
services: cognitive services
documentationcenter: ''
author: juliako
ms.service: cognitive-services
ms.topic: article
ms.date: 07/31/2018
ms.author: juliako
ms.openlocfilehash: 797c09d72402cfc1ee2524e7792cc1310a53fb1e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867204"
---
# <a name="view-and-edit-video-indexer-insights"></a><span data-ttu-id="4a01b-103">View and edit Video Indexer insights</span><span class="sxs-lookup"><span data-stu-id="4a01b-103">View and edit Video Indexer insights</span></span>

<span data-ttu-id="4a01b-104">This topic shows you how to view and edit the Video Indexer insights of a video.</span><span class="sxs-lookup"><span data-stu-id="4a01b-104">This topic shows you how to view and edit the Video Indexer insights of a video.</span></span>

1. <span data-ttu-id="4a01b-105">Sign in to your [Video Indexer](https://api-portal.videoindexer.ai/) account.</span><span class="sxs-lookup"><span data-stu-id="4a01b-105">Sign in to your [Video Indexer](https://api-portal.videoindexer.ai/) account.</span></span>
2. <span data-ttu-id="4a01b-106">Find a video from which you want to create your Video Indexer insights.</span><span class="sxs-lookup"><span data-stu-id="4a01b-106">Find a video from which you want to create your Video Indexer insights.</span></span> <span data-ttu-id="4a01b-107">For more information, see [Find exact moments within videos](video-indexer-search.md).</span><span class="sxs-lookup"><span data-stu-id="4a01b-107">For more information, see [Find exact moments within videos](video-indexer-search.md).</span></span>
3. <span data-ttu-id="4a01b-108">Press **Play**.</span><span class="sxs-lookup"><span data-stu-id="4a01b-108">Press **Play**.</span></span>

    <span data-ttu-id="4a01b-109">The page shows the video's summarized insights.</span><span class="sxs-lookup"><span data-stu-id="4a01b-109">The page shows the video's summarized insights.</span></span> 

    ![Insights](./media/video-indexer-view-edit/video-indexer-summarized-insights.png)

4. <span data-ttu-id="4a01b-111">View the summarized insights of the video.</span><span class="sxs-lookup"><span data-stu-id="4a01b-111">View the summarized insights of the video.</span></span> 

    <span data-ttu-id="4a01b-112">Summarized insights show an aggregated view of the data: faces, keywords, sentiments.</span><span class="sxs-lookup"><span data-stu-id="4a01b-112">Summarized insights show an aggregated view of the data: faces, keywords, sentiments.</span></span> <span data-ttu-id="4a01b-113">For example, you can see the faces of people and the time ranges each face appears in and the % of the time it is shown.</span><span class="sxs-lookup"><span data-stu-id="4a01b-113">For example, you can see the faces of people and the time ranges each face appears in and the % of the time it is shown.</span></span>

    <span data-ttu-id="4a01b-114">The player and the insights are synchronized.</span><span class="sxs-lookup"><span data-stu-id="4a01b-114">The player and the insights are synchronized.</span></span> <span data-ttu-id="4a01b-115">For example, if you click a keyword or the transcript line, the player brings you to that moment in the video.</span><span class="sxs-lookup"><span data-stu-id="4a01b-115">For example, if you click a keyword or the transcript line, the player brings you to that moment in the video.</span></span> <span data-ttu-id="4a01b-116">You can achieve the player/insights view and synchronization in your application.</span><span class="sxs-lookup"><span data-stu-id="4a01b-116">You can achieve the player/insights view and synchronization in your application.</span></span> <span data-ttu-id="4a01b-117">For more information, see [Embed Azure Indexer widgets into your application](video-indexer-embed-widgets.md).</span><span class="sxs-lookup"><span data-stu-id="4a01b-117">For more information, see [Embed Azure Indexer widgets into your application](video-indexer-embed-widgets.md).</span></span> 

3. <span data-ttu-id="4a01b-118">Edit the Video Indexer insights.</span><span class="sxs-lookup"><span data-stu-id="4a01b-118">Edit the Video Indexer insights.</span></span>

    <span data-ttu-id="4a01b-119">Press Edit under the video.</span><span class="sxs-lookup"><span data-stu-id="4a01b-119">Press Edit under the video.</span></span> <span data-ttu-id="4a01b-120">The page that shows you the full breakdown of a video is displayed.</span><span class="sxs-lookup"><span data-stu-id="4a01b-120">The page that shows you the full breakdown of a video is displayed.</span></span> <span data-ttu-id="4a01b-121">The breakdown is broken into blocks.</span><span class="sxs-lookup"><span data-stu-id="4a01b-121">The breakdown is broken into blocks.</span></span> <span data-ttu-id="4a01b-122">Blocks are here to make it easier to go through the data.</span><span class="sxs-lookup"><span data-stu-id="4a01b-122">Blocks are here to make it easier to go through the data.</span></span> <span data-ttu-id="4a01b-123">For example, block might be broken down based on when speakers change or there is a long pause.</span><span class="sxs-lookup"><span data-stu-id="4a01b-123">For example, block might be broken down based on when speakers change or there is a long pause.</span></span> <span data-ttu-id="4a01b-124">You can create your own playlist that contains only lines that you want.</span><span class="sxs-lookup"><span data-stu-id="4a01b-124">You can create your own playlist that contains only lines that you want.</span></span> <span data-ttu-id="4a01b-125">To show only specific parts of the source video, you can filter by topics/keywords, sentiments, people, speakers.</span><span class="sxs-lookup"><span data-stu-id="4a01b-125">To show only specific parts of the source video, you can filter by topics/keywords, sentiments, people, speakers.</span></span> <span data-ttu-id="4a01b-126">You can choose to only view the video's transcript or OCR.</span><span class="sxs-lookup"><span data-stu-id="4a01b-126">You can choose to only view the video's transcript or OCR.</span></span>  

    ![Insights](./media/video-indexer-view-edit/video-indexer-create-new-playlist.png)

## <a name="next-steps"></a><span data-ttu-id="4a01b-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="4a01b-128">Next steps</span></span>

<span data-ttu-id="4a01b-129">[Learn how to create your own Video Indexer insights based on some other video](video-indexer-create-new.md).</span><span class="sxs-lookup"><span data-stu-id="4a01b-129">[Learn how to create your own Video Indexer insights based on some other video](video-indexer-create-new.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4a01b-130">See also</span><span class="sxs-lookup"><span data-stu-id="4a01b-130">See also</span></span>

[<span data-ttu-id="4a01b-131">Video Indexer overview</span><span class="sxs-lookup"><span data-stu-id="4a01b-131">Video Indexer overview</span></span>](video-indexer-overview.md)

