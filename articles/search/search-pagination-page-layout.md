---
title: How to page search results in Azure Search | Microsoft Docs
description: Pagination in Azure Search, a hosted cloud search service on Microsoft Azure.
services: search
documentationcenter: ''
author: HeidiSteen
manager: jhubbard
editor: ''
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: 1676c8c7054cbab886365f37a0cdef12894bde01
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563040"
---
# <a name="how-to-page-search-results-in-azure-search"></a><span data-ttu-id="753d1-103">How to page search results in Azure Search</span><span class="sxs-lookup"><span data-stu-id="753d1-103">How to page search results in Azure Search</span></span>
<span data-ttu-id="753d1-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span><span class="sxs-lookup"><span data-stu-id="753d1-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="753d1-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span><span class="sxs-lookup"><span data-stu-id="753d1-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span></span> <span data-ttu-id="753d1-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span><span class="sxs-lookup"><span data-stu-id="753d1-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span></span>

> [!NOTE]
> <span data-ttu-id="753d1-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span><span class="sxs-lookup"><span data-stu-id="753d1-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="753d1-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span><span class="sxs-lookup"><span data-stu-id="753d1-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span></span> <span data-ttu-id="753d1-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span><span class="sxs-lookup"><span data-stu-id="753d1-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="753d1-110">Total hits and Page Counts</span><span class="sxs-lookup"><span data-stu-id="753d1-110">Total hits and Page Counts</span></span>
<span data-ttu-id="753d1-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span><span class="sxs-lookup"><span data-stu-id="753d1-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span></span>

![][1]

<span data-ttu-id="753d1-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span><span class="sxs-lookup"><span data-stu-id="753d1-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span></span> <span data-ttu-id="753d1-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="753d1-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="753d1-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span><span class="sxs-lookup"><span data-stu-id="753d1-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="753d1-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span><span class="sxs-lookup"><span data-stu-id="753d1-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span></span> <span data-ttu-id="753d1-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span><span class="sxs-lookup"><span data-stu-id="753d1-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="753d1-117">Layout</span><span class="sxs-lookup"><span data-stu-id="753d1-117">Layout</span></span>
<span data-ttu-id="753d1-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span><span class="sxs-lookup"><span data-stu-id="753d1-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span></span>

 ![][2]

<span data-ttu-id="753d1-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span><span class="sxs-lookup"><span data-stu-id="753d1-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span></span>

<span data-ttu-id="753d1-120">To return a subset of fields for a tiled layout:</span><span class="sxs-lookup"><span data-stu-id="753d1-120">To return a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="753d1-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span><span class="sxs-lookup"><span data-stu-id="753d1-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span></span> <span data-ttu-id="753d1-122">In the index and documents, define a field that stores the URL address of the external content.</span><span class="sxs-lookup"><span data-stu-id="753d1-122">In the index and documents, define a field that stores the URL address of the external content.</span></span> <span data-ttu-id="753d1-123">You can then use the field as an image reference.</span><span class="sxs-lookup"><span data-stu-id="753d1-123">You can then use the field as an image reference.</span></span> <span data-ttu-id="753d1-124">The URL to the image should be in the document.</span><span class="sxs-lookup"><span data-stu-id="753d1-124">The URL to the image should be in the document.</span></span>

<span data-ttu-id="753d1-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span><span class="sxs-lookup"><span data-stu-id="753d1-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span></span> <span data-ttu-id="753d1-126">The data type of the key is `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="753d1-126">The data type of the key is `Edm.String`.</span></span> <span data-ttu-id="753d1-127">In this example, it is *246810*.</span><span class="sxs-lookup"><span data-stu-id="753d1-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="753d1-128">Sort by relevance, rating, or price</span><span class="sxs-lookup"><span data-stu-id="753d1-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="753d1-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span><span class="sxs-lookup"><span data-stu-id="753d1-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="753d1-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="753d1-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="753d1-131">Relevance is strongly associated with scoring profiles.</span><span class="sxs-lookup"><span data-stu-id="753d1-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="753d1-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span><span class="sxs-lookup"><span data-stu-id="753d1-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span></span>

<span data-ttu-id="753d1-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span><span class="sxs-lookup"><span data-stu-id="753d1-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span></span> <span data-ttu-id="753d1-134">For example, given this page element:</span><span class="sxs-lookup"><span data-stu-id="753d1-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="753d1-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span><span class="sxs-lookup"><span data-stu-id="753d1-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="753d1-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span><span class="sxs-lookup"><span data-stu-id="753d1-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="753d1-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span><span class="sxs-lookup"><span data-stu-id="753d1-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span></span> <span data-ttu-id="753d1-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="753d1-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="753d1-139">Faceted navigation</span><span class="sxs-lookup"><span data-stu-id="753d1-139">Faceted navigation</span></span>
<span data-ttu-id="753d1-140">Search navigation is common on a results page, often located at the side or top of a page.</span><span class="sxs-lookup"><span data-stu-id="753d1-140">Search navigation is common on a results page, often located at the side or top of a page.</span></span> <span data-ttu-id="753d1-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span><span class="sxs-lookup"><span data-stu-id="753d1-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="753d1-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span><span class="sxs-lookup"><span data-stu-id="753d1-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-the-page-level"></a><span data-ttu-id="753d1-143">Filters at the page level</span><span class="sxs-lookup"><span data-stu-id="753d1-143">Filters at the page level</span></span>
<span data-ttu-id="753d1-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span><span class="sxs-lookup"><span data-stu-id="753d1-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span></span> 

<span data-ttu-id="753d1-145">You can send a filter with or without a search expression.</span><span class="sxs-lookup"><span data-stu-id="753d1-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="753d1-146">For example, the following request will filter on brand name, returning only those documents that match it.</span><span class="sxs-lookup"><span data-stu-id="753d1-146">For example, the following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="753d1-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span><span class="sxs-lookup"><span data-stu-id="753d1-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="753d1-148">See Also</span><span class="sxs-lookup"><span data-stu-id="753d1-148">See Also</span></span>
* [<span data-ttu-id="753d1-149">Azure Search Service REST API</span><span class="sxs-lookup"><span data-stu-id="753d1-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="753d1-150">Index Operations</span><span class="sxs-lookup"><span data-stu-id="753d1-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="753d1-151">Document Operations</span><span class="sxs-lookup"><span data-stu-id="753d1-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="753d1-152">Video and tutorials about Azure Search</span><span class="sxs-lookup"><span data-stu-id="753d1-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="753d1-153">Faceted Navigation in Azure Search</span><span class="sxs-lookup"><span data-stu-id="753d1-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-pagination-page-layout/Pages-5-BuildSort.png 





