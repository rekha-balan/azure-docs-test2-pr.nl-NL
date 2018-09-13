---
title: Entity Search endpoint | Microsoft Docs
description: Summary of the Entity Search API endpoint.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 12/05/2017
ms.author: v-gedod
ms.openlocfilehash: a2557c6000445544b3b47a05d7d356ccaa9928b4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869302"
---
# <a name="entity-search-endpoint"></a><span data-ttu-id="909d0-103">Entity Search endpoint</span><span class="sxs-lookup"><span data-stu-id="909d0-103">Entity Search endpoint</span></span>
<span data-ttu-id="909d0-104">The **Entity Search API**  includes one endpoint that returns entities from the Web based on a query.</span><span class="sxs-lookup"><span data-stu-id="909d0-104">The **Entity Search API**  includes one endpoint that returns entities from the Web based on a query.</span></span>

## <a name="endpoint"></a><span data-ttu-id="909d0-105">Endpoint</span><span class="sxs-lookup"><span data-stu-id="909d0-105">Endpoint</span></span>
<span data-ttu-id="909d0-106">To get entity results using the **Bing API**, send a `GET` request to the following endpoint.</span><span class="sxs-lookup"><span data-stu-id="909d0-106">To get entity results using the **Bing API**, send a `GET` request to the following endpoint.</span></span> <span data-ttu-id="909d0-107">Use the headers and URL parameters to define further specifications.</span><span class="sxs-lookup"><span data-stu-id="909d0-107">Use the headers and URL parameters to define further specifications.</span></span>

<span data-ttu-id="909d0-108">**Endpoint:** Returns entities that are relevant to the user's search query defined by `?q=""`.</span><span class="sxs-lookup"><span data-stu-id="909d0-108">**Endpoint:** Returns entities that are relevant to the user's search query defined by `?q=""`.</span></span>
```
 GET https://api.cognitive.microsoft.com/bing/v7.0/entities
```

<span data-ttu-id="909d0-109">For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Entity Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="909d0-109">For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Entity Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference) reference.</span></span>

## <a name="response-json"></a><span data-ttu-id="909d0-110">Response JSON</span><span class="sxs-lookup"><span data-stu-id="909d0-110">Response JSON</span></span>
<span data-ttu-id="909d0-111">The response to a entity search request includes results as JSON objects.</span><span class="sxs-lookup"><span data-stu-id="909d0-111">The response to a entity search request includes results as JSON objects.</span></span> <span data-ttu-id="909d0-112">For examples of the results, see [Get started](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/quick-start).</span><span class="sxs-lookup"><span data-stu-id="909d0-112">For examples of the results, see [Get started](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/quick-start).</span></span>

## <a name="next-steps"></a><span data-ttu-id="909d0-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="909d0-113">Next steps</span></span>
<span data-ttu-id="909d0-114">The **Bing** APIs support search actions that return results according to their type.</span><span class="sxs-lookup"><span data-stu-id="909d0-114">The **Bing** APIs support search actions that return results according to their type.</span></span> <span data-ttu-id="909d0-115">All search endpoints return results as JSON response objects.</span><span class="sxs-lookup"><span data-stu-id="909d0-115">All search endpoints return results as JSON response objects.</span></span>  <span data-ttu-id="909d0-116">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span><span class="sxs-lookup"><span data-stu-id="909d0-116">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span></span>

<span data-ttu-id="909d0-117">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span><span class="sxs-lookup"><span data-stu-id="909d0-117">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span></span>
<span data-ttu-id="909d0-118">For examples using the Entity search API, see [Get started](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/quick-start) and [Resizing and cropping thumbnail images](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/resize-and-crop-thumbnails).</span><span class="sxs-lookup"><span data-stu-id="909d0-118">For examples using the Entity search API, see [Get started](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/quick-start) and [Resizing and cropping thumbnail images](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/resize-and-crop-thumbnails).</span></span>