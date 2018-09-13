---
title: How to use Fiddler to evaluate and test Azure Search REST APIs | Microsoft Docs
description: Use Fiddler for a code-free approach to verifying Azure Search availability and trying out the REST APIs.
services: search
documentationcenter: ''
author: HeidiSteen
manager: mblythe
editor: ''
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: b8361f49bb7e9447e3933b39dc28eeae708e02bb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554598"
---
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="0eaa2-103">Use Fiddler to evaluate and test Azure Search REST APIs</span><span class="sxs-lookup"><span data-stu-id="0eaa2-103">Use Fiddler to evaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [Overview](search-query-overview.md)
> * [Search Explorer](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

<span data-ttu-id="0eaa2-109">This article explains how to use Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), to issue HTTP requests to and view responses using the Azure Search REST API, without having to write any code.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-109">This article explains how to use Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), to issue HTTP requests to and view responses using the Azure Search REST API, without having to write any code.</span></span> <span data-ttu-id="0eaa2-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="0eaa2-111">The Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="0eaa2-111">The Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="0eaa2-112">In the following steps, you'll create an index, upload documents, query the index, and then query the system for service information.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-112">In the following steps, you'll create an index, upload documents, query the index, and then query the system for service information.</span></span>

<span data-ttu-id="0eaa2-113">To complete these steps, you will need an Azure Search service and `api-key`.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-113">To complete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="0eaa2-114">See [Create an Azure Search service in the portal](search-create-service-portal.md) for instructions on how to get started.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-114">See [Create an Azure Search service in the portal](search-create-service-portal.md) for instructions on how to get started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="0eaa2-115">Create an index</span><span class="sxs-lookup"><span data-stu-id="0eaa2-115">Create an index</span></span>
1. <span data-ttu-id="0eaa2-116">Start Fiddler.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-116">Start Fiddler.</span></span> <span data-ttu-id="0eaa2-117">On the **File** menu, turn off **Capture Traffic** to hide extraneous HTTP activity that is unrelated to the current task.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-117">On the **File** menu, turn off **Capture Traffic** to hide extraneous HTTP activity that is unrelated to the current task.</span></span>
2. <span data-ttu-id="0eaa2-118">On the **Composer** tab, you'll formulate a request that looks like the following screen shot.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-118">On the **Composer** tab, you'll formulate a request that looks like the following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="0eaa2-119">Select **PUT**.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-119">Select **PUT**.</span></span>
4. <span data-ttu-id="0eaa2-120">Enter a URL that specifies the service URL, request attributes, and the api-version.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-120">Enter a URL that specifies the service URL, request attributes, and the api-version.</span></span> <span data-ttu-id="0eaa2-121">A few pointers to keep in mind:</span><span class="sxs-lookup"><span data-stu-id="0eaa2-121">A few pointers to keep in mind:</span></span>

   * <span data-ttu-id="0eaa2-122">Use HTTPS as the prefix.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-122">Use HTTPS as the prefix.</span></span>
   * <span data-ttu-id="0eaa2-123">Request attribute is "/indexes/hotels".</span><span class="sxs-lookup"><span data-stu-id="0eaa2-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="0eaa2-124">This tells Search to create an index named 'hotels'.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-124">This tells Search to create an index named 'hotels'.</span></span>
   * <span data-ttu-id="0eaa2-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="0eaa2-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="0eaa2-126">API versions are important because Azure Search deploys updates regularly.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="0eaa2-127">On rare occasions, a service update may introduce a breaking change to the API.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-127">On rare occasions, a service update may introduce a breaking change to the API.</span></span> <span data-ttu-id="0eaa2-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="0eaa2-129">The full URL should look similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-129">The full URL should look similar to the following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="0eaa2-130">Specify the request header, replacing the host and api-key with values that are valid for your service.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-130">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="0eaa2-131">In Request Body, paste in the fields that make up the index definition.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-131">In Request Body, paste in the fields that make up the index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="0eaa2-132">Click **Execute**.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-132">Click **Execute**.</span></span>

<span data-ttu-id="0eaa2-133">In a few seconds, you should see an HTTP 201 response in the session list, indicating the index was created successfully.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-133">In a few seconds, you should see an HTTP 201 response in the session list, indicating the index was created successfully.</span></span>

<span data-ttu-id="0eaa2-134">If you get HTTP 504, verify the URL specifies HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-134">If you get HTTP 504, verify the URL specifies HTTPS.</span></span> <span data-ttu-id="0eaa2-135">If you see HTTP 400 or 404, check the request body to verify there were no copy-paste errors.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-135">If you see HTTP 400 or 404, check the request body to verify there were no copy-paste errors.</span></span> <span data-ttu-id="0eaa2-136">An HTTP 403 typically indicates a problem with the api-key (either an invalid key or a syntax problem with how the api-key is specified).</span><span class="sxs-lookup"><span data-stu-id="0eaa2-136">An HTTP 403 typically indicates a problem with the api-key (either an invalid key or a syntax problem with how the api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="0eaa2-137">Load documents</span><span class="sxs-lookup"><span data-stu-id="0eaa2-137">Load documents</span></span>
<span data-ttu-id="0eaa2-138">On the **Composer** tab, your request to post documents will look like the following.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-138">On the **Composer** tab, your request to post documents will look like the following.</span></span> <span data-ttu-id="0eaa2-139">The body of the request contains the search data for 4 hotels.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-139">The body of the request contains the search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="0eaa2-140">Select **POST**.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-140">Select **POST**.</span></span>
2. <span data-ttu-id="0eaa2-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="0eaa2-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="0eaa2-142">The full URL should look similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-142">The full URL should look similar to the following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="0eaa2-143">Request Header should be the same as before.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-143">Request Header should be the same as before.</span></span> <span data-ttu-id="0eaa2-144">Remember that you replaced the host and api-key with values that are valid for your service.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-144">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="0eaa2-145">The Request Body contains four documents to be added to the hotels index.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-145">The Request Body contains four documents to be added to the hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be the one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="0eaa2-146">Click **Execute**.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-146">Click **Execute**.</span></span>

<span data-ttu-id="0eaa2-147">In a few seconds, you should see an HTTP 200 response in the session list.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-147">In a few seconds, you should see an HTTP 200 response in the session list.</span></span> <span data-ttu-id="0eaa2-148">This indicates the documents were created successfully.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-148">This indicates the documents were created successfully.</span></span> <span data-ttu-id="0eaa2-149">If you get a 207, at least one document failed to upload.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-149">If you get a 207, at least one document failed to upload.</span></span> <span data-ttu-id="0eaa2-150">If you get a 404, you have a syntax error in either the header or body of the request.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-150">If you get a 404, you have a syntax error in either the header or body of the request.</span></span>

## <a name="query-the-index"></a><span data-ttu-id="0eaa2-151">Query the index</span><span class="sxs-lookup"><span data-stu-id="0eaa2-151">Query the index</span></span>
<span data-ttu-id="0eaa2-152">Now that an index and documents are loaded, you can issue queries against them.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="0eaa2-153">On the **Composer** tab, a **GET** command that queries your service will look similar to the following screen shot.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-153">On the **Composer** tab, a **GET** command that queries your service will look similar to the following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="0eaa2-154">Select **GET**.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-154">Select **GET**.</span></span>
2. <span data-ttu-id="0eaa2-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="0eaa2-156">By way of example, use the following URL, replacing the sample host name with one that is valid for your service.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-156">By way of example, use the following URL, replacing the sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="0eaa2-157">This query searches on the term “motel” and retrieves facet categories for ratings.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-157">This query searches on the term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="0eaa2-158">Request Header should be the same as before.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-158">Request Header should be the same as before.</span></span> <span data-ttu-id="0eaa2-159">Remember that you replaced the host and api-key with values that are valid for your service.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-159">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="0eaa2-160">The response code should be 200, and the response output should look similar to the following screen shot.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-160">The response code should be 200, and the response output should look similar to the following screen shot.</span></span>

   ![][4]

<span data-ttu-id="0eaa2-161">The following example query is from the [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-161">The following example query is from the [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="0eaa2-162">Many of the example queries in this topic include spaces, which are not allowed in Fiddler.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-162">Many of the example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="0eaa2-163">Replace each space with a + character before pasting in the query string before attempting the query in Fiddler.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-163">Replace each space with a + character before pasting in the query string before attempting the query in Fiddler.</span></span>

<span data-ttu-id="0eaa2-164">**Before spaces are replaced:**</span><span class="sxs-lookup"><span data-stu-id="0eaa2-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="0eaa2-165">**After spaces are replaced with +:**</span><span class="sxs-lookup"><span data-stu-id="0eaa2-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a><span data-ttu-id="0eaa2-166">Query the system</span><span class="sxs-lookup"><span data-stu-id="0eaa2-166">Query the system</span></span>
<span data-ttu-id="0eaa2-167">You can also query the system to get document counts and storage consumption.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-167">You can also query the system to get document counts and storage consumption.</span></span> <span data-ttu-id="0eaa2-168">On the **Composer** tab, your request will look similar to the following, and the response will return a count for the number of documents and space used.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-168">On the **Composer** tab, your request will look similar to the following, and the response will return a count for the number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="0eaa2-169">Select **GET**.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-169">Select **GET**.</span></span>
2. <span data-ttu-id="0eaa2-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span><span class="sxs-lookup"><span data-stu-id="0eaa2-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="0eaa2-171">Specify the request header, replacing the host and api-key with values that are valid for your service.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-171">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="0eaa2-172">Leave the request body empty.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-172">Leave the request body empty.</span></span>
5. <span data-ttu-id="0eaa2-173">Click **Execute**.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-173">Click **Execute**.</span></span> <span data-ttu-id="0eaa2-174">You should see an HTTP 200 status code in the session list.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-174">You should see an HTTP 200 status code in the session list.</span></span> <span data-ttu-id="0eaa2-175">Select the entry posted for your command.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-175">Select the entry posted for your command.</span></span>
6. <span data-ttu-id="0eaa2-176">Click the **Inspectors** tab, click the **Headers** tab, and then select the JSON format.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-176">Click the **Inspectors** tab, click the **Headers** tab, and then select the JSON format.</span></span> <span data-ttu-id="0eaa2-177">You should see the document count and storage size (in KB).</span><span class="sxs-lookup"><span data-stu-id="0eaa2-177">You should see the document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0eaa2-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="0eaa2-178">Next steps</span></span>
<span data-ttu-id="0eaa2-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach to managing and using Azure Search.</span><span class="sxs-lookup"><span data-stu-id="0eaa2-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach to managing and using Azure Search.</span></span>

<!--Image References-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png





