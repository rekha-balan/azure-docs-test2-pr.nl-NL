---
title: Query your Azure Search Index using the REST API | Microsoft Docs
description: Build a search query in Azure search and use search parameters to filter and sort search results.
services: search
documentationcenter: ''
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 449110cfda1a08b73b5e21cbf495e59f32d80339
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563042"
---
# <a name="query-your-azure-search-index-using-the-rest-api"></a><span data-ttu-id="02bb6-103">Query your Azure Search index using the REST API</span><span class="sxs-lookup"><span data-stu-id="02bb6-103">Query your Azure Search index using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [Overview](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

<span data-ttu-id="02bb6-108">This article shows you how to query an index using the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="02bb6-108">This article shows you how to query an index using the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="02bb6-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="02bb6-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="02bb6-110">Identify your Azure Search service's query api-key</span><span class="sxs-lookup"><span data-stu-id="02bb6-110">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="02bb6-111">A key component of every search operation against the Azure Search REST API is the *api-key* that was generated for the service you provisioned.</span><span class="sxs-lookup"><span data-stu-id="02bb6-111">A key component of every search operation against the Azure Search REST API is the *api-key* that was generated for the service you provisioned.</span></span> <span data-ttu-id="02bb6-112">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span><span class="sxs-lookup"><span data-stu-id="02bb6-112">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="02bb6-113">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="02bb6-113">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="02bb6-114">Go to your Azure Search service's blade</span><span class="sxs-lookup"><span data-stu-id="02bb6-114">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="02bb6-115">Click the "Keys" icon</span><span class="sxs-lookup"><span data-stu-id="02bb6-115">Click the "Keys" icon</span></span>

<span data-ttu-id="02bb6-116">Your service has *admin keys* and *query keys*.</span><span class="sxs-lookup"><span data-stu-id="02bb6-116">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="02bb6-117">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span><span class="sxs-lookup"><span data-stu-id="02bb6-117">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="02bb6-118">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="02bb6-118">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="02bb6-119">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span><span class="sxs-lookup"><span data-stu-id="02bb6-119">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="02bb6-120">For the purposes of querying an index, you can use one of your query keys.</span><span class="sxs-lookup"><span data-stu-id="02bb6-120">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="02bb6-121">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="02bb6-121">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="02bb6-122">Formulate your query</span><span class="sxs-lookup"><span data-stu-id="02bb6-122">Formulate your query</span></span>
<span data-ttu-id="02bb6-123">There are two ways to [search your index using the REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="02bb6-123">There are two ways to [search your index using the REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="02bb6-124">One way is to issue an HTTP POST request where your query parameters are defined in a JSON object in the request body.</span><span class="sxs-lookup"><span data-stu-id="02bb6-124">One way is to issue an HTTP POST request where your query parameters are defined in a JSON object in the request body.</span></span> <span data-ttu-id="02bb6-125">The other way is to issue an HTTP GET request where your query parameters are defined within the request URL.</span><span class="sxs-lookup"><span data-stu-id="02bb6-125">The other way is to issue an HTTP GET request where your query parameters are defined within the request URL.</span></span> <span data-ttu-id="02bb6-126">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on the size of query parameters than GET.</span><span class="sxs-lookup"><span data-stu-id="02bb6-126">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on the size of query parameters than GET.</span></span> <span data-ttu-id="02bb6-127">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span><span class="sxs-lookup"><span data-stu-id="02bb6-127">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="02bb6-128">For both POST and GET, you need to provide your *service name*, *index name*, and the proper *API version* (the current API version is `2016-09-01` at the time of publishing this document) in the request URL.</span><span class="sxs-lookup"><span data-stu-id="02bb6-128">For both POST and GET, you need to provide your *service name*, *index name*, and the proper *API version* (the current API version is `2016-09-01` at the time of publishing this document) in the request URL.</span></span> <span data-ttu-id="02bb6-129">For GET, the *query string* at the end of the URL is where you provide the query parameters.</span><span class="sxs-lookup"><span data-stu-id="02bb6-129">For GET, the *query string* at the end of the URL is where you provide the query parameters.</span></span> <span data-ttu-id="02bb6-130">See below for the URL format:</span><span class="sxs-lookup"><span data-stu-id="02bb6-130">See below for the URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="02bb6-131">The format for POST is the same, but with only api-version in the query string parameters.</span><span class="sxs-lookup"><span data-stu-id="02bb6-131">The format for POST is the same, but with only api-version in the query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="02bb6-132">Example Queries</span><span class="sxs-lookup"><span data-stu-id="02bb6-132">Example Queries</span></span>
<span data-ttu-id="02bb6-133">Here are a few example queries on an index named "hotels".</span><span class="sxs-lookup"><span data-stu-id="02bb6-133">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="02bb6-134">These queries are shown in both GET and POST format.</span><span class="sxs-lookup"><span data-stu-id="02bb6-134">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="02bb6-135">Search the entire index for the term 'budget' and return only the `hotelName` field:</span><span class="sxs-lookup"><span data-stu-id="02bb6-135">Search the entire index for the term 'budget' and return only the `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="02bb6-136">Apply a filter to the index to find hotels cheaper than $150 per night, and return the `hotelId` and `description`:</span><span class="sxs-lookup"><span data-stu-id="02bb6-136">Apply a filter to the index to find hotels cheaper than $150 per night, and return the `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="02bb6-137">Search the entire index, order by a specific field (`lastRenovationDate`) in descending order, take the top two results, and show only `hotelName` and `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="02bb6-137">Search the entire index, order by a specific field (`lastRenovationDate`) in descending order, take the top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a><span data-ttu-id="02bb6-138">Submit your HTTP request</span><span class="sxs-lookup"><span data-stu-id="02bb6-138">Submit your HTTP request</span></span>
<span data-ttu-id="02bb6-139">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span><span class="sxs-lookup"><span data-stu-id="02bb6-139">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="02bb6-140">Request and Request Headers</span><span class="sxs-lookup"><span data-stu-id="02bb6-140">Request and Request Headers</span></span>
<span data-ttu-id="02bb6-141">You must define two request headers for GET, or three for POST:</span><span class="sxs-lookup"><span data-stu-id="02bb6-141">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="02bb6-142">The `api-key` header must be set to the query key you found in step I above.</span><span class="sxs-lookup"><span data-stu-id="02bb6-142">The `api-key` header must be set to the query key you found in step I above.</span></span> <span data-ttu-id="02bb6-143">You can also use an admin key as the `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access to indexes and documents.</span><span class="sxs-lookup"><span data-stu-id="02bb6-143">You can also use an admin key as the `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access to indexes and documents.</span></span>
2. <span data-ttu-id="02bb6-144">The `Accept` header must be set to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="02bb6-144">The `Accept` header must be set to `application/json`.</span></span>
3. <span data-ttu-id="02bb6-145">For POST only, the `Content-Type` header should also be set to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="02bb6-145">For POST only, the `Content-Type` header should also be set to `application/json`.</span></span>

<span data-ttu-id="02bb6-146">See below for an HTTP GET request to search the "hotels" index using the Azure Search REST API, using a simple query that searches for the term "motel":</span><span class="sxs-lookup"><span data-stu-id="02bb6-146">See below for an HTTP GET request to search the "hotels" index using the Azure Search REST API, using a simple query that searches for the term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="02bb6-147">Here is the same example query, this time using HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="02bb6-147">Here is the same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="02bb6-148">A successful query request will result in a Status Code of `200 OK` and the search results are returned as JSON in the response body.</span><span class="sxs-lookup"><span data-stu-id="02bb6-148">A successful query request will result in a Status Code of `200 OK` and the search results are returned as JSON in the response body.</span></span> <span data-ttu-id="02bb6-149">Here is what the results for the above query look like, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the REST API](search-import-data-rest-api.md) (note that the JSON has been formatted for clarity).</span><span class="sxs-lookup"><span data-stu-id="02bb6-149">Here is what the results for the above query look like, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the REST API](search-import-data-rest-api.md) (note that the JSON has been formatted for clarity).</span></span>

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

<span data-ttu-id="02bb6-150">To learn more, please visit the "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="02bb6-150">To learn more, please visit the "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="02bb6-151">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="02bb6-151">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
