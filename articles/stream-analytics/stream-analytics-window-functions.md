---
title: Introduction to Stream Analytics Window functions | Microsoft Docs
description: Learn about the three Window functions in Stream Analytics (tumbling, hopping, sliding).
keywords: tumbling window, sliding window, hopping window
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 762e23828d556fa0cfc15e284eb6d73d66afc336
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548912"
---
# <a name="introduction-to-stream-analytics-window-functions"></a><span data-ttu-id="98dc8-104">Introduction to Stream Analytics Window functions</span><span class="sxs-lookup"><span data-stu-id="98dc8-104">Introduction to Stream Analytics Window functions</span></span>
<span data-ttu-id="98dc8-105">In many real time streaming scenarios, it is necessary to perform operations only on the data contained in temporal windows.</span><span class="sxs-lookup"><span data-stu-id="98dc8-105">In many real time streaming scenarios, it is necessary to perform operations only on the data contained in temporal windows.</span></span> <span data-ttu-id="98dc8-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves the needle on developer productivity in authoring complex stream processing jobs.</span><span class="sxs-lookup"><span data-stu-id="98dc8-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves the needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="98dc8-107">Stream Analytics enables developers to use [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows to perform temporal operations on streaming data.</span><span class="sxs-lookup"><span data-stu-id="98dc8-107">Stream Analytics enables developers to use [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows to perform temporal operations on streaming data.</span></span> <span data-ttu-id="98dc8-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at the **end** of the window.</span><span class="sxs-lookup"><span data-stu-id="98dc8-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at the **end** of the window.</span></span> <span data-ttu-id="98dc8-109">The output of the window will be single event based on the aggregate function used.</span><span class="sxs-lookup"><span data-stu-id="98dc8-109">The output of the window will be single event based on the aggregate function used.</span></span> <span data-ttu-id="98dc8-110">The event will have the time stamp of the end of the window and all Window functions are defined with a fixed length.</span><span class="sxs-lookup"><span data-stu-id="98dc8-110">The event will have the time stamp of the end of the window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="98dc8-111">Lastly it is important to note that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span><span class="sxs-lookup"><span data-stu-id="98dc8-111">Lastly it is important to note that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Stream Analytics Window functions concepts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="98dc8-113">Tumbling Window</span><span class="sxs-lookup"><span data-stu-id="98dc8-113">Tumbling Window</span></span>
<span data-ttu-id="98dc8-114">Tumbling window functions are used to segment a data stream into distinct time segments and perform a function against them, such as the example below.</span><span class="sxs-lookup"><span data-stu-id="98dc8-114">Tumbling window functions are used to segment a data stream into distinct time segments and perform a function against them, such as the example below.</span></span> <span data-ttu-id="98dc8-115">The key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong to more than one tumbling window.</span><span class="sxs-lookup"><span data-stu-id="98dc8-115">The key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong to more than one tumbling window.</span></span>

![Stream Analytics Window functions tumbling intro](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="98dc8-117">Hopping Window</span><span class="sxs-lookup"><span data-stu-id="98dc8-117">Hopping Window</span></span>
<span data-ttu-id="98dc8-118">Hopping window functions hop forward in time by a fixed period.</span><span class="sxs-lookup"><span data-stu-id="98dc8-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="98dc8-119">It may be easy to think of them as Tumbling windows that can overlap, so events can belong to more than one Hopping window result set.</span><span class="sxs-lookup"><span data-stu-id="98dc8-119">It may be easy to think of them as Tumbling windows that can overlap, so events can belong to more than one Hopping window result set.</span></span> <span data-ttu-id="98dc8-120">To make a Hopping window the same as a Tumbling window one would simply specify the hop size to be the same as the window size.</span><span class="sxs-lookup"><span data-stu-id="98dc8-120">To make a Hopping window the same as a Tumbling window one would simply specify the hop size to be the same as the window size.</span></span> 

![Stream Analytics Window functions hopping intro](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="98dc8-122">Sliding Window</span><span class="sxs-lookup"><span data-stu-id="98dc8-122">Sliding Window</span></span>
<span data-ttu-id="98dc8-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span><span class="sxs-lookup"><span data-stu-id="98dc8-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="98dc8-124">Every window will have at least one event and the window continuously moves forward by an € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="98dc8-124">Every window will have at least one event and the window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="98dc8-125">Like Hopping Windows, events can belong to more than one Sliding Window.</span><span class="sxs-lookup"><span data-stu-id="98dc8-125">Like Hopping Windows, events can belong to more than one Sliding Window.</span></span>

![Stream Analytics Window functions sliding intro](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="98dc8-127">Getting help with Window functions</span><span class="sxs-lookup"><span data-stu-id="98dc8-127">Getting help with Window functions</span></span>
<span data-ttu-id="98dc8-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="98dc8-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="98dc8-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="98dc8-129">Next steps</span></span>
* [<span data-ttu-id="98dc8-130">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="98dc8-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="98dc8-131">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="98dc8-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="98dc8-132">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="98dc8-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="98dc8-133">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="98dc8-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="98dc8-134">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="98dc8-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)





