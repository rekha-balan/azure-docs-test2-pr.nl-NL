---
title: Autosuggest endpoint | Microsoft Docs
description: Summary of the Autosuggest API endpoint.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-autosuggest
ms.topic: article
ms.date: 12/05/2017
ms.author: v-gedod
ms.openlocfilehash: 5aaddd09006cb6f1812bb6ae213a2f5e6720fb1b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856486"
---
# <a name="autosuggest-endpoint"></a><span data-ttu-id="c5cd9-103">Autosuggest endpoint</span><span class="sxs-lookup"><span data-stu-id="c5cd9-103">Autosuggest endpoint</span></span>

<span data-ttu-id="c5cd9-104">The **Autosuggest API**  includes one endpoint, which returns a list of suggested queries from a partial search term.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-104">The **Autosuggest API**  includes one endpoint, which returns a list of suggested queries from a partial search term.</span></span>

## <a name="endpoint"></a><span data-ttu-id="c5cd9-105">Endpoint</span><span class="sxs-lookup"><span data-stu-id="c5cd9-105">Endpoint</span></span>

<span data-ttu-id="c5cd9-106">To get suggested queries using the Bing API, send a `GET` request to the following endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-106">To get suggested queries using the Bing API, send a `GET` request to the following endpoint.</span></span> <span data-ttu-id="c5cd9-107">Use the headers and URL parameters to define further specifications.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-107">Use the headers and URL parameters to define further specifications.</span></span>

<span data-ttu-id="c5cd9-108">**Endpoint:** Returns search suggestions as JSON results that are relevant to the user's input defined by `?q=""`.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-108">**Endpoint:** Returns search suggestions as JSON results that are relevant to the user's input defined by `?q=""`.</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/Suggestions 
```

<span data-ttu-id="c5cd9-109">For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Autosuggest API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-109">For details about headers, parameters, market codes, response objects, errors, etc., see the [Bing Autosuggest API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference) reference.</span></span>

## <a name="response-json"></a><span data-ttu-id="c5cd9-110">Response JSON</span><span class="sxs-lookup"><span data-stu-id="c5cd9-110">Response JSON</span></span>

<span data-ttu-id="c5cd9-111">The response to an autosuggest request includes results as JSON objects.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-111">The response to an autosuggest request includes results as JSON objects.</span></span> <span data-ttu-id="c5cd9-112">For examples of parsing the results see the [tutorial](tutorials/autosuggest.md) and [source code](tutorials/autosuggest-source.md).</span><span class="sxs-lookup"><span data-stu-id="c5cd9-112">For examples of parsing the results see the [tutorial](tutorials/autosuggest.md) and [source code](tutorials/autosuggest-source.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5cd9-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5cd9-113">Next steps</span></span>

<span data-ttu-id="c5cd9-114">The **Bing** APIs support search actions that return results according to their type.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-114">The **Bing** APIs support search actions that return results according to their type.</span></span> <span data-ttu-id="c5cd9-115">All search endpoints return results as JSON response objects.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-115">All search endpoints return results as JSON response objects.</span></span>
<span data-ttu-id="c5cd9-116">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-116">All endpoints support queries that return a specific language and/or location by longitude, latitude, and search radius.</span></span>

<span data-ttu-id="c5cd9-117">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span><span class="sxs-lookup"><span data-stu-id="c5cd9-117">For complete information about the parameters supported by each endpoint, see the reference pages for each type.</span></span>
<span data-ttu-id="c5cd9-118">For examples of basic requests using the Autosuggest API, see [Autosuggest Quickstarts](https://docs.microsoft.com/azure/cognitive-services/Bing-Autosuggest).</span><span class="sxs-lookup"><span data-stu-id="c5cd9-118">For examples of basic requests using the Autosuggest API, see [Autosuggest Quickstarts](https://docs.microsoft.com/azure/cognitive-services/Bing-Autosuggest).</span></span>