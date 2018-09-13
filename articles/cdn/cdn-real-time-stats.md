---
title: Real-time stats in Azure CDN | Microsoft Docs
description: Real-time statistics provides real-time data about the performance of Azure CDN when delivering content to your clients.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808254"
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="4839e-103">Real-time stats in Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4839e-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="4839e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4839e-104">Overview</span></span>
<span data-ttu-id="4839e-105">This document explains real-time stats in Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="4839e-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="4839e-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span><span class="sxs-lookup"><span data-stu-id="4839e-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="4839e-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span><span class="sxs-lookup"><span data-stu-id="4839e-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="4839e-108">The following graphs are available:</span><span class="sxs-lookup"><span data-stu-id="4839e-108">The following graphs are available:</span></span>

* [<span data-ttu-id="4839e-109">Bandwidth</span><span class="sxs-lookup"><span data-stu-id="4839e-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="4839e-110">Status Codes</span><span class="sxs-lookup"><span data-stu-id="4839e-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="4839e-111">Cache Statuses</span><span class="sxs-lookup"><span data-stu-id="4839e-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="4839e-112">Connections</span><span class="sxs-lookup"><span data-stu-id="4839e-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="4839e-113">Accessing real-time stats</span><span class="sxs-lookup"><span data-stu-id="4839e-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="4839e-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="4839e-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![CDN profile blade](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="4839e-116">From the CDN profile blade, click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="4839e-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN profile blade manage button](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="4839e-118">The CDN management portal opens.</span><span class="sxs-lookup"><span data-stu-id="4839e-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="4839e-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span><span class="sxs-lookup"><span data-stu-id="4839e-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="4839e-120">Click on **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="4839e-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN management portal](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="4839e-122">The real-time stats graphs are displayed.</span><span class="sxs-lookup"><span data-stu-id="4839e-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="4839e-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span><span class="sxs-lookup"><span data-stu-id="4839e-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="4839e-124">The graphs update automatically every few seconds.</span><span class="sxs-lookup"><span data-stu-id="4839e-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="4839e-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span><span class="sxs-lookup"><span data-stu-id="4839e-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="4839e-126">Bandwidth</span><span class="sxs-lookup"><span data-stu-id="4839e-126">Bandwidth</span></span>
![Bandwidth graph](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="4839e-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span><span class="sxs-lookup"><span data-stu-id="4839e-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="4839e-129">The shaded portion of the graph indicates bandwidth usage.</span><span class="sxs-lookup"><span data-stu-id="4839e-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="4839e-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span><span class="sxs-lookup"><span data-stu-id="4839e-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="4839e-131">Status Codes</span><span class="sxs-lookup"><span data-stu-id="4839e-131">Status Codes</span></span>
![Status code graph](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="4839e-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span><span class="sxs-lookup"><span data-stu-id="4839e-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="4839e-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="4839e-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="4839e-135">A list of HTTP status codes is displayed directly above the graph.</span><span class="sxs-lookup"><span data-stu-id="4839e-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="4839e-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span><span class="sxs-lookup"><span data-stu-id="4839e-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="4839e-137">By default, a line is displayed for each of these status codes in the graph.</span><span class="sxs-lookup"><span data-stu-id="4839e-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="4839e-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span><span class="sxs-lookup"><span data-stu-id="4839e-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="4839e-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span><span class="sxs-lookup"><span data-stu-id="4839e-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="4839e-140">You can temporarily hide logged data for a particular status code.</span><span class="sxs-lookup"><span data-stu-id="4839e-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="4839e-141">From the legend directly below the graph, click the status code you want to hide.</span><span class="sxs-lookup"><span data-stu-id="4839e-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="4839e-142">The status code will be immediately hidden from the graph.</span><span class="sxs-lookup"><span data-stu-id="4839e-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="4839e-143">Clicking that status code again will cause that option to be displayed again.</span><span class="sxs-lookup"><span data-stu-id="4839e-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="4839e-144">Cache Statuses</span><span class="sxs-lookup"><span data-stu-id="4839e-144">Cache Statuses</span></span>
![Cache Statuses graph](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="4839e-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span><span class="sxs-lookup"><span data-stu-id="4839e-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="4839e-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="4839e-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="4839e-148">A list of cache status codes is displayed directly above the graph.</span><span class="sxs-lookup"><span data-stu-id="4839e-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="4839e-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span><span class="sxs-lookup"><span data-stu-id="4839e-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="4839e-150">By default, a line is displayed for each of these status codes in the graph.</span><span class="sxs-lookup"><span data-stu-id="4839e-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="4839e-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span><span class="sxs-lookup"><span data-stu-id="4839e-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="4839e-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span><span class="sxs-lookup"><span data-stu-id="4839e-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="4839e-153">You can temporarily hide logged data for a particular status code.</span><span class="sxs-lookup"><span data-stu-id="4839e-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="4839e-154">From the legend directly below the graph, click the status code you want to hide.</span><span class="sxs-lookup"><span data-stu-id="4839e-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="4839e-155">The status code will be immediately hidden from the graph.</span><span class="sxs-lookup"><span data-stu-id="4839e-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="4839e-156">Clicking that status code again will cause that option to be displayed again.</span><span class="sxs-lookup"><span data-stu-id="4839e-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="4839e-157">Connections</span><span class="sxs-lookup"><span data-stu-id="4839e-157">Connections</span></span>
![Connections graph](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="4839e-159">This graph indicates how many connections have been established to your edge servers.</span><span class="sxs-lookup"><span data-stu-id="4839e-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="4839e-160">Each request for an asset that passes through our CDN results in a connection.</span><span class="sxs-lookup"><span data-stu-id="4839e-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4839e-161">Next Steps</span><span class="sxs-lookup"><span data-stu-id="4839e-161">Next Steps</span></span>
* <span data-ttu-id="4839e-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="4839e-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="4839e-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="4839e-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="4839e-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="4839e-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

