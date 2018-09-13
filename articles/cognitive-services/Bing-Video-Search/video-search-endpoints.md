---
title: Video search endpoints | Microsoft Docs
description: Summary of the Video search API endpoint.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 12/04/2017
ms.author: v-gedod
ms.openlocfilehash: 9836d9928362ab37b0a81ff5043d99f9bf353f22
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868077"
---
# <a name="video-search-endpoints"></a><span data-ttu-id="8c288-103">Video Search endpoints</span><span class="sxs-lookup"><span data-stu-id="8c288-103">Video Search endpoints</span></span>
<span data-ttu-id="8c288-104">The **Video Search API**  includes three endpoints.</span><span class="sxs-lookup"><span data-stu-id="8c288-104">The **Video Search API**  includes three endpoints.</span></span>  <span data-ttu-id="8c288-105">Endpoint 1 returns videos from the Web based on a query.</span><span class="sxs-lookup"><span data-stu-id="8c288-105">Endpoint 1 returns videos from the Web based on a query.</span></span> <span data-ttu-id="8c288-106">Endpoint 2 returns insights about a video based on the `modules` URL parameter.</span><span class="sxs-lookup"><span data-stu-id="8c288-106">Endpoint 2 returns insights about a video based on the `modules` URL parameter.</span></span>  <span data-ttu-id="8c288-107">Endpoint 3 returns trending images.</span><span class="sxs-lookup"><span data-stu-id="8c288-107">Endpoint 3 returns trending images.</span></span>

## <a name="endpoints"></a><span data-ttu-id="8c288-108">Endpoints</span><span class="sxs-lookup"><span data-stu-id="8c288-108">Endpoints</span></span>
<span data-ttu-id="8c288-109">To get video results using the Bing API, send a `GET` request to one of the following endpoints.</span><span class="sxs-lookup"><span data-stu-id="8c288-109">To get video results using the Bing API, send a `GET` request to one of the following endpoints.</span></span> <span data-ttu-id="8c288-110">Use the headers and URL parameters to define further specifications.</span><span class="sxs-lookup"><span data-stu-id="8c288-110">Use the headers and URL parameters to define further specifications.</span></span>

<span data-ttu-id="8c288-111">**Endpoint1:** Returns videos that are relevant to the user's search query defined by `?q=""`.</span><span class="sxs-lookup"><span data-stu-id="8c288-111">**Endpoint1:** Returns videos that are relevant to the user's search query defined by `?q=""`.</span></span>
``` 
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search
```

<span data-ttu-id="8c288-112">**Endpoint 2:** Returns insights about a video, such as related videos.</span><span class="sxs-lookup"><span data-stu-id="8c288-112">**Endpoint 2:** Returns insights about a video, such as related videos.</span></span> <span data-ttu-id="8c288-113">Include the `modules` [query parameter](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query-parameters), which is a comma-delimited list of insights to request.</span><span class="sxs-lookup"><span data-stu-id="8c288-113">Include the `modules` [query parameter](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query-parameters), which is a comma-delimited list of insights to request.</span></span>
``` 
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/details
```

<span data-ttu-id="8c288-114">**Endpoint 3:** Returns videos that are trending based on search requests made by others.</span><span class="sxs-lookup"><span data-stu-id="8c288-114">**Endpoint 3:** Returns videos that are trending based on search requests made by others.</span></span> <span data-ttu-id="8c288-115">The videos are separated into different categories, for example, based on noteworthy people or events.</span><span class="sxs-lookup"><span data-stu-id="8c288-115">The videos are separated into different categories, for example, based on noteworthy people or events.</span></span>
```
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/trending
```

<span data-ttu-id="8c288-116">For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Video Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="8c288-116">For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Video Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) reference.</span></span>
## <a name="response-json"></a><span data-ttu-id="8c288-117">Response JSON</span><span class="sxs-lookup"><span data-stu-id="8c288-117">Response JSON</span></span>
<span data-ttu-id="8c288-118">The response to a videos search request includes results as JSON objects.</span><span class="sxs-lookup"><span data-stu-id="8c288-118">The response to a videos search request includes results as JSON objects.</span></span> <span data-ttu-id="8c288-119">For examples of parsing the results see the [tutorial](https://docs.microsoft.com/azure/cognitive-services/bing-video-search/tutorial-bing-video-search-single-page-app) and [source code](https://docs.microsoft.com/azure/cognitive-services/bing-video-search/tutorial-bing-video-search-single-page-app-source).</span><span class="sxs-lookup"><span data-stu-id="8c288-119">For examples of parsing the results see the [tutorial](https://docs.microsoft.com/azure/cognitive-services/bing-video-search/tutorial-bing-video-search-single-page-app) and [source code](https://docs.microsoft.com/azure/cognitive-services/bing-video-search/tutorial-bing-video-search-single-page-app-source).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c288-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c288-120">Next steps</span></span>
<span data-ttu-id="8c288-121">The **Bing** APIs support search actions that return results according to their type.</span><span class="sxs-lookup"><span data-stu-id="8c288-121">The **Bing** APIs support search actions that return results according to their type.</span></span> <span data-ttu-id="8c288-122">All search endpoints return results as JSON response objects.</span><span class="sxs-lookup"><span data-stu-id="8c288-122">All search endpoints return results as JSON response objects.</span></span>  <span data-ttu-id="8c288-123">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span><span class="sxs-lookup"><span data-stu-id="8c288-123">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span></span>

<span data-ttu-id="8c288-124">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span><span class="sxs-lookup"><span data-stu-id="8c288-124">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span></span>
<span data-ttu-id="8c288-125">For examples of basic requests using the Video search API, see [Video Search Quick-starts](https://docs.microsoft.com/azure/cognitive-services/bing-video-search).</span><span class="sxs-lookup"><span data-stu-id="8c288-125">For examples of basic requests using the Video search API, see [Video Search Quick-starts](https://docs.microsoft.com/azure/cognitive-services/bing-video-search).</span></span>