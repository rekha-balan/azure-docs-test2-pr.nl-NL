---
title: Azure Video Indexer concepts | Microsoft Docs
description: This topic describes some concepts of the Video Indexer service.
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 07/31/2018
ms.author: juliako
ms.openlocfilehash: 224c8b05027f51fb99c8d58be34c3604032c0f77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868074"
---
# <a name="video-indexer-concepts"></a><span data-ttu-id="83210-103">Video Indexer concepts</span><span class="sxs-lookup"><span data-stu-id="83210-103">Video Indexer concepts</span></span>
 
<span data-ttu-id="83210-104">This topic describes some concepts of the Video Indexer service.</span><span class="sxs-lookup"><span data-stu-id="83210-104">This topic describes some concepts of the Video Indexer service.</span></span>
    
## <a name="summarized-insights"></a><span data-ttu-id="83210-105">Summarized insights</span><span class="sxs-lookup"><span data-stu-id="83210-105">Summarized insights</span></span>

<span data-ttu-id="83210-106">Summarized insights contain an aggregated view of the data: faces, keywords, sentiments.</span><span class="sxs-lookup"><span data-stu-id="83210-106">Summarized insights contain an aggregated view of the data: faces, keywords, sentiments.</span></span> <span data-ttu-id="83210-107">For example, instead of going over each of the thousands of time ranges and checking which faces are in it, the summarized insights contains all the faces and for each one, the time ranges it appears in and the % of the time it is shown.</span><span class="sxs-lookup"><span data-stu-id="83210-107">For example, instead of going over each of the thousands of time ranges and checking which faces are in it, the summarized insights contains all the faces and for each one, the time ranges it appears in and the % of the time it is shown.</span></span>

## <a name="topicskeywords"></a><span data-ttu-id="83210-108">Topics/keywords</span><span class="sxs-lookup"><span data-stu-id="83210-108">Topics/keywords</span></span>

<span data-ttu-id="83210-109">Topics/keywords are in the list of key phrases that Video Indexer extracts from the text.</span><span class="sxs-lookup"><span data-stu-id="83210-109">Topics/keywords are in the list of key phrases that Video Indexer extracts from the text.</span></span> <span data-ttu-id="83210-110">For example, a Scott Guthrie video might contain the following topics/keywords: Security, Azure, Microsoft Cloud, Revenue.</span><span class="sxs-lookup"><span data-stu-id="83210-110">For example, a Scott Guthrie video might contain the following topics/keywords: Security, Azure, Microsoft Cloud, Revenue.</span></span>

## <a name="sentiments"></a><span data-ttu-id="83210-111">Sentiments</span><span class="sxs-lookup"><span data-stu-id="83210-111">Sentiments</span></span>

<span data-ttu-id="83210-112">When Video Indexer analyzes transcripts, it detects sentiments as well.</span><span class="sxs-lookup"><span data-stu-id="83210-112">When Video Indexer analyzes transcripts, it detects sentiments as well.</span></span> <span data-ttu-id="83210-113">For example, "this is a very exciting event" is a positive sentiment.</span><span class="sxs-lookup"><span data-stu-id="83210-113">For example, "this is a very exciting event" is a positive sentiment.</span></span>

## <a name="time-range-vs-adjusted-time-range"></a><span data-ttu-id="83210-114">time range vs. adjusted time range</span><span class="sxs-lookup"><span data-stu-id="83210-114">time range vs. adjusted time range</span></span>

<span data-ttu-id="83210-115">TimeRange is the time range in the original video.</span><span class="sxs-lookup"><span data-stu-id="83210-115">TimeRange is the time range in the original video.</span></span> <span data-ttu-id="83210-116">AdjustedTimeRange is the time range relative to the current playlist.</span><span class="sxs-lookup"><span data-stu-id="83210-116">AdjustedTimeRange is the time range relative to the current playlist.</span></span> <span data-ttu-id="83210-117">Since you can create a playlist from different lines of different videos, you can take a 1-hour video and use just 1 line from it, for example, 10:00-10:15.</span><span class="sxs-lookup"><span data-stu-id="83210-117">Since you can create a playlist from different lines of different videos, you can take a 1-hour video and use just 1 line from it, for example, 10:00-10:15.</span></span> <span data-ttu-id="83210-118">In that case, you will have a playlist with 1 line, where the time range is 10:00-10:15 but the adjustedTimeRange is 00:00-00:15.</span><span class="sxs-lookup"><span data-stu-id="83210-118">In that case, you will have a playlist with 1 line, where the time range is 10:00-10:15 but the adjustedTimeRange is 00:00-00:15.</span></span>
 
## <a name="blocks"></a><span data-ttu-id="83210-119">Blocks</span><span class="sxs-lookup"><span data-stu-id="83210-119">Blocks</span></span>

<span data-ttu-id="83210-120">Blocks are meant to make it easier to go through the data.</span><span class="sxs-lookup"><span data-stu-id="83210-120">Blocks are meant to make it easier to go through the data.</span></span> <span data-ttu-id="83210-121">For example, block might be broken down based on when speakers change or there is a long pause.</span><span class="sxs-lookup"><span data-stu-id="83210-121">For example, block might be broken down based on when speakers change or there is a long pause.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83210-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="83210-122">Next steps</span></span>

<span data-ttu-id="83210-123">For information about how to get started, see [How to sign up and upload your first video](video-indexer-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83210-123">For information about how to get started, see [How to sign up and upload your first video](video-indexer-get-started.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="83210-124">See also</span><span class="sxs-lookup"><span data-stu-id="83210-124">See also</span></span>

[<span data-ttu-id="83210-125">Video Indexer overview</span><span class="sxs-lookup"><span data-stu-id="83210-125">Video Indexer overview</span></span>](video-indexer-overview.md)
