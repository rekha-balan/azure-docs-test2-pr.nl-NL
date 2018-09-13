---
title: How to implement faceted navigation in Azure Search | Microsoft Docs
description: Add Faceted navigation to applications that integrate with Azure Search, a cloud hosted search service on Microsoft Azure.
services: search
documentationcenter: ''
author: HeidiSteen
manager: mblythe
editor: ''
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c11268bafbf520694200e7d9b3fe925153c4166c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662763"
---
# <a name="how-to-implement-faceted-navigation-in-azure-search"></a><span data-ttu-id="a9c3a-103">How to implement faceted navigation in Azure Search</span><span class="sxs-lookup"><span data-stu-id="a9c3a-103">How to implement faceted navigation in Azure Search</span></span>
<span data-ttu-id="a9c3a-104">Faceted navigation is a filtering mechanism that provides self-directed drilldown navigation in search applications.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-104">Faceted navigation is a filtering mechanism that provides self-directed drilldown navigation in search applications.</span></span> <span data-ttu-id="a9c3a-105">The term 'faceted navigation' may be unfamiliar, but you've probably used it before.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-105">The term 'faceted navigation' may be unfamiliar, but you've probably used it before.</span></span> <span data-ttu-id="a9c3a-106">As the following example shows, faceted navigation is nothing more than the categories used to filter results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-106">As the following example shows, faceted navigation is nothing more than the categories used to filter results.</span></span>

 ![Azure Search Job Portal Demo][1]

<span data-ttu-id="a9c3a-108">Faceted navigation is an alternative entry point to search.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-108">Faceted navigation is an alternative entry point to search.</span></span> <span data-ttu-id="a9c3a-109">It offers a convenient alternative to typing complex search expressions by hand.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-109">It offers a convenient alternative to typing complex search expressions by hand.</span></span> <span data-ttu-id="a9c3a-110">Facets can help you find what you're looking for, while ensuring that you don’t get zero results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-110">Facets can help you find what you're looking for, while ensuring that you don’t get zero results.</span></span> <span data-ttu-id="a9c3a-111">As a developer, facets let you expose the most useful search criteria for navigating your search corpus.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-111">As a developer, facets let you expose the most useful search criteria for navigating your search corpus.</span></span> <span data-ttu-id="a9c3a-112">In online retail applications, faceted navigation is often built over brands, departments (kid’s shoes), size, price, popularity, and ratings.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-112">In online retail applications, faceted navigation is often built over brands, departments (kid’s shoes), size, price, popularity, and ratings.</span></span> 

<span data-ttu-id="a9c3a-113">Implementing faceted navigation differs across search technologies.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-113">Implementing faceted navigation differs across search technologies.</span></span> <span data-ttu-id="a9c3a-114">In Azure Search, faceted navigation is built at query time, using fields that you previously attributed in your schema.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-114">In Azure Search, faceted navigation is built at query time, using fields that you previously attributed in your schema.</span></span>

-   <span data-ttu-id="a9c3a-115">In the queries that your application builds, a query must send *facet query parameters* to get the available facet filter values for that document result set.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-115">In the queries that your application builds, a query must send *facet query parameters* to get the available facet filter values for that document result set.</span></span>

-   <span data-ttu-id="a9c3a-116">To actually trim the document result set, the application must also apply a `$filter` expression.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-116">To actually trim the document result set, the application must also apply a `$filter` expression.</span></span>

<span data-ttu-id="a9c3a-117">In your application development, writing code that constructs queries constitutes the bulk of the work.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-117">In your application development, writing code that constructs queries constitutes the bulk of the work.</span></span> <span data-ttu-id="a9c3a-118">Many of the application behaviors that you would expect from faceted navigation are provided by the service, including built-in support for defining ranges and getting counts for facet results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-118">Many of the application behaviors that you would expect from faceted navigation are provided by the service, including built-in support for defining ranges and getting counts for facet results.</span></span> <span data-ttu-id="a9c3a-119">The service also includes sensible defaults that help you avoid unwieldy navigation structures.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-119">The service also includes sensible defaults that help you avoid unwieldy navigation structures.</span></span> 

## <a name="sample-code-and-demo"></a><span data-ttu-id="a9c3a-120">Sample code and demo</span><span class="sxs-lookup"><span data-stu-id="a9c3a-120">Sample code and demo</span></span>
<span data-ttu-id="a9c3a-121">This article uses a job search portal as an example.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-121">This article uses a job search portal as an example.</span></span> <span data-ttu-id="a9c3a-122">The example is implemented as an ASP.NET MVC application.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-122">The example is implemented as an ASP.NET MVC application.</span></span>

-   <span data-ttu-id="a9c3a-123">See and test the working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-123">See and test the working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="a9c3a-124">Download the code from the [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-124">Download the code from the [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

## <a name="get-started"></a><span data-ttu-id="a9c3a-125">Get started</span><span class="sxs-lookup"><span data-stu-id="a9c3a-125">Get started</span></span>
<span data-ttu-id="a9c3a-126">If you're new to search development, the best way to think of faceted navigation is that it shows the possibilities for self-directed search.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-126">If you're new to search development, the best way to think of faceted navigation is that it shows the possibilities for self-directed search.</span></span> <span data-ttu-id="a9c3a-127">It’s a type of drill-down search experience, based on predefined filters, used for quickly narrowing down search results through point-and-click actions.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-127">It’s a type of drill-down search experience, based on predefined filters, used for quickly narrowing down search results through point-and-click actions.</span></span> 

### <a name="interaction-model"></a><span data-ttu-id="a9c3a-128">Interaction model</span><span class="sxs-lookup"><span data-stu-id="a9c3a-128">Interaction model</span></span>

<span data-ttu-id="a9c3a-129">The search experience for faceted navigation is iterative, so let’s start by understanding it as a sequence of queries that unfold in response to user actions.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-129">The search experience for faceted navigation is iterative, so let’s start by understanding it as a sequence of queries that unfold in response to user actions.</span></span>

<span data-ttu-id="a9c3a-130">The starting point is an application page that provides faceted navigation, typically placed on the periphery.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-130">The starting point is an application page that provides faceted navigation, typically placed on the periphery.</span></span> <span data-ttu-id="a9c3a-131">Faceted navigation is often a tree structure, with checkboxes for each value, or clickable text.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-131">Faceted navigation is often a tree structure, with checkboxes for each value, or clickable text.</span></span> 

1. <span data-ttu-id="a9c3a-132">A query sent to Azure Search specifies the faceted navigation structure via one or more facet query parameters.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-132">A query sent to Azure Search specifies the faceted navigation structure via one or more facet query parameters.</span></span> <span data-ttu-id="a9c3a-133">For instance, the query might include `facet=Rating`, perhaps with a `:values` or `:sort` option to further refine the presentation.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-133">For instance, the query might include `facet=Rating`, perhaps with a `:values` or `:sort` option to further refine the presentation.</span></span>
2. <span data-ttu-id="a9c3a-134">The presentation layer renders a search page that provides faceted navigation, using the facets specified on the request.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-134">The presentation layer renders a search page that provides faceted navigation, using the facets specified on the request.</span></span>
3. <span data-ttu-id="a9c3a-135">Given a faceted navigation structure that includes Rating, you click "4" to indicate that only products with a rating of 4 or higher should be shown.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-135">Given a faceted navigation structure that includes Rating, you click "4" to indicate that only products with a rating of 4 or higher should be shown.</span></span> 
4. <span data-ttu-id="a9c3a-136">In response, the application sends a query that includes `$filter=Rating ge 4`</span><span class="sxs-lookup"><span data-stu-id="a9c3a-136">In response, the application sends a query that includes `$filter=Rating ge 4`</span></span> 
5. <span data-ttu-id="a9c3a-137">The presentation layer updates the page, showing a reduced result set, containing just those items that satisfy the new criteria (in this case, products rated 4 and up).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-137">The presentation layer updates the page, showing a reduced result set, containing just those items that satisfy the new criteria (in this case, products rated 4 and up).</span></span>

<span data-ttu-id="a9c3a-138">A facet is a query parameter, but do not confuse it with query input.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-138">A facet is a query parameter, but do not confuse it with query input.</span></span> <span data-ttu-id="a9c3a-139">It is never used as selection criteria in a query.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-139">It is never used as selection criteria in a query.</span></span> <span data-ttu-id="a9c3a-140">Instead, think of facet query parameters as inputs to the navigation structure that comes back in the response.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-140">Instead, think of facet query parameters as inputs to the navigation structure that comes back in the response.</span></span> <span data-ttu-id="a9c3a-141">For each facet query parameter you provide, Azure Search evaluates how many documents are in the partial results for each facet value.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-141">For each facet query parameter you provide, Azure Search evaluates how many documents are in the partial results for each facet value.</span></span>

<span data-ttu-id="a9c3a-142">Notice the `$filter` in step 4.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-142">Notice the `$filter` in step 4.</span></span> <span data-ttu-id="a9c3a-143">The filter is an important aspect of faceted navigation.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-143">The filter is an important aspect of faceted navigation.</span></span> <span data-ttu-id="a9c3a-144">Although facets and filters are independent in the API, you need both to deliver the experience you intend.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-144">Although facets and filters are independent in the API, you need both to deliver the experience you intend.</span></span> 

### <a name="app-design-pattern"></a><span data-ttu-id="a9c3a-145">App design pattern</span><span class="sxs-lookup"><span data-stu-id="a9c3a-145">App design pattern</span></span>

<span data-ttu-id="a9c3a-146">In application code, the pattern is to use facet query parameters to return the faceted navigation structure along with facet results, plus a $filter expression.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-146">In application code, the pattern is to use facet query parameters to return the faceted navigation structure along with facet results, plus a $filter expression.</span></span>  <span data-ttu-id="a9c3a-147">The filter expression handles the click event on the facet value.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-147">The filter expression handles the click event on the facet value.</span></span> <span data-ttu-id="a9c3a-148">Think of the `$filter` expression as the code behind the actual trimming of search results returned to the presentation layer.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-148">Think of the `$filter` expression as the code behind the actual trimming of search results returned to the presentation layer.</span></span> <span data-ttu-id="a9c3a-149">Given a Colors facet, clicking the color Red is implemented through a `$filter` expression that selects only those items that have a color of red.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-149">Given a Colors facet, clicking the color Red is implemented through a `$filter` expression that selects only those items that have a color of red.</span></span> 

### <a name="query-basics"></a><span data-ttu-id="a9c3a-150">Query basics</span><span class="sxs-lookup"><span data-stu-id="a9c3a-150">Query basics</span></span>

<span data-ttu-id="a9c3a-151">In Azure Search, a request is specified through one or more query parameters (see [Search Documents](http://msdn.microsoft.com/library/azure/dn798927.aspx) for a description of each one).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-151">In Azure Search, a request is specified through one or more query parameters (see [Search Documents](http://msdn.microsoft.com/library/azure/dn798927.aspx) for a description of each one).</span></span> <span data-ttu-id="a9c3a-152">None of the query parameters are required, but you must have at least one in order for a query to be valid.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-152">None of the query parameters are required, but you must have at least one in order for a query to be valid.</span></span>

<span data-ttu-id="a9c3a-153">Precision, understood as the ability to filter out irrelevant hits, is achieved through one or both of these expressions:</span><span class="sxs-lookup"><span data-stu-id="a9c3a-153">Precision, understood as the ability to filter out irrelevant hits, is achieved through one or both of these expressions:</span></span>

-   <span data-ttu-id="a9c3a-154">**search=**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-154">**search=**</span></span>  
    <span data-ttu-id="a9c3a-155">The value of this parameter constitutes the search expression.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-155">The value of this parameter constitutes the search expression.</span></span> <span data-ttu-id="a9c3a-156">It might be a single piece of text, or a complex search expression that includes multiple terms and operators.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-156">It might be a single piece of text, or a complex search expression that includes multiple terms and operators.</span></span> <span data-ttu-id="a9c3a-157">On the server, a search expression is used for full-text search, querying searchable fields in the index for matching terms, returning results in rank order.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-157">On the server, a search expression is used for full-text search, querying searchable fields in the index for matching terms, returning results in rank order.</span></span> <span data-ttu-id="a9c3a-158">If you set `search` to null, query execution is over the entire index (that is, `search=*`).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-158">If you set `search` to null, query execution is over the entire index (that is, `search=*`).</span></span> <span data-ttu-id="a9c3a-159">In this case, other elements of the query, such as a `$filter` or scoring profile, are the primary factors affecting which documents are returned `($filter`) and in what order (`scoringProfile` or `$orderby`).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-159">In this case, other elements of the query, such as a `$filter` or scoring profile, are the primary factors affecting which documents are returned `($filter`) and in what order (`scoringProfile` or `$orderby`).</span></span>

-   <span data-ttu-id="a9c3a-160">**$filter=**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-160">**$filter=**</span></span>  
    <span data-ttu-id="a9c3a-161">A filter is a powerful mechanism for limiting the size of search results based on the values of specific document attributes.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-161">A filter is a powerful mechanism for limiting the size of search results based on the values of specific document attributes.</span></span> <span data-ttu-id="a9c3a-162">A `$filter` is evaluated first, followed by faceting logic that generates the available values and corresponding counts for each value</span><span class="sxs-lookup"><span data-stu-id="a9c3a-162">A `$filter` is evaluated first, followed by faceting logic that generates the available values and corresponding counts for each value</span></span>

<span data-ttu-id="a9c3a-163">Complex search expressions decrease the performance of the query.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-163">Complex search expressions decrease the performance of the query.</span></span> <span data-ttu-id="a9c3a-164">Where possible, use well-constructed filter expressions to increase precision and improve query performance.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-164">Where possible, use well-constructed filter expressions to increase precision and improve query performance.</span></span>

<span data-ttu-id="a9c3a-165">To better understand how a filter adds more precision, compare a complex search expression to one that includes a filter expression:</span><span class="sxs-lookup"><span data-stu-id="a9c3a-165">To better understand how a filter adds more precision, compare a complex search expression to one that includes a filter expression:</span></span>

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

<span data-ttu-id="a9c3a-166">Both queries are valid, but the second is superior if you’re looking for non-motels with parking in Seattle.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-166">Both queries are valid, but the second is superior if you’re looking for non-motels with parking in Seattle.</span></span>
-   <span data-ttu-id="a9c3a-167">The first query relies on those specific words being mentioned or not mentioned in string fields like Name, Description, and any other field containing searchable data.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-167">The first query relies on those specific words being mentioned or not mentioned in string fields like Name, Description, and any other field containing searchable data.</span></span>
-   <span data-ttu-id="a9c3a-168">The second query looks for precise matches on structured data and is likely to be much more accurate.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-168">The second query looks for precise matches on structured data and is likely to be much more accurate.</span></span>

<span data-ttu-id="a9c3a-169">In applications that include faceted navigation, make sure that each user action over a faceted navigation structure is accompanied by a narrowing of search results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-169">In applications that include faceted navigation, make sure that each user action over a faceted navigation structure is accompanied by a narrowing of search results.</span></span> <span data-ttu-id="a9c3a-170">To narrow results, use a filter expression.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-170">To narrow results, use a filter expression.</span></span>

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a><span data-ttu-id="a9c3a-171">Build a faceted navigation app</span><span class="sxs-lookup"><span data-stu-id="a9c3a-171">Build a faceted navigation app</span></span>
<span data-ttu-id="a9c3a-172">You implement faceted navigation with Azure Search in your application code that builds the search request.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-172">You implement faceted navigation with Azure Search in your application code that builds the search request.</span></span> <span data-ttu-id="a9c3a-173">The faceted navigation relies on elements in your schema that you defined previously.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-173">The faceted navigation relies on elements in your schema that you defined previously.</span></span>

<span data-ttu-id="a9c3a-174">Predefined in your search index is the `Facetable [true|false]` index attribute, set on selected fields to enable or disable their use in a faceted navigation structure.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-174">Predefined in your search index is the `Facetable [true|false]` index attribute, set on selected fields to enable or disable their use in a faceted navigation structure.</span></span> <span data-ttu-id="a9c3a-175">Without `"Facetable" = true`, a field cannot be used in facet navigation.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-175">Without `"Facetable" = true`, a field cannot be used in facet navigation.</span></span>

<span data-ttu-id="a9c3a-176">The presentation layer in your code provides the user experience.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-176">The presentation layer in your code provides the user experience.</span></span> <span data-ttu-id="a9c3a-177">It should list the constituent parts of the faceted navigation, such as the label, values, check boxes, and the count.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-177">It should list the constituent parts of the faceted navigation, such as the label, values, check boxes, and the count.</span></span> <span data-ttu-id="a9c3a-178">The Azure Search REST API is platform agnostic, so use whatever language and platform you want.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-178">The Azure Search REST API is platform agnostic, so use whatever language and platform you want.</span></span> <span data-ttu-id="a9c3a-179">The important thing is to include UI elements that support incremental refresh, with updated UI state as each additional facet is selected.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-179">The important thing is to include UI elements that support incremental refresh, with updated UI state as each additional facet is selected.</span></span> 

<span data-ttu-id="a9c3a-180">At query time, your application code creates a request that includes `facet=[string]`, a request parameter that provides the field to facet by.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-180">At query time, your application code creates a request that includes `facet=[string]`, a request parameter that provides the field to facet by.</span></span> <span data-ttu-id="a9c3a-181">A query can have multiple facets, such as `&facet=color&facet=category&facet=rating`, each one separated by an ampersand (&) character.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-181">A query can have multiple facets, such as `&facet=color&facet=category&facet=rating`, each one separated by an ampersand (&) character.</span></span>

<span data-ttu-id="a9c3a-182">Application code must also construct a `$filter` expression to handle the click events in faceted navigation.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-182">Application code must also construct a `$filter` expression to handle the click events in faceted navigation.</span></span> <span data-ttu-id="a9c3a-183">A `$filter` reduces the search results, using the facet value as filter criteria.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-183">A `$filter` reduces the search results, using the facet value as filter criteria.</span></span>

<span data-ttu-id="a9c3a-184">Azure Search returns the search results, based on one or more terms that you enter, along with updates to the faceted navigation structure.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-184">Azure Search returns the search results, based on one or more terms that you enter, along with updates to the faceted navigation structure.</span></span> <span data-ttu-id="a9c3a-185">In Azure Search, faceted navigation is a single-level construction, with facet values, and counts of how many results are found for each one.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-185">In Azure Search, faceted navigation is a single-level construction, with facet values, and counts of how many results are found for each one.</span></span>

<span data-ttu-id="a9c3a-186">In the following sections, we take a closer look at how to build each part.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-186">In the following sections, we take a closer look at how to build each part.</span></span>

<a name="buildindex"></a>

## <a name="build-the-index"></a><span data-ttu-id="a9c3a-187">Build the index</span><span class="sxs-lookup"><span data-stu-id="a9c3a-187">Build the index</span></span>
<span data-ttu-id="a9c3a-188">Faceting is enabled on a field-by-field basis in the index, via this index attribute: `"Facetable": true`.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-188">Faceting is enabled on a field-by-field basis in the index, via this index attribute: `"Facetable": true`.</span></span>  
<span data-ttu-id="a9c3a-189">All field types that could possibly be used in faceted navigation are `Facetable` by default.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-189">All field types that could possibly be used in faceted navigation are `Facetable` by default.</span></span> <span data-ttu-id="a9c3a-190">Such field types include `Edm.String`, `Edm.DateTimeOffset`, and all the numeric field types (essentially, all field types are facetable except `Edm.GeographyPoint`, which can’t be used in faceted navigation).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-190">Such field types include `Edm.String`, `Edm.DateTimeOffset`, and all the numeric field types (essentially, all field types are facetable except `Edm.GeographyPoint`, which can’t be used in faceted navigation).</span></span> 

<span data-ttu-id="a9c3a-191">When building an index, a best practice for faceted navigation is to explicitly turn faceting off for fields that should never be used as a facet.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-191">When building an index, a best practice for faceted navigation is to explicitly turn faceting off for fields that should never be used as a facet.</span></span>  <span data-ttu-id="a9c3a-192">In particular, string fields for singleton values, such as an ID or product name, should be set to `"Facetable": false` to prevent their accidental (and ineffective) use in faceted navigation.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-192">In particular, string fields for singleton values, such as an ID or product name, should be set to `"Facetable": false` to prevent their accidental (and ineffective) use in faceted navigation.</span></span> <span data-ttu-id="a9c3a-193">Turning faceting off where you don’t need it helps keep the size of the index small, and typically improves performance.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-193">Turning faceting off where you don’t need it helps keep the size of the index small, and typically improves performance.</span></span>

<span data-ttu-id="a9c3a-194">Following is part of the schema for the Job Portal Demo sample app, trimmed of some attributes to reduce the size:</span><span class="sxs-lookup"><span data-stu-id="a9c3a-194">Following is part of the schema for the Job Portal Demo sample app, trimmed of some attributes to reduce the size:</span></span>

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

<span data-ttu-id="a9c3a-195">As you can see in the sample schema, `Facetable` is turned off for string fields that shouldn’t be used as facets, such as ID values.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-195">As you can see in the sample schema, `Facetable` is turned off for string fields that shouldn’t be used as facets, such as ID values.</span></span> <span data-ttu-id="a9c3a-196">Turning faceting off where you don’t need it helps keep the size of the index small, and typically improves performance.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-196">Turning faceting off where you don’t need it helps keep the size of the index small, and typically improves performance.</span></span>

> [!TIP]
> <span data-ttu-id="a9c3a-197">As a best practice, include the full set of index attributes for each field.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-197">As a best practice, include the full set of index attributes for each field.</span></span> <span data-ttu-id="a9c3a-198">Although `Facetable` is on by default for almost all fields, purposely setting each attribute can help you think through the implications of each schema decision.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-198">Although `Facetable` is on by default for almost all fields, purposely setting each attribute can help you think through the implications of each schema decision.</span></span> 

<a name="checkdata"></a>

## <a name="check-the-data"></a><span data-ttu-id="a9c3a-199">Check the data</span><span class="sxs-lookup"><span data-stu-id="a9c3a-199">Check the data</span></span>
<span data-ttu-id="a9c3a-200">The quality of your data has a direct effect on whether the faceted navigation structure materializes as you expect it to.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-200">The quality of your data has a direct effect on whether the faceted navigation structure materializes as you expect it to.</span></span> <span data-ttu-id="a9c3a-201">It also affects the ease of constructing filters to reduce the result set.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-201">It also affects the ease of constructing filters to reduce the result set.</span></span>

<span data-ttu-id="a9c3a-202">If you want to facet by Brand or Price, each document should contain values for *BrandName* and *ProductPrice* that are valid, consistent, and productive as a filter option.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-202">If you want to facet by Brand or Price, each document should contain values for *BrandName* and *ProductPrice* that are valid, consistent, and productive as a filter option.</span></span>

<span data-ttu-id="a9c3a-203">Here are a few reminders of what to scrub for:</span><span class="sxs-lookup"><span data-stu-id="a9c3a-203">Here are a few reminders of what to scrub for:</span></span>

* <span data-ttu-id="a9c3a-204">For every field that you want to facet by, ask yourself whether it contains values that are suitable as filters in self-directed search.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-204">For every field that you want to facet by, ask yourself whether it contains values that are suitable as filters in self-directed search.</span></span> <span data-ttu-id="a9c3a-205">The values should be short, descriptive, and sufficiently distinctive to offer a clear choice between competing options.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-205">The values should be short, descriptive, and sufficiently distinctive to offer a clear choice between competing options.</span></span>
* <span data-ttu-id="a9c3a-206">Misspellings or nearly matching values.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-206">Misspellings or nearly matching values.</span></span> <span data-ttu-id="a9c3a-207">If you facet on Color, and field values include Orange and Ornage (a misspelling), a facet based on the Color field would pick up both.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-207">If you facet on Color, and field values include Orange and Ornage (a misspelling), a facet based on the Color field would pick up both.</span></span>
* <span data-ttu-id="a9c3a-208">Mixed case text can also wreak havoc in faceted navigation, with orange and Orange appearing as two different values.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-208">Mixed case text can also wreak havoc in faceted navigation, with orange and Orange appearing as two different values.</span></span> 
* <span data-ttu-id="a9c3a-209">Single and plural versions of the same value can result in a separate facet for each.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-209">Single and plural versions of the same value can result in a separate facet for each.</span></span>

<span data-ttu-id="a9c3a-210">As you can imagine, diligence in preparing the data is an essential aspect of effective faceted navigation.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-210">As you can imagine, diligence in preparing the data is an essential aspect of effective faceted navigation.</span></span>

<a name="presentationlayer"></a>

## <a name="build-the-ui"></a><span data-ttu-id="a9c3a-211">Build the UI</span><span class="sxs-lookup"><span data-stu-id="a9c3a-211">Build the UI</span></span>
<span data-ttu-id="a9c3a-212">Working back from the presentation layer can help you uncover requirements that might be missed otherwise, and understand which capabilities are essential to the search experience.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-212">Working back from the presentation layer can help you uncover requirements that might be missed otherwise, and understand which capabilities are essential to the search experience.</span></span>

<span data-ttu-id="a9c3a-213">In terms of faceted navigation, your web or application page displays the faceted navigation structure, detects user input on the page, and inserts the changed elements.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-213">In terms of faceted navigation, your web or application page displays the faceted navigation structure, detects user input on the page, and inserts the changed elements.</span></span> 

<span data-ttu-id="a9c3a-214">For web applications, AJAX is commonly used in the presentation layer because it allows you to refresh incremental changes.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-214">For web applications, AJAX is commonly used in the presentation layer because it allows you to refresh incremental changes.</span></span> <span data-ttu-id="a9c3a-215">You could also use ASP.NET MVC or any other visualization platform that can connect to an Azure Search service over HTTP.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-215">You could also use ASP.NET MVC or any other visualization platform that can connect to an Azure Search service over HTTP.</span></span> <span data-ttu-id="a9c3a-216">The sample application referenced throughout this article -- the **Azure Search Job Portal Demo** – happens to be an ASP.NET MVC application.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-216">The sample application referenced throughout this article -- the **Azure Search Job Portal Demo** – happens to be an ASP.NET MVC application.</span></span>

<span data-ttu-id="a9c3a-217">In the sample, faceted navigation is built into the search results page.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-217">In the sample, faceted navigation is built into the search results page.</span></span> <span data-ttu-id="a9c3a-218">The following example, taken from the `index.cshtml` file of the sample application, shows the static HTML structure for displaying faceted navigation on the search results page.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-218">The following example, taken from the `index.cshtml` file of the sample application, shows the static HTML structure for displaying faceted navigation on the search results page.</span></span> <span data-ttu-id="a9c3a-219">The list of facets is built or rebuilt dynamically when you submit a search term, or select or clear a facet.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-219">The list of facets is built or rebuilt dynamically when you submit a search term, or select or clear a facet.</span></span>

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

<span data-ttu-id="a9c3a-220">The following code snippet from the `index.cshtml` page dynamically builds the HTML to display the first facet, Business Title.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-220">The following code snippet from the `index.cshtml` page dynamically builds the HTML to display the first facet, Business Title.</span></span> <span data-ttu-id="a9c3a-221">Similar functions dynamically build the HTML for the other facets.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-221">Similar functions dynamically build the HTML for the other facets.</span></span> <span data-ttu-id="a9c3a-222">Each facet has a label and a count, which displays the number of items found for that facet result.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-222">Each facet has a label and a count, which displays the number of items found for that facet result.</span></span>

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> <span data-ttu-id="a9c3a-223">When you design the search results page, remember to add a mechanism for clearing facets.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-223">When you design the search results page, remember to add a mechanism for clearing facets.</span></span> <span data-ttu-id="a9c3a-224">If you add check boxes, you can easily see how to clear the filters.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-224">If you add check boxes, you can easily see how to clear the filters.</span></span> <span data-ttu-id="a9c3a-225">For other layouts, you might need a breadcrumb pattern or another creative approach.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-225">For other layouts, you might need a breadcrumb pattern or another creative approach.</span></span> <span data-ttu-id="a9c3a-226">For example, in the Job Search Portal sample application, you can click the `[X]` after a selected facet to clear the facet.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-226">For example, in the Job Search Portal sample application, you can click the `[X]` after a selected facet to clear the facet.</span></span>

<a name="buildquery"></a>

## <a name="build-the-query"></a><span data-ttu-id="a9c3a-227">Build the query</span><span class="sxs-lookup"><span data-stu-id="a9c3a-227">Build the query</span></span>
<span data-ttu-id="a9c3a-228">The code that you write for building queries should specify all parts of a valid query, including search expressions, facets, filters, scoring profiles– anything used to formulate a request.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-228">The code that you write for building queries should specify all parts of a valid query, including search expressions, facets, filters, scoring profiles– anything used to formulate a request.</span></span> <span data-ttu-id="a9c3a-229">In this section, we explore where facets fit into a query, and how filters are used with facets to deliver a reduced result set.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-229">In this section, we explore where facets fit into a query, and how filters are used with facets to deliver a reduced result set.</span></span>

<span data-ttu-id="a9c3a-230">Notice that facets are integral in this sample application.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-230">Notice that facets are integral in this sample application.</span></span> <span data-ttu-id="a9c3a-231">The search experience in the Job Portal Demo is designed around faceted navigation and filters.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-231">The search experience in the Job Portal Demo is designed around faceted navigation and filters.</span></span> <span data-ttu-id="a9c3a-232">The prominent placement of faceted navigation on the page demonstrates its importance.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-232">The prominent placement of faceted navigation on the page demonstrates its importance.</span></span> 

<span data-ttu-id="a9c3a-233">An example is often a good place to begin.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-233">An example is often a good place to begin.</span></span> <span data-ttu-id="a9c3a-234">The following example, taken from the `JobsSearch.cs` file, builds a request that creates facet navigation based on Business Title, Location, Posting Type, and Minimum Salary.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-234">The following example, taken from the `JobsSearch.cs` file, builds a request that creates facet navigation based on Business Title, Location, Posting Type, and Minimum Salary.</span></span> 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

<span data-ttu-id="a9c3a-235">A facet query parameter is set to a field and depending on the data type, can be further parameterized by comma-delimited list that includes `count:<integer>`, `sort:<>`, `interval:<integer>`, and `values:<list>`.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-235">A facet query parameter is set to a field and depending on the data type, can be further parameterized by comma-delimited list that includes `count:<integer>`, `sort:<>`, `interval:<integer>`, and `values:<list>`.</span></span> <span data-ttu-id="a9c3a-236">A values list is supported for numeric data when setting up ranges.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-236">A values list is supported for numeric data when setting up ranges.</span></span> <span data-ttu-id="a9c3a-237">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for usage details.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-237">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for usage details.</span></span>

<span data-ttu-id="a9c3a-238">Along with facets, the request formulated by your application should also build filters to narrow down the set of candidate documents based on a facet value selection.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-238">Along with facets, the request formulated by your application should also build filters to narrow down the set of candidate documents based on a facet value selection.</span></span> <span data-ttu-id="a9c3a-239">For a bike store, faceted navigation provides clues to questions like *What colors, manufacturers, and types of bikes are available?*.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-239">For a bike store, faceted navigation provides clues to questions like *What colors, manufacturers, and types of bikes are available?*.</span></span> <span data-ttu-id="a9c3a-240">Filtering answers questions like *Which exact bikes are red, mountain bikes, in this price range?*.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-240">Filtering answers questions like *Which exact bikes are red, mountain bikes, in this price range?*.</span></span> <span data-ttu-id="a9c3a-241">When you click "Red" to indicate that only Red products should be shown, the next query the application sends includes `$filter=Color eq ‘Red’`.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-241">When you click "Red" to indicate that only Red products should be shown, the next query the application sends includes `$filter=Color eq ‘Red’`.</span></span>

<span data-ttu-id="a9c3a-242">The following code snippet from the `JobsSearch.cs` page adds the selected Business Title to the filter if you select a value from the Business Title facet.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-242">The following code snippet from the `JobsSearch.cs` page adds the selected Business Title to the filter if you select a value from the Business Title facet.</span></span>

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a><span data-ttu-id="a9c3a-243">Tips and best practices</span><span class="sxs-lookup"><span data-stu-id="a9c3a-243">Tips and best practices</span></span>

### <a name="indexing-tips"></a><span data-ttu-id="a9c3a-244">Indexing tips</span><span class="sxs-lookup"><span data-stu-id="a9c3a-244">Indexing tips</span></span>
<span data-ttu-id="a9c3a-245">**Improve index efficiency if you don't use a Search box**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-245">**Improve index efficiency if you don't use a Search box**</span></span>

<span data-ttu-id="a9c3a-246">If your application uses faceted navigation exclusively (that is, no search box), you can mark the field as `searchable=false`, `facetable=true` to produce a more compact index.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-246">If your application uses faceted navigation exclusively (that is, no search box), you can mark the field as `searchable=false`, `facetable=true` to produce a more compact index.</span></span> <span data-ttu-id="a9c3a-247">In addition, indexing occurs only on whole facet values, with no word-break or indexing of the component parts of a multi-word value.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-247">In addition, indexing occurs only on whole facet values, with no word-break or indexing of the component parts of a multi-word value.</span></span>

<span data-ttu-id="a9c3a-248">**Specify which fields can be used as facets**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-248">**Specify which fields can be used as facets**</span></span>

<span data-ttu-id="a9c3a-249">Recall that the schema of the index determines which fields are available to use as a facet.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-249">Recall that the schema of the index determines which fields are available to use as a facet.</span></span> <span data-ttu-id="a9c3a-250">Assuming a field is facetable, the query specifies which fields to facet by.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-250">Assuming a field is facetable, the query specifies which fields to facet by.</span></span> <span data-ttu-id="a9c3a-251">The field by which you are faceting provides the values that appear below the label.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-251">The field by which you are faceting provides the values that appear below the label.</span></span> 

<span data-ttu-id="a9c3a-252">The values that appear under each label are retrieved from the index.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-252">The values that appear under each label are retrieved from the index.</span></span> <span data-ttu-id="a9c3a-253">For example, if the facet field is *Color*, the values available for additional filtering are the values for that field - Red, Black, and so forth.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-253">For example, if the facet field is *Color*, the values available for additional filtering are the values for that field - Red, Black, and so forth.</span></span>

<span data-ttu-id="a9c3a-254">For Numeric and DateTime values only, you can explicitly set values on the facet field (for example, `facet=Rating,values:1|2|3|4|5`).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-254">For Numeric and DateTime values only, you can explicitly set values on the facet field (for example, `facet=Rating,values:1|2|3|4|5`).</span></span> <span data-ttu-id="a9c3a-255">A values list is allowed for these field types to simplify the separation of facet results into contiguous ranges (either ranges based on numeric values or time periods).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-255">A values list is allowed for these field types to simplify the separation of facet results into contiguous ranges (either ranges based on numeric values or time periods).</span></span> 

<span data-ttu-id="a9c3a-256">**By default you can only have one level of faceted navigation**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-256">**By default you can only have one level of faceted navigation**</span></span> 

<span data-ttu-id="a9c3a-257">As noted, there is no direct support for nesting facets in a hierarchy.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-257">As noted, there is no direct support for nesting facets in a hierarchy.</span></span> <span data-ttu-id="a9c3a-258">By default, faceted navigation in Azure Search only supports one level of filters.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-258">By default, faceted navigation in Azure Search only supports one level of filters.</span></span> <span data-ttu-id="a9c3a-259">However, workarounds do exist.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-259">However, workarounds do exist.</span></span> <span data-ttu-id="a9c3a-260">You can encode a hierarchical facet structure in a `Collection(Edm.String)` with one entry point per hierarchy.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-260">You can encode a hierarchical facet structure in a `Collection(Edm.String)` with one entry point per hierarchy.</span></span> <span data-ttu-id="a9c3a-261">Implementing this workaround is beyond the scope of this article.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-261">Implementing this workaround is beyond the scope of this article.</span></span> 

### <a name="querying-tips"></a><span data-ttu-id="a9c3a-262">Querying tips</span><span class="sxs-lookup"><span data-stu-id="a9c3a-262">Querying tips</span></span>
<span data-ttu-id="a9c3a-263">**Validate fields**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-263">**Validate fields**</span></span>

<span data-ttu-id="a9c3a-264">If you build the list of facets dynamically based on untrusted user input, validate that the names of the faceted fields are valid.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-264">If you build the list of facets dynamically based on untrusted user input, validate that the names of the faceted fields are valid.</span></span> <span data-ttu-id="a9c3a-265">Or, escape the names when building URLs by using either `Uri.EscapeDataString()` in .NET, or the equivalent in your platform of choice.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-265">Or, escape the names when building URLs by using either `Uri.EscapeDataString()` in .NET, or the equivalent in your platform of choice.</span></span>

### <a name="filtering-tips"></a><span data-ttu-id="a9c3a-266">Filtering tips</span><span class="sxs-lookup"><span data-stu-id="a9c3a-266">Filtering tips</span></span>
<span data-ttu-id="a9c3a-267">**Increase search precision with filters**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-267">**Increase search precision with filters**</span></span>

<span data-ttu-id="a9c3a-268">Use filters.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-268">Use filters.</span></span> <span data-ttu-id="a9c3a-269">If you rely on just search expressions alone, stemming could cause a document to be returned that doesn’t have the precise facet value in any of its fields.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-269">If you rely on just search expressions alone, stemming could cause a document to be returned that doesn’t have the precise facet value in any of its fields.</span></span>

<span data-ttu-id="a9c3a-270">**Increase search performance with filters**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-270">**Increase search performance with filters**</span></span>

<span data-ttu-id="a9c3a-271">Filters narrow down the set of candidate documents for search and exclude them from ranking.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-271">Filters narrow down the set of candidate documents for search and exclude them from ranking.</span></span> <span data-ttu-id="a9c3a-272">If you have a large set of documents, using a selective facet drill-down often gives you better performance.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-272">If you have a large set of documents, using a selective facet drill-down often gives you better performance.</span></span>
  
<span data-ttu-id="a9c3a-273">**Filter only the faceted fields**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-273">**Filter only the faceted fields**</span></span>

<span data-ttu-id="a9c3a-274">In faceted drill-down, you typically want to only include documents that have the facet value in a specific (faceted) field, not anywhere across all searchable fields.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-274">In faceted drill-down, you typically want to only include documents that have the facet value in a specific (faceted) field, not anywhere across all searchable fields.</span></span> <span data-ttu-id="a9c3a-275">Adding a filter reinforces the target field by directing the service to search only in the faceted field for a matching value.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-275">Adding a filter reinforces the target field by directing the service to search only in the faceted field for a matching value.</span></span>

<span data-ttu-id="a9c3a-276">**Trim facet results with more filters**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-276">**Trim facet results with more filters**</span></span>

<span data-ttu-id="a9c3a-277">Facet results are documents found in the search results that match a facet term.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-277">Facet results are documents found in the search results that match a facet term.</span></span> <span data-ttu-id="a9c3a-278">In the following example, in search results for *cloud computing*, 254 items also have *internal specification* as a content type.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-278">In the following example, in search results for *cloud computing*, 254 items also have *internal specification* as a content type.</span></span> <span data-ttu-id="a9c3a-279">Items are not necessarily mutually exclusive.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-279">Items are not necessarily mutually exclusive.</span></span> <span data-ttu-id="a9c3a-280">If an item meets the criteria of both filters, it is counted in each one.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-280">If an item meets the criteria of both filters, it is counted in each one.</span></span> <span data-ttu-id="a9c3a-281">This duplication is possible when faceting on `Collection(Edm.String)` fields, which are often used to implement document tagging.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-281">This duplication is possible when faceting on `Collection(Edm.String)` fields, which are often used to implement document tagging.</span></span>

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

<span data-ttu-id="a9c3a-282">In general, if you find that facet results are consistently too large, we recommend that you add more filters to give users more options for narrowing the search.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-282">In general, if you find that facet results are consistently too large, we recommend that you add more filters to give users more options for narrowing the search.</span></span>

### <a name="tips-about-result-count"></a><span data-ttu-id="a9c3a-283">Tips about result count</span><span class="sxs-lookup"><span data-stu-id="a9c3a-283">Tips about result count</span></span>

<span data-ttu-id="a9c3a-284">**Limit the number of items in the facet navigation**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-284">**Limit the number of items in the facet navigation**</span></span>

<span data-ttu-id="a9c3a-285">For each faceted field in the navigation tree, there is a default limit of 10 values.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-285">For each faceted field in the navigation tree, there is a default limit of 10 values.</span></span> <span data-ttu-id="a9c3a-286">This default makes sense for navigation structures because it keeps the values list to a manageable size.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-286">This default makes sense for navigation structures because it keeps the values list to a manageable size.</span></span> <span data-ttu-id="a9c3a-287">You can override the default by assigning a value to count.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-287">You can override the default by assigning a value to count.</span></span>

* <span data-ttu-id="a9c3a-288">`&facet=city,count:5` specifies that only the first five cities found in the top ranked results are returned as a facet result.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-288">`&facet=city,count:5` specifies that only the first five cities found in the top ranked results are returned as a facet result.</span></span> <span data-ttu-id="a9c3a-289">Consider a sample query with a search term of “airport” and 32 matches.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-289">Consider a sample query with a search term of “airport” and 32 matches.</span></span> <span data-ttu-id="a9c3a-290">If the query specifies `&facet=city,count:5`, only the first five unique cities with the most documents in the search results are included in the facet results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-290">If the query specifies `&facet=city,count:5`, only the first five unique cities with the most documents in the search results are included in the facet results.</span></span>

<span data-ttu-id="a9c3a-291">Notice the distinction between facet results and search results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-291">Notice the distinction between facet results and search results.</span></span> <span data-ttu-id="a9c3a-292">Search results are all the documents that match the query.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-292">Search results are all the documents that match the query.</span></span> <span data-ttu-id="a9c3a-293">Facet results are the matches for each facet value.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-293">Facet results are the matches for each facet value.</span></span> <span data-ttu-id="a9c3a-294">In the example, search results include City names that are not in the facet classification list (5 in our example).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-294">In the example, search results include City names that are not in the facet classification list (5 in our example).</span></span> <span data-ttu-id="a9c3a-295">Results that are filtered out through faceted navigation become visible when you clear facets, or choose other facets besides City.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-295">Results that are filtered out through faceted navigation become visible when you clear facets, or choose other facets besides City.</span></span> 

> [!NOTE]
> <span data-ttu-id="a9c3a-296">Discussing `count` when there is more than one type can be confusing.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-296">Discussing `count` when there is more than one type can be confusing.</span></span> <span data-ttu-id="a9c3a-297">The following table offers a brief summary of how the term is used in Azure Search API, sample code, and documentation.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-297">The following table offers a brief summary of how the term is used in Azure Search API, sample code, and documentation.</span></span> 

* `@colorFacet.count`<br/>
  <span data-ttu-id="a9c3a-298">In presentation code, you should see a count parameter on the facet, used to display the number of facet results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-298">In presentation code, you should see a count parameter on the facet, used to display the number of facet results.</span></span> <span data-ttu-id="a9c3a-299">In facet results, count indicates the number of documents that match on the facet term or range.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-299">In facet results, count indicates the number of documents that match on the facet term or range.</span></span>
* `&facet=City,count:12`<br/>
  <span data-ttu-id="a9c3a-300">In a facet query, you can set count to a value.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-300">In a facet query, you can set count to a value.</span></span>  <span data-ttu-id="a9c3a-301">The default is 10, but you can set it higher or lower.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-301">The default is 10, but you can set it higher or lower.</span></span> <span data-ttu-id="a9c3a-302">Setting `count:12` gets the top 12 matches in facet results by document count.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-302">Setting `count:12` gets the top 12 matches in facet results by document count.</span></span>
* <span data-ttu-id="a9c3a-303">"`@odata.count`"</span><span class="sxs-lookup"><span data-stu-id="a9c3a-303">"`@odata.count`"</span></span><br/>
  <span data-ttu-id="a9c3a-304">In the query response, this value indicates the number of matching items in the search results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-304">In the query response, this value indicates the number of matching items in the search results.</span></span> <span data-ttu-id="a9c3a-305">On average, it’s larger than the sum of all facet results combined, due to the presence of items that match the search term, but have no facet value matches.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-305">On average, it’s larger than the sum of all facet results combined, due to the presence of items that match the search term, but have no facet value matches.</span></span>

<span data-ttu-id="a9c3a-306">**Get counts in facet results**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-306">**Get counts in facet results**</span></span>

<span data-ttu-id="a9c3a-307">When you add a filter to a faceted query, you might want to retain the facet statement (for example, `facet=Rating&$filter=Rating ge 4`).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-307">When you add a filter to a faceted query, you might want to retain the facet statement (for example, `facet=Rating&$filter=Rating ge 4`).</span></span> <span data-ttu-id="a9c3a-308">Technically, facet=Rating isn’t needed, but keeping it returns the counts of facet values for ratings 4 and higher.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-308">Technically, facet=Rating isn’t needed, but keeping it returns the counts of facet values for ratings 4 and higher.</span></span> <span data-ttu-id="a9c3a-309">For example, if you click "4" and the query includes a filter for greater or equal to "4", counts are returned for each rating that is 4 and higher.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-309">For example, if you click "4" and the query includes a filter for greater or equal to "4", counts are returned for each rating that is 4 and higher.</span></span>  

<span data-ttu-id="a9c3a-310">**Make sure you get accurate facet counts**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-310">**Make sure you get accurate facet counts**</span></span>

<span data-ttu-id="a9c3a-311">Under certain circumstances, you might find that facet counts do not match the result sets (see [Faceted navigation in Azure Search (forum post)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-311">Under certain circumstances, you might find that facet counts do not match the result sets (see [Faceted navigation in Azure Search (forum post)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).</span></span>

<span data-ttu-id="a9c3a-312">Facet counts can be inaccurate due to the sharding architecture.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-312">Facet counts can be inaccurate due to the sharding architecture.</span></span> <span data-ttu-id="a9c3a-313">Every search index has multiple shards, and each shard reports the top N facets by document count, which is then combined into a single result.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-313">Every search index has multiple shards, and each shard reports the top N facets by document count, which is then combined into a single result.</span></span> <span data-ttu-id="a9c3a-314">If some shards have many matching values, while others have fewer, you may find that some facet values are missing or under-counted in the results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-314">If some shards have many matching values, while others have fewer, you may find that some facet values are missing or under-counted in the results.</span></span>

<span data-ttu-id="a9c3a-315">Although this behavior could change at any time, if you encounter this behavior today, you can work around it by artificially inflating the count:<number> to a large number to enforce full reporting from each shard.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-315">Although this behavior could change at any time, if you encounter this behavior today, you can work around it by artificially inflating the count:<number> to a large number to enforce full reporting from each shard.</span></span> <span data-ttu-id="a9c3a-316">If the value of count: is greater than or equal to the number of unique values in the field, you are guaranteed accurate results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-316">If the value of count: is greater than or equal to the number of unique values in the field, you are guaranteed accurate results.</span></span> <span data-ttu-id="a9c3a-317">However, when document counts are high, there is a performance penalty, so use this option judiciously.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-317">However, when document counts are high, there is a performance penalty, so use this option judiciously.</span></span>

### <a name="user-interface-tips"></a><span data-ttu-id="a9c3a-318">User interface tips</span><span class="sxs-lookup"><span data-stu-id="a9c3a-318">User interface tips</span></span>
<span data-ttu-id="a9c3a-319">**Add labels for each field in facet navigation**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-319">**Add labels for each field in facet navigation**</span></span>

<span data-ttu-id="a9c3a-320">Labels are typically defined in the HTML or form (`index.cshtml` in the sample application).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-320">Labels are typically defined in the HTML or form (`index.cshtml` in the sample application).</span></span> <span data-ttu-id="a9c3a-321">There is no API in Azure Search for facet navigation labels or any other metadata.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-321">There is no API in Azure Search for facet navigation labels or any other metadata.</span></span>

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a><span data-ttu-id="a9c3a-322">Filter based on a range</span><span class="sxs-lookup"><span data-stu-id="a9c3a-322">Filter based on a range</span></span>
<span data-ttu-id="a9c3a-323">Faceting over ranges of values is a common search application requirement.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-323">Faceting over ranges of values is a common search application requirement.</span></span> <span data-ttu-id="a9c3a-324">Ranges are supported for numeric data and DateTime values.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-324">Ranges are supported for numeric data and DateTime values.</span></span> <span data-ttu-id="a9c3a-325">You can read more about each approach in [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-325">You can read more about each approach in [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx).</span></span>

<span data-ttu-id="a9c3a-326">Azure Search simplifies range construction by providing two approaches for computing a range.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-326">Azure Search simplifies range construction by providing two approaches for computing a range.</span></span> <span data-ttu-id="a9c3a-327">For both approaches, Azure Search creates the appropriate ranges given the inputs you’ve provided.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-327">For both approaches, Azure Search creates the appropriate ranges given the inputs you’ve provided.</span></span> <span data-ttu-id="a9c3a-328">For instance, if you specify range values of 10|20|30, it automatically creates ranges of 0-10, 10-20, 20-30.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-328">For instance, if you specify range values of 10|20|30, it automatically creates ranges of 0-10, 10-20, 20-30.</span></span> <span data-ttu-id="a9c3a-329">Your application can optionally remove any intervals that are empty.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-329">Your application can optionally remove any intervals that are empty.</span></span> 

<span data-ttu-id="a9c3a-330">**Approach 1: Use the interval parameter**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-330">**Approach 1: Use the interval parameter**</span></span>  
<span data-ttu-id="a9c3a-331">To set price facets in $10 increments, you would specify: `&facet=price,interval:10`</span><span class="sxs-lookup"><span data-stu-id="a9c3a-331">To set price facets in $10 increments, you would specify: `&facet=price,interval:10`</span></span>

<span data-ttu-id="a9c3a-332">**Approach 2: Use a values list**</span><span class="sxs-lookup"><span data-stu-id="a9c3a-332">**Approach 2: Use a values list**</span></span>  
<span data-ttu-id="a9c3a-333">For numeric data, you can use a values list.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-333">For numeric data, you can use a values list.</span></span>  <span data-ttu-id="a9c3a-334">Consider the facet range for a `listPrice` field, rendered as follows:</span><span class="sxs-lookup"><span data-stu-id="a9c3a-334">Consider the facet range for a `listPrice` field, rendered as follows:</span></span>

  ![Sample values list][5]

<span data-ttu-id="a9c3a-336">To specify a facet range like the one in the preceding screen shot, use a values list:</span><span class="sxs-lookup"><span data-stu-id="a9c3a-336">To specify a facet range like the one in the preceding screen shot, use a values list:</span></span>

    facet=listPrice,values:10|25|100|500|1000|2500

<span data-ttu-id="a9c3a-337">Each range is built using 0 as a starting point, a value from the list as an endpoint, and then trimmed of the previous range to create discrete intervals.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-337">Each range is built using 0 as a starting point, a value from the list as an endpoint, and then trimmed of the previous range to create discrete intervals.</span></span> <span data-ttu-id="a9c3a-338">Azure Search does these things as part of faceted navigation.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-338">Azure Search does these things as part of faceted navigation.</span></span> <span data-ttu-id="a9c3a-339">You do not have to write code for structuring each interval.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-339">You do not have to write code for structuring each interval.</span></span>

### <a name="build-a-filter-for-a-range"></a><span data-ttu-id="a9c3a-340">Build a filter for a range</span><span class="sxs-lookup"><span data-stu-id="a9c3a-340">Build a filter for a range</span></span>
<span data-ttu-id="a9c3a-341">To filter documents based on a range you select, you can use the `"ge"` and `"lt"` filter operators in a two-part expression that defines the endpoints of the range.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-341">To filter documents based on a range you select, you can use the `"ge"` and `"lt"` filter operators in a two-part expression that defines the endpoints of the range.</span></span> <span data-ttu-id="a9c3a-342">For example, if you choose the range 10-25 for a `listPrice` field, the filter would be `$filter=listPrice ge 10 and listPrice lt 25`.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-342">For example, if you choose the range 10-25 for a `listPrice` field, the filter would be `$filter=listPrice ge 10 and listPrice lt 25`.</span></span> <span data-ttu-id="a9c3a-343">In the sample code, the filter expression uses **priceFrom** and **priceTo** parameters to set the endpoints.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-343">In the sample code, the filter expression uses **priceFrom** and **priceTo** parameters to set the endpoints.</span></span> 

  ![Query for a range of values][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a><span data-ttu-id="a9c3a-345">Filter based on distance</span><span class="sxs-lookup"><span data-stu-id="a9c3a-345">Filter based on distance</span></span>
<span data-ttu-id="a9c3a-346">It’s common to see filters that help you choose a store, restaurant, or destination based on its proximity to your current location.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-346">It’s common to see filters that help you choose a store, restaurant, or destination based on its proximity to your current location.</span></span> <span data-ttu-id="a9c3a-347">While this type of filter might look like faceted navigation, it’s just a filter.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-347">While this type of filter might look like faceted navigation, it’s just a filter.</span></span> <span data-ttu-id="a9c3a-348">We mention it here for those of you who are specifically looking for implementation advice for that particular design problem.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-348">We mention it here for those of you who are specifically looking for implementation advice for that particular design problem.</span></span>

<span data-ttu-id="a9c3a-349">There are two Geospatial functions in Azure Search, **geo.distance** and **geo.intersects**.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-349">There are two Geospatial functions in Azure Search, **geo.distance** and **geo.intersects**.</span></span>

* <span data-ttu-id="a9c3a-350">The **geo.distance** function returns the distance in kilometers between two points.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-350">The **geo.distance** function returns the distance in kilometers between two points.</span></span> <span data-ttu-id="a9c3a-351">One point is a field and other is a constant passed as part of the filter.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-351">One point is a field and other is a constant passed as part of the filter.</span></span> 
* <span data-ttu-id="a9c3a-352">The **geo.intersects** function returns true if a given point is within a given polygon.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-352">The **geo.intersects** function returns true if a given point is within a given polygon.</span></span> <span data-ttu-id="a9c3a-353">The point is a field and the polygon is specified as a constant list of coordinates passed as part of the filter.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-353">The point is a field and the polygon is specified as a constant list of coordinates passed as part of the filter.</span></span>

<span data-ttu-id="a9c3a-354">You can find filter examples in [OData expression syntax (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-354">You can find filter examples in [OData expression syntax (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).</span></span>

<a name="tryitout"></a>

## <a name="try-the-demo"></a><span data-ttu-id="a9c3a-355">Try the demo</span><span class="sxs-lookup"><span data-stu-id="a9c3a-355">Try the demo</span></span>
<span data-ttu-id="a9c3a-356">The Azure Search Job Portal Demo contains the examples referenced in this article.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-356">The Azure Search Job Portal Demo contains the examples referenced in this article.</span></span>

-   <span data-ttu-id="a9c3a-357">See and test the working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-357">See and test the working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="a9c3a-358">Download the code from the [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-358">Download the code from the [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

<span data-ttu-id="a9c3a-359">As you work with search results, watch the URL for changes in query construction.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-359">As you work with search results, watch the URL for changes in query construction.</span></span> <span data-ttu-id="a9c3a-360">This application happens to append facets to the URI as you select each one.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-360">This application happens to append facets to the URI as you select each one.</span></span>

1. <span data-ttu-id="a9c3a-361">To use the mapping functionality of the demo app, get a Bing Maps key from the [Bing Maps Dev Center](https://www.bingmapsportal.com/).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-361">To use the mapping functionality of the demo app, get a Bing Maps key from the [Bing Maps Dev Center](https://www.bingmapsportal.com/).</span></span> <span data-ttu-id="a9c3a-362">Paste it over the existing key in the `index.cshtml` page.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-362">Paste it over the existing key in the `index.cshtml` page.</span></span> <span data-ttu-id="a9c3a-363">The `BingApiKey` setting in the `Web.config` file is not used.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-363">The `BingApiKey` setting in the `Web.config` file is not used.</span></span> 

2. <span data-ttu-id="a9c3a-364">Run the application.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-364">Run the application.</span></span> <span data-ttu-id="a9c3a-365">Take the optional tour, or dismiss the dialog box.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-365">Take the optional tour, or dismiss the dialog box.</span></span>
   
3. <span data-ttu-id="a9c3a-366">Enter a search term, such as "analyst", and click the Search icon.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-366">Enter a search term, such as "analyst", and click the Search icon.</span></span> <span data-ttu-id="a9c3a-367">The query executes quickly.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-367">The query executes quickly.</span></span>
   
   <span data-ttu-id="a9c3a-368">A faceted navigation structure is also returned with the search results.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-368">A faceted navigation structure is also returned with the search results.</span></span> <span data-ttu-id="a9c3a-369">In the search result page, the faceted navigation structure includes counts for each facet result.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-369">In the search result page, the faceted navigation structure includes counts for each facet result.</span></span> <span data-ttu-id="a9c3a-370">No facets are selected, so all matching results are returned.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-370">No facets are selected, so all matching results are returned.</span></span>
   
   ![Search results before selecting facets][11]

4. <span data-ttu-id="a9c3a-372">Click a Business Title, Location, or Minimum Salary.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-372">Click a Business Title, Location, or Minimum Salary.</span></span> <span data-ttu-id="a9c3a-373">Facets were null on the initial search, but as they take on values, the search results are trimmed of items that no longer match.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-373">Facets were null on the initial search, but as they take on values, the search results are trimmed of items that no longer match.</span></span>
   
   ![Search results after selecting facets][12]

5. <span data-ttu-id="a9c3a-375">To clear the faceted query so that you can try different query behaviors, click the `[X]` after the selected facets to clear the facets.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-375">To clear the faceted query so that you can try different query behaviors, click the `[X]` after the selected facets to clear the facets.</span></span>
   
<a name="nextstep"></a>

## <a name="learn-more"></a><span data-ttu-id="a9c3a-376">Learn more</span><span class="sxs-lookup"><span data-stu-id="a9c3a-376">Learn more</span></span>
<span data-ttu-id="a9c3a-377">Watch [Azure Search Deep Dive](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410).</span><span class="sxs-lookup"><span data-stu-id="a9c3a-377">Watch [Azure Search Deep Dive](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410).</span></span> <span data-ttu-id="a9c3a-378">At 45:25, there is a demo on how to implement facets.</span><span class="sxs-lookup"><span data-stu-id="a9c3a-378">At 45:25, there is a demo on how to implement facets.</span></span>

<span data-ttu-id="a9c3a-379">For more insights on design principles for faceted navigation, we recommend the following links:</span><span class="sxs-lookup"><span data-stu-id="a9c3a-379">For more insights on design principles for faceted navigation, we recommend the following links:</span></span>

* [<span data-ttu-id="a9c3a-380">Designing for Faceted Search</span><span class="sxs-lookup"><span data-stu-id="a9c3a-380">Designing for Faceted Search</span></span>](http://www.uie.com/articles/faceted_search/)
* [<span data-ttu-id="a9c3a-381">Design Patterns: Faceted Navigation</span><span class="sxs-lookup"><span data-stu-id="a9c3a-381">Design Patterns: Faceted Navigation</span></span>](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How to build it]: #howtobuildit
[Build the presentation layer]: #presentationlayer
[Build the index]: #buildindex
[Check for data quality]: #checkdata
[Build the query]: #buildquery
[Tips on how to control faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/azure-search-faceting-example.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-3-schema.PNG
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-7-appstart.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-8-appbike.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/Facet-10-appTitle.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/faceted-search-before-facets.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx













