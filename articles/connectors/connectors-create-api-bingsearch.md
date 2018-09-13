---
title: Connect to Bing Search - Azure Logic Apps | Microsoft Docs
description: Find news with Bing Search REST APIs and Azure Logic Apps
author: ecfan
manager: jeconnoc
ms.author: estfan
ms.date: 05/21/2018
ms.topic: article
ms.service: logic-apps
services: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.openlocfilehash: 8ac67f9df0e5baccc668c2aeb70f65d96e574df5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800194"
---
# <a name="find-news-with-bing-search-and-azure-logic-apps"></a><span data-ttu-id="2da5d-103">Find news with Bing Search and Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2da5d-103">Find news with Bing Search and Azure Logic Apps</span></span> 

<span data-ttu-id="2da5d-104">This article shows how you can find news, videos, and other items through Bing Search from inside a logic app with the Bing Search connector.</span><span class="sxs-lookup"><span data-stu-id="2da5d-104">This article shows how you can find news, videos, and other items through Bing Search from inside a logic app with the Bing Search connector.</span></span> <span data-ttu-id="2da5d-105">That way, you can create logic apps that automate tasks and workflows for processing search results and make those items available for other actions.</span><span class="sxs-lookup"><span data-stu-id="2da5d-105">That way, you can create logic apps that automate tasks and workflows for processing search results and make those items available for other actions.</span></span> 

<span data-ttu-id="2da5d-106">For example, you can find news items based on search criteria, and have Twitter post those items as tweets in your Twitter feed.</span><span class="sxs-lookup"><span data-stu-id="2da5d-106">For example, you can find news items based on search criteria, and have Twitter post those items as tweets in your Twitter feed.</span></span>

<span data-ttu-id="2da5d-107">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="2da5d-107">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> <span data-ttu-id="2da5d-108">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="2da5d-108">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>
<span data-ttu-id="2da5d-109">For connector-specific technical information, see the <a href="https://docs.microsoft.com/connectors/bingsearch/" target="blank">Bing Search connector reference</a>.</span><span class="sxs-lookup"><span data-stu-id="2da5d-109">For connector-specific technical information, see the <a href="https://docs.microsoft.com/connectors/bingsearch/" target="blank">Bing Search connector reference</a>.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2da5d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2da5d-110">Prerequisites</span></span>

* <span data-ttu-id="2da5d-111">A [Cognitive Services account](../cognitive-services/cognitive-services-apis-create-account.md)</span><span class="sxs-lookup"><span data-stu-id="2da5d-111">A [Cognitive Services account](../cognitive-services/cognitive-services-apis-create-account.md)</span></span>

* <span data-ttu-id="2da5d-112">A [Bing Search API key](https://azure.microsoft.com/try/cognitive-services/?api=bing-news-search-api), which provides access from your logic app to the Bing Search APIs</span><span class="sxs-lookup"><span data-stu-id="2da5d-112">A [Bing Search API key](https://azure.microsoft.com/try/cognitive-services/?api=bing-news-search-api), which provides access from your logic app to the Bing Search APIs</span></span> 

* <span data-ttu-id="2da5d-113">The logic app where you want to access your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="2da5d-113">The logic app where you want to access your Event Hub.</span></span> <span data-ttu-id="2da5d-114">To start your logic app with a Bing Search trigger, you need a [blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="2da5d-114">To start your logic app with a Bing Search trigger, you need a [blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> 

<a name="add-trigger"></a>

## <a name="add-a-bing-search-trigger"></a><span data-ttu-id="2da5d-115">Add a Bing Search trigger</span><span class="sxs-lookup"><span data-stu-id="2da5d-115">Add a Bing Search trigger</span></span>

<span data-ttu-id="2da5d-116">In Azure Logic Apps, every logic app must start with a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts), which fires when a specific event happens or when a specific condition is met.</span><span class="sxs-lookup"><span data-stu-id="2da5d-116">In Azure Logic Apps, every logic app must start with a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts), which fires when a specific event happens or when a specific condition is met.</span></span> <span data-ttu-id="2da5d-117">Each time the trigger fires, the Logic Apps engine creates a logic app instance and starts running your app's workflow.</span><span class="sxs-lookup"><span data-stu-id="2da5d-117">Each time the trigger fires, the Logic Apps engine creates a logic app instance and starts running your app's workflow.</span></span>

1. <span data-ttu-id="2da5d-118">In the Azure portal or Visual Studio, create a blank logic app, which opens Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="2da5d-118">In the Azure portal or Visual Studio, create a blank logic app, which opens Logic App Designer.</span></span> <span data-ttu-id="2da5d-119">This example uses the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2da5d-119">This example uses the Azure portal.</span></span>

2. <span data-ttu-id="2da5d-120">In the search box, enter "Bing search" as your filter.</span><span class="sxs-lookup"><span data-stu-id="2da5d-120">In the search box, enter "Bing search" as your filter.</span></span> <span data-ttu-id="2da5d-121">From the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="2da5d-121">From the triggers list, select the trigger you want.</span></span> 

   <span data-ttu-id="2da5d-122">This example uses this trigger: **Bing Search - On new news article**</span><span class="sxs-lookup"><span data-stu-id="2da5d-122">This example uses this trigger: **Bing Search - On new news article**</span></span>

   ![Find Bing Search trigger](./media/connectors-create-api-bing-search/add-trigger.png)

3. <span data-ttu-id="2da5d-124">If you're prompted for connection details, [create your Bing Search connection now](#create-connection).</span><span class="sxs-lookup"><span data-stu-id="2da5d-124">If you're prompted for connection details, [create your Bing Search connection now](#create-connection).</span></span> <span data-ttu-id="2da5d-125">Or, if your connection already exists, provide the necessary information for the trigger.</span><span class="sxs-lookup"><span data-stu-id="2da5d-125">Or, if your connection already exists, provide the necessary information for the trigger.</span></span>

   <span data-ttu-id="2da5d-126">For this example, provide criteria for returning matching news articles from Bing Search.</span><span class="sxs-lookup"><span data-stu-id="2da5d-126">For this example, provide criteria for returning matching news articles from Bing Search.</span></span>

   | <span data-ttu-id="2da5d-127">Property</span><span class="sxs-lookup"><span data-stu-id="2da5d-127">Property</span></span> | <span data-ttu-id="2da5d-128">Required</span><span class="sxs-lookup"><span data-stu-id="2da5d-128">Required</span></span> | <span data-ttu-id="2da5d-129">Value</span><span class="sxs-lookup"><span data-stu-id="2da5d-129">Value</span></span> | <span data-ttu-id="2da5d-130">Description</span><span class="sxs-lookup"><span data-stu-id="2da5d-130">Description</span></span> | 
   |----------|----------|-------|-------------| 
   | <span data-ttu-id="2da5d-131">Search Query</span><span class="sxs-lookup"><span data-stu-id="2da5d-131">Search Query</span></span> | <span data-ttu-id="2da5d-132">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-132">Yes</span></span> | <span data-ttu-id="2da5d-133"><*search-words*></span><span class="sxs-lookup"><span data-stu-id="2da5d-133"><*search-words*></span></span> | <span data-ttu-id="2da5d-134">Enter the search keywords you want to use.</span><span class="sxs-lookup"><span data-stu-id="2da5d-134">Enter the search keywords you want to use.</span></span> |
   | <span data-ttu-id="2da5d-135">Market</span><span class="sxs-lookup"><span data-stu-id="2da5d-135">Market</span></span> | <span data-ttu-id="2da5d-136">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-136">Yes</span></span> | <span data-ttu-id="2da5d-137"><*locale*></span><span class="sxs-lookup"><span data-stu-id="2da5d-137"><*locale*></span></span> | <span data-ttu-id="2da5d-138">The search locale.</span><span class="sxs-lookup"><span data-stu-id="2da5d-138">The search locale.</span></span> <span data-ttu-id="2da5d-139">The default is "en-US", but you can select another value.</span><span class="sxs-lookup"><span data-stu-id="2da5d-139">The default is "en-US", but you can select another value.</span></span> | 
   | <span data-ttu-id="2da5d-140">Safe Search</span><span class="sxs-lookup"><span data-stu-id="2da5d-140">Safe Search</span></span> | <span data-ttu-id="2da5d-141">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-141">Yes</span></span> | <span data-ttu-id="2da5d-142"><*search-level*></span><span class="sxs-lookup"><span data-stu-id="2da5d-142"><*search-level*></span></span> | <span data-ttu-id="2da5d-143">The filter level for excluding adult content.</span><span class="sxs-lookup"><span data-stu-id="2da5d-143">The filter level for excluding adult content.</span></span> <span data-ttu-id="2da5d-144">The default is "Moderate", but you select another level.</span><span class="sxs-lookup"><span data-stu-id="2da5d-144">The default is "Moderate", but you select another level.</span></span> | 
   | <span data-ttu-id="2da5d-145">Count</span><span class="sxs-lookup"><span data-stu-id="2da5d-145">Count</span></span> | <span data-ttu-id="2da5d-146">No</span><span class="sxs-lookup"><span data-stu-id="2da5d-146">No</span></span> | <span data-ttu-id="2da5d-147"><*results-count*></span><span class="sxs-lookup"><span data-stu-id="2da5d-147"><*results-count*></span></span> | <span data-ttu-id="2da5d-148">Return the specified number of results.</span><span class="sxs-lookup"><span data-stu-id="2da5d-148">Return the specified number of results.</span></span> <span data-ttu-id="2da5d-149">The default is 20, but you can specify another value.</span><span class="sxs-lookup"><span data-stu-id="2da5d-149">The default is 20, but you can specify another value.</span></span> <span data-ttu-id="2da5d-150">The actual number of returned results might be less than the specified number.</span><span class="sxs-lookup"><span data-stu-id="2da5d-150">The actual number of returned results might be less than the specified number.</span></span> | 
   | <span data-ttu-id="2da5d-151">Offset</span><span class="sxs-lookup"><span data-stu-id="2da5d-151">Offset</span></span> | <span data-ttu-id="2da5d-152">No</span><span class="sxs-lookup"><span data-stu-id="2da5d-152">No</span></span> | <span data-ttu-id="2da5d-153"><*skip-value*></span><span class="sxs-lookup"><span data-stu-id="2da5d-153"><*skip-value*></span></span> | <span data-ttu-id="2da5d-154">The number of results to skip before returning results</span><span class="sxs-lookup"><span data-stu-id="2da5d-154">The number of results to skip before returning results</span></span> | 
   ||||| 

   <span data-ttu-id="2da5d-155">For example:</span><span class="sxs-lookup"><span data-stu-id="2da5d-155">For example:</span></span>

   ![Set up trigger](./media/connectors-create-api-bing-search/bing-search-trigger.png)

4. <span data-ttu-id="2da5d-157">Select the interval and frequency for how often you want the trigger to check for results.</span><span class="sxs-lookup"><span data-stu-id="2da5d-157">Select the interval and frequency for how often you want the trigger to check for results.</span></span>

5. <span data-ttu-id="2da5d-158">When you're done, on the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="2da5d-158">When you're done, on the designer toolbar, choose **Save**.</span></span> 

6. <span data-ttu-id="2da5d-159">Now continue adding one or more actions to your logic app for the tasks you want to perform with the trigger results.</span><span class="sxs-lookup"><span data-stu-id="2da5d-159">Now continue adding one or more actions to your logic app for the tasks you want to perform with the trigger results.</span></span>

<a name="add-action"></a>

## <a name="add-a-bing-search-action"></a><span data-ttu-id="2da5d-160">Add a Bing Search action</span><span class="sxs-lookup"><span data-stu-id="2da5d-160">Add a Bing Search action</span></span>

<span data-ttu-id="2da5d-161">In Azure Logic Apps, an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) is a step in your workflow that follows a trigger or another action.</span><span class="sxs-lookup"><span data-stu-id="2da5d-161">In Azure Logic Apps, an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) is a step in your workflow that follows a trigger or another action.</span></span> <span data-ttu-id="2da5d-162">For this example, the logic app starts with a Bing Search trigger that returns news articles matching the specified criteria.</span><span class="sxs-lookup"><span data-stu-id="2da5d-162">For this example, the logic app starts with a Bing Search trigger that returns news articles matching the specified criteria.</span></span> 

1. <span data-ttu-id="2da5d-163">In the Azure portal or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="2da5d-163">In the Azure portal or Visual Studio, open your logic app in Logic App Designer.</span></span> <span data-ttu-id="2da5d-164">This example uses the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2da5d-164">This example uses the Azure portal.</span></span>

2. <span data-ttu-id="2da5d-165">Under the trigger or action, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="2da5d-165">Under the trigger or action, choose **New step** > **Add an action**.</span></span>

   <span data-ttu-id="2da5d-166">This example uses this trigger: **Bing Search - On new news article**</span><span class="sxs-lookup"><span data-stu-id="2da5d-166">This example uses this trigger: **Bing Search - On new news article**</span></span>

   ![Add action](./media/connectors-create-api-bing-search/add-action.png)

   <span data-ttu-id="2da5d-168">To add an action between existing steps, move your mouse over the connecting arrow.</span><span class="sxs-lookup"><span data-stu-id="2da5d-168">To add an action between existing steps, move your mouse over the connecting arrow.</span></span> 
   <span data-ttu-id="2da5d-169">Choose the plus sign (**+**) that appears, and then choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="2da5d-169">Choose the plus sign (**+**) that appears, and then choose **Add an action**.</span></span>

3. <span data-ttu-id="2da5d-170">In the search box, enter "Bing search" as your filter.</span><span class="sxs-lookup"><span data-stu-id="2da5d-170">In the search box, enter "Bing search" as your filter.</span></span>
<span data-ttu-id="2da5d-171">From the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="2da5d-171">From the actions list, select the action you want.</span></span>

   <span data-ttu-id="2da5d-172">This example uses this action: **Bing Search - List news by query**</span><span class="sxs-lookup"><span data-stu-id="2da5d-172">This example uses this action: **Bing Search - List news by query**</span></span>

   ![Find Bing Search action](./media/connectors-create-api-bing-search/bing-search-select-action.png)

4. <span data-ttu-id="2da5d-174">If you're prompted for connection details, [create your Bing Search connection now](#create-connection).</span><span class="sxs-lookup"><span data-stu-id="2da5d-174">If you're prompted for connection details, [create your Bing Search connection now](#create-connection).</span></span> <span data-ttu-id="2da5d-175">Or, if your connection already exists, provide the necessary information for the action.</span><span class="sxs-lookup"><span data-stu-id="2da5d-175">Or, if your connection already exists, provide the necessary information for the action.</span></span> 

   <span data-ttu-id="2da5d-176">For this example, provide the criteria for returning a subset of the trigger's results.</span><span class="sxs-lookup"><span data-stu-id="2da5d-176">For this example, provide the criteria for returning a subset of the trigger's results.</span></span>

   | <span data-ttu-id="2da5d-177">Property</span><span class="sxs-lookup"><span data-stu-id="2da5d-177">Property</span></span> | <span data-ttu-id="2da5d-178">Required</span><span class="sxs-lookup"><span data-stu-id="2da5d-178">Required</span></span> | <span data-ttu-id="2da5d-179">Value</span><span class="sxs-lookup"><span data-stu-id="2da5d-179">Value</span></span> | <span data-ttu-id="2da5d-180">Description</span><span class="sxs-lookup"><span data-stu-id="2da5d-180">Description</span></span> | 
   |----------|----------|-------|-------------| 
   | <span data-ttu-id="2da5d-181">Search Query</span><span class="sxs-lookup"><span data-stu-id="2da5d-181">Search Query</span></span> | <span data-ttu-id="2da5d-182">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-182">Yes</span></span> | <span data-ttu-id="2da5d-183"><*search-expression*></span><span class="sxs-lookup"><span data-stu-id="2da5d-183"><*search-expression*></span></span> | <span data-ttu-id="2da5d-184">Enter an expression for querying the trigger results.</span><span class="sxs-lookup"><span data-stu-id="2da5d-184">Enter an expression for querying the trigger results.</span></span> <span data-ttu-id="2da5d-185">You can select from the fields in the dynamic content list, or create an expression with the expression builder.</span><span class="sxs-lookup"><span data-stu-id="2da5d-185">You can select from the fields in the dynamic content list, or create an expression with the expression builder.</span></span> |
   | <span data-ttu-id="2da5d-186">Market</span><span class="sxs-lookup"><span data-stu-id="2da5d-186">Market</span></span> | <span data-ttu-id="2da5d-187">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-187">Yes</span></span> | <span data-ttu-id="2da5d-188"><*locale*></span><span class="sxs-lookup"><span data-stu-id="2da5d-188"><*locale*></span></span> | <span data-ttu-id="2da5d-189">The search locale.</span><span class="sxs-lookup"><span data-stu-id="2da5d-189">The search locale.</span></span> <span data-ttu-id="2da5d-190">The default is "en-US", but you can select another value.</span><span class="sxs-lookup"><span data-stu-id="2da5d-190">The default is "en-US", but you can select another value.</span></span> | 
   | <span data-ttu-id="2da5d-191">Safe Search</span><span class="sxs-lookup"><span data-stu-id="2da5d-191">Safe Search</span></span> | <span data-ttu-id="2da5d-192">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-192">Yes</span></span> | <span data-ttu-id="2da5d-193"><*search-level*></span><span class="sxs-lookup"><span data-stu-id="2da5d-193"><*search-level*></span></span> | <span data-ttu-id="2da5d-194">The filter level for excluding adult content.</span><span class="sxs-lookup"><span data-stu-id="2da5d-194">The filter level for excluding adult content.</span></span> <span data-ttu-id="2da5d-195">The default is "Moderate", but you select another level.</span><span class="sxs-lookup"><span data-stu-id="2da5d-195">The default is "Moderate", but you select another level.</span></span> | 
   | <span data-ttu-id="2da5d-196">Count</span><span class="sxs-lookup"><span data-stu-id="2da5d-196">Count</span></span> | <span data-ttu-id="2da5d-197">No</span><span class="sxs-lookup"><span data-stu-id="2da5d-197">No</span></span> | <span data-ttu-id="2da5d-198"><*results-count*></span><span class="sxs-lookup"><span data-stu-id="2da5d-198"><*results-count*></span></span> | <span data-ttu-id="2da5d-199">Return the specified number of results.</span><span class="sxs-lookup"><span data-stu-id="2da5d-199">Return the specified number of results.</span></span> <span data-ttu-id="2da5d-200">The default is 20, but you can specify another value.</span><span class="sxs-lookup"><span data-stu-id="2da5d-200">The default is 20, but you can specify another value.</span></span> <span data-ttu-id="2da5d-201">The actual number of returned results might be less than the specified number.</span><span class="sxs-lookup"><span data-stu-id="2da5d-201">The actual number of returned results might be less than the specified number.</span></span> | 
   | <span data-ttu-id="2da5d-202">Offset</span><span class="sxs-lookup"><span data-stu-id="2da5d-202">Offset</span></span> | <span data-ttu-id="2da5d-203">No</span><span class="sxs-lookup"><span data-stu-id="2da5d-203">No</span></span> | <span data-ttu-id="2da5d-204"><*skip-value*></span><span class="sxs-lookup"><span data-stu-id="2da5d-204"><*skip-value*></span></span> | <span data-ttu-id="2da5d-205">The number of results to skip before returning results</span><span class="sxs-lookup"><span data-stu-id="2da5d-205">The number of results to skip before returning results</span></span> | 
   ||||| 

   <span data-ttu-id="2da5d-206">For example, suppose you want those results whose category name includes the word "tech".</span><span class="sxs-lookup"><span data-stu-id="2da5d-206">For example, suppose you want those results whose category name includes the word "tech".</span></span> 
   
   1. <span data-ttu-id="2da5d-207">Click in the **Search Query** box so the dynamic content list appears.</span><span class="sxs-lookup"><span data-stu-id="2da5d-207">Click in the **Search Query** box so the dynamic content list appears.</span></span> 
   <span data-ttu-id="2da5d-208">From that list, choose **Expression** so the expression builder appears.</span><span class="sxs-lookup"><span data-stu-id="2da5d-208">From that list, choose **Expression** so the expression builder appears.</span></span> 

      ![Bing Search trigger](./media/connectors-create-api-bing-search/bing-search-action.png)

      <span data-ttu-id="2da5d-210">Now you can start creating your expression.</span><span class="sxs-lookup"><span data-stu-id="2da5d-210">Now you can start creating your expression.</span></span>

   2. <span data-ttu-id="2da5d-211">From the functions list, select the **contains()** function, which then appears in the expression box.</span><span class="sxs-lookup"><span data-stu-id="2da5d-211">From the functions list, select the **contains()** function, which then appears in the expression box.</span></span> <span data-ttu-id="2da5d-212">Click **Dynamic content** so that the field list reappears, but make sure your cursor stays inside the parentheses.</span><span class="sxs-lookup"><span data-stu-id="2da5d-212">Click **Dynamic content** so that the field list reappears, but make sure your cursor stays inside the parentheses.</span></span>

      ![Select a function](./media/connectors-create-api-bing-search/expression-select-function.png)

   3. <span data-ttu-id="2da5d-214">From the field list, select **Category**, which converts to a parameter.</span><span class="sxs-lookup"><span data-stu-id="2da5d-214">From the field list, select **Category**, which converts to a parameter.</span></span> 
   <span data-ttu-id="2da5d-215">Add a comma after the first parameter, and after the comma, add this word: `'tech'`</span><span class="sxs-lookup"><span data-stu-id="2da5d-215">Add a comma after the first parameter, and after the comma, add this word: `'tech'`</span></span> 

      ![Select a field](./media/connectors-create-api-bing-search/expression-select-field.png)
   
   4. <span data-ttu-id="2da5d-217">When you're done, choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="2da5d-217">When you're done, choose **OK**.</span></span>

      <span data-ttu-id="2da5d-218">The expression now appears in the **Search Query** box in this format:</span><span class="sxs-lookup"><span data-stu-id="2da5d-218">The expression now appears in the **Search Query** box in this format:</span></span>

      ![Finished expression](./media/connectors-create-api-bing-search/resolved-expression.png)

      <span data-ttu-id="2da5d-220">In code view, this expression appears in this format:</span><span class="sxs-lookup"><span data-stu-id="2da5d-220">In code view, this expression appears in this format:</span></span>

      `"@{contains(triggerBody()?['category'],'tech')}"`

5. <span data-ttu-id="2da5d-221">When you're done, on the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="2da5d-221">When you're done, on the designer toolbar, choose **Save**.</span></span>

<a name="create-connection"></a>

## <a name="connect-to-bing-search"></a><span data-ttu-id="2da5d-222">Connect to Bing Search</span><span class="sxs-lookup"><span data-stu-id="2da5d-222">Connect to Bing Search</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)] 

1. <span data-ttu-id="2da5d-223">When you're prompted for connection information, provide these details:</span><span class="sxs-lookup"><span data-stu-id="2da5d-223">When you're prompted for connection information, provide these details:</span></span>

   | <span data-ttu-id="2da5d-224">Property</span><span class="sxs-lookup"><span data-stu-id="2da5d-224">Property</span></span> | <span data-ttu-id="2da5d-225">Required</span><span class="sxs-lookup"><span data-stu-id="2da5d-225">Required</span></span> | <span data-ttu-id="2da5d-226">Value</span><span class="sxs-lookup"><span data-stu-id="2da5d-226">Value</span></span> | <span data-ttu-id="2da5d-227">Description</span><span class="sxs-lookup"><span data-stu-id="2da5d-227">Description</span></span> | 
   |----------|----------|-------|-------------| 
   | <span data-ttu-id="2da5d-228">Connection Name</span><span class="sxs-lookup"><span data-stu-id="2da5d-228">Connection Name</span></span> | <span data-ttu-id="2da5d-229">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-229">Yes</span></span> | <span data-ttu-id="2da5d-230"><*connection-name*></span><span class="sxs-lookup"><span data-stu-id="2da5d-230"><*connection-name*></span></span> | <span data-ttu-id="2da5d-231">The name to create for your connection</span><span class="sxs-lookup"><span data-stu-id="2da5d-231">The name to create for your connection</span></span> |
   | <span data-ttu-id="2da5d-232">API Version</span><span class="sxs-lookup"><span data-stu-id="2da5d-232">API Version</span></span> | <span data-ttu-id="2da5d-233">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-233">Yes</span></span> | <span data-ttu-id="2da5d-234"><*API-version*></span><span class="sxs-lookup"><span data-stu-id="2da5d-234"><*API-version*></span></span> | <span data-ttu-id="2da5d-235">By default, the Bing Search API version is set to the current version.</span><span class="sxs-lookup"><span data-stu-id="2da5d-235">By default, the Bing Search API version is set to the current version.</span></span> <span data-ttu-id="2da5d-236">You can select an earlier version as necessary.</span><span class="sxs-lookup"><span data-stu-id="2da5d-236">You can select an earlier version as necessary.</span></span> | 
   | <span data-ttu-id="2da5d-237">API Key</span><span class="sxs-lookup"><span data-stu-id="2da5d-237">API Key</span></span> | <span data-ttu-id="2da5d-238">Yes</span><span class="sxs-lookup"><span data-stu-id="2da5d-238">Yes</span></span> | <span data-ttu-id="2da5d-239"><*API-key*></span><span class="sxs-lookup"><span data-stu-id="2da5d-239"><*API-key*></span></span> | <span data-ttu-id="2da5d-240">The Bing Search API key that you got earlier.</span><span class="sxs-lookup"><span data-stu-id="2da5d-240">The Bing Search API key that you got earlier.</span></span> <span data-ttu-id="2da5d-241">If you don't have a key, get your [API key now](https://azure.microsoft.com/try/cognitive-services/?api=bing-news-search-api).</span><span class="sxs-lookup"><span data-stu-id="2da5d-241">If you don't have a key, get your [API key now](https://azure.microsoft.com/try/cognitive-services/?api=bing-news-search-api).</span></span> |  
   |||||  

   <span data-ttu-id="2da5d-242">For example:</span><span class="sxs-lookup"><span data-stu-id="2da5d-242">For example:</span></span>

   ![Create connection](./media/connectors-create-api-bing-search/bing-search-create-connection.png)

2. <span data-ttu-id="2da5d-244">When you're done, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="2da5d-244">When you're done, choose **Create**.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="2da5d-245">Connector reference</span><span class="sxs-lookup"><span data-stu-id="2da5d-245">Connector reference</span></span>

<span data-ttu-id="2da5d-246">For technical details, such as triggers, actions, and limits, as described by the connector's Swagger file, see the [connector's reference page](/connectors/bingsearch/).</span><span class="sxs-lookup"><span data-stu-id="2da5d-246">For technical details, such as triggers, actions, and limits, as described by the connector's Swagger file, see the [connector's reference page](/connectors/bingsearch/).</span></span> 

## <a name="get-support"></a><span data-ttu-id="2da5d-247">Get support</span><span class="sxs-lookup"><span data-stu-id="2da5d-247">Get support</span></span>

* <span data-ttu-id="2da5d-248">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="2da5d-248">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="2da5d-249">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="2da5d-249">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2da5d-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="2da5d-250">Next steps</span></span>

* <span data-ttu-id="2da5d-251">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="2da5d-251">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>
