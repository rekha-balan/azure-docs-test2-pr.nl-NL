---
title: Upload data (REST API - Azure Search) | Microsoft Docs
description: Learn how to upload data to an index in Azure Search using the REST API.
author: brjohnstmsft
manager: jlembicz
ms.author: brjohnst
services: search
ms.service: search
ms.devlang: rest-api
ms.topic: quickstart
ms.date: 04/20/2018
ms.openlocfilehash: 53b20c9db7efe1f8876eec7c0167dc151aa38786
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805095"
---
# <a name="upload-data-to-azure-search-using-the-rest-api"></a><span data-ttu-id="fe8a7-103">Upload data to Azure Search using the REST API</span><span class="sxs-lookup"><span data-stu-id="fe8a7-103">Upload data to Azure Search using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [Overview](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

<span data-ttu-id="fe8a7-107">This article will show you how to use the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) to import data into an Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-107">This article will show you how to use the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) to import data into an Azure Search index.</span></span>

<span data-ttu-id="fe8a7-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="fe8a7-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="fe8a7-109">In order to push documents into your index using the REST API, you will issue an HTTP POST request to your index's URL endpoint.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-109">In order to push documents into your index using the REST API, you will issue an HTTP POST request to your index's URL endpoint.</span></span> <span data-ttu-id="fe8a7-110">The body of the HTTP request body is a JSON object containing the documents to be added, modified, or deleted.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-110">The body of the HTTP request body is a JSON object containing the documents to be added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="fe8a7-111">Identify your Azure Search service's admin api-key</span><span class="sxs-lookup"><span data-stu-id="fe8a7-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="fe8a7-112">When issuing HTTP requests against your service using the REST API, *each* API request must include the api-key that was generated for the Search service you provisioned.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-112">When issuing HTTP requests against your service using the REST API, *each* API request must include the api-key that was generated for the Search service you provisioned.</span></span> <span data-ttu-id="fe8a7-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="fe8a7-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="fe8a7-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="fe8a7-115">Go to your Azure Search service's blade</span><span class="sxs-lookup"><span data-stu-id="fe8a7-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="fe8a7-116">Click on the "Keys" icon</span><span class="sxs-lookup"><span data-stu-id="fe8a7-116">Click on the "Keys" icon</span></span>

<span data-ttu-id="fe8a7-117">Your service will have *admin keys* and *query keys*.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="fe8a7-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="fe8a7-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="fe8a7-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="fe8a7-121">For the purposes of importing data into an index, you can use either your primary or secondary admin key.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-121">For the purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="fe8a7-122">Decide which indexing action to use</span><span class="sxs-lookup"><span data-stu-id="fe8a7-122">Decide which indexing action to use</span></span>
<span data-ttu-id="fe8a7-123">When using the REST API, you will issue HTTP POST requests with JSON request bodies to your Azure Search index's endpoint URL.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-123">When using the REST API, you will issue HTTP POST requests with JSON request bodies to your Azure Search index's endpoint URL.</span></span> <span data-ttu-id="fe8a7-124">The JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like to add to your index, update, or delete.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-124">The JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like to add to your index, update, or delete.</span></span>

<span data-ttu-id="fe8a7-125">Each JSON object in the "value" array represents a document to be indexed.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-125">Each JSON object in the "value" array represents a document to be indexed.</span></span> <span data-ttu-id="fe8a7-126">Each of these objects contains the document's key and specifies the desired indexing action (upload, merge, delete, etc).</span><span class="sxs-lookup"><span data-stu-id="fe8a7-126">Each of these objects contains the document's key and specifies the desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="fe8a7-127">Depending on which of the below actions you choose, only certain fields must be included for each document:</span><span class="sxs-lookup"><span data-stu-id="fe8a7-127">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="fe8a7-128">Description</span><span class="sxs-lookup"><span data-stu-id="fe8a7-128">Description</span></span> | <span data-ttu-id="fe8a7-129">Necessary fields for each document</span><span class="sxs-lookup"><span data-stu-id="fe8a7-129">Necessary fields for each document</span></span> | <span data-ttu-id="fe8a7-130">Notes</span><span class="sxs-lookup"><span data-stu-id="fe8a7-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="fe8a7-131">An `upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-131">An `upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="fe8a7-132">key, plus any other fields you wish to define</span><span class="sxs-lookup"><span data-stu-id="fe8a7-132">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="fe8a7-133">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-133">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="fe8a7-134">This occurs even when the field was previously set to a non-null value.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-134">This occurs even when the field was previously set to a non-null value.</span></span> |
| `merge` |<span data-ttu-id="fe8a7-135">Updates an existing document with the specified fields.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-135">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="fe8a7-136">If the document does not exist in the index, the merge will fail.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-136">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="fe8a7-137">key, plus any other fields you wish to define</span><span class="sxs-lookup"><span data-stu-id="fe8a7-137">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="fe8a7-138">Any field you specify in a merge will replace the existing field in the document.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-138">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="fe8a7-139">This includes fields of type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="fe8a7-140">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-140">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="fe8a7-141">It will not be `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="fe8a7-142">This action behaves like `merge` if a document with the given key already exists in the index.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-142">This action behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="fe8a7-143">If the document does not exist, it behaves like `upload` with a new document.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-143">If the document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="fe8a7-144">key, plus any other fields you wish to define</span><span class="sxs-lookup"><span data-stu-id="fe8a7-144">key, plus any other fields you wish to define</span></span> |- |
| `delete` |<span data-ttu-id="fe8a7-145">Removes the specified document from the index.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-145">Removes the specified document from the index.</span></span> |<span data-ttu-id="fe8a7-146">key only</span><span class="sxs-lookup"><span data-stu-id="fe8a7-146">key only</span></span> |<span data-ttu-id="fe8a7-147">Any fields you specify other than the key field will be ignored.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-147">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="fe8a7-148">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to null.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-148">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to null.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="fe8a7-149">Construct your HTTP request and request body</span><span class="sxs-lookup"><span data-stu-id="fe8a7-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="fe8a7-150">Now that you have gathered the necessary field values for your index actions, you are ready to construct the actual HTTP request and JSON request body to import your data.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-150">Now that you have gathered the necessary field values for your index actions, you are ready to construct the actual HTTP request and JSON request body to import your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="fe8a7-151">Request and Request Headers</span><span class="sxs-lookup"><span data-stu-id="fe8a7-151">Request and Request Headers</span></span>
<span data-ttu-id="fe8a7-152">In the URL, you will need to provide your service name, index name ("hotels" in this case), as well as the proper API version (the current API version is `2017-11-11` at the time of publishing this document).</span><span class="sxs-lookup"><span data-stu-id="fe8a7-152">In the URL, you will need to provide your service name, index name ("hotels" in this case), as well as the proper API version (the current API version is `2017-11-11` at the time of publishing this document).</span></span> <span data-ttu-id="fe8a7-153">You will need to define the `Content-Type` and `api-key` request headers.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-153">You will need to define the `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="fe8a7-154">For the latter, use one of your service's admin keys.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-154">For the latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="fe8a7-155">Request Body</span><span class="sxs-lookup"><span data-stu-id="fe8a7-155">Request Body</span></span>
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close to town hall and the river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="fe8a7-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="fe8a7-157">Assume that this example "hotels" index is already populated with a number of documents.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="fe8a7-158">Note how we did not have to specify all the possible document fields when using `mergeOrUpload` and how we only specified the document key (`hotelId`) when using `delete`.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-158">Note how we did not have to specify all the possible document fields when using `mergeOrUpload` and how we only specified the document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="fe8a7-159">Also, note that you can only include up to 1000 documents (or 16 MB) in a single indexing request.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-159">Also, note that you can only include up to 1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="fe8a7-160">Understand your HTTP response code</span><span class="sxs-lookup"><span data-stu-id="fe8a7-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="fe8a7-161">200</span><span class="sxs-lookup"><span data-stu-id="fe8a7-161">200</span></span>
<span data-ttu-id="fe8a7-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="fe8a7-163">The JSON body of the HTTP response will be as follows:</span><span class="sxs-lookup"><span data-stu-id="fe8a7-163">The JSON body of the HTTP response will be as follows:</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a><span data-ttu-id="fe8a7-164">207</span><span class="sxs-lookup"><span data-stu-id="fe8a7-164">207</span></span>
<span data-ttu-id="fe8a7-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="fe8a7-166">The JSON body of the HTTP response will contain information about the unsuccessful document(s).</span><span class="sxs-lookup"><span data-stu-id="fe8a7-166">The JSON body of the HTTP response will contain information about the unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "The search service is too busy to process this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> This often means that the load on your search service is reaching a point where indexing requests will begin to return `503` responses. In this case, we highly recommend that your client code back off and wait before retrying. This will give the system some time to recover, increasing the chances that future requests will succeed. Rapidly retrying your requests will only prolong the situation.
>
>

#### <a name="429"></a><span data-ttu-id="fe8a7-171">429</span><span class="sxs-lookup"><span data-stu-id="fe8a7-171">429</span></span>
<span data-ttu-id="fe8a7-172">A status code of `429` will be returned when you have exceeded your quota on the number of documents per index.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-172">A status code of `429` will be returned when you have exceeded your quota on the number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="fe8a7-173">503</span><span class="sxs-lookup"><span data-stu-id="fe8a7-173">503</span></span>
<span data-ttu-id="fe8a7-174">A status code of `503` will be returned if none of the items in the request were successfully indexed.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-174">A status code of `503` will be returned if none of the items in the request were successfully indexed.</span></span> <span data-ttu-id="fe8a7-175">This error means that the system is under heavy load and your request can't be processed at this time.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-175">This error means that the system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> In this case, we highly recommend that your client code back off and wait before retrying. This will give the system some time to recover, increasing the chances that future requests will succeed. Rapidly retrying your requests will only prolong the situation.
>
>

<span data-ttu-id="fe8a7-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="fe8a7-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="fe8a7-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="fe8a7-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe8a7-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe8a7-181">Next steps</span></span>
<span data-ttu-id="fe8a7-182">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-182">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="fe8a7-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span><span class="sxs-lookup"><span data-stu-id="fe8a7-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
