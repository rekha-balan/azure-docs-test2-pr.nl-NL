---
title: Search Traffic Analytics for Azure Search | Microsoft Docs
description: Enable Search traffic analytics for Azure Search, a cloud hosted search service on Microsoft Azure, to unlock insights about your users and your data.
services: search
documentationcenter: ''
author: bernitorres
manager: jlembicz
editor: ''
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: ec8b3a9845d519dcd121a1a65652284e5a5919b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556298"
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="0257b-103">What is search traffic analytics</span><span class="sxs-lookup"><span data-stu-id="0257b-103">What is search traffic analytics</span></span>
<span data-ttu-id="0257b-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span><span class="sxs-lookup"><span data-stu-id="0257b-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="0257b-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span><span class="sxs-lookup"><span data-stu-id="0257b-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="0257b-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span><span class="sxs-lookup"><span data-stu-id="0257b-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="0257b-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span><span class="sxs-lookup"><span data-stu-id="0257b-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span></span>

<span data-ttu-id="0257b-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span><span class="sxs-lookup"><span data-stu-id="0257b-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span></span> <span data-ttu-id="0257b-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span><span class="sxs-lookup"><span data-stu-id="0257b-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span></span>

## <a name="identify-the-relevant-search-data"></a><span data-ttu-id="0257b-110">Identify the relevant search data</span><span class="sxs-lookup"><span data-stu-id="0257b-110">Identify the relevant search data</span></span>

<span data-ttu-id="0257b-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span><span class="sxs-lookup"><span data-stu-id="0257b-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span></span> <span data-ttu-id="0257b-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span><span class="sxs-lookup"><span data-stu-id="0257b-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span></span>

<span data-ttu-id="0257b-113">There are two signals Search Traffic Analytics needs:</span><span class="sxs-lookup"><span data-stu-id="0257b-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="0257b-114">User generated search events: only search queries initiated by a user are interesting.</span><span class="sxs-lookup"><span data-stu-id="0257b-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="0257b-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span><span class="sxs-lookup"><span data-stu-id="0257b-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="0257b-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span><span class="sxs-lookup"><span data-stu-id="0257b-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="0257b-117">A click generally means that a document is a relevant result for a specific search query.</span><span class="sxs-lookup"><span data-stu-id="0257b-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="0257b-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span><span class="sxs-lookup"><span data-stu-id="0257b-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span></span> <span data-ttu-id="0257b-119">These search insights are impossible to obtain with only search traffic logs.</span><span class="sxs-lookup"><span data-stu-id="0257b-119">These search insights are impossible to obtain with only search traffic logs.</span></span>

## <a name="how-to-implement-search-traffic-analytics"></a><span data-ttu-id="0257b-120">How to implement search traffic analytics</span><span class="sxs-lookup"><span data-stu-id="0257b-120">How to implement search traffic analytics</span></span>

<span data-ttu-id="0257b-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span><span class="sxs-lookup"><span data-stu-id="0257b-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span></span> <span data-ttu-id="0257b-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span><span class="sxs-lookup"><span data-stu-id="0257b-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="0257b-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span><span class="sxs-lookup"><span data-stu-id="0257b-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span></span>

<span data-ttu-id="0257b-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span><span class="sxs-lookup"><span data-stu-id="0257b-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="0257b-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span><span class="sxs-lookup"><span data-stu-id="0257b-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span></span>

![Search Traffic Analytics instructions][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="0257b-127">1. Select an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="0257b-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="0257b-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span><span class="sxs-lookup"><span data-stu-id="0257b-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span></span> <span data-ttu-id="0257b-129">You can use a resource that's already in use to log the required custom events.</span><span class="sxs-lookup"><span data-stu-id="0257b-129">You can use a resource that's already in use to log the required custom events.</span></span>

<span data-ttu-id="0257b-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span><span class="sxs-lookup"><span data-stu-id="0257b-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="0257b-131">Select the one that best fits the platform you are using.</span><span class="sxs-lookup"><span data-stu-id="0257b-131">Select the one that best fits the platform you are using.</span></span>

<span data-ttu-id="0257b-132">You need the instrumentation key for creating the telemetry client for your application.</span><span class="sxs-lookup"><span data-stu-id="0257b-132">You need the instrumentation key for creating the telemetry client for your application.</span></span> <span data-ttu-id="0257b-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span><span class="sxs-lookup"><span data-stu-id="0257b-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="0257b-134">2. Instrument your application</span><span class="sxs-lookup"><span data-stu-id="0257b-134">2. Instrument your application</span></span>

<span data-ttu-id="0257b-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span><span class="sxs-lookup"><span data-stu-id="0257b-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span></span> <span data-ttu-id="0257b-136">There are four steps to this process:</span><span class="sxs-lookup"><span data-stu-id="0257b-136">There are four steps to this process:</span></span>

<span data-ttu-id="0257b-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span><span class="sxs-lookup"><span data-stu-id="0257b-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span></span>

<span data-ttu-id="0257b-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="0257b-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="0257b-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0257b-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="0257b-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="0257b-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="0257b-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span><span class="sxs-lookup"><span data-stu-id="0257b-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="0257b-142">Azure Search provides you with a Search Id when you request it with a header:</span><span class="sxs-lookup"><span data-stu-id="0257b-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="0257b-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="0257b-143">*C#*</span></span>

    // This sample uses the Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="0257b-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0257b-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="0257b-145">**III. Log Search events**</span><span class="sxs-lookup"><span data-stu-id="0257b-145">**III. Log Search events**</span></span>

<span data-ttu-id="0257b-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span><span class="sxs-lookup"><span data-stu-id="0257b-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="0257b-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span><span class="sxs-lookup"><span data-stu-id="0257b-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="0257b-148">Request count on user generated queries by adding $count=true to your search query.</span><span class="sxs-lookup"><span data-stu-id="0257b-148">Request count on user generated queries by adding $count=true to your search query.</span></span> <span data-ttu-id="0257b-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="0257b-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="0257b-150">Remember to only log search queries that are generated by users.</span><span class="sxs-lookup"><span data-stu-id="0257b-150">Remember to only log search queries that are generated by users.</span></span>
>

<span data-ttu-id="0257b-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="0257b-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="0257b-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0257b-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="0257b-153">**IV. Log Click events**</span><span class="sxs-lookup"><span data-stu-id="0257b-153">**IV. Log Click events**</span></span>

<span data-ttu-id="0257b-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span><span class="sxs-lookup"><span data-stu-id="0257b-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="0257b-155">Use Application Insights custom events to log these events with the following schema:</span><span class="sxs-lookup"><span data-stu-id="0257b-155">Use Application Insights custom events to log these events with the following schema:</span></span>

<span data-ttu-id="0257b-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span><span class="sxs-lookup"><span data-stu-id="0257b-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span></span>

> [!NOTE]
> <span data-ttu-id="0257b-157">Position refers to the cardinal order in your application.</span><span class="sxs-lookup"><span data-stu-id="0257b-157">Position refers to the cardinal order in your application.</span></span> <span data-ttu-id="0257b-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span><span class="sxs-lookup"><span data-stu-id="0257b-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span></span>
>

<span data-ttu-id="0257b-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="0257b-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="0257b-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0257b-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="0257b-161">3. Analyze with Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0257b-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="0257b-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="0257b-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="0257b-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span><span class="sxs-lookup"><span data-stu-id="0257b-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span></span>

<span data-ttu-id="0257b-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0257b-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="0257b-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span><span class="sxs-lookup"><span data-stu-id="0257b-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span></span>

![Application Insights Data in the Search Traffic Analytics blade][2]

<span data-ttu-id="0257b-167">Metrics included in the Power BI desktop template:</span><span class="sxs-lookup"><span data-stu-id="0257b-167">Metrics included in the Power BI desktop template:</span></span>

*   <span data-ttu-id="0257b-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span><span class="sxs-lookup"><span data-stu-id="0257b-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span></span>
*   <span data-ttu-id="0257b-169">Searches without clicks: terms for top queries that register no clicks</span><span class="sxs-lookup"><span data-stu-id="0257b-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="0257b-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span><span class="sxs-lookup"><span data-stu-id="0257b-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="0257b-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span><span class="sxs-lookup"><span data-stu-id="0257b-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="0257b-172">Time to click: clicks bucketed by time since the search query</span><span class="sxs-lookup"><span data-stu-id="0257b-172">Time to click: clicks bucketed by time since the search query</span></span>

![Power BI template for reading from Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="0257b-174">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0257b-174">Next Steps</span></span>
<span data-ttu-id="0257b-175">Instrument your search application to get powerful and insightful data about your search service.</span><span class="sxs-lookup"><span data-stu-id="0257b-175">Instrument your search application to get powerful and insightful data about your search service.</span></span>

<span data-ttu-id="0257b-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="0257b-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="0257b-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span><span class="sxs-lookup"><span data-stu-id="0257b-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span></span>

<span data-ttu-id="0257b-178">Learn more about creating amazing reports.</span><span class="sxs-lookup"><span data-stu-id="0257b-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="0257b-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span><span class="sxs-lookup"><span data-stu-id="0257b-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-traffic-analytics/AzureSearch-AppInsightsData.PNG
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-traffic-analytics/AzureSearch-PBITemplate.PNG



