---
title: Azure Application Insights Usage Impact | Microsoft docs
description: Analyze how different properties potentially impact conversion rates for parts of your apps.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 01/25/2018
ms.reviewer: daviste
ms.author: mbullwin
ms.openlocfilehash: 9188776fdd213f01523069b08bd898f48bee57a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867731"
---
# <a name="impact-analysis-with-application-insights"></a><span data-ttu-id="8bf0d-103">Impact analysis with Application Insights</span><span class="sxs-lookup"><span data-stu-id="8bf0d-103">Impact analysis with Application Insights</span></span>

<span data-ttu-id="8bf0d-104">Impact analyzes how load times and other properties influence conversion rates for various parts of your app.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-104">Impact analyzes how load times and other properties influence conversion rates for various parts of your app.</span></span> <span data-ttu-id="8bf0d-105">To put it more precisely, it discovers how **any dimension** of a **page view**, **custom event**, or **request** affects the usage of a different **page view** or **custom event**.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-105">To put it more precisely, it discovers how **any dimension** of a **page view**, **custom event**, or **request** affects the usage of a different **page view** or **custom event**.</span></span> 

![Impact tool](./media/app-insights-usage-impact/0001-impact.png)

## <a name="still-not-sure-what-impact-does"></a><span data-ttu-id="8bf0d-107">Still not sure what Impact does?</span><span class="sxs-lookup"><span data-stu-id="8bf0d-107">Still not sure what Impact does?</span></span>

<span data-ttu-id="8bf0d-108">One way to think of Impact is as the ultimate tool for settling arguments with someone on your team about how slowness in some aspect of your site is affecting whether users stick around.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-108">One way to think of Impact is as the ultimate tool for settling arguments with someone on your team about how slowness in some aspect of your site is affecting whether users stick around.</span></span> <span data-ttu-id="8bf0d-109">While users may tolerate a certain amount of slowness, Impact gives you insight into how best to balance optimization and performance to maximize user conversion.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-109">While users may tolerate a certain amount of slowness, Impact gives you insight into how best to balance optimization and performance to maximize user conversion.</span></span>

<span data-ttu-id="8bf0d-110">But analyzing performance is just a subset of Impact's capabilities.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-110">But analyzing performance is just a subset of Impact's capabilities.</span></span> <span data-ttu-id="8bf0d-111">Since Impact supports custom events and dimensions, answering questions like how does user browser choice correlate with different rates of conversion are just a few clicks away.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-111">Since Impact supports custom events and dimensions, answering questions like how does user browser choice correlate with different rates of conversion are just a few clicks away.</span></span>

![Screenshot conversion by browsers](./media/app-insights-usage-impact/0004-browsers.png)

> [!NOTE]
> <span data-ttu-id="8bf0d-113">Your Application Insights resource must contain page views or custom events to use the Impact tool.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-113">Your Application Insights resource must contain page views or custom events to use the Impact tool.</span></span> <span data-ttu-id="8bf0d-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="8bf0d-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span> <span data-ttu-id="8bf0d-115">Also keep in mind that since you are analyzing correlation, sample size matters.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-115">Also keep in mind that since you are analyzing correlation, sample size matters.</span></span>
>
>

## <a name="is-page-load-time-impacting-how-many-people-convert-on-my-page"></a><span data-ttu-id="8bf0d-116">Is page load time impacting how many people convert on my page?</span><span class="sxs-lookup"><span data-stu-id="8bf0d-116">Is page load time impacting how many people convert on my page?</span></span>

<span data-ttu-id="8bf0d-117">To begin answering questions with the Impact tool, choose an initial page view, custom event, or request.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-117">To begin answering questions with the Impact tool, choose an initial page view, custom event, or request.</span></span>

![Impact tool](./media/app-insights-usage-impact/0002-dropdown.png)

1. <span data-ttu-id="8bf0d-119">Select a page view from the **For the page view** dropdown.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-119">Select a page view from the **For the page view** dropdown.</span></span>
2. <span data-ttu-id="8bf0d-120">Leave the **analyze how its** dropdown on the default selection of **Duration** (In this context **Duration** is an alias for **Page Load Time**.)</span><span class="sxs-lookup"><span data-stu-id="8bf0d-120">Leave the **analyze how its** dropdown on the default selection of **Duration** (In this context **Duration** is an alias for **Page Load Time**.)</span></span>
3. <span data-ttu-id="8bf0d-121">For the **impacts the usage of** dropdown, select a custom event.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-121">For the **impacts the usage of** dropdown, select a custom event.</span></span> <span data-ttu-id="8bf0d-122">This event should correspond to a UI element on the page view you selected in step 1.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-122">This event should correspond to a UI element on the page view you selected in step 1.</span></span>

![Screenshot of results](./media/app-insights-usage-impact/0003-results.png)

<span data-ttu-id="8bf0d-124">In this instance as **Product Page** load time increases the conversion rate to **Purchase Product clicked** goes down.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-124">In this instance as **Product Page** load time increases the conversion rate to **Purchase Product clicked** goes down.</span></span> <span data-ttu-id="8bf0d-125">Based on the distribution above, an optimal page load duration of 3.5 seconds could be targeted to achieve a potential 55% conversion rate.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-125">Based on the distribution above, an optimal page load duration of 3.5 seconds could be targeted to achieve a potential 55% conversion rate.</span></span> <span data-ttu-id="8bf0d-126">Further performance improvements to reduce load time below 3.5 seconds do not currently correlate with additional conversion benefits.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-126">Further performance improvements to reduce load time below 3.5 seconds do not currently correlate with additional conversion benefits.</span></span>

## <a name="what-if-im-tracking-page-views-or-load-times-in-custom-ways"></a><span data-ttu-id="8bf0d-127">What if I’m tracking page views or load times in custom ways?</span><span class="sxs-lookup"><span data-stu-id="8bf0d-127">What if I’m tracking page views or load times in custom ways?</span></span>

<span data-ttu-id="8bf0d-128">Impact supports both standard and custom properties and measurements.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-128">Impact supports both standard and custom properties and measurements.</span></span> <span data-ttu-id="8bf0d-129">Use whatever you want.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-129">Use whatever you want.</span></span> <span data-ttu-id="8bf0d-130">Instead of duration, use filters on the primary and secondary events to get more specific.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-130">Instead of duration, use filters on the primary and secondary events to get more specific.</span></span>

## <a name="do-users-from-different-countries-or-regions-convert-at-different-rates"></a><span data-ttu-id="8bf0d-131">Do users from different countries or regions convert at different rates?</span><span class="sxs-lookup"><span data-stu-id="8bf0d-131">Do users from different countries or regions convert at different rates?</span></span>

1. <span data-ttu-id="8bf0d-132">Select a page view from the **For the page view** dropdown.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-132">Select a page view from the **For the page view** dropdown.</span></span>
2. <span data-ttu-id="8bf0d-133">Choose “Country or region” in **analyze how its** dropdown</span><span class="sxs-lookup"><span data-stu-id="8bf0d-133">Choose “Country or region” in **analyze how its** dropdown</span></span>
3. <span data-ttu-id="8bf0d-134">For the **impacts the usage of** dropdown, select a custom event that corresponds to a UI element on the page view you chose in step 1.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-134">For the **impacts the usage of** dropdown, select a custom event that corresponds to a UI element on the page view you chose in step 1.</span></span>

<span data-ttu-id="8bf0d-135">In this case, the results no longer fit into a continuous x-axis model as they did in the first example.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-135">In this case, the results no longer fit into a continuous x-axis model as they did in the first example.</span></span> <span data-ttu-id="8bf0d-136">Instead, a visualization similar to a segmented funnel is presented.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-136">Instead, a visualization similar to a segmented funnel is presented.</span></span> <span data-ttu-id="8bf0d-137">Sort by **Usage** to view the variation of conversion to your custom event based on country.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-137">Sort by **Usage** to view the variation of conversion to your custom event based on country.</span></span>


## <a name="how-does-the-impact-tool-calculate-these-conversion-rates"></a><span data-ttu-id="8bf0d-138">How does the Impact tool calculate these conversion rates?</span><span class="sxs-lookup"><span data-stu-id="8bf0d-138">How does the Impact tool calculate these conversion rates?</span></span>

<span data-ttu-id="8bf0d-139">Under the hood, the Impact tool relies on the [Pearson correlation coefficient] (https://en.wikipedia.org/wiki/Pearson_correlation_coefficient).</span><span class="sxs-lookup"><span data-stu-id="8bf0d-139">Under the hood, the Impact tool relies on the [Pearson correlation coefficient] (https://en.wikipedia.org/wiki/Pearson_correlation_coefficient).</span></span> <span data-ttu-id="8bf0d-140">Results are computed between -1 and 1 with -1 representing zero correlation and 1 representing a positive correlation.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-140">Results are computed between -1 and 1 with -1 representing zero correlation and 1 representing a positive correlation.</span></span>

<span data-ttu-id="8bf0d-141">The basic breakdown of how Impact Analysis works is as follows:</span><span class="sxs-lookup"><span data-stu-id="8bf0d-141">The basic breakdown of how Impact Analysis works is as follows:</span></span>

<span data-ttu-id="8bf0d-142">Let _A_ = the main page view/custom event/request you select in the first dropdown.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-142">Let _A_ = the main page view/custom event/request you select in the first dropdown.</span></span> <span data-ttu-id="8bf0d-143">(**For the page view**).</span><span class="sxs-lookup"><span data-stu-id="8bf0d-143">(**For the page view**).</span></span>

<span data-ttu-id="8bf0d-144">Let _B_ = the secondary page view/custom event you select (**impacts the usage of**).</span><span class="sxs-lookup"><span data-stu-id="8bf0d-144">Let _B_ = the secondary page view/custom event you select (**impacts the usage of**).</span></span>

<span data-ttu-id="8bf0d-145">Impact looks at a sample of all the sessions from users in the selected time range.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-145">Impact looks at a sample of all the sessions from users in the selected time range.</span></span> <span data-ttu-id="8bf0d-146">For each session, it looks for each occurrence of _A_.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-146">For each session, it looks for each occurrence of _A_.</span></span>

<span data-ttu-id="8bf0d-147">Sessions are then broken into two different kinds of _subsessions_ based on one of two conditions:</span><span class="sxs-lookup"><span data-stu-id="8bf0d-147">Sessions are then broken into two different kinds of _subsessions_ based on one of two conditions:</span></span>

- <span data-ttu-id="8bf0d-148">A converted subsession consists of a session ending with a _B_ event and encompasses all _A_ events that occur prior to _B_.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-148">A converted subsession consists of a session ending with a _B_ event and encompasses all _A_ events that occur prior to _B_.</span></span>
- <span data-ttu-id="8bf0d-149">An unconverted subsession occurs when all _A_'s occur without a terminal _B_.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-149">An unconverted subsession occurs when all _A_'s occur without a terminal _B_.</span></span>

<span data-ttu-id="8bf0d-150">How Impact is ultimately calculated varies based on whether we are analyzing by metric or by dimension.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-150">How Impact is ultimately calculated varies based on whether we are analyzing by metric or by dimension.</span></span> <span data-ttu-id="8bf0d-151">For metrics all _A_'s in a subsession are averaged.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-151">For metrics all _A_'s in a subsession are averaged.</span></span> <span data-ttu-id="8bf0d-152">Whereas for dimensions the value of each _A_ contributes _1/N_ to the value assigned to _B_ where _N_ is the number of _A_'s in the subsession.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-152">Whereas for dimensions the value of each _A_ contributes _1/N_ to the value assigned to _B_ where _N_ is the number of _A_'s in the subsession.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bf0d-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bf0d-153">Next steps</span></span>

- <span data-ttu-id="8bf0d-154">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="8bf0d-154">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="8bf0d-155">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span><span class="sxs-lookup"><span data-stu-id="8bf0d-155">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="8bf0d-156">Funnels</span><span class="sxs-lookup"><span data-stu-id="8bf0d-156">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="8bf0d-157">Retention</span><span class="sxs-lookup"><span data-stu-id="8bf0d-157">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="8bf0d-158">User Flows</span><span class="sxs-lookup"><span data-stu-id="8bf0d-158">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="8bf0d-159">Workbooks</span><span class="sxs-lookup"><span data-stu-id="8bf0d-159">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="8bf0d-160">Add user context</span><span class="sxs-lookup"><span data-stu-id="8bf0d-160">Add user context</span></span>](app-insights-usage-send-user-context.md)