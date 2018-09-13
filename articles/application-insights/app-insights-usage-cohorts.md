---
title: Azure Application Insights usage cohorts | Microsoft Docs
description: Analyze different sets or users, sessions, events, or operations that have something in common
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/10/2018
ms.reviewer: daviste
ms.author: mbullwin
ms.openlocfilehash: 2157af8d6c3b8eea372c060a70c78559d8ffe6ad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855919"
---
# <a name="application-insights-cohorts"></a><span data-ttu-id="d43b6-103">Application Insights cohorts</span><span class="sxs-lookup"><span data-stu-id="d43b6-103">Application Insights cohorts</span></span>

<span data-ttu-id="d43b6-104">A cohort is a set of users, sessions, events, or operations that have something in common.</span><span class="sxs-lookup"><span data-stu-id="d43b6-104">A cohort is a set of users, sessions, events, or operations that have something in common.</span></span> <span data-ttu-id="d43b6-105">In Azure Application Insights, cohorts are defined by an analytics query.</span><span class="sxs-lookup"><span data-stu-id="d43b6-105">In Azure Application Insights, cohorts are defined by an analytics query.</span></span> <span data-ttu-id="d43b6-106">In cases where you have to analyze a specific set of users or events repeatedly, cohorts can give you more flexibility to express exactly the set you’re interested in.</span><span class="sxs-lookup"><span data-stu-id="d43b6-106">In cases where you have to analyze a specific set of users or events repeatedly, cohorts can give you more flexibility to express exactly the set you’re interested in.</span></span>

![Cohorts pane](.\media\app-insights-usage-cohorts\001.png)

## <a name="cohorts-versus-basic-filters"></a><span data-ttu-id="d43b6-108">Cohorts versus basic filters</span><span class="sxs-lookup"><span data-stu-id="d43b6-108">Cohorts versus basic filters</span></span>

<span data-ttu-id="d43b6-109">Cohorts are used in ways similar to filters.</span><span class="sxs-lookup"><span data-stu-id="d43b6-109">Cohorts are used in ways similar to filters.</span></span> <span data-ttu-id="d43b6-110">But cohorts' definitions are built from custom analytics queries, so they're much more adaptable and complex.</span><span class="sxs-lookup"><span data-stu-id="d43b6-110">But cohorts' definitions are built from custom analytics queries, so they're much more adaptable and complex.</span></span> <span data-ttu-id="d43b6-111">Unlike filters, you can save cohorts so other members of your team can reuse them.</span><span class="sxs-lookup"><span data-stu-id="d43b6-111">Unlike filters, you can save cohorts so other members of your team can reuse them.</span></span>

<span data-ttu-id="d43b6-112">You might define a cohort of users who have all tried a new feature in your app.</span><span class="sxs-lookup"><span data-stu-id="d43b6-112">You might define a cohort of users who have all tried a new feature in your app.</span></span> <span data-ttu-id="d43b6-113">You can save this cohort in your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="d43b6-113">You can save this cohort in your Application Insights resource.</span></span> <span data-ttu-id="d43b6-114">It's easy to analyze this saved group of specific users in the future.</span><span class="sxs-lookup"><span data-stu-id="d43b6-114">It's easy to analyze this saved group of specific users in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="d43b6-115">After they're created, cohorts are available from the Users, Sessions, Events, and User Flows tools.</span><span class="sxs-lookup"><span data-stu-id="d43b6-115">After they're created, cohorts are available from the Users, Sessions, Events, and User Flows tools.</span></span>

## <a name="example-engaged-users"></a><span data-ttu-id="d43b6-116">Example: Engaged users</span><span class="sxs-lookup"><span data-stu-id="d43b6-116">Example: Engaged users</span></span>

<span data-ttu-id="d43b6-117">Your team defines an engaged user as anyone who uses your app five or more times in a given month.</span><span class="sxs-lookup"><span data-stu-id="d43b6-117">Your team defines an engaged user as anyone who uses your app five or more times in a given month.</span></span> <span data-ttu-id="d43b6-118">In this section, you define a cohort of these engaged users.</span><span class="sxs-lookup"><span data-stu-id="d43b6-118">In this section, you define a cohort of these engaged users.</span></span>

1. <span data-ttu-id="d43b6-119">Open the Cohorts tool.</span><span class="sxs-lookup"><span data-stu-id="d43b6-119">Open the Cohorts tool.</span></span>

2. <span data-ttu-id="d43b6-120">Select the **Template Gallery** tab. You see a collection of templates for various cohorts.</span><span class="sxs-lookup"><span data-stu-id="d43b6-120">Select the **Template Gallery** tab. You see a collection of templates for various cohorts.</span></span>

3. <span data-ttu-id="d43b6-121">Select **Engaged Users -- by Days Used**.</span><span class="sxs-lookup"><span data-stu-id="d43b6-121">Select **Engaged Users -- by Days Used**.</span></span>

    <span data-ttu-id="d43b6-122">There are three parameters for this cohort:</span><span class="sxs-lookup"><span data-stu-id="d43b6-122">There are three parameters for this cohort:</span></span>
    * <span data-ttu-id="d43b6-123">**Activities**, where you choose which events and page views count as “usage.”</span><span class="sxs-lookup"><span data-stu-id="d43b6-123">**Activities**, where you choose which events and page views count as “usage.”</span></span>
    * <span data-ttu-id="d43b6-124">**Period**, the definition of a month.</span><span class="sxs-lookup"><span data-stu-id="d43b6-124">**Period**, the definition of a month.</span></span>
    * <span data-ttu-id="d43b6-125">**UsedAtleastCustom**, the number of times users need to use something within a period to count as engaged.</span><span class="sxs-lookup"><span data-stu-id="d43b6-125">**UsedAtleastCustom**, the number of times users need to use something within a period to count as engaged.</span></span>

4. <span data-ttu-id="d43b6-126">Change **UsedAtleastCustom** to **5+ days**, and leave **Period** on the default of 28 days.</span><span class="sxs-lookup"><span data-stu-id="d43b6-126">Change **UsedAtleastCustom** to **5+ days**, and leave **Period** on the default of 28 days.</span></span>

    ![Engaged users](.\media\app-insights-usage-cohorts\003.png)

    <span data-ttu-id="d43b6-128">Now this cohort represents all user IDs sent with any custom event or page view on 5 separate days in the past 28.</span><span class="sxs-lookup"><span data-stu-id="d43b6-128">Now this cohort represents all user IDs sent with any custom event or page view on 5 separate days in the past 28.</span></span>

5. <span data-ttu-id="d43b6-129">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d43b6-129">Select **Save**.</span></span>

   > [!TIP]
   >  <span data-ttu-id="d43b6-130">Give your cohort a name, like “Engaged Users (5+ Days).”</span><span class="sxs-lookup"><span data-stu-id="d43b6-130">Give your cohort a name, like “Engaged Users (5+ Days).”</span></span> <span data-ttu-id="d43b6-131">Save it to “My reports” or “Shared reports,” depending on whether you want other people who have access to this Application Insights resource to see this cohort.</span><span class="sxs-lookup"><span data-stu-id="d43b6-131">Save it to “My reports” or “Shared reports,” depending on whether you want other people who have access to this Application Insights resource to see this cohort.</span></span>

6. <span data-ttu-id="d43b6-132">Select **Back to Gallery**.</span><span class="sxs-lookup"><span data-stu-id="d43b6-132">Select **Back to Gallery**.</span></span>

### <a name="what-can-you-do-by-using-this-cohort"></a><span data-ttu-id="d43b6-133">What can you do by using this cohort?</span><span class="sxs-lookup"><span data-stu-id="d43b6-133">What can you do by using this cohort?</span></span>

<span data-ttu-id="d43b6-134">Open the Users tool.</span><span class="sxs-lookup"><span data-stu-id="d43b6-134">Open the Users tool.</span></span> <span data-ttu-id="d43b6-135">In the **Show** drop-down box, choose the cohort you created under **Users who belong to**.</span><span class="sxs-lookup"><span data-stu-id="d43b6-135">In the **Show** drop-down box, choose the cohort you created under **Users who belong to**.</span></span>

<span data-ttu-id="d43b6-136">Now the Users tool is filtered to this cohort of users:</span><span class="sxs-lookup"><span data-stu-id="d43b6-136">Now the Users tool is filtered to this cohort of users:</span></span>

![Users pane filtered to a particular cohort](.\media\app-insights-usage-cohorts\004.png)

<span data-ttu-id="d43b6-138">A few important things to notice:</span><span class="sxs-lookup"><span data-stu-id="d43b6-138">A few important things to notice:</span></span>
* <span data-ttu-id="d43b6-139">You can't create this set through normal filters.</span><span class="sxs-lookup"><span data-stu-id="d43b6-139">You can't create this set through normal filters.</span></span> <span data-ttu-id="d43b6-140">The date logic is more advanced.</span><span class="sxs-lookup"><span data-stu-id="d43b6-140">The date logic is more advanced.</span></span>
* <span data-ttu-id="d43b6-141">You can further filter this cohort by using the normal filters in the Users tool.</span><span class="sxs-lookup"><span data-stu-id="d43b6-141">You can further filter this cohort by using the normal filters in the Users tool.</span></span> <span data-ttu-id="d43b6-142">So although the cohort is defined on 28-day windows, you can still adjust the time range in the Users tool to be 30, 60, or 90 days.</span><span class="sxs-lookup"><span data-stu-id="d43b6-142">So although the cohort is defined on 28-day windows, you can still adjust the time range in the Users tool to be 30, 60, or 90 days.</span></span>

<span data-ttu-id="d43b6-143">These filters support more sophisticated questions that are impossible to express through the query builder.</span><span class="sxs-lookup"><span data-stu-id="d43b6-143">These filters support more sophisticated questions that are impossible to express through the query builder.</span></span> <span data-ttu-id="d43b6-144">An example is _people who were engaged in the past 28 days. How did those same people behave over the past 60 days?_</span><span class="sxs-lookup"><span data-stu-id="d43b6-144">An example is _people who were engaged in the past 28 days. How did those same people behave over the past 60 days?_</span></span>

## <a name="example-events-cohort"></a><span data-ttu-id="d43b6-145">Example: Events cohort</span><span class="sxs-lookup"><span data-stu-id="d43b6-145">Example: Events cohort</span></span>

<span data-ttu-id="d43b6-146">You can also make cohorts of events.</span><span class="sxs-lookup"><span data-stu-id="d43b6-146">You can also make cohorts of events.</span></span> <span data-ttu-id="d43b6-147">In this section, you define a cohort of the events and page views.</span><span class="sxs-lookup"><span data-stu-id="d43b6-147">In this section, you define a cohort of the events and page views.</span></span> <span data-ttu-id="d43b6-148">Then you see how to use them from the other tools.</span><span class="sxs-lookup"><span data-stu-id="d43b6-148">Then you see how to use them from the other tools.</span></span> <span data-ttu-id="d43b6-149">This cohort might define a set of events that your team considers _active usage_ or a set related to a certain new feature.</span><span class="sxs-lookup"><span data-stu-id="d43b6-149">This cohort might define a set of events that your team considers _active usage_ or a set related to a certain new feature.</span></span>

1. <span data-ttu-id="d43b6-150">Open the Cohorts tool.</span><span class="sxs-lookup"><span data-stu-id="d43b6-150">Open the Cohorts tool.</span></span>

2. <span data-ttu-id="d43b6-151">Select the **Template Gallery** tab. You’ll see a collection of templates for various cohorts.</span><span class="sxs-lookup"><span data-stu-id="d43b6-151">Select the **Template Gallery** tab. You’ll see a collection of templates for various cohorts.</span></span>

3. <span data-ttu-id="d43b6-152">Select **Events Picker**.</span><span class="sxs-lookup"><span data-stu-id="d43b6-152">Select **Events Picker**.</span></span>

    ![Screenshot of events picker](.\media\app-insights-usage-cohorts\006.png)

4. <span data-ttu-id="d43b6-154">In the **Activities** drop-down box, select the events you want to be in the cohort.</span><span class="sxs-lookup"><span data-stu-id="d43b6-154">In the **Activities** drop-down box, select the events you want to be in the cohort.</span></span>

5. <span data-ttu-id="d43b6-155">Save the cohort and give it a name.</span><span class="sxs-lookup"><span data-stu-id="d43b6-155">Save the cohort and give it a name.</span></span>

## <a name="example-active-users-where-you-modify-a-query"></a><span data-ttu-id="d43b6-156">Example: Active users where you modify a query</span><span class="sxs-lookup"><span data-stu-id="d43b6-156">Example: Active users where you modify a query</span></span>

<span data-ttu-id="d43b6-157">The previous two cohorts were defined by using drop-down boxes.</span><span class="sxs-lookup"><span data-stu-id="d43b6-157">The previous two cohorts were defined by using drop-down boxes.</span></span> <span data-ttu-id="d43b6-158">But you can also define cohorts by using analytics queries for total flexibility.</span><span class="sxs-lookup"><span data-stu-id="d43b6-158">But you can also define cohorts by using analytics queries for total flexibility.</span></span> <span data-ttu-id="d43b6-159">To see how, create a cohort of users from the United Kingdom.</span><span class="sxs-lookup"><span data-stu-id="d43b6-159">To see how, create a cohort of users from the United Kingdom.</span></span>

![Animated image walking through use of Cohorts tool](.\media\app-insights-usage-cohorts\cohorts0001.gif)

1. <span data-ttu-id="d43b6-161">Open the Cohorts tool, select the **Template Gallery** tab, and select **Blank Users cohort**.</span><span class="sxs-lookup"><span data-stu-id="d43b6-161">Open the Cohorts tool, select the **Template Gallery** tab, and select **Blank Users cohort**.</span></span>

    ![Blank users cohort](.\media\app-insights-usage-cohorts\001.png)

    <span data-ttu-id="d43b6-163">There are three sections:</span><span class="sxs-lookup"><span data-stu-id="d43b6-163">There are three sections:</span></span>
    * <span data-ttu-id="d43b6-164">A Markdown text section, where you describe the cohort in more detail for others on your team.</span><span class="sxs-lookup"><span data-stu-id="d43b6-164">A Markdown text section, where you describe the cohort in more detail for others on your team.</span></span>

    * <span data-ttu-id="d43b6-165">A parameters section, where you make your own parameters, like **Activities** and other drop-down boxes from the previous two examples.</span><span class="sxs-lookup"><span data-stu-id="d43b6-165">A parameters section, where you make your own parameters, like **Activities** and other drop-down boxes from the previous two examples.</span></span>

    * <span data-ttu-id="d43b6-166">A query section, where you define the cohort by using an analytics query.</span><span class="sxs-lookup"><span data-stu-id="d43b6-166">A query section, where you define the cohort by using an analytics query.</span></span>

    <span data-ttu-id="d43b6-167">In the query section, you [write an analytics query](https://docs.loganalytics.io/index).</span><span class="sxs-lookup"><span data-stu-id="d43b6-167">In the query section, you [write an analytics query](https://docs.loganalytics.io/index).</span></span> <span data-ttu-id="d43b6-168">The query selects the certain set of rows that describe the cohort you want to define.</span><span class="sxs-lookup"><span data-stu-id="d43b6-168">The query selects the certain set of rows that describe the cohort you want to define.</span></span> <span data-ttu-id="d43b6-169">The Cohorts tool then implicitly adds a “| summarize by user_Id” clause to the query.</span><span class="sxs-lookup"><span data-stu-id="d43b6-169">The Cohorts tool then implicitly adds a “| summarize by user_Id” clause to the query.</span></span> <span data-ttu-id="d43b6-170">This data is previewed below the query in a table, so you can make sure your query is returning results.</span><span class="sxs-lookup"><span data-stu-id="d43b6-170">This data is previewed below the query in a table, so you can make sure your query is returning results.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d43b6-171">If you don’t see the query, try resizing the section to make it taller and reveal the query.</span><span class="sxs-lookup"><span data-stu-id="d43b6-171">If you don’t see the query, try resizing the section to make it taller and reveal the query.</span></span> <span data-ttu-id="d43b6-172">The animated .gif at the beginning of this section illustrates the resizing behavior.</span><span class="sxs-lookup"><span data-stu-id="d43b6-172">The animated .gif at the beginning of this section illustrates the resizing behavior.</span></span>

2. <span data-ttu-id="d43b6-173">Copy and paste the following text into the query editor:</span><span class="sxs-lookup"><span data-stu-id="d43b6-173">Copy and paste the following text into the query editor:</span></span>

    ```KQL
    union customEvents, pageViews
    | where client_CountryOrRegion == "United Kingdom"
    ```

3. <span data-ttu-id="d43b6-174">Select **Run Query**.</span><span class="sxs-lookup"><span data-stu-id="d43b6-174">Select **Run Query**.</span></span> <span data-ttu-id="d43b6-175">If you don't see user IDs appear in the table, change to a country where your application has users.</span><span class="sxs-lookup"><span data-stu-id="d43b6-175">If you don't see user IDs appear in the table, change to a country where your application has users.</span></span>

4. <span data-ttu-id="d43b6-176">Save and name the cohort.</span><span class="sxs-lookup"><span data-stu-id="d43b6-176">Save and name the cohort.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d43b6-177">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="d43b6-177">Frequently asked questions</span></span>

<span data-ttu-id="d43b6-178">_I’ve defined a cohort of users from a certain country. When I compare this cohort in the Users tool to just setting a filter on that country, I see different results. Why?_</span><span class="sxs-lookup"><span data-stu-id="d43b6-178">_I’ve defined a cohort of users from a certain country. When I compare this cohort in the Users tool to just setting a filter on that country, I see different results. Why?_</span></span>

<span data-ttu-id="d43b6-179">Cohorts and filters are different.</span><span class="sxs-lookup"><span data-stu-id="d43b6-179">Cohorts and filters are different.</span></span> <span data-ttu-id="d43b6-180">Suppose you have a cohort of users from the United Kingdom (defined like the previous example), and you compare its results to setting the filter “Country or region = United Kingdom.”</span><span class="sxs-lookup"><span data-stu-id="d43b6-180">Suppose you have a cohort of users from the United Kingdom (defined like the previous example), and you compare its results to setting the filter “Country or region = United Kingdom.”</span></span>

* <span data-ttu-id="d43b6-181">The cohort version shows all events from users who sent one or more events from the United Kingdom in the current time range.</span><span class="sxs-lookup"><span data-stu-id="d43b6-181">The cohort version shows all events from users who sent one or more events from the United Kingdom in the current time range.</span></span> <span data-ttu-id="d43b6-182">If you split by country or region, you likely see many countries and regions.</span><span class="sxs-lookup"><span data-stu-id="d43b6-182">If you split by country or region, you likely see many countries and regions.</span></span>
* <span data-ttu-id="d43b6-183">The filters version only shows events from the United Kingdom.</span><span class="sxs-lookup"><span data-stu-id="d43b6-183">The filters version only shows events from the United Kingdom.</span></span> <span data-ttu-id="d43b6-184">But if you split by country or region, you see only the United Kingdom.</span><span class="sxs-lookup"><span data-stu-id="d43b6-184">But if you split by country or region, you see only the United Kingdom.</span></span>

## <a name="learn-more"></a><span data-ttu-id="d43b6-185">Learn more</span><span class="sxs-lookup"><span data-stu-id="d43b6-185">Learn more</span></span>
- [<span data-ttu-id="d43b6-186">Analytics query language</span><span class="sxs-lookup"><span data-stu-id="d43b6-186">Analytics query language</span></span>](https://go.microsoft.com/fwlink/?linkid=856587)
- [<span data-ttu-id="d43b6-187">Users, sessions, events</span><span class="sxs-lookup"><span data-stu-id="d43b6-187">Users, sessions, events</span></span>](app-insights-usage-segmentation.md)
- [<span data-ttu-id="d43b6-188">User flows</span><span class="sxs-lookup"><span data-stu-id="d43b6-188">User flows</span></span>](app-insights-usage-flows.md)
- [<span data-ttu-id="d43b6-189">Usage overview</span><span class="sxs-lookup"><span data-stu-id="d43b6-189">Usage overview</span></span>](app-insights-usage-overview.md)