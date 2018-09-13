---
title: Image search endpoints | Microsoft Docs
description: Summary of the Image search API endpoint.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 11/30/2017
ms.author: v-gedod
ms.openlocfilehash: 0d5f28bfdb45b27b04df068f75e8a20d0235d12b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868903"
---
# <a name="image-search-endpoints"></a><span data-ttu-id="67536-103">Image Search endpoints</span><span class="sxs-lookup"><span data-stu-id="67536-103">Image Search endpoints</span></span>
<span data-ttu-id="67536-104">The **Image Search API**  includes three endpoints.</span><span class="sxs-lookup"><span data-stu-id="67536-104">The **Image Search API**  includes three endpoints.</span></span>  <span data-ttu-id="67536-105">Endpoint 1 returns images from the Web based on a query.</span><span class="sxs-lookup"><span data-stu-id="67536-105">Endpoint 1 returns images from the Web based on a query.</span></span> <span data-ttu-id="67536-106">Endpoint 2 returns [ImageInsights](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imageinsightsresponse).</span><span class="sxs-lookup"><span data-stu-id="67536-106">Endpoint 2 returns [ImageInsights](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imageinsightsresponse).</span></span>  <span data-ttu-id="67536-107">Endpoint 3 returns trending images.</span><span class="sxs-lookup"><span data-stu-id="67536-107">Endpoint 3 returns trending images.</span></span>
## <a name="endpoints"></a><span data-ttu-id="67536-108">Endpoints</span><span class="sxs-lookup"><span data-stu-id="67536-108">Endpoints</span></span>
<span data-ttu-id="67536-109">To get image results using the Bing API, send a request to one of the following endpoints.</span><span class="sxs-lookup"><span data-stu-id="67536-109">To get image results using the Bing API, send a request to one of the following endpoints.</span></span> <span data-ttu-id="67536-110">Use the headers and URL parameters to define further specifications.</span><span class="sxs-lookup"><span data-stu-id="67536-110">Use the headers and URL parameters to define further specifications.</span></span>

<span data-ttu-id="67536-111">**Endpoint 1:** Returns images that are relevant to the user's search query defined by `?q=""`.</span><span class="sxs-lookup"><span data-stu-id="67536-111">**Endpoint 1:** Returns images that are relevant to the user's search query defined by `?q=""`.</span></span>
``` 
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search
```

<span data-ttu-id="67536-112">**Endpoint 2:** Returns insights about an image, using either `GET` or `POST`.</span><span class="sxs-lookup"><span data-stu-id="67536-112">**Endpoint 2:** Returns insights about an image, using either `GET` or `POST`.</span></span>
``` 
 GET or POST https://api.cognitive.microsoft.com/bing/v7.0/images/details
```
<span data-ttu-id="67536-113">A GET request returns insights about an image, such as Web pages that include the image.</span><span class="sxs-lookup"><span data-stu-id="67536-113">A GET request returns insights about an image, such as Web pages that include the image.</span></span> <span data-ttu-id="67536-114">Include the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) parameter with a `GET` request.</span><span class="sxs-lookup"><span data-stu-id="67536-114">Include the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) parameter with a `GET` request.</span></span>

<span data-ttu-id="67536-115">Or, you can include a binary image in the body of a `POST` request and set the [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) parameter to `RecognizedEntities`.</span><span class="sxs-lookup"><span data-stu-id="67536-115">Or, you can include a binary image in the body of a `POST` request and set the [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) parameter to `RecognizedEntities`.</span></span> <span data-ttu-id="67536-116">This will return an [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v5-reference#insightstoken) to use as a parameter in a subsequent `GET` request, which returns information about people in the image.</span><span class="sxs-lookup"><span data-stu-id="67536-116">This will return an [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v5-reference#insightstoken) to use as a parameter in a subsequent `GET` request, which returns information about people in the image.</span></span>  <span data-ttu-id="67536-117">Set `modules` to `All` to get all insights, except `RecognizedEntities` in the results of the `POST` without making another call using the `insightsToken`.</span><span class="sxs-lookup"><span data-stu-id="67536-117">Set `modules` to `All` to get all insights, except `RecognizedEntities` in the results of the `POST` without making another call using the `insightsToken`.</span></span> 


<span data-ttu-id="67536-118">**Endpoint 3:** Returns images that are trending based on search requests made by others.</span><span class="sxs-lookup"><span data-stu-id="67536-118">**Endpoint 3:** Returns images that are trending based on search requests made by others.</span></span> <span data-ttu-id="67536-119">The images are separated into different categories, for example, based on noteworthy people or events.</span><span class="sxs-lookup"><span data-stu-id="67536-119">The images are separated into different categories, for example, based on noteworthy people or events.</span></span>
```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/trending
```

<span data-ttu-id="67536-120">For a list of markets that support trending images, see [Trending Images](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/trending-images).</span><span class="sxs-lookup"><span data-stu-id="67536-120">For a list of markets that support trending images, see [Trending Images](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/trending-images).</span></span>

<span data-ttu-id="67536-121">For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Image Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="67536-121">For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Image Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference) reference.</span></span>
## <a name="response-json"></a><span data-ttu-id="67536-122">Response JSON</span><span class="sxs-lookup"><span data-stu-id="67536-122">Response JSON</span></span>
<span data-ttu-id="67536-123">The response to an image search request includes results as JSON objects.</span><span class="sxs-lookup"><span data-stu-id="67536-123">The response to an image search request includes results as JSON objects.</span></span> <span data-ttu-id="67536-124">For examples of parsing the results see the [tutorial](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/tutorial-bing-image-search-single-page-app) and [source code](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/tutorial-bing-image-search-single-page-app-source).</span><span class="sxs-lookup"><span data-stu-id="67536-124">For examples of parsing the results see the [tutorial](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/tutorial-bing-image-search-single-page-app) and [source code](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/tutorial-bing-image-search-single-page-app-source).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67536-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="67536-125">Next steps</span></span>
<span data-ttu-id="67536-126">The **Bing** APIs support search actions that return results according to their type.</span><span class="sxs-lookup"><span data-stu-id="67536-126">The **Bing** APIs support search actions that return results according to their type.</span></span> <span data-ttu-id="67536-127">All search endpoints return results as JSON response objects.</span><span class="sxs-lookup"><span data-stu-id="67536-127">All search endpoints return results as JSON response objects.</span></span>  <span data-ttu-id="67536-128">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span><span class="sxs-lookup"><span data-stu-id="67536-128">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span></span>

<span data-ttu-id="67536-129">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span><span class="sxs-lookup"><span data-stu-id="67536-129">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span></span>
<span data-ttu-id="67536-130">For examples of basic requests using the Image search API, see [Image Search Quick-starts](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/search-the-web).</span><span class="sxs-lookup"><span data-stu-id="67536-130">For examples of basic requests using the Image search API, see [Image Search Quick-starts](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/search-the-web).</span></span>