---
title: How to search for an address using the Azure Maps Search service  | Microsoft Docs
description: Learn how to search for an address using the Azure Maps Search service
author: dsk-2015
ms.author: dkshir
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: fe3bb3a778a42696cd15f9e4265448479bf043a1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856316"
---
# <a name="how-to-find-an-address-using-the-azure-maps-search-service"></a><span data-ttu-id="26af5-103">How to find an address using the Azure Maps search service</span><span class="sxs-lookup"><span data-stu-id="26af5-103">How to find an address using the Azure Maps search service</span></span>

<span data-ttu-id="26af5-104">The Maps search service is a RESTful set of APIs designed for developers to search for addresses, places, points of interest, business listings, and other geographic information.</span><span class="sxs-lookup"><span data-stu-id="26af5-104">The Maps search service is a RESTful set of APIs designed for developers to search for addresses, places, points of interest, business listings, and other geographic information.</span></span> <span data-ttu-id="26af5-105">The service assigns a latitude/longitude to a specific address, cross street, geographic feature, or point of interest (POI).</span><span class="sxs-lookup"><span data-stu-id="26af5-105">The service assigns a latitude/longitude to a specific address, cross street, geographic feature, or point of interest (POI).</span></span> <span data-ttu-id="26af5-106">Latitude and longitude values returned by the search can be used as parameters in other Maps services like route and traffic flow.</span><span class="sxs-lookup"><span data-stu-id="26af5-106">Latitude and longitude values returned by the search can be used as parameters in other Maps services like route and traffic flow.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26af5-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="26af5-107">Prerequisites</span></span>

<span data-ttu-id="26af5-108">To make any calls to the Maps service APIs, you need a Maps account and key.</span><span class="sxs-lookup"><span data-stu-id="26af5-108">To make any calls to the Maps service APIs, you need a Maps account and key.</span></span> <span data-ttu-id="26af5-109">For information on creating an account and retrieving a key, see [How to manage your Azure Maps account and keys](how-to-manage-account-keys.md).</span><span class="sxs-lookup"><span data-stu-id="26af5-109">For information on creating an account and retrieving a key, see [How to manage your Azure Maps account and keys](how-to-manage-account-keys.md).</span></span>

<span data-ttu-id="26af5-110">This article uses the [Postman app](https://www.getpostman.com/apps) to build REST calls.</span><span class="sxs-lookup"><span data-stu-id="26af5-110">This article uses the [Postman app](https://www.getpostman.com/apps) to build REST calls.</span></span> <span data-ttu-id="26af5-111">You can use any API development environment that you prefer.</span><span class="sxs-lookup"><span data-stu-id="26af5-111">You can use any API development environment that you prefer.</span></span> 


## <a name="using-fuzzy-search"></a><span data-ttu-id="26af5-112">Using fuzzy search</span><span class="sxs-lookup"><span data-stu-id="26af5-112">Using fuzzy search</span></span>

<span data-ttu-id="26af5-113">The default API for the search service is [fuzzy search](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy), which handles inputs of any combination of address or POI tokens.</span><span class="sxs-lookup"><span data-stu-id="26af5-113">The default API for the search service is [fuzzy search](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy), which handles inputs of any combination of address or POI tokens.</span></span> <span data-ttu-id="26af5-114">This search API is the canonical 'single-line search' and is useful when you do not know what your user inputs as a search query.</span><span class="sxs-lookup"><span data-stu-id="26af5-114">This search API is the canonical 'single-line search' and is useful when you do not know what your user inputs as a search query.</span></span> <span data-ttu-id="26af5-115">The fuzzy search API is a combination of POI search and geocoding.</span><span class="sxs-lookup"><span data-stu-id="26af5-115">The fuzzy search API is a combination of POI search and geocoding.</span></span> <span data-ttu-id="26af5-116">The API can also be weighted with a contextual position (lat./lon.</span><span class="sxs-lookup"><span data-stu-id="26af5-116">The API can also be weighted with a contextual position (lat./lon.</span></span> <span data-ttu-id="26af5-117">pair), fully constrained by a coordinate and radius, or it can be executed more generally without any geo biasing anchor point.</span><span class="sxs-lookup"><span data-stu-id="26af5-117">pair), fully constrained by a coordinate and radius, or it can be executed more generally without any geo biasing anchor point.</span></span>

<span data-ttu-id="26af5-118">Most Search queries default to 'maxFuzzyLevel=1' to gain performance and reduce unusual results.</span><span class="sxs-lookup"><span data-stu-id="26af5-118">Most Search queries default to 'maxFuzzyLevel=1' to gain performance and reduce unusual results.</span></span> <span data-ttu-id="26af5-119">This default can be overridden as needed per request by passing in the query parameter 'maxFuzzyLevel=2' or '3'.</span><span class="sxs-lookup"><span data-stu-id="26af5-119">This default can be overridden as needed per request by passing in the query parameter 'maxFuzzyLevel=2' or '3'.</span></span>

### <a name="search-for-an-address-using-fuzzy-search"></a><span data-ttu-id="26af5-120">Search for an address using Fuzzy Search</span><span class="sxs-lookup"><span data-stu-id="26af5-120">Search for an address using Fuzzy Search</span></span>

1. <span data-ttu-id="26af5-121">Open the Postman app, click New | Create New, and select **GET request**.</span><span class="sxs-lookup"><span data-stu-id="26af5-121">Open the Postman app, click New | Create New, and select **GET request**.</span></span> <span data-ttu-id="26af5-122">Enter a Request name of **Fuzzy search**, select a collection or folder to save it to, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="26af5-122">Enter a Request name of **Fuzzy search**, select a collection or folder to save it to, and click **Save**.</span></span>

2. <span data-ttu-id="26af5-123">On the Builder tab, select the **GET** HTTP method and enter the request URL for your API endpoint.</span><span class="sxs-lookup"><span data-stu-id="26af5-123">On the Builder tab, select the **GET** HTTP method and enter the request URL for your API endpoint.</span></span>

    ![<span data-ttu-id="26af5-124">Fuzzy Search</span><span class="sxs-lookup"><span data-stu-id="26af5-124">Fuzzy Search</span></span> ](./media/how-to-search-for-address/fuzzy_search_url.png)

    | <span data-ttu-id="26af5-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="26af5-125">Parameter</span></span> | <span data-ttu-id="26af5-126">Suggested value</span><span class="sxs-lookup"><span data-stu-id="26af5-126">Suggested value</span></span> |
    |---------------|------------------------------------------------|
    | <span data-ttu-id="26af5-127">HTTP method</span><span class="sxs-lookup"><span data-stu-id="26af5-127">HTTP method</span></span> | <span data-ttu-id="26af5-128">GET</span><span class="sxs-lookup"><span data-stu-id="26af5-128">GET</span></span> |
    | <span data-ttu-id="26af5-129">Request URL</span><span class="sxs-lookup"><span data-stu-id="26af5-129">Request URL</span></span> | https://atlas.microsoft.com/search/fuzzy/json? |
    | <span data-ttu-id="26af5-130">Authorization</span><span class="sxs-lookup"><span data-stu-id="26af5-130">Authorization</span></span> | <span data-ttu-id="26af5-131">No Auth</span><span class="sxs-lookup"><span data-stu-id="26af5-131">No Auth</span></span> |

    <span data-ttu-id="26af5-132">The **json** attribute in the URL path determines the response format.</span><span class="sxs-lookup"><span data-stu-id="26af5-132">The **json** attribute in the URL path determines the response format.</span></span> <span data-ttu-id="26af5-133">You are using json throughout this article for ease of use and readability.</span><span class="sxs-lookup"><span data-stu-id="26af5-133">You are using json throughout this article for ease of use and readability.</span></span> <span data-ttu-id="26af5-134">You can find the available response formats in the **Get Search Fuzzy** definition of the [Maps Functional API reference] (https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy).</span><span class="sxs-lookup"><span data-stu-id="26af5-134">You can find the available response formats in the **Get Search Fuzzy** definition of the [Maps Functional API reference] (https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy).</span></span>

3. <span data-ttu-id="26af5-135">Click **Params**, and enter the following Key / Value pairs to use as query or path parameters in the request URL:</span><span class="sxs-lookup"><span data-stu-id="26af5-135">Click **Params**, and enter the following Key / Value pairs to use as query or path parameters in the request URL:</span></span>

    ![<span data-ttu-id="26af5-136">Fuzzy Search</span><span class="sxs-lookup"><span data-stu-id="26af5-136">Fuzzy Search</span></span> ](./media/how-to-search-for-address/fuzzy_search_params.png)

    | <span data-ttu-id="26af5-137">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-137">Key</span></span> | <span data-ttu-id="26af5-138">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-138">Value</span></span> |
    |------------------|-------------------------|
    | <span data-ttu-id="26af5-139">api-version</span><span class="sxs-lookup"><span data-stu-id="26af5-139">api-version</span></span> | <span data-ttu-id="26af5-140">1.0</span><span class="sxs-lookup"><span data-stu-id="26af5-140">1.0</span></span> |
    | <span data-ttu-id="26af5-141">subscription-key</span><span class="sxs-lookup"><span data-stu-id="26af5-141">subscription-key</span></span> | <span data-ttu-id="26af5-142">\<your Azure Maps key\></span><span class="sxs-lookup"><span data-stu-id="26af5-142">\<your Azure Maps key\></span></span> |
    | <span data-ttu-id="26af5-143">query</span><span class="sxs-lookup"><span data-stu-id="26af5-143">query</span></span> | <span data-ttu-id="26af5-144">pizza</span><span class="sxs-lookup"><span data-stu-id="26af5-144">pizza</span></span> |

4. <span data-ttu-id="26af5-145">Click **Send** and review the response body.</span><span class="sxs-lookup"><span data-stu-id="26af5-145">Click **Send** and review the response body.</span></span> 

    <span data-ttu-id="26af5-146">The ambiguous query string of "pizza" returned 10 point of interest (POI) results with categories falling in "pizza" and "restaurant".</span><span class="sxs-lookup"><span data-stu-id="26af5-146">The ambiguous query string of "pizza" returned 10 point of interest (POI) results with categories falling in "pizza" and "restaurant".</span></span> <span data-ttu-id="26af5-147">Each result returns a street address, latitude / longitude values, view port, and entry points for the location.</span><span class="sxs-lookup"><span data-stu-id="26af5-147">Each result returns a street address, latitude / longitude values, view port, and entry points for the location.</span></span>
    
    <span data-ttu-id="26af5-148">The results are varied for this query, not tied to any particular reference location.</span><span class="sxs-lookup"><span data-stu-id="26af5-148">The results are varied for this query, not tied to any particular reference location.</span></span> <span data-ttu-id="26af5-149">You can use the **countrySet** parameter to specify only the countries for which your application needs coverage, as the default behavior is to search the entire world, potentially returning unnecessary results.</span><span class="sxs-lookup"><span data-stu-id="26af5-149">You can use the **countrySet** parameter to specify only the countries for which your application needs coverage, as the default behavior is to search the entire world, potentially returning unnecessary results.</span></span>

5. <span data-ttu-id="26af5-150">Add the following Key / Value pair to the **Params** section and click **Send**:</span><span class="sxs-lookup"><span data-stu-id="26af5-150">Add the following Key / Value pair to the **Params** section and click **Send**:</span></span>

    | <span data-ttu-id="26af5-151">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-151">Key</span></span> | <span data-ttu-id="26af5-152">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-152">Value</span></span> |
    |------------------|-------------------------|
    | <span data-ttu-id="26af5-153">countrySet</span><span class="sxs-lookup"><span data-stu-id="26af5-153">countrySet</span></span> | <span data-ttu-id="26af5-154">US</span><span class="sxs-lookup"><span data-stu-id="26af5-154">US</span></span> |
    
    <span data-ttu-id="26af5-155">The results are now bounded by the country code and the query returns pizza restaurants in the United States.</span><span class="sxs-lookup"><span data-stu-id="26af5-155">The results are now bounded by the country code and the query returns pizza restaurants in the United States.</span></span>
    
    <span data-ttu-id="26af5-156">To provide results oriented on a particular location, you can query a point of interest and use the returned latitude and longitude values in your call to the Fuzzy Search service.</span><span class="sxs-lookup"><span data-stu-id="26af5-156">To provide results oriented on a particular location, you can query a point of interest and use the returned latitude and longitude values in your call to the Fuzzy Search service.</span></span> <span data-ttu-id="26af5-157">In this case, you used the Search service to return the location of the Seattle Space Needle and used the lat.</span><span class="sxs-lookup"><span data-stu-id="26af5-157">In this case, you used the Search service to return the location of the Seattle Space Needle and used the lat.</span></span> <span data-ttu-id="26af5-158">/ lon.</span><span class="sxs-lookup"><span data-stu-id="26af5-158">/ lon.</span></span> <span data-ttu-id="26af5-159">values to orient the search.</span><span class="sxs-lookup"><span data-stu-id="26af5-159">values to orient the search.</span></span>
    
4. <span data-ttu-id="26af5-160">In Params, enter the following Key / Value pairs and click **Send**:</span><span class="sxs-lookup"><span data-stu-id="26af5-160">In Params, enter the following Key / Value pairs and click **Send**:</span></span>

    ![<span data-ttu-id="26af5-161">Fuzzy Search</span><span class="sxs-lookup"><span data-stu-id="26af5-161">Fuzzy Search</span></span> ](./media/how-to-search-for-address/fuzzy_search_latlon.png)
    
    | <span data-ttu-id="26af5-162">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-162">Key</span></span> | <span data-ttu-id="26af5-163">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-163">Value</span></span> |
    |-----|------------|
    | <span data-ttu-id="26af5-164">lat</span><span class="sxs-lookup"><span data-stu-id="26af5-164">lat</span></span> | <span data-ttu-id="26af5-165">47.62039</span><span class="sxs-lookup"><span data-stu-id="26af5-165">47.62039</span></span> |
    | <span data-ttu-id="26af5-166">lon</span><span class="sxs-lookup"><span data-stu-id="26af5-166">lon</span></span> | <span data-ttu-id="26af5-167">-122.34928</span><span class="sxs-lookup"><span data-stu-id="26af5-167">-122.34928</span></span> |

## <a name="search-for-address-properties-and-coordinates"></a><span data-ttu-id="26af5-168">Search for address properties and coordinates</span><span class="sxs-lookup"><span data-stu-id="26af5-168">Search for address properties and coordinates</span></span> 

<span data-ttu-id="26af5-169">You can pass a complete or partial street address to the search address API and receive a response that includes detailed address properties such as municipality or subdivision, as well as positional values in latitude and longitude.</span><span class="sxs-lookup"><span data-stu-id="26af5-169">You can pass a complete or partial street address to the search address API and receive a response that includes detailed address properties such as municipality or subdivision, as well as positional values in latitude and longitude.</span></span>

1. <span data-ttu-id="26af5-170">In Postman, click **New Request** | **GET request** and name it **Address Search**.</span><span class="sxs-lookup"><span data-stu-id="26af5-170">In Postman, click **New Request** | **GET request** and name it **Address Search**.</span></span>
2. <span data-ttu-id="26af5-171">On the Builder tab, select the **GET** HTTP method, enter the request URL for your API endpoint, and select an authorization protocol, if any.</span><span class="sxs-lookup"><span data-stu-id="26af5-171">On the Builder tab, select the **GET** HTTP method, enter the request URL for your API endpoint, and select an authorization protocol, if any.</span></span>

    ![<span data-ttu-id="26af5-172">Address Search</span><span class="sxs-lookup"><span data-stu-id="26af5-172">Address Search</span></span> ](./media/how-to-search-for-address/address_search_url.png)
    
    | <span data-ttu-id="26af5-173">Parameter</span><span class="sxs-lookup"><span data-stu-id="26af5-173">Parameter</span></span> | <span data-ttu-id="26af5-174">Suggested value</span><span class="sxs-lookup"><span data-stu-id="26af5-174">Suggested value</span></span> |
    |---------------|------------------------------------------------|
    | <span data-ttu-id="26af5-175">HTTP method</span><span class="sxs-lookup"><span data-stu-id="26af5-175">HTTP method</span></span> | <span data-ttu-id="26af5-176">GET</span><span class="sxs-lookup"><span data-stu-id="26af5-176">GET</span></span> |
    | <span data-ttu-id="26af5-177">Request URL</span><span class="sxs-lookup"><span data-stu-id="26af5-177">Request URL</span></span> | https://atlas.microsoft.com/search/address/json? |
    | <span data-ttu-id="26af5-178">Authorization</span><span class="sxs-lookup"><span data-stu-id="26af5-178">Authorization</span></span> | <span data-ttu-id="26af5-179">No Auth</span><span class="sxs-lookup"><span data-stu-id="26af5-179">No Auth</span></span> |

2. <span data-ttu-id="26af5-180">Click **Params**, and enter the following Key / Value pairs to use as query or path parameters in the request URL:</span><span class="sxs-lookup"><span data-stu-id="26af5-180">Click **Params**, and enter the following Key / Value pairs to use as query or path parameters in the request URL:</span></span>
    
    ![<span data-ttu-id="26af5-181">Address Search</span><span class="sxs-lookup"><span data-stu-id="26af5-181">Address Search</span></span> ](./media/how-to-search-for-address/address_search_params.png)
    
    | <span data-ttu-id="26af5-182">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-182">Key</span></span> | <span data-ttu-id="26af5-183">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-183">Value</span></span> |
    |------------------|-------------------------|
    | <span data-ttu-id="26af5-184">api-version</span><span class="sxs-lookup"><span data-stu-id="26af5-184">api-version</span></span> | <span data-ttu-id="26af5-185">1.0</span><span class="sxs-lookup"><span data-stu-id="26af5-185">1.0</span></span> |
    | <span data-ttu-id="26af5-186">subscription-key</span><span class="sxs-lookup"><span data-stu-id="26af5-186">subscription-key</span></span> | <span data-ttu-id="26af5-187">\<your Azure Maps key\></span><span class="sxs-lookup"><span data-stu-id="26af5-187">\<your Azure Maps key\></span></span> |
    | <span data-ttu-id="26af5-188">query</span><span class="sxs-lookup"><span data-stu-id="26af5-188">query</span></span> | <span data-ttu-id="26af5-189">400 Broad St, Seattle, WA 98109</span><span class="sxs-lookup"><span data-stu-id="26af5-189">400 Broad St, Seattle, WA 98109</span></span> |
    
3. <span data-ttu-id="26af5-190">Click **Send** and review the response body.</span><span class="sxs-lookup"><span data-stu-id="26af5-190">Click **Send** and review the response body.</span></span> 
    
    <span data-ttu-id="26af5-191">In this case, you specified a complete address query and receive a single result in the response body.</span><span class="sxs-lookup"><span data-stu-id="26af5-191">In this case, you specified a complete address query and receive a single result in the response body.</span></span> 
    
4. <span data-ttu-id="26af5-192">In Params, edit the query string to the following value:</span><span class="sxs-lookup"><span data-stu-id="26af5-192">In Params, edit the query string to the following value:</span></span>
    ```
        400 Broad, Seattle
    ```

5. <span data-ttu-id="26af5-193">Add the following Key / Value pair to the **Params** section and click **Send**:</span><span class="sxs-lookup"><span data-stu-id="26af5-193">Add the following Key / Value pair to the **Params** section and click **Send**:</span></span>

    | <span data-ttu-id="26af5-194">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-194">Key</span></span> | <span data-ttu-id="26af5-195">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-195">Value</span></span> |
    |-----|------------|
    | <span data-ttu-id="26af5-196">typeahead</span><span class="sxs-lookup"><span data-stu-id="26af5-196">typeahead</span></span> | <span data-ttu-id="26af5-197">true</span><span class="sxs-lookup"><span data-stu-id="26af5-197">true</span></span> |

    <span data-ttu-id="26af5-198">The **typeahead** flag tells the Address Search API to treat the query as a partial input and return an array of predictive values.</span><span class="sxs-lookup"><span data-stu-id="26af5-198">The **typeahead** flag tells the Address Search API to treat the query as a partial input and return an array of predictive values.</span></span>

## <a name="search-for-a-street-address-using-reverse-address-search"></a><span data-ttu-id="26af5-199">Search for a street address using Reverse Address Search</span><span class="sxs-lookup"><span data-stu-id="26af5-199">Search for a street address using Reverse Address Search</span></span>
1. <span data-ttu-id="26af5-200">In Postman, click **New Request** | **GET request** and name it **Reverse Address Search**.</span><span class="sxs-lookup"><span data-stu-id="26af5-200">In Postman, click **New Request** | **GET request** and name it **Reverse Address Search**.</span></span>

2. <span data-ttu-id="26af5-201">On the Builder tab, select the **GET** HTTP method and enter the request URL for your API endpoint.</span><span class="sxs-lookup"><span data-stu-id="26af5-201">On the Builder tab, select the **GET** HTTP method and enter the request URL for your API endpoint.</span></span>
    
    ![<span data-ttu-id="26af5-202">Reverse Address Search URL</span><span class="sxs-lookup"><span data-stu-id="26af5-202">Reverse Address Search URL</span></span> ](./media/how-to-search-for-address/reverse_address_search_url.png)
    
    | <span data-ttu-id="26af5-203">Parameter</span><span class="sxs-lookup"><span data-stu-id="26af5-203">Parameter</span></span> | <span data-ttu-id="26af5-204">Suggested value</span><span class="sxs-lookup"><span data-stu-id="26af5-204">Suggested value</span></span> |
    |---------------|------------------------------------------------|
    | <span data-ttu-id="26af5-205">HTTP method</span><span class="sxs-lookup"><span data-stu-id="26af5-205">HTTP method</span></span> | <span data-ttu-id="26af5-206">GET</span><span class="sxs-lookup"><span data-stu-id="26af5-206">GET</span></span> |
    | <span data-ttu-id="26af5-207">Request URL</span><span class="sxs-lookup"><span data-stu-id="26af5-207">Request URL</span></span> | https://atlas.microsoft.com/search/address/reverse/json? |
    | <span data-ttu-id="26af5-208">Authorization</span><span class="sxs-lookup"><span data-stu-id="26af5-208">Authorization</span></span> | <span data-ttu-id="26af5-209">No Auth</span><span class="sxs-lookup"><span data-stu-id="26af5-209">No Auth</span></span> |
    
2. <span data-ttu-id="26af5-210">Click **Params**, and enter the following Key / Value pairs to use as query or path parameters in the request URL:</span><span class="sxs-lookup"><span data-stu-id="26af5-210">Click **Params**, and enter the following Key / Value pairs to use as query or path parameters in the request URL:</span></span>
    
    ![<span data-ttu-id="26af5-211">Reverse Address Search Parameters</span><span class="sxs-lookup"><span data-stu-id="26af5-211">Reverse Address Search Parameters</span></span> ](./media/how-to-search-for-address/reverse_address_search_params.png)
    
    | <span data-ttu-id="26af5-212">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-212">Key</span></span> | <span data-ttu-id="26af5-213">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-213">Value</span></span> |
    |------------------|-------------------------|
    | <span data-ttu-id="26af5-214">api-version</span><span class="sxs-lookup"><span data-stu-id="26af5-214">api-version</span></span> | <span data-ttu-id="26af5-215">1.0</span><span class="sxs-lookup"><span data-stu-id="26af5-215">1.0</span></span> |
    | <span data-ttu-id="26af5-216">subscription-key</span><span class="sxs-lookup"><span data-stu-id="26af5-216">subscription-key</span></span> | <span data-ttu-id="26af5-217">\<your Azure Maps key\></span><span class="sxs-lookup"><span data-stu-id="26af5-217">\<your Azure Maps key\></span></span> |
    | <span data-ttu-id="26af5-218">query</span><span class="sxs-lookup"><span data-stu-id="26af5-218">query</span></span> | <span data-ttu-id="26af5-219">47.59093,-122.33263</span><span class="sxs-lookup"><span data-stu-id="26af5-219">47.59093,-122.33263</span></span> |
    
3. <span data-ttu-id="26af5-220">Click **Send** and review the response body.</span><span class="sxs-lookup"><span data-stu-id="26af5-220">Click **Send** and review the response body.</span></span> 
    
    <span data-ttu-id="26af5-221">The response includes the POI entry for Safeco Field with a poi category of "stadium".</span><span class="sxs-lookup"><span data-stu-id="26af5-221">The response includes the POI entry for Safeco Field with a poi category of "stadium".</span></span> 
    
4. <span data-ttu-id="26af5-222">Add the following Key / Value pair to the **Params** section and click **Send**:</span><span class="sxs-lookup"><span data-stu-id="26af5-222">Add the following Key / Value pair to the **Params** section and click **Send**:</span></span>

    | <span data-ttu-id="26af5-223">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-223">Key</span></span> | <span data-ttu-id="26af5-224">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-224">Value</span></span> |
    |-----|------------|
    | <span data-ttu-id="26af5-225">number</span><span class="sxs-lookup"><span data-stu-id="26af5-225">number</span></span> | <span data-ttu-id="26af5-226">true</span><span class="sxs-lookup"><span data-stu-id="26af5-226">true</span></span> |

    <span data-ttu-id="26af5-227">If the [number](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse#search_getsearchaddressreverse_uri_parameters) query parameter is sent with the request, the response may include the side of the street (Left/Right) and also an offset position for that number.</span><span class="sxs-lookup"><span data-stu-id="26af5-227">If the [number](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse#search_getsearchaddressreverse_uri_parameters) query parameter is sent with the request, the response may include the side of the street (Left/Right) and also an offset position for that number.</span></span>
    
5. <span data-ttu-id="26af5-228">Add the following Key / Value pair to the **Params** section and click **Send**:</span><span class="sxs-lookup"><span data-stu-id="26af5-228">Add the following Key / Value pair to the **Params** section and click **Send**:</span></span>

    | <span data-ttu-id="26af5-229">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-229">Key</span></span> | <span data-ttu-id="26af5-230">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-230">Value</span></span> |
    |-----|------------|
    | <span data-ttu-id="26af5-231">returnSpeedLimit</span><span class="sxs-lookup"><span data-stu-id="26af5-231">returnSpeedLimit</span></span> | <span data-ttu-id="26af5-232">true</span><span class="sxs-lookup"><span data-stu-id="26af5-232">true</span></span> |
    
    <span data-ttu-id="26af5-233">When the [returnSpeedLimit](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse#search_getsearchaddressreverse_uri_parameters) query parameter is set, the response return of the posted speed limit.</span><span class="sxs-lookup"><span data-stu-id="26af5-233">When the [returnSpeedLimit](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse#search_getsearchaddressreverse_uri_parameters) query parameter is set, the response return of the posted speed limit.</span></span>

6. <span data-ttu-id="26af5-234">Add the following Key / Value pair to the **Params** section and click **Send**:</span><span class="sxs-lookup"><span data-stu-id="26af5-234">Add the following Key / Value pair to the **Params** section and click **Send**:</span></span>

    | <span data-ttu-id="26af5-235">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-235">Key</span></span> | <span data-ttu-id="26af5-236">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-236">Value</span></span> |
    |-----|------------|
    | <span data-ttu-id="26af5-237">returnRoadUse</span><span class="sxs-lookup"><span data-stu-id="26af5-237">returnRoadUse</span></span> | <span data-ttu-id="26af5-238">true</span><span class="sxs-lookup"><span data-stu-id="26af5-238">true</span></span> |

    <span data-ttu-id="26af5-239">When the [returnRoadUse](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse#search_getsearchaddressreverse_uri_parameters) query parameter is set, the response returns the road use array for reversegeocodes at street level.</span><span class="sxs-lookup"><span data-stu-id="26af5-239">When the [returnRoadUse](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse#search_getsearchaddressreverse_uri_parameters) query parameter is set, the response returns the road use array for reversegeocodes at street level.</span></span>

7. <span data-ttu-id="26af5-240">Add the following Key / Value pair to the **Params** section and click **Send**:</span><span class="sxs-lookup"><span data-stu-id="26af5-240">Add the following Key / Value pair to the **Params** section and click **Send**:</span></span>

    | <span data-ttu-id="26af5-241">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-241">Key</span></span> | <span data-ttu-id="26af5-242">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-242">Value</span></span> |
    |-----|------------|
    | <span data-ttu-id="26af5-243">roadUse</span><span class="sxs-lookup"><span data-stu-id="26af5-243">roadUse</span></span> | <span data-ttu-id="26af5-244">true</span><span class="sxs-lookup"><span data-stu-id="26af5-244">true</span></span> |

    <span data-ttu-id="26af5-245">You can restrict the reverse geocode query to a specific type of road use using the [roadUse](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse#search_getsearchaddressreverse_uri_parameters) query parameter.</span><span class="sxs-lookup"><span data-stu-id="26af5-245">You can restrict the reverse geocode query to a specific type of road use using the [roadUse](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse#search_getsearchaddressreverse_uri_parameters) query parameter.</span></span>
    
## <a name="search-for-the-cross-street-using-reverse-address-cross-street-search"></a><span data-ttu-id="26af5-246">Search for the cross street using Reverse Address Cross Street Search</span><span class="sxs-lookup"><span data-stu-id="26af5-246">Search for the cross street using Reverse Address Cross Street Search</span></span>

1. <span data-ttu-id="26af5-247">In Postman, click **New Request** | **GET request** and name it **Reverse Address Cross Street Search**.</span><span class="sxs-lookup"><span data-stu-id="26af5-247">In Postman, click **New Request** | **GET request** and name it **Reverse Address Cross Street Search**.</span></span>

2. <span data-ttu-id="26af5-248">On the Builder tab, select the **GET** HTTP method and enter the request URL for your API endpoint.</span><span class="sxs-lookup"><span data-stu-id="26af5-248">On the Builder tab, select the **GET** HTTP method and enter the request URL for your API endpoint.</span></span>
    
    ![<span data-ttu-id="26af5-249">Reverse Address Cross Street Search</span><span class="sxs-lookup"><span data-stu-id="26af5-249">Reverse Address Cross Street Search</span></span> ](./media/how-to-search-for-address/reverse_address_search_url.png)
    
    | <span data-ttu-id="26af5-250">Parameter</span><span class="sxs-lookup"><span data-stu-id="26af5-250">Parameter</span></span> | <span data-ttu-id="26af5-251">Suggested value</span><span class="sxs-lookup"><span data-stu-id="26af5-251">Suggested value</span></span> |
    |---------------|------------------------------------------------|
    | <span data-ttu-id="26af5-252">HTTP method</span><span class="sxs-lookup"><span data-stu-id="26af5-252">HTTP method</span></span> | <span data-ttu-id="26af5-253">GET</span><span class="sxs-lookup"><span data-stu-id="26af5-253">GET</span></span> |
    | <span data-ttu-id="26af5-254">Request URL</span><span class="sxs-lookup"><span data-stu-id="26af5-254">Request URL</span></span> | https://atlas.microsoft.com/search/address/reverse/crossstreet/json? |
    | <span data-ttu-id="26af5-255">Authorization</span><span class="sxs-lookup"><span data-stu-id="26af5-255">Authorization</span></span> | <span data-ttu-id="26af5-256">No Auth</span><span class="sxs-lookup"><span data-stu-id="26af5-256">No Auth</span></span> |
    
3. <span data-ttu-id="26af5-257">Click **Params**, and enter the following Key / Value pairs to use as query or path parameters in the request URL:</span><span class="sxs-lookup"><span data-stu-id="26af5-257">Click **Params**, and enter the following Key / Value pairs to use as query or path parameters in the request URL:</span></span>
    
    | <span data-ttu-id="26af5-258">Key</span><span class="sxs-lookup"><span data-stu-id="26af5-258">Key</span></span> | <span data-ttu-id="26af5-259">Value</span><span class="sxs-lookup"><span data-stu-id="26af5-259">Value</span></span> |
    |------------------|-------------------------|
    | <span data-ttu-id="26af5-260">api-version</span><span class="sxs-lookup"><span data-stu-id="26af5-260">api-version</span></span> | <span data-ttu-id="26af5-261">1.0</span><span class="sxs-lookup"><span data-stu-id="26af5-261">1.0</span></span> |
    | <span data-ttu-id="26af5-262">subscription-key</span><span class="sxs-lookup"><span data-stu-id="26af5-262">subscription-key</span></span> | <span data-ttu-id="26af5-263">\<your Azure Maps key\></span><span class="sxs-lookup"><span data-stu-id="26af5-263">\<your Azure Maps key\></span></span> |
    | <span data-ttu-id="26af5-264">query</span><span class="sxs-lookup"><span data-stu-id="26af5-264">query</span></span> | <span data-ttu-id="26af5-265">47.59093,-122.33263</span><span class="sxs-lookup"><span data-stu-id="26af5-265">47.59093,-122.33263</span></span> |
    
4. <span data-ttu-id="26af5-266">Click **Send** and review the response body.</span><span class="sxs-lookup"><span data-stu-id="26af5-266">Click **Send** and review the response body.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="26af5-267">Next steps</span><span class="sxs-lookup"><span data-stu-id="26af5-267">Next steps</span></span>
- <span data-ttu-id="26af5-268">Explore the [Azure Maps search service](https://docs.microsoft.com/rest/api/maps/search) API documentation</span><span class="sxs-lookup"><span data-stu-id="26af5-268">Explore the [Azure Maps search service](https://docs.microsoft.com/rest/api/maps/search) API documentation</span></span> 
