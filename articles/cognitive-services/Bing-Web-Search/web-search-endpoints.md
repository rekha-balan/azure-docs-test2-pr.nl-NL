---
title: Web search endpoint | Microsoft Docs
description: Summary of the Web search API endpoint.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 11/28/2017
ms.author: v-gedod
ms.openlocfilehash: 72fbe1a0eb4379ad032e649f7299e37a0214adfb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869846"
---
# <a name="web-search-endpoint"></a><span data-ttu-id="120cb-103">Web Search endpoint</span><span class="sxs-lookup"><span data-stu-id="120cb-103">Web Search endpoint</span></span>
<span data-ttu-id="120cb-104">The **Web Search API** returns Web pages, news, images, videos, and [entities](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web).</span><span class="sxs-lookup"><span data-stu-id="120cb-104">The **Web Search API** returns Web pages, news, images, videos, and [entities](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web).</span></span> <span data-ttu-id="120cb-105">Entities contain summary information about a person, place, or topic.</span><span class="sxs-lookup"><span data-stu-id="120cb-105">Entities contain summary information about a person, place, or topic.</span></span>
## <a name="endpoint"></a><span data-ttu-id="120cb-106">Endpoint</span><span class="sxs-lookup"><span data-stu-id="120cb-106">Endpoint</span></span>
<span data-ttu-id="120cb-107">To get Web search results using the Bing API, send a `GET` request to the following endpoint.</span><span class="sxs-lookup"><span data-stu-id="120cb-107">To get Web search results using the Bing API, send a `GET` request to the following endpoint.</span></span> <span data-ttu-id="120cb-108">The headers and URL parameters define further specifications.</span><span class="sxs-lookup"><span data-stu-id="120cb-108">The headers and URL parameters define further specifications.</span></span>

<span data-ttu-id="120cb-109">**Endpoint**: Returns Web results that are relevant to the user's search query defined by `?q=""`.</span><span class="sxs-lookup"><span data-stu-id="120cb-109">**Endpoint**: Returns Web results that are relevant to the user's search query defined by `?q=""`.</span></span>
```
GET https://api.cognitive.microsoft.com/bing/v7.0/search
```
<span data-ttu-id="120cb-110">Endpoint: For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Web API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="120cb-110">Endpoint: For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Web API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference) reference.</span></span>

## <a name="response-json"></a><span data-ttu-id="120cb-111">Response JSON</span><span class="sxs-lookup"><span data-stu-id="120cb-111">Response JSON</span></span>
<span data-ttu-id="120cb-112">The response to a Web search request includes all results as JSON objects.</span><span class="sxs-lookup"><span data-stu-id="120cb-112">The response to a Web search request includes all results as JSON objects.</span></span> <span data-ttu-id="120cb-113">Parsing the result requires procedures that handle the elements of each type.</span><span class="sxs-lookup"><span data-stu-id="120cb-113">Parsing the result requires procedures that handle the elements of each type.</span></span> <span data-ttu-id="120cb-114">See the [tutorial](https://docs.microsoft.com/azure/cognitive-services/bing-web-search/tutorial-bing-web-search-single-page-app) and [source code](https://docs.microsoft.com/azure/cognitive-services/bing-web-search/tutorial-bing-web-search-single-page-app-source) for examples.</span><span class="sxs-lookup"><span data-stu-id="120cb-114">See the [tutorial](https://docs.microsoft.com/azure/cognitive-services/bing-web-search/tutorial-bing-web-search-single-page-app) and [source code](https://docs.microsoft.com/azure/cognitive-services/bing-web-search/tutorial-bing-web-search-single-page-app-source) for examples.</span></span>

## <a name="next-steps"></a><span data-ttu-id="120cb-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="120cb-115">Next steps</span></span>
<span data-ttu-id="120cb-116">The **Bing** APIs support search actions that return results according to their type.</span><span class="sxs-lookup"><span data-stu-id="120cb-116">The **Bing** APIs support search actions that return results according to their type.</span></span> <span data-ttu-id="120cb-117">All search endpoints return results as JSON response objects.</span><span class="sxs-lookup"><span data-stu-id="120cb-117">All search endpoints return results as JSON response objects.</span></span>  <span data-ttu-id="120cb-118">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span><span class="sxs-lookup"><span data-stu-id="120cb-118">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span></span>

<span data-ttu-id="120cb-119">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span><span class="sxs-lookup"><span data-stu-id="120cb-119">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span></span>
<span data-ttu-id="120cb-120">For examples of basic requests using the Web search API, see [Search the Web Quick-starts](https://docs.microsoft.com/azure/cognitive-services/bing-web-search/search-the-web).</span><span class="sxs-lookup"><span data-stu-id="120cb-120">For examples of basic requests using the Web search API, see [Search the Web Quick-starts](https://docs.microsoft.com/azure/cognitive-services/bing-web-search/search-the-web).</span></span>