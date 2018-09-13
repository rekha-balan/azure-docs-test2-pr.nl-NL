---
title: Investigate and share usage data with interactive Workbooks in Azure Application Insights | Microsoft docs
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
ms.date: 06/12/2017
ms.reviewer: daviste
ms.author: mbullwin
ms.openlocfilehash: 016a26acc153fba1c38d926fd5389d02755c2ff5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856519"
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="d3101-103">Investigate and share usage data with interactive workbooks in Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3101-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="d3101-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span><span class="sxs-lookup"><span data-stu-id="d3101-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="d3101-105">Workbooks are editable by other team members with access to the same Azure resource.</span><span class="sxs-lookup"><span data-stu-id="d3101-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="d3101-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span><span class="sxs-lookup"><span data-stu-id="d3101-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="d3101-107">Workbooks are helpful for scenarios like:</span><span class="sxs-lookup"><span data-stu-id="d3101-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="d3101-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span><span class="sxs-lookup"><span data-stu-id="d3101-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="d3101-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span><span class="sxs-lookup"><span data-stu-id="d3101-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="d3101-110">Sharing the results of an A/B experiment in your app with other members of your team.</span><span class="sxs-lookup"><span data-stu-id="d3101-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="d3101-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span><span class="sxs-lookup"><span data-stu-id="d3101-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="d3101-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span><span class="sxs-lookup"><span data-stu-id="d3101-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="d3101-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span><span class="sxs-lookup"><span data-stu-id="d3101-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="d3101-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="d3101-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="d3101-115">Editing, rearranging, cloning, and deleting workbook sections</span><span class="sxs-lookup"><span data-stu-id="d3101-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="d3101-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span><span class="sxs-lookup"><span data-stu-id="d3101-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="d3101-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span><span class="sxs-lookup"><span data-stu-id="d3101-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Application Insights Workbooks section editing controls](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="d3101-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span><span class="sxs-lookup"><span data-stu-id="d3101-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="d3101-120">To create a duplicate of a section, click the **Clone this section** icon.</span><span class="sxs-lookup"><span data-stu-id="d3101-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="d3101-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span><span class="sxs-lookup"><span data-stu-id="d3101-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="d3101-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span><span class="sxs-lookup"><span data-stu-id="d3101-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="d3101-123">To remove a section permanently, click the **Remove** icon.</span><span class="sxs-lookup"><span data-stu-id="d3101-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="d3101-124">Adding usage data visualization sections</span><span class="sxs-lookup"><span data-stu-id="d3101-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="d3101-125">Workbooks offer four types of built-in usage analytics visualizations.</span><span class="sxs-lookup"><span data-stu-id="d3101-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="d3101-126">Each answers a common question about the usage of your app.</span><span class="sxs-lookup"><span data-stu-id="d3101-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="d3101-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span><span class="sxs-lookup"><span data-stu-id="d3101-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="d3101-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span><span class="sxs-lookup"><span data-stu-id="d3101-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![Users section in Workbooks](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="d3101-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span><span class="sxs-lookup"><span data-stu-id="d3101-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="d3101-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span><span class="sxs-lookup"><span data-stu-id="d3101-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="d3101-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span><span class="sxs-lookup"><span data-stu-id="d3101-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="d3101-133">Each of these three section types offers the same sets of controls and visualizations:</span><span class="sxs-lookup"><span data-stu-id="d3101-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="d3101-134">Learn more about editing Users, Sessions, and Events sections</span><span class="sxs-lookup"><span data-stu-id="d3101-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="d3101-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span><span class="sxs-lookup"><span data-stu-id="d3101-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![Retention section in Workbooks](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="d3101-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span><span class="sxs-lookup"><span data-stu-id="d3101-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="d3101-138">Learn more about editing Retention sections</span><span class="sxs-lookup"><span data-stu-id="d3101-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="d3101-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span><span class="sxs-lookup"><span data-stu-id="d3101-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="d3101-140">Adding Application Insights Analytics sections</span><span class="sxs-lookup"><span data-stu-id="d3101-140">Adding Application Insights Analytics sections</span></span>

![Analytics section in Workbooks](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="d3101-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span><span class="sxs-lookup"><span data-stu-id="d3101-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="d3101-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span><span class="sxs-lookup"><span data-stu-id="d3101-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="d3101-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span><span class="sxs-lookup"><span data-stu-id="d3101-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="d3101-145">How many exceptions did your site throw during the same time period as a decline in usage?</span><span class="sxs-lookup"><span data-stu-id="d3101-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="d3101-146">What was the distribution of page load times for users viewing some page?</span><span class="sxs-lookup"><span data-stu-id="d3101-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="d3101-147">How many users viewed some set of pages on your site, but not some other set of pages?</span><span class="sxs-lookup"><span data-stu-id="d3101-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="d3101-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span><span class="sxs-lookup"><span data-stu-id="d3101-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="d3101-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span><span class="sxs-lookup"><span data-stu-id="d3101-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="d3101-150">Adding text and Markdown sections</span><span class="sxs-lookup"><span data-stu-id="d3101-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="d3101-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span><span class="sxs-lookup"><span data-stu-id="d3101-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="d3101-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span><span class="sxs-lookup"><span data-stu-id="d3101-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="d3101-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span><span class="sxs-lookup"><span data-stu-id="d3101-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="d3101-154">Saving and sharing workbooks with your team</span><span class="sxs-lookup"><span data-stu-id="d3101-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="d3101-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="d3101-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="d3101-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span><span class="sxs-lookup"><span data-stu-id="d3101-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="d3101-157">To share a workbook that's currently in **My Reports**:</span><span class="sxs-lookup"><span data-stu-id="d3101-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="d3101-158">Click **Open** in the action bar</span><span class="sxs-lookup"><span data-stu-id="d3101-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="d3101-159">Click the "..." button beside the workbook you want to share</span><span class="sxs-lookup"><span data-stu-id="d3101-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="d3101-160">Click **Move to Shared Reports**.</span><span class="sxs-lookup"><span data-stu-id="d3101-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="d3101-161">To share a workbook with a link or via email, click **Share** in the action bar.</span><span class="sxs-lookup"><span data-stu-id="d3101-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="d3101-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span><span class="sxs-lookup"><span data-stu-id="d3101-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="d3101-163">To make edits, recipients need at least Contributor permissions for the resource.</span><span class="sxs-lookup"><span data-stu-id="d3101-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="d3101-164">To pin a link to a workbook to an Azure Dashboard:</span><span class="sxs-lookup"><span data-stu-id="d3101-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="d3101-165">Click **Open** in the action bar</span><span class="sxs-lookup"><span data-stu-id="d3101-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="d3101-166">Click the "..." button beside the workbook you want to pin</span><span class="sxs-lookup"><span data-stu-id="d3101-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="d3101-167">Click **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="d3101-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3101-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3101-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3101-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3101-169">Next steps</span></span>
- <span data-ttu-id="d3101-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="d3101-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="d3101-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span><span class="sxs-lookup"><span data-stu-id="d3101-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="d3101-172">Users, Sessions, Events</span><span class="sxs-lookup"><span data-stu-id="d3101-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="d3101-173">Funnels</span><span class="sxs-lookup"><span data-stu-id="d3101-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="d3101-174">Retention</span><span class="sxs-lookup"><span data-stu-id="d3101-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="d3101-175">User Flows</span><span class="sxs-lookup"><span data-stu-id="d3101-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="d3101-176">Add user context</span><span class="sxs-lookup"><span data-stu-id="d3101-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
