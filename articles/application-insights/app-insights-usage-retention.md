---
title: User retention analysis for web applications with Azure Application Insights | Microsoft docs
description: How many users return to your app?
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 05/03/2017
ms.author: mbullwin
ms.openlocfilehash: 6e042034d52551d58e290b54ca3547dedbc89c47
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865149"
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="c0828-103">User retention analysis for web applications with Application Insights</span><span class="sxs-lookup"><span data-stu-id="c0828-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="c0828-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span><span class="sxs-lookup"><span data-stu-id="c0828-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="c0828-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span><span class="sxs-lookup"><span data-stu-id="c0828-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="c0828-106">This knowledge can help you improve both your user experience and your business strategy.</span><span class="sxs-lookup"><span data-stu-id="c0828-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="c0828-107">Get started</span><span class="sxs-lookup"><span data-stu-id="c0828-107">Get started</span></span>

<span data-ttu-id="c0828-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0828-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="c0828-109">The Retention tool</span><span class="sxs-lookup"><span data-stu-id="c0828-109">The Retention tool</span></span>

![Retention tool](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="c0828-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span><span class="sxs-lookup"><span data-stu-id="c0828-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="c0828-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span><span class="sxs-lookup"><span data-stu-id="c0828-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="c0828-113">You can select different combination of events to narrow the focus on specific user activities.</span><span class="sxs-lookup"><span data-stu-id="c0828-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="c0828-114">Add one or more filters on properties.</span><span class="sxs-lookup"><span data-stu-id="c0828-114">Add one or more filters on properties.</span></span> <span data-ttu-id="c0828-115">For example, you can focus on users in a particular country or region.</span><span class="sxs-lookup"><span data-stu-id="c0828-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="c0828-116">Click **Update** after setting the filters.</span><span class="sxs-lookup"><span data-stu-id="c0828-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="c0828-117">The overall retention chart shows a summary of user retention across the selected time period.</span><span class="sxs-lookup"><span data-stu-id="c0828-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="c0828-118">The grid shows the number of users retained according to the query builder in #2.</span><span class="sxs-lookup"><span data-stu-id="c0828-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="c0828-119">Each row represents a cohort of users who performed any event in the time period shown.</span><span class="sxs-lookup"><span data-stu-id="c0828-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="c0828-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span><span class="sxs-lookup"><span data-stu-id="c0828-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="c0828-121">Some users may return in more than one period.</span><span class="sxs-lookup"><span data-stu-id="c0828-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="c0828-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span><span class="sxs-lookup"><span data-stu-id="c0828-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![Retention mouse hover](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="c0828-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span><span class="sxs-lookup"><span data-stu-id="c0828-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="c0828-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span><span class="sxs-lookup"><span data-stu-id="c0828-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="c0828-126">Use business events to track retention</span><span class="sxs-lookup"><span data-stu-id="c0828-126">Use business events to track retention</span></span>

<span data-ttu-id="c0828-127">To get the most useful retention analysis, measure events that represent significant business activities.</span><span class="sxs-lookup"><span data-stu-id="c0828-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="c0828-128">For example, many users might open a page in your app without playing the game that it displays.</span><span class="sxs-lookup"><span data-stu-id="c0828-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="c0828-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span><span class="sxs-lookup"><span data-stu-id="c0828-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="c0828-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span><span class="sxs-lookup"><span data-stu-id="c0828-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="c0828-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span><span class="sxs-lookup"><span data-stu-id="c0828-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="c0828-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c0828-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="c0828-133">If you write it in the web page code or in Node.JS, it looks like this:</span><span class="sxs-lookup"><span data-stu-id="c0828-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="c0828-134">Or in ASP.NET server code:</span><span class="sxs-lookup"><span data-stu-id="c0828-134">Or in ASP.NET server code:</span></span>

```csharp
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="c0828-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="c0828-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0828-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0828-136">Next steps</span></span>
- <span data-ttu-id="c0828-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="c0828-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="c0828-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span><span class="sxs-lookup"><span data-stu-id="c0828-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="c0828-139">Users, Sessions, Events</span><span class="sxs-lookup"><span data-stu-id="c0828-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="c0828-140">Funnels</span><span class="sxs-lookup"><span data-stu-id="c0828-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="c0828-141">User Flows</span><span class="sxs-lookup"><span data-stu-id="c0828-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="c0828-142">Workbooks</span><span class="sxs-lookup"><span data-stu-id="c0828-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="c0828-143">Add user context</span><span class="sxs-lookup"><span data-stu-id="c0828-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


