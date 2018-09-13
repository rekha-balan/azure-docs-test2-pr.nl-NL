---
title: How to view the Azure Maps API usage | Microsoft Docs
description: Learn how to view the metrics for your Azure Maps API calls in the portal.
author: dsk-2015
ms.author: dkshir
ms.date: 08/06/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: e62d2ff1fdd6bc94244511a2de95c4268a58d6f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856999"
---
# <a name="how-to-view-the-azure-maps-api-usage"></a><span data-ttu-id="e6391-103">How to view the Azure Maps API usage</span><span class="sxs-lookup"><span data-stu-id="e6391-103">How to view the Azure Maps API usage</span></span>
<span data-ttu-id="e6391-104">This article shows you how to view the API usage metrics for your Azure Maps account in the [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6391-104">This article shows you how to view the API usage metrics for your Azure Maps account in the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="e6391-105">The metrics are shown in a convenient graph format along a customizable time duration.</span><span class="sxs-lookup"><span data-stu-id="e6391-105">The metrics are shown in a convenient graph format along a customizable time duration.</span></span> 

## <a name="view-metric-snapshot"></a><span data-ttu-id="e6391-106">View metric snapshot</span><span class="sxs-lookup"><span data-stu-id="e6391-106">View metric snapshot</span></span> 

<span data-ttu-id="e6391-107">You can see some common metrics on the **Overview** page of your Maps account.</span><span class="sxs-lookup"><span data-stu-id="e6391-107">You can see some common metrics on the **Overview** page of your Maps account.</span></span> <span data-ttu-id="e6391-108">It currently shows *Total Requests*, *Total Errors*, and *Availability* over a selectable time duration.</span><span class="sxs-lookup"><span data-stu-id="e6391-108">It currently shows *Total Requests*, *Total Errors*, and *Availability* over a selectable time duration.</span></span> 

![Azure Maps Metrics Overview](media/how-to-view-api-usage/portal-overview.png)

<span data-ttu-id="e6391-110">Continue to the next section if you need to customize these graphs for your particular analysis.</span><span class="sxs-lookup"><span data-stu-id="e6391-110">Continue to the next section if you need to customize these graphs for your particular analysis.</span></span>


## <a name="view-detailed-metrics"></a><span data-ttu-id="e6391-111">View detailed metrics</span><span class="sxs-lookup"><span data-stu-id="e6391-111">View detailed metrics</span></span>

1. <span data-ttu-id="e6391-112">Sign in to your Azure subscription in the [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6391-112">Sign in to your Azure subscription in the [portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="e6391-113">Click the **All resources** menu item on the left-hand side and navigate to your *Azure Maps Account*.</span><span class="sxs-lookup"><span data-stu-id="e6391-113">Click the **All resources** menu item on the left-hand side and navigate to your *Azure Maps Account*.</span></span>

3. <span data-ttu-id="e6391-114">Once your Maps account is open, click on the **Metrics** menu on the left.</span><span class="sxs-lookup"><span data-stu-id="e6391-114">Once your Maps account is open, click on the **Metrics** menu on the left.</span></span>

4. <span data-ttu-id="e6391-115">On the **Metrics** pane, choose between one of the following:</span><span class="sxs-lookup"><span data-stu-id="e6391-115">On the **Metrics** pane, choose between one of the following:</span></span>

    1. <span data-ttu-id="e6391-116">**Availability**, which shows the *Average* of API availability over a period of time, or</span><span class="sxs-lookup"><span data-stu-id="e6391-116">**Availability**, which shows the *Average* of API availability over a period of time, or</span></span> 
    2. <span data-ttu-id="e6391-117">**Usage**, which shows how the usage *Count* for your account.</span><span class="sxs-lookup"><span data-stu-id="e6391-117">**Usage**, which shows how the usage *Count* for your account.</span></span> 

    ![Azure Maps Metrics pane](media/how-to-view-api-usage/portal-metrics.png)

5. <span data-ttu-id="e6391-119">Once you have selected the metrics, you may select the *Time range* by selecting on the **Last 12 hours (Automatic)** which is the default value.</span><span class="sxs-lookup"><span data-stu-id="e6391-119">Once you have selected the metrics, you may select the *Time range* by selecting on the **Last 12 hours (Automatic)** which is the default value.</span></span> <span data-ttu-id="e6391-120">You may also select the *Time granularity*, as well as choose to show the time as *local* or *GMT* in the same drop-down.</span><span class="sxs-lookup"><span data-stu-id="e6391-120">You may also select the *Time granularity*, as well as choose to show the time as *local* or *GMT* in the same drop-down.</span></span> <span data-ttu-id="e6391-121">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="e6391-121">Click **Apply**.</span></span>

    ![Azure Maps Metrics Time range](media/how-to-view-api-usage/time-range.png)
 
6. <span data-ttu-id="e6391-123">Once you add your metric, you can then **Add filter** from amongst the properties relevant to that metric, and then select the value of the property that you want to see the graph for.</span><span class="sxs-lookup"><span data-stu-id="e6391-123">Once you add your metric, you can then **Add filter** from amongst the properties relevant to that metric, and then select the value of the property that you want to see the graph for.</span></span> 

    ![Azure Maps Metrics Filter](media/how-to-view-api-usage/filter.png)

7. <span data-ttu-id="e6391-125">You may also **Apply splitting** for your metric based on your selected metric property.</span><span class="sxs-lookup"><span data-stu-id="e6391-125">You may also **Apply splitting** for your metric based on your selected metric property.</span></span> <span data-ttu-id="e6391-126">This allows the graph to be split into multiple graphs, one each for each value of that property.</span><span class="sxs-lookup"><span data-stu-id="e6391-126">This allows the graph to be split into multiple graphs, one each for each value of that property.</span></span> <span data-ttu-id="e6391-127">For example, in the following picture, the color of each graph corresponds to the property value shown at the bottom of the graph.</span><span class="sxs-lookup"><span data-stu-id="e6391-127">For example, in the following picture, the color of each graph corresponds to the property value shown at the bottom of the graph.</span></span>

    ![Azure Maps Metrics Splitting](media/how-to-view-api-usage/splitting.png)
 
8. <span data-ttu-id="e6391-129">You may also observe multiple metrics on the same graph, simply by clicking on the **Add metric** button on top.</span><span class="sxs-lookup"><span data-stu-id="e6391-129">You may also observe multiple metrics on the same graph, simply by clicking on the **Add metric** button on top.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e6391-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6391-130">Next steps</span></span>

<span data-ttu-id="e6391-131">Now that you have learned how to track your Azure Maps usage, you may proceed to read more about the APIs you are using with the:</span><span class="sxs-lookup"><span data-stu-id="e6391-131">Now that you have learned how to track your Azure Maps usage, you may proceed to read more about the APIs you are using with the:</span></span>

* [<span data-ttu-id="e6391-132">Azure Maps REST API documentation</span><span class="sxs-lookup"><span data-stu-id="e6391-132">Azure Maps REST API documentation</span></span>](https://docs.microsoft.com/rest/api/maps)
