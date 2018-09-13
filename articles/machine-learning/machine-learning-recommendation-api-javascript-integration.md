---
title: 'Machine Learning Recommendations: JavaScript Integration | Microsoft Docs'
description: Azure Machine Learning Recommendations - JavaScript Integration - documentation
services: machine-learning
documentationcenter: ''
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: machine-learning-datamarket-deprecation
ms.openlocfilehash: 5a814a8ec5ed32aca71f2c990b531479cb1fc051
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564734"
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="43517-103">Azure Machine Learning Recommendations - JavaScript Integration</span><span class="sxs-lookup"><span data-stu-id="43517-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="43517-104">You should start using the Recommendations API Cognitive Service instead of this version.</span><span class="sxs-lookup"><span data-stu-id="43517-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="43517-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span><span class="sxs-lookup"><span data-stu-id="43517-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="43517-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span><span class="sxs-lookup"><span data-stu-id="43517-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="43517-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="43517-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="43517-108">This document depict how to integrate your site using JavaScript.</span><span class="sxs-lookup"><span data-stu-id="43517-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="43517-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span><span class="sxs-lookup"><span data-stu-id="43517-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="43517-110">All operations done via JS can be also done from server side.</span><span class="sxs-lookup"><span data-stu-id="43517-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="43517-111">1. General Overview</span><span class="sxs-lookup"><span data-stu-id="43517-111">1. General Overview</span></span>
<span data-ttu-id="43517-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span><span class="sxs-lookup"><span data-stu-id="43517-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="43517-113">Send Events into Azure ML Recommendations.</span><span class="sxs-lookup"><span data-stu-id="43517-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="43517-114">This will enable to build a recommendation model.</span><span class="sxs-lookup"><span data-stu-id="43517-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="43517-115">Consume the recommendations.</span><span class="sxs-lookup"><span data-stu-id="43517-115">Consume the recommendations.</span></span> <span data-ttu-id="43517-116">After the model is built you can consume the recommendations.</span><span class="sxs-lookup"><span data-stu-id="43517-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="43517-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span><span class="sxs-lookup"><span data-stu-id="43517-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="43517-118"><ins>Phase I</ins></span><span class="sxs-lookup"><span data-stu-id="43517-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="43517-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span><span class="sxs-lookup"><span data-stu-id="43517-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="43517-121"><ins>Phase II</ins></span><span class="sxs-lookup"><span data-stu-id="43517-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="43517-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span><span class="sxs-lookup"><span data-stu-id="43517-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="43517-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span><span class="sxs-lookup"><span data-stu-id="43517-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="43517-124">The results include a list of items id. Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span><span class="sxs-lookup"><span data-stu-id="43517-124">The results include a list of items id. Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![Drawing2][2]

<span data-ttu-id="43517-126">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span><span class="sxs-lookup"><span data-stu-id="43517-126">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="43517-127">The data received here is leaner than the one in the first option.</span><span class="sxs-lookup"><span data-stu-id="43517-127">The data received here is leaner than the one in the first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="43517-129">2. Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43517-129">2. Prerequisites</span></span>
1. <span data-ttu-id="43517-130">Create a new model using the APIs.</span><span class="sxs-lookup"><span data-stu-id="43517-130">Create a new model using the APIs.</span></span> <span data-ttu-id="43517-131">See the Quick start guide on how to do it.</span><span class="sxs-lookup"><span data-stu-id="43517-131">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="43517-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span><span class="sxs-lookup"><span data-stu-id="43517-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="43517-133">(This will be used for the basic authentication to enable the JS code to call the APIs).</span><span class="sxs-lookup"><span data-stu-id="43517-133">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="43517-134">3. Send Data Acquisition events using JavaScript</span><span class="sxs-lookup"><span data-stu-id="43517-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="43517-135">The following steps facilitate sending events:</span><span class="sxs-lookup"><span data-stu-id="43517-135">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="43517-136">Include JQuery library in your code.</span><span class="sxs-lookup"><span data-stu-id="43517-136">Include JQuery library in your code.</span></span> <span data-ttu-id="43517-137">You can download it from nuget in the following URL.</span><span class="sxs-lookup"><span data-stu-id="43517-137">You can download it from nuget in the following URL.</span></span>
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. <span data-ttu-id="43517-138">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="43517-138">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="43517-139">Initialize Azure ML Recommendations library with the appropriate parameters.</span><span class="sxs-lookup"><span data-stu-id="43517-139">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <script>
         AzureMLRecommendationsStart("<base64encoding of username:key>",
         "<model_id>");
     </script>
4. <span data-ttu-id="43517-140">Send the appropriate event.</span><span class="sxs-lookup"><span data-stu-id="43517-140">Send the appropriate event.</span></span> <span data-ttu-id="43517-141">See detailed section below on all type of events (example of click event)</span><span class="sxs-lookup"><span data-stu-id="43517-141">See detailed section below on all type of events (example of click event)</span></span>
   
     <script>
         if (typeof AzureMLRecommendationsEvent=="undefined") {         
                     AzureMLRecommendationsEvent = [];
                 }
         AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" });
     </script>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="43517-142">3.1.</span><span class="sxs-lookup"><span data-stu-id="43517-142">3.1.</span></span>    <span data-ttu-id="43517-143">Limitations and Browser Support</span><span class="sxs-lookup"><span data-stu-id="43517-143">Limitations and Browser Support</span></span>
<span data-ttu-id="43517-144">This is a reference implementation and it is given as is.</span><span class="sxs-lookup"><span data-stu-id="43517-144">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="43517-145">It should support all major browsers.</span><span class="sxs-lookup"><span data-stu-id="43517-145">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="43517-146">3.2.</span><span class="sxs-lookup"><span data-stu-id="43517-146">3.2.</span></span>    <span data-ttu-id="43517-147">Type of Events</span><span class="sxs-lookup"><span data-stu-id="43517-147">Type of Events</span></span>
<span data-ttu-id="43517-148">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span><span class="sxs-lookup"><span data-stu-id="43517-148">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="43517-149">There is an additional event that is used to set the user context called Login.</span><span class="sxs-lookup"><span data-stu-id="43517-149">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="43517-150">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="43517-150">3.2.1.</span></span> <span data-ttu-id="43517-151">Click Event</span><span class="sxs-lookup"><span data-stu-id="43517-151">Click Event</span></span>
<span data-ttu-id="43517-152">This event should be used any time a user clicked on an item.</span><span class="sxs-lookup"><span data-stu-id="43517-152">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="43517-153">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span><span class="sxs-lookup"><span data-stu-id="43517-153">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="43517-154">Parameters:</span><span class="sxs-lookup"><span data-stu-id="43517-154">Parameters:</span></span>

* <span data-ttu-id="43517-155">event (string, mandatory) - “click”</span><span class="sxs-lookup"><span data-stu-id="43517-155">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="43517-156">item (string, mandatory) - Unique identifier of the item</span><span class="sxs-lookup"><span data-stu-id="43517-156">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="43517-157">itemName (string, optional) - the name of the item</span><span class="sxs-lookup"><span data-stu-id="43517-157">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="43517-158">itemDescription (string, optional) - the description of the item</span><span class="sxs-lookup"><span data-stu-id="43517-158">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="43517-159">itemCategory (string, optional) - the category of the item</span><span class="sxs-lookup"><span data-stu-id="43517-159">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="43517-160">Or with optional data:</span><span class="sxs-lookup"><span data-stu-id="43517-160">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="43517-161">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="43517-161">3.2.2.</span></span> <span data-ttu-id="43517-162">Recommendation Click Event</span><span class="sxs-lookup"><span data-stu-id="43517-162">Recommendation Click Event</span></span>
<span data-ttu-id="43517-163">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span><span class="sxs-lookup"><span data-stu-id="43517-163">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="43517-164">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span><span class="sxs-lookup"><span data-stu-id="43517-164">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="43517-165">Parameters:</span><span class="sxs-lookup"><span data-stu-id="43517-165">Parameters:</span></span>

* <span data-ttu-id="43517-166">event (string, mandatory) - “recommendationclick”</span><span class="sxs-lookup"><span data-stu-id="43517-166">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="43517-167">item (string, mandatory) - Unique identifier of the item</span><span class="sxs-lookup"><span data-stu-id="43517-167">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="43517-168">itemName (string, optional) - the name of the item</span><span class="sxs-lookup"><span data-stu-id="43517-168">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="43517-169">itemDescription (string, optional) - the description of the item</span><span class="sxs-lookup"><span data-stu-id="43517-169">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="43517-170">itemCategory (string, optional) - the category of the item</span><span class="sxs-lookup"><span data-stu-id="43517-170">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="43517-171">seeds (string array, optional) - the seeds that generated the recommendation query.</span><span class="sxs-lookup"><span data-stu-id="43517-171">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="43517-172">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span><span class="sxs-lookup"><span data-stu-id="43517-172">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="43517-173">Or with optional data:</span><span class="sxs-lookup"><span data-stu-id="43517-173">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="43517-174">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="43517-174">3.2.3.</span></span> <span data-ttu-id="43517-175">Add Shopping Cart Event</span><span class="sxs-lookup"><span data-stu-id="43517-175">Add Shopping Cart Event</span></span>
<span data-ttu-id="43517-176">This event should be used when the user add an item to the shopping cart.</span><span class="sxs-lookup"><span data-stu-id="43517-176">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="43517-177">Parameters:</span><span class="sxs-lookup"><span data-stu-id="43517-177">Parameters:</span></span>

* <span data-ttu-id="43517-178">event (string, mandatory) - “addshopcart”</span><span class="sxs-lookup"><span data-stu-id="43517-178">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="43517-179">item (string, mandatory) - Unique identifier of the item</span><span class="sxs-lookup"><span data-stu-id="43517-179">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="43517-180">itemName (string, optional) - the name of the item</span><span class="sxs-lookup"><span data-stu-id="43517-180">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="43517-181">itemDescription (string, optional) - the description of the item</span><span class="sxs-lookup"><span data-stu-id="43517-181">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="43517-182">itemCategory (string, optional) - the category of the item</span><span class="sxs-lookup"><span data-stu-id="43517-182">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="43517-183">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="43517-183">3.2.4.</span></span> <span data-ttu-id="43517-184">Remove Shopping Cart Event</span><span class="sxs-lookup"><span data-stu-id="43517-184">Remove Shopping Cart Event</span></span>
<span data-ttu-id="43517-185">This event should be used when the user removes an item to the shopping cart.</span><span class="sxs-lookup"><span data-stu-id="43517-185">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="43517-186">Parameters:</span><span class="sxs-lookup"><span data-stu-id="43517-186">Parameters:</span></span>

* <span data-ttu-id="43517-187">event (string, mandatory) - “removeshopcart”</span><span class="sxs-lookup"><span data-stu-id="43517-187">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="43517-188">item (string, mandatory) - Unique identifier of the item</span><span class="sxs-lookup"><span data-stu-id="43517-188">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="43517-189">itemName (string, optional) - the name of the item</span><span class="sxs-lookup"><span data-stu-id="43517-189">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="43517-190">itemDescription (string, optional) - the description of the item</span><span class="sxs-lookup"><span data-stu-id="43517-190">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="43517-191">itemCategory (string, optional) - the category of the item</span><span class="sxs-lookup"><span data-stu-id="43517-191">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="43517-192">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="43517-192">3.2.5.</span></span> <span data-ttu-id="43517-193">Purchase Event</span><span class="sxs-lookup"><span data-stu-id="43517-193">Purchase Event</span></span>
<span data-ttu-id="43517-194">This event should be used when the user purchased his shopping cart.</span><span class="sxs-lookup"><span data-stu-id="43517-194">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="43517-195">Parameters:</span><span class="sxs-lookup"><span data-stu-id="43517-195">Parameters:</span></span>

* <span data-ttu-id="43517-196">event (string) - “purchase”</span><span class="sxs-lookup"><span data-stu-id="43517-196">event (string) - “purchase”</span></span>
* <span data-ttu-id="43517-197">items ( Purchased[] ) - Array holding an entry for each item purchased.</span><span class="sxs-lookup"><span data-stu-id="43517-197">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="43517-198">Purchased format:</span><span class="sxs-lookup"><span data-stu-id="43517-198">Purchased format:</span></span>
  * <span data-ttu-id="43517-199">item (string) - Unique identifier of the item.</span><span class="sxs-lookup"><span data-stu-id="43517-199">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="43517-200">count (int or string) - number of items that were purchased.</span><span class="sxs-lookup"><span data-stu-id="43517-200">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="43517-201">price (float or string) - optional field - the price of the item.</span><span class="sxs-lookup"><span data-stu-id="43517-201">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="43517-202">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span><span class="sxs-lookup"><span data-stu-id="43517-202">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="43517-203">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="43517-203">3.2.6.</span></span> <span data-ttu-id="43517-204">User Login Event</span><span class="sxs-lookup"><span data-stu-id="43517-204">User Login Event</span></span>
<span data-ttu-id="43517-205">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span><span class="sxs-lookup"><span data-stu-id="43517-205">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="43517-206">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span><span class="sxs-lookup"><span data-stu-id="43517-206">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="43517-207">This event should be used after the user login to your site.</span><span class="sxs-lookup"><span data-stu-id="43517-207">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="43517-208">Parameters:</span><span class="sxs-lookup"><span data-stu-id="43517-208">Parameters:</span></span>

* <span data-ttu-id="43517-209">event (string) - “userlogin”</span><span class="sxs-lookup"><span data-stu-id="43517-209">event (string) - “userlogin”</span></span>
* <span data-ttu-id="43517-210">user (string) - unique identification of the user.</span><span class="sxs-lookup"><span data-stu-id="43517-210">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="43517-211">4. Consume Recommendations via JavaScript</span><span class="sxs-lookup"><span data-stu-id="43517-211">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="43517-212">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span><span class="sxs-lookup"><span data-stu-id="43517-212">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="43517-213">The recommendation response includes the recommended items Ids, their names and their ratings.</span><span class="sxs-lookup"><span data-stu-id="43517-213">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="43517-214">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span><span class="sxs-lookup"><span data-stu-id="43517-214">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="43517-215">4.1 Consume Recommendations</span><span class="sxs-lookup"><span data-stu-id="43517-215">4.1 Consume Recommendations</span></span>
<span data-ttu-id="43517-216">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="43517-216">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="43517-217">See section 2.</span><span class="sxs-lookup"><span data-stu-id="43517-217">See section 2.</span></span>

<span data-ttu-id="43517-218">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="43517-218">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="43517-219">Parameters:</span><span class="sxs-lookup"><span data-stu-id="43517-219">Parameters:</span></span>

* <span data-ttu-id="43517-220">items (array of strings) - One or more items to get recommendations for.</span><span class="sxs-lookup"><span data-stu-id="43517-220">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="43517-221">If you consume an Fbt build then you can set here only one item.</span><span class="sxs-lookup"><span data-stu-id="43517-221">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="43517-222">numberOfResults (int) - number of required results.</span><span class="sxs-lookup"><span data-stu-id="43517-222">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="43517-223">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span><span class="sxs-lookup"><span data-stu-id="43517-223">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="43517-224">Processing function - a function that will handle the recommendations returned.</span><span class="sxs-lookup"><span data-stu-id="43517-224">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="43517-225">The data is returned as an array of:</span><span class="sxs-lookup"><span data-stu-id="43517-225">The data is returned as an array of:</span></span>
  * <span data-ttu-id="43517-226">Item - item unique id</span><span class="sxs-lookup"><span data-stu-id="43517-226">Item - item unique id</span></span>
  * <span data-ttu-id="43517-227">name - item name (if exist in catalog)</span><span class="sxs-lookup"><span data-stu-id="43517-227">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="43517-228">rating - recommendation rating</span><span class="sxs-lookup"><span data-stu-id="43517-228">rating - recommendation rating</span></span>
  * <span data-ttu-id="43517-229">metadata - a string that represents the metadata of the item</span><span class="sxs-lookup"><span data-stu-id="43517-229">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="43517-230">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span><span class="sxs-lookup"><span data-stu-id="43517-230">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-recommendation-api-javascript-integration/Drawing3.png



