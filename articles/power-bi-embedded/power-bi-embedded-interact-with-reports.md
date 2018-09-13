---
title: Interact with reports using the JavaScript API | Microsoft Docs
description: Power BI Embedded, interact with reports using the JavaScript API
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: f0586efbf0654cd5f96e02cef73ca1bc3c270ec7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550272"
---
# <a name="interact-with-power-bi-reports-using-the-javascript-api"></a><span data-ttu-id="5eba7-103">Interact with Power BI reports using the JavaScript API</span><span class="sxs-lookup"><span data-stu-id="5eba7-103">Interact with Power BI reports using the JavaScript API</span></span>
<span data-ttu-id="5eba7-104">The Power BI JavaScript API enables you to easily embed Power BI reports into your applications.</span><span class="sxs-lookup"><span data-stu-id="5eba7-104">The Power BI JavaScript API enables you to easily embed Power BI reports into your applications.</span></span> <span data-ttu-id="5eba7-105">With the API, your applications can programmatically interact with different report elements like pages and filters.</span><span class="sxs-lookup"><span data-stu-id="5eba7-105">With the API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="5eba7-106">This interactivity makes Power BI reports a more integrated part of your application.</span><span class="sxs-lookup"><span data-stu-id="5eba7-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="5eba7-107">You embed a Power BI report in your application by using an iframe that is hosted as part of the application.</span><span class="sxs-lookup"><span data-stu-id="5eba7-107">You embed a Power BI report in your application by using an iframe that is hosted as part of the application.</span></span> <span data-ttu-id="5eba7-108">The iframe acts as a boundary between your application and the report, as you can see in the following image.</span><span class="sxs-lookup"><span data-stu-id="5eba7-108">The iframe acts as a boundary between your application and the report, as you can see in the following image.</span></span> 

![Power BI embedded iframe without Javascript API](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="5eba7-110">The iframe makes the embedding process a lot easier, but without the JavaScript API the report and your application can't interact with each other.</span><span class="sxs-lookup"><span data-stu-id="5eba7-110">The iframe makes the embedding process a lot easier, but without the JavaScript API the report and your application can't interact with each other.</span></span> <span data-ttu-id="5eba7-111">This lack of interaction can make it feel like the report is not really part of the application.</span><span class="sxs-lookup"><span data-stu-id="5eba7-111">This lack of interaction can make it feel like the report is not really part of the application.</span></span> <span data-ttu-id="5eba7-112">The report and application really need to communicate back and forth, as in the following image.</span><span class="sxs-lookup"><span data-stu-id="5eba7-112">The report and application really need to communicate back and forth, as in the following image.</span></span>

![Power BI embedded iframe with Javascript API](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="5eba7-114">The Power BI JavaScript API enables you to write code that can securely pass through the iframe boundary.</span><span class="sxs-lookup"><span data-stu-id="5eba7-114">The Power BI JavaScript API enables you to write code that can securely pass through the iframe boundary.</span></span> <span data-ttu-id="5eba7-115">This enables your application to programmatically perform an action in a report, and to listen for events from actions that users make within the report.</span><span class="sxs-lookup"><span data-stu-id="5eba7-115">This enables your application to programmatically perform an action in a report, and to listen for events from actions that users make within the report.</span></span>

## <a name="what-can-you-do-with-the-power-bi-javascript-api"></a><span data-ttu-id="5eba7-116">What can you do with the Power BI JavaScript API?</span><span class="sxs-lookup"><span data-stu-id="5eba7-116">What can you do with the Power BI JavaScript API?</span></span>
<span data-ttu-id="5eba7-117">With the JavaScript API you can manage reports, navigate to pages in a report, filter a report, and handle embedding events.</span><span class="sxs-lookup"><span data-stu-id="5eba7-117">With the JavaScript API you can manage reports, navigate to pages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="5eba7-118">The following diagram shows the structure of the API.</span><span class="sxs-lookup"><span data-stu-id="5eba7-118">The following diagram shows the structure of the API.</span></span>

![Power BI JavaScript API diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="5eba7-120">Manage reports</span><span class="sxs-lookup"><span data-stu-id="5eba7-120">Manage reports</span></span>
<span data-ttu-id="5eba7-121">The Javascript API enables you to manage behavior at the report and page level:</span><span class="sxs-lookup"><span data-stu-id="5eba7-121">The Javascript API enables you to manage behavior at the report and page level:</span></span>

* <span data-ttu-id="5eba7-122">Embed a specific Power BI Report securely in your application - try the [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="5eba7-122">Embed a specific Power BI Report securely in your application - try the [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="5eba7-123">Set access token</span><span class="sxs-lookup"><span data-stu-id="5eba7-123">Set access token</span></span>
* <span data-ttu-id="5eba7-124">Configure the report</span><span class="sxs-lookup"><span data-stu-id="5eba7-124">Configure the report</span></span>
  * <span data-ttu-id="5eba7-125">Enable and disable the filter pane and page navigation pane - try the [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="5eba7-125">Enable and disable the filter pane and page navigation pane - try the [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="5eba7-126">Set defaults for pages and filters - try the [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="5eba7-126">Set defaults for pages and filters - try the [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="5eba7-127">Enter and exit full screen mode</span><span class="sxs-lookup"><span data-stu-id="5eba7-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="5eba7-128">Learn more about embedding a report</span><span class="sxs-lookup"><span data-stu-id="5eba7-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-to-pages-in-a-report"></a><span data-ttu-id="5eba7-129">Navigate to pages in a report</span><span class="sxs-lookup"><span data-stu-id="5eba7-129">Navigate to pages in a report</span></span>
<span data-ttu-id="5eba7-130">The JavaScript API enbales you to discover all pages in a report and to set the current page.</span><span class="sxs-lookup"><span data-stu-id="5eba7-130">The JavaScript API enbales you to discover all pages in a report and to set the current page.</span></span> <span data-ttu-id="5eba7-131">Try the [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="5eba7-131">Try the [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="5eba7-132">Learn more about page navigation</span><span class="sxs-lookup"><span data-stu-id="5eba7-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="5eba7-133">Filter a report</span><span class="sxs-lookup"><span data-stu-id="5eba7-133">Filter a report</span></span>
<span data-ttu-id="5eba7-134">The JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span><span class="sxs-lookup"><span data-stu-id="5eba7-134">The JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="5eba7-135">Try the [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span><span class="sxs-lookup"><span data-stu-id="5eba7-135">Try the [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="5eba7-136">Basic filters</span><span class="sxs-lookup"><span data-stu-id="5eba7-136">Basic filters</span></span>
<span data-ttu-id="5eba7-137">A basic filter is placed on a column or hierarchy level and contains a list of values to include or exclude.</span><span class="sxs-lookup"><span data-stu-id="5eba7-137">A basic filter is placed on a column or hierarchy level and contains a list of values to include or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="5eba7-138">Advanced filters</span><span class="sxs-lookup"><span data-stu-id="5eba7-138">Advanced filters</span></span>
<span data-ttu-id="5eba7-139">Advanced filters use the logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span><span class="sxs-lookup"><span data-stu-id="5eba7-139">Advanced filters use the logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="5eba7-140">Supported conditions are:</span><span class="sxs-lookup"><span data-stu-id="5eba7-140">Supported conditions are:</span></span>

* <span data-ttu-id="5eba7-141">None</span><span class="sxs-lookup"><span data-stu-id="5eba7-141">None</span></span>
* <span data-ttu-id="5eba7-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="5eba7-142">LessThan</span></span>
* <span data-ttu-id="5eba7-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="5eba7-143">LessThanOrEqual</span></span>
* <span data-ttu-id="5eba7-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="5eba7-144">GreaterThan</span></span>
* <span data-ttu-id="5eba7-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="5eba7-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="5eba7-146">Contains</span><span class="sxs-lookup"><span data-stu-id="5eba7-146">Contains</span></span>
* <span data-ttu-id="5eba7-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="5eba7-147">DoesNotContain</span></span>
* <span data-ttu-id="5eba7-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="5eba7-148">StartsWith</span></span>
* <span data-ttu-id="5eba7-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="5eba7-149">DoesNotStartWith</span></span>
* <span data-ttu-id="5eba7-150">Is</span><span class="sxs-lookup"><span data-stu-id="5eba7-150">Is</span></span>
* <span data-ttu-id="5eba7-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="5eba7-151">IsNot</span></span>
* <span data-ttu-id="5eba7-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="5eba7-152">IsBlank</span></span>
* <span data-ttu-id="5eba7-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="5eba7-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="5eba7-154">Learn more about filtering</span><span class="sxs-lookup"><span data-stu-id="5eba7-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="5eba7-155">Handling events</span><span class="sxs-lookup"><span data-stu-id="5eba7-155">Handling events</span></span>
<span data-ttu-id="5eba7-156">In addition to sending information into the iframe, your application can also receive information on the following events coming from the iframe:</span><span class="sxs-lookup"><span data-stu-id="5eba7-156">In addition to sending information into the iframe, your application can also receive information on the following events coming from the iframe:</span></span>

* <span data-ttu-id="5eba7-157">Embed</span><span class="sxs-lookup"><span data-stu-id="5eba7-157">Embed</span></span>
  * <span data-ttu-id="5eba7-158">loaded</span><span class="sxs-lookup"><span data-stu-id="5eba7-158">loaded</span></span>
  * <span data-ttu-id="5eba7-159">error</span><span class="sxs-lookup"><span data-stu-id="5eba7-159">error</span></span>
* <span data-ttu-id="5eba7-160">Reports</span><span class="sxs-lookup"><span data-stu-id="5eba7-160">Reports</span></span>
  * <span data-ttu-id="5eba7-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="5eba7-161">pageChanged</span></span>
  * <span data-ttu-id="5eba7-162">dataSelected (coming soon)</span><span class="sxs-lookup"><span data-stu-id="5eba7-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="5eba7-163">Learn more about handling events</span><span class="sxs-lookup"><span data-stu-id="5eba7-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="5eba7-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="5eba7-164">Next steps</span></span>
<span data-ttu-id="5eba7-165">For more information about the Power BI JavaScript API, check out the following links:</span><span class="sxs-lookup"><span data-stu-id="5eba7-165">For more information about the Power BI JavaScript API, check out the following links:</span></span>

* [<span data-ttu-id="5eba7-166">JavaScript API Wiki</span><span class="sxs-lookup"><span data-stu-id="5eba7-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="5eba7-167">Object model reference</span><span class="sxs-lookup"><span data-stu-id="5eba7-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="5eba7-168">Samples</span><span class="sxs-lookup"><span data-stu-id="5eba7-168">Samples</span></span>
  * [<span data-ttu-id="5eba7-169">Angular</span><span class="sxs-lookup"><span data-stu-id="5eba7-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="5eba7-170">Ember</span><span class="sxs-lookup"><span data-stu-id="5eba7-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="5eba7-171">Live demo</span><span class="sxs-lookup"><span data-stu-id="5eba7-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)




