---
title: Query your Azure Search Index using the .NET SDK | Microsoft Docs
description: Build a search query in Azure search and use search parameters to filter and sort search results.
services: search
manager: jhubbard
documentationcenter: ''
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: brjohnst
ms.openlocfilehash: 88d5148806e58d61b7b64327e07809eea5126211
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550881"
---
# <a name="query-your-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="56f90-103">Query your Azure Search index using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="56f90-103">Query your Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [Overview](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

<span data-ttu-id="56f90-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="56f90-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="56f90-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="56f90-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

<span data-ttu-id="56f90-110">Note that all sample code in this article is written in C#.</span><span class="sxs-lookup"><span data-stu-id="56f90-110">Note that all sample code in this article is written in C#.</span></span> <span data-ttu-id="56f90-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="56f90-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="56f90-112">Identify your Azure Search service's query api-key</span><span class="sxs-lookup"><span data-stu-id="56f90-112">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="56f90-113">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="56f90-113">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span></span> <span data-ttu-id="56f90-114">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span><span class="sxs-lookup"><span data-stu-id="56f90-114">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="56f90-115">The .NET SDK will send this api-key on every request to your service.</span><span class="sxs-lookup"><span data-stu-id="56f90-115">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="56f90-116">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span><span class="sxs-lookup"><span data-stu-id="56f90-116">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="56f90-117">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="56f90-117">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="56f90-118">Go to your Azure Search service's blade</span><span class="sxs-lookup"><span data-stu-id="56f90-118">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="56f90-119">Click on the "Keys" icon</span><span class="sxs-lookup"><span data-stu-id="56f90-119">Click on the "Keys" icon</span></span>

<span data-ttu-id="56f90-120">Your service will have *admin keys* and *query keys*.</span><span class="sxs-lookup"><span data-stu-id="56f90-120">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="56f90-121">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span><span class="sxs-lookup"><span data-stu-id="56f90-121">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="56f90-122">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="56f90-122">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="56f90-123">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span><span class="sxs-lookup"><span data-stu-id="56f90-123">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="56f90-124">For the purposes of querying an index, you can use one of your query keys.</span><span class="sxs-lookup"><span data-stu-id="56f90-124">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="56f90-125">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="56f90-125">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="56f90-126">Create an instance of the SearchIndexClient class</span><span class="sxs-lookup"><span data-stu-id="56f90-126">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="56f90-127">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span><span class="sxs-lookup"><span data-stu-id="56f90-127">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="56f90-128">This class has several constructors.</span><span class="sxs-lookup"><span data-stu-id="56f90-128">This class has several constructors.</span></span> <span data-ttu-id="56f90-129">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span><span class="sxs-lookup"><span data-stu-id="56f90-129">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="56f90-130">`SearchCredentials` wraps your api-key.</span><span class="sxs-lookup"><span data-stu-id="56f90-130">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="56f90-131">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`app.config` or `web.config`):</span><span class="sxs-lookup"><span data-stu-id="56f90-131">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`app.config` or `web.config`):</span></span>

```csharp
string searchServiceName = ConfigurationManager.AppSettings["SearchServiceName"];
string queryApiKey = ConfigurationManager.AppSettings["SearchServiceQueryApiKey"];

SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
```

<span data-ttu-id="56f90-132">`SearchIndexClient` has a `Documents` property.</span><span class="sxs-lookup"><span data-stu-id="56f90-132">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="56f90-133">This property provides all the methods you need to query Azure Search indexes.</span><span class="sxs-lookup"><span data-stu-id="56f90-133">This property provides all the methods you need to query Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="56f90-134">Query your index</span><span class="sxs-lookup"><span data-stu-id="56f90-134">Query your index</span></span>
<span data-ttu-id="56f90-135">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="56f90-135">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="56f90-136">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span><span class="sxs-lookup"><span data-stu-id="56f90-136">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="56f90-137">Types of Queries</span><span class="sxs-lookup"><span data-stu-id="56f90-137">Types of Queries</span></span>
<span data-ttu-id="56f90-138">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span><span class="sxs-lookup"><span data-stu-id="56f90-138">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="56f90-139">A `search` query searches for one or more terms in all *searchable* fields in your index.</span><span class="sxs-lookup"><span data-stu-id="56f90-139">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="56f90-140">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span><span class="sxs-lookup"><span data-stu-id="56f90-140">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="56f90-141">Both searches and filters are performed using the `Documents.Search` method.</span><span class="sxs-lookup"><span data-stu-id="56f90-141">Both searches and filters are performed using the `Documents.Search` method.</span></span> <span data-ttu-id="56f90-142">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span><span class="sxs-lookup"><span data-stu-id="56f90-142">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span></span> <span data-ttu-id="56f90-143">To filter without searching, just pass `"*"` for the `searchText` parameter.</span><span class="sxs-lookup"><span data-stu-id="56f90-143">To filter without searching, just pass `"*"` for the `searchText` parameter.</span></span> <span data-ttu-id="56f90-144">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span><span class="sxs-lookup"><span data-stu-id="56f90-144">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="56f90-145">Example Queries</span><span class="sxs-lookup"><span data-stu-id="56f90-145">Example Queries</span></span>
<span data-ttu-id="56f90-146">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="56f90-146">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="56f90-147">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="56f90-147">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="56f90-148">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span><span class="sxs-lookup"><span data-stu-id="56f90-148">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span></span> <span data-ttu-id="56f90-149">This method is described in the next section.</span><span class="sxs-lookup"><span data-stu-id="56f90-149">This method is described in the next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
Console.WriteLine("and return the hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take the top two results, and show only hotelName and ");
Console.WriteLine("lastRenovationDate:\n");

parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="56f90-150">Handle search results</span><span class="sxs-lookup"><span data-stu-id="56f90-150">Handle search results</span></span>
<span data-ttu-id="56f90-151">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span><span class="sxs-lookup"><span data-stu-id="56f90-151">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span></span> <span data-ttu-id="56f90-152">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span><span class="sxs-lookup"><span data-stu-id="56f90-152">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="56f90-153">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="56f90-153">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search the entire index for the term 'budget' and return only the hotelName field:

Name: Roach Motel

Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close to town hall and the river

Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search the entire index for the term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="56f90-154">The sample code above uses the console to output search results.</span><span class="sxs-lookup"><span data-stu-id="56f90-154">The sample code above uses the console to output search results.</span></span> <span data-ttu-id="56f90-155">You will likewise need to display search results in your own application.</span><span class="sxs-lookup"><span data-stu-id="56f90-155">You will likewise need to display search results in your own application.</span></span> <span data-ttu-id="56f90-156">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span><span class="sxs-lookup"><span data-stu-id="56f90-156">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span></span>

