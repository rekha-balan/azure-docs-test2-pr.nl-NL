---
title: Create an Azure Search index using the REST API | Microsoft Docs
description: Create an index in code using the Azure Search HTTP REST API.
services: search
documentationcenter: ''
author: ashmaka
manager: jhubbard
editor: ''
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 7f4bccda8a7cebff0d80627320d34062d4d55add
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551533"
---
# <a name="create-an-azure-search-index-using-the-rest-api"></a><span data-ttu-id="e870d-103">Create an Azure Search index using the REST API</span><span class="sxs-lookup"><span data-stu-id="e870d-103">Create an Azure Search index using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [Overview](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

<span data-ttu-id="e870d-108">This article will walk you through the process of creating an Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) using the Azure Search REST API.</span><span class="sxs-lookup"><span data-stu-id="e870d-108">This article will walk you through the process of creating an Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) using the Azure Search REST API.</span></span>

<span data-ttu-id="e870d-109">Before following this guide and creating an index, you should have already [created an Azure Search service](search-create-service-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e870d-109">Before following this guide and creating an index, you should have already [created an Azure Search service](search-create-service-portal.md).</span></span>

<span data-ttu-id="e870d-110">To create an Azure Search index using the REST API, you will issue a single HTTP POST request to your Azure Search service's URL endpoint.</span><span class="sxs-lookup"><span data-stu-id="e870d-110">To create an Azure Search index using the REST API, you will issue a single HTTP POST request to your Azure Search service's URL endpoint.</span></span> <span data-ttu-id="e870d-111">Your index definition will be contained in the request body as well-formed JSON content.</span><span class="sxs-lookup"><span data-stu-id="e870d-111">Your index definition will be contained in the request body as well-formed JSON content.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="e870d-112">Identify your Azure Search service's admin api-key</span><span class="sxs-lookup"><span data-stu-id="e870d-112">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="e870d-113">Now that you have provisioned an Azure Search service, you can issue HTTP requests against your service's URL endpoint using the REST API.</span><span class="sxs-lookup"><span data-stu-id="e870d-113">Now that you have provisioned an Azure Search service, you can issue HTTP requests against your service's URL endpoint using the REST API.</span></span> <span data-ttu-id="e870d-114">*All* API requests must include the api-key that was generated for the Search service you provisioned.</span><span class="sxs-lookup"><span data-stu-id="e870d-114">*All* API requests must include the api-key that was generated for the Search service you provisioned.</span></span> <span data-ttu-id="e870d-115">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span><span class="sxs-lookup"><span data-stu-id="e870d-115">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="e870d-116">To find your service's api-keys you must log into the [Azure portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="e870d-116">To find your service's api-keys you must log into the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="e870d-117">Go to your Azure Search service's blade</span><span class="sxs-lookup"><span data-stu-id="e870d-117">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="e870d-118">Click on the "Keys" icon</span><span class="sxs-lookup"><span data-stu-id="e870d-118">Click on the "Keys" icon</span></span>

<span data-ttu-id="e870d-119">Your service will have *admin keys* and *query keys*.</span><span class="sxs-lookup"><span data-stu-id="e870d-119">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="e870d-120">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span><span class="sxs-lookup"><span data-stu-id="e870d-120">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="e870d-121">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="e870d-121">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="e870d-122">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span><span class="sxs-lookup"><span data-stu-id="e870d-122">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="e870d-123">For the purposes of creating an index, you can use either your primary or secondary admin key.</span><span class="sxs-lookup"><span data-stu-id="e870d-123">For the purposes of creating an index, you can use either your primary or secondary admin key.</span></span>

## <a name="define-your-azure-search-index-using-well-formed-json"></a><span data-ttu-id="e870d-124">Define your Azure Search index using well-formed JSON</span><span class="sxs-lookup"><span data-stu-id="e870d-124">Define your Azure Search index using well-formed JSON</span></span>
<span data-ttu-id="e870d-125">A single HTTP POST request to your service will create your index.</span><span class="sxs-lookup"><span data-stu-id="e870d-125">A single HTTP POST request to your service will create your index.</span></span> <span data-ttu-id="e870d-126">The body of your HTTP POST request will contain a single JSON object that defines your Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="e870d-126">The body of your HTTP POST request will contain a single JSON object that defines your Azure Search index.</span></span>

1. <span data-ttu-id="e870d-127">The first property of this JSON object is the name of your index.</span><span class="sxs-lookup"><span data-stu-id="e870d-127">The first property of this JSON object is the name of your index.</span></span>
2. <span data-ttu-id="e870d-128">The second property of this JSON object is a JSON array named `fields` that contains a separate JSON object for each field in your index.</span><span class="sxs-lookup"><span data-stu-id="e870d-128">The second property of this JSON object is a JSON array named `fields` that contains a separate JSON object for each field in your index.</span></span> <span data-ttu-id="e870d-129">Each of these JSON objects contain multiple name/value pairs for each of the field attributes including "name," "type," etc.</span><span class="sxs-lookup"><span data-stu-id="e870d-129">Each of these JSON objects contain multiple name/value pairs for each of the field attributes including "name," "type," etc.</span></span>

<span data-ttu-id="e870d-130">It is important that you keep your search user experience and business needs in mind when designing your index as each field must be assigned the [proper attributes](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span><span class="sxs-lookup"><span data-stu-id="e870d-130">It is important that you keep your search user experience and business needs in mind when designing your index as each field must be assigned the [proper attributes](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span></span> <span data-ttu-id="e870d-131">These attributes control which search features (filtering, faceting, sorting full-text search, etc.) apply to which fields.</span><span class="sxs-lookup"><span data-stu-id="e870d-131">These attributes control which search features (filtering, faceting, sorting full-text search, etc.) apply to which fields.</span></span> <span data-ttu-id="e870d-132">For any attribute you do not specify, the default will be to enable the corresponding search feature unless you specifically disable it.</span><span class="sxs-lookup"><span data-stu-id="e870d-132">For any attribute you do not specify, the default will be to enable the corresponding search feature unless you specifically disable it.</span></span>

<span data-ttu-id="e870d-133">For our example, we've named our index "hotels" and defined our fields as follows:</span><span class="sxs-lookup"><span data-stu-id="e870d-133">For our example, we've named our index "hotels" and defined our fields as follows:</span></span>

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

<span data-ttu-id="e870d-134">We have carefully chosen the index attributes for each field based on how we think they will be used in an application.</span><span class="sxs-lookup"><span data-stu-id="e870d-134">We have carefully chosen the index attributes for each field based on how we think they will be used in an application.</span></span> <span data-ttu-id="e870d-135">For example, `hotelId` is a unique key that people searching for hotels likely won't know, so we disable full-text search for that field by setting `searchable` to `false`, which saves space in the index.</span><span class="sxs-lookup"><span data-stu-id="e870d-135">For example, `hotelId` is a unique key that people searching for hotels likely won't know, so we disable full-text search for that field by setting `searchable` to `false`, which saves space in the index.</span></span>

<span data-ttu-id="e870d-136">Please note that exactly one field in your index of type `Edm.String` must be the designated as the 'key' field.</span><span class="sxs-lookup"><span data-stu-id="e870d-136">Please note that exactly one field in your index of type `Edm.String` must be the designated as the 'key' field.</span></span>

<span data-ttu-id="e870d-137">The index definition above uses a language analyzer for the `description_fr` field because it is intended to store French text.</span><span class="sxs-lookup"><span data-stu-id="e870d-137">The index definition above uses a language analyzer for the `description_fr` field because it is intended to store French text.</span></span> <span data-ttu-id="e870d-138">See [the Language support topic](https://docs.microsoft.com/rest/api/searchservice/Language-support) as well as the corresponding [blog post](https://azure.microsoft.com/blog/language-support-in-azure-search/) for more information about language analyzers.</span><span class="sxs-lookup"><span data-stu-id="e870d-138">See [the Language support topic](https://docs.microsoft.com/rest/api/searchservice/Language-support) as well as the corresponding [blog post](https://azure.microsoft.com/blog/language-support-in-azure-search/) for more information about language analyzers.</span></span>

## <a name="issue-the-http-request"></a><span data-ttu-id="e870d-139">Issue the HTTP request</span><span class="sxs-lookup"><span data-stu-id="e870d-139">Issue the HTTP request</span></span>
1. <span data-ttu-id="e870d-140">Using your index definition as the request body, issue an HTTP POST request to your Azure Search service endpoint URL.</span><span class="sxs-lookup"><span data-stu-id="e870d-140">Using your index definition as the request body, issue an HTTP POST request to your Azure Search service endpoint URL.</span></span> <span data-ttu-id="e870d-141">In the URL, be sure to use your service name as the host name, and put the proper `api-version` as a query string parameter (the current API version is `2016-09-01` at the time of publishing this document).</span><span class="sxs-lookup"><span data-stu-id="e870d-141">In the URL, be sure to use your service name as the host name, and put the proper `api-version` as a query string parameter (the current API version is `2016-09-01` at the time of publishing this document).</span></span>
2. <span data-ttu-id="e870d-142">In the request headers, specify the `Content-Type` as `application/json`.</span><span class="sxs-lookup"><span data-stu-id="e870d-142">In the request headers, specify the `Content-Type` as `application/json`.</span></span> <span data-ttu-id="e870d-143">You will also need to provide your service's admin key that you identified in Step I in the `api-key` header.</span><span class="sxs-lookup"><span data-stu-id="e870d-143">You will also need to provide your service's admin key that you identified in Step I in the `api-key` header.</span></span>

<span data-ttu-id="e870d-144">You will have to provide your own service name and api key to issue the request below:</span><span class="sxs-lookup"><span data-stu-id="e870d-144">You will have to provide your own service name and api key to issue the request below:</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


<span data-ttu-id="e870d-145">For a successful request, you should see status code 201 (Created).</span><span class="sxs-lookup"><span data-stu-id="e870d-145">For a successful request, you should see status code 201 (Created).</span></span> <span data-ttu-id="e870d-146">For more information on creating an index via the REST API, please visit the [API reference here](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span><span class="sxs-lookup"><span data-stu-id="e870d-146">For more information on creating an index via the REST API, please visit the [API reference here](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span></span> <span data-ttu-id="e870d-147">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="e870d-147">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

<span data-ttu-id="e870d-148">When you're done with an index and want to delete it, just issue an HTTP DELETE request.</span><span class="sxs-lookup"><span data-stu-id="e870d-148">When you're done with an index and want to delete it, just issue an HTTP DELETE request.</span></span> <span data-ttu-id="e870d-149">For example, this is how we would delete the "hotels" index:</span><span class="sxs-lookup"><span data-stu-id="e870d-149">For example, this is how we would delete the "hotels" index:</span></span>

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a><span data-ttu-id="e870d-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="e870d-150">Next steps</span></span>
<span data-ttu-id="e870d-151">After creating an Azure Search index, you will be ready to [upload your content into the index](search-what-is-data-import.md) so you can start searching your data.</span><span class="sxs-lookup"><span data-stu-id="e870d-151">After creating an Azure Search index, you will be ready to [upload your content into the index](search-what-is-data-import.md) so you can start searching your data.</span></span>
