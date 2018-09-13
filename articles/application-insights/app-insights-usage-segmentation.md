---
title: User, session, and event analysis in Azure Application Insights | Microsoft docs
description: Demographic analysis of users of your web app.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 01/24/2018
ms.reviewer: daviste
ms.author: mbullwin
ms.openlocfilehash: 2bc10a292855832b7ddb9b8e3a59fbe0f17d8dc6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869870"
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="3d511-103">Users, sessions, and events analysis in Application Insights</span><span class="sxs-lookup"><span data-stu-id="3d511-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="3d511-104">Find out when people use your web app, what pages they're most interested in, where your users are located, and what browsers and operating systems they use.</span><span class="sxs-lookup"><span data-stu-id="3d511-104">Find out when people use your web app, what pages they're most interested in, where your users are located, and what browsers and operating systems they use.</span></span> <span data-ttu-id="3d511-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d511-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

![Screenshot of Application Insights Users](./media/app-insights-usage-segmentation/0001-users.png)

## <a name="get-started"></a><span data-ttu-id="3d511-107">Get started</span><span class="sxs-lookup"><span data-stu-id="3d511-107">Get started</span></span>

<span data-ttu-id="3d511-108">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d511-108">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="3d511-109">The Users, Sessions, and Events segmentation tool</span><span class="sxs-lookup"><span data-stu-id="3d511-109">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="3d511-110">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span><span class="sxs-lookup"><span data-stu-id="3d511-110">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="3d511-111">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span><span class="sxs-lookup"><span data-stu-id="3d511-111">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="3d511-112">**Users tool**: How many people used your app and its features.</span><span class="sxs-lookup"><span data-stu-id="3d511-112">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="3d511-113">Users are counted by using anonymous IDs stored in browser cookies.</span><span class="sxs-lookup"><span data-stu-id="3d511-113">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="3d511-114">A single person using different browsers or machines will be counted as more than one user.</span><span class="sxs-lookup"><span data-stu-id="3d511-114">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="3d511-115">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span><span class="sxs-lookup"><span data-stu-id="3d511-115">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="3d511-116">A session is counted after half an hour of user inactivity, or after 24 hours of continuous use.</span><span class="sxs-lookup"><span data-stu-id="3d511-116">A session is counted after half an hour of user inactivity, or after 24 hours of continuous use.</span></span>
* <span data-ttu-id="3d511-117">**Events tool**: How often certain pages and features of your app are used.</span><span class="sxs-lookup"><span data-stu-id="3d511-117">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="3d511-118">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="3d511-118">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="3d511-119">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span><span class="sxs-lookup"><span data-stu-id="3d511-119">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="3d511-120">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="3d511-120">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

## <a name="querying-for-certain-users"></a><span data-ttu-id="3d511-121">Querying for certain users</span><span class="sxs-lookup"><span data-stu-id="3d511-121">Querying for certain users</span></span>

<span data-ttu-id="3d511-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span><span class="sxs-lookup"><span data-stu-id="3d511-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span>

* <span data-ttu-id="3d511-123">Show: Choose a cohort of users to analyze.</span><span class="sxs-lookup"><span data-stu-id="3d511-123">Show: Choose a cohort of users to analyze.</span></span>
* <span data-ttu-id="3d511-124">Who used: Choose custom events and page views.</span><span class="sxs-lookup"><span data-stu-id="3d511-124">Who used: Choose custom events and page views.</span></span>
* <span data-ttu-id="3d511-125">During: Choose a time range.</span><span class="sxs-lookup"><span data-stu-id="3d511-125">During: Choose a time range.</span></span>
* <span data-ttu-id="3d511-126">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span><span class="sxs-lookup"><span data-stu-id="3d511-126">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span>
* <span data-ttu-id="3d511-127">Split By: Choose a property by which to split or segment the data.</span><span class="sxs-lookup"><span data-stu-id="3d511-127">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="3d511-128">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span><span class="sxs-lookup"><span data-stu-id="3d511-128">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="3d511-129">Saving and sharing reports</span><span class="sxs-lookup"><span data-stu-id="3d511-129">Saving and sharing reports</span></span> 
<span data-ttu-id="3d511-130">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span><span class="sxs-lookup"><span data-stu-id="3d511-130">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>

<span data-ttu-id="3d511-131">To share a link to a Users, Sessions, or Events report; click **Share** in the toolbar, then copy the link.</span><span class="sxs-lookup"><span data-stu-id="3d511-131">To share a link to a Users, Sessions, or Events report; click **Share** in the toolbar, then copy the link.</span></span>

<span data-ttu-id="3d511-132">To share a copy of the data in a Users, Sessions, or Events report; click **Share** in the toolbar, then click the **Word icon** to create a Word document with the data.</span><span class="sxs-lookup"><span data-stu-id="3d511-132">To share a copy of the data in a Users, Sessions, or Events report; click **Share** in the toolbar, then click the **Word icon** to create a Word document with the data.</span></span> <span data-ttu-id="3d511-133">Or, click the **Word icon** above the main chart.</span><span class="sxs-lookup"><span data-stu-id="3d511-133">Or, click the **Word icon** above the main chart.</span></span>

## <a name="meet-your-users"></a><span data-ttu-id="3d511-134">Meet your users</span><span class="sxs-lookup"><span data-stu-id="3d511-134">Meet your users</span></span>

<span data-ttu-id="3d511-135">The **Meet your users** section shows information about five sample users matched by the current query.</span><span class="sxs-lookup"><span data-stu-id="3d511-135">The **Meet your users** section shows information about five sample users matched by the current query.</span></span> <span data-ttu-id="3d511-136">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span><span class="sxs-lookup"><span data-stu-id="3d511-136">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d511-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d511-137">Next steps</span></span>

- <span data-ttu-id="3d511-138">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="3d511-138">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="3d511-139">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span><span class="sxs-lookup"><span data-stu-id="3d511-139">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="3d511-140">Funnels</span><span class="sxs-lookup"><span data-stu-id="3d511-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="3d511-141">Retention</span><span class="sxs-lookup"><span data-stu-id="3d511-141">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="3d511-142">User Flows</span><span class="sxs-lookup"><span data-stu-id="3d511-142">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="3d511-143">Workbooks</span><span class="sxs-lookup"><span data-stu-id="3d511-143">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="3d511-144">Add user context</span><span class="sxs-lookup"><span data-stu-id="3d511-144">Add user context</span></span>](app-insights-usage-send-user-context.md)