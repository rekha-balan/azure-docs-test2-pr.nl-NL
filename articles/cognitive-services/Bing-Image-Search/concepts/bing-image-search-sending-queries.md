---
title: Send queries to the Bing Image Search API | Microsoft Docs
description: Learn about sending and customizing search queries sent to the Bing Image Search API.
services: cognitive-services
author: aahill
manager: cgronlun
ms.assetid: C2862E98-8BCC-423B-9C4A-AC79A287BE38
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: conceptual
ms.date: 8/8/2018
ms.author: aahi
ms.openlocfilehash: bf0db0b6d2aa54a853ba86b570ca05fba902dbc1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864828"
---
# <a name="send-queries-to-the-bing-image-search-api"></a><span data-ttu-id="3b1ce-103">Send queries to the Bing Image Search API</span><span class="sxs-lookup"><span data-stu-id="3b1ce-103">Send queries to the Bing Image Search API</span></span>

<span data-ttu-id="3b1ce-104">The Bing Image Search API provides an experience similar to Bing.com/Images.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-104">The Bing Image Search API provides an experience similar to Bing.com/Images.</span></span> <span data-ttu-id="3b1ce-105">You can use it to send a search query to Bing and get back a list of relevant images.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-105">You can use it to send a search query to Bing and get back a list of relevant images.</span></span>

## <a name="use-and-suggest-search-terms"></a><span data-ttu-id="3b1ce-106">Use and suggest search terms</span><span class="sxs-lookup"><span data-stu-id="3b1ce-106">Use and suggest search terms</span></span>

<span data-ttu-id="3b1ce-107">After a search term is entered, URL-encode the term before you set the [**q**](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query) query parameter.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-107">After a search term is entered, URL-encode the term before you set the [**q**](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query) query parameter.</span></span> <span data-ttu-id="3b1ce-108">For example, if you enter *sailing dinghies*, set `q` to `sailing+dinghies` or `sailing%20dinghies`.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-108">For example, if you enter *sailing dinghies*, set `q` to `sailing+dinghies` or `sailing%20dinghies`.</span></span>

<span data-ttu-id="3b1ce-109">If your app has a search box where search terms are entered, you can use the [Bing Autosuggest API](../../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-109">If your app has a search box where search terms are entered, you can use the [Bing Autosuggest API](../../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span></span> <span data-ttu-id="3b1ce-110">The API can display suggested search terms in real time.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-110">The API can display suggested search terms in real time.</span></span> <span data-ttu-id="3b1ce-111">The API returns suggested query strings based on partial search terms and Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-111">The API returns suggested query strings based on partial search terms and Cognitive Services.</span></span>

## <a name="pivot-the-query"></a><span data-ttu-id="3b1ce-112">Pivot the query</span><span class="sxs-lookup"><span data-stu-id="3b1ce-112">Pivot the query</span></span>

<span data-ttu-id="3b1ce-113">If Bing can segment the original search query, the returned [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) object contains `pivotSuggestions`.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-113">If Bing can segment the original search query, the returned [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) object contains `pivotSuggestions`.</span></span> <span data-ttu-id="3b1ce-114">Pivot suggestions can be displayed as optional search terms to the user.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-114">Pivot suggestions can be displayed as optional search terms to the user.</span></span> <span data-ttu-id="3b1ce-115">For example, if the original query was *Microsoft Surface*, Bing might segment the query into *Microsoft* and *Surface* and provide suggested pivots for each.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-115">For example, if the original query was *Microsoft Surface*, Bing might segment the query into *Microsoft* and *Surface* and provide suggested pivots for each.</span></span> <span data-ttu-id="3b1ce-116">These suggestions can be displayed as optional query terms to the user.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-116">These suggestions can be displayed as optional query terms to the user.</span></span>

<span data-ttu-id="3b1ce-117">The following example shows the pivot suggestions for *Microsoft Surface*:</span><span class="sxs-lookup"><span data-stu-id="3b1ce-117">The following example shows the pivot suggestions for *Microsoft Surface*:</span></span>  

```json
{
    "_type": "Images",
    "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=microsoft%20surface&FORM=OIIARP",
    "totalEstimatedMatches": 1000,
    "value": [...],
    "queryExpansions": [...],
    "pivotSuggestions": [{
        "pivot": "microsoft",
        "suggestions": [{
            "text": "Contoso Surface",
            "displayText": "Contoso",
            "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=OtterBox+Surface&FORM=IRQBPS",
            "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=Contoso...",
                    "searchLink": "https:\/\/api.cognitive.microsoft.com\/api...",
            "thumbnail": {
                "thumbnailUrl": "https:\/\/tse3.mm.bing.net\/th?q=Contoso+Surface..."
            }
        },
        {
            "text": "Adatum Surface",
            "displayText": "Adatum",
            "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Adatum+Surface&FORM=IRQBPS",
            "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=...",
            "thumbnail": {
                "thumbnailUrl": "https:\/\/tse3.mm.bing.net\/th?q=Adatum+Surface&pid=Ap..."
            }
        },
        ...
        ]
    },
    {
        "pivot": "surface",
        "suggestions": [{
            "text": "Microsoft Surface4",
            "displayText": "Surface4",
            "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Surface...",
            "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?...",
            "thumbnail": {
                "thumbnailUrl": "https:\/\/tse4.mm.bing.net\/th?q=Microsoft..."
            }
        },
        {
            "text": "Microsoft Tablet",
            "displayText": "Tablet",
            "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Tablet&FORM=IRQBPS",
            "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?...",
            "thumbnail": {
                "thumbnailUrl": "https:\/\/tse3.mm.bing.net\/th?q=Microsoft+Tablet..."
            }
        },
        ...
    ],
    "nextOffsetAddCount": 0
}
```

<span data-ttu-id="3b1ce-118">The `pivotSuggestions` field contains the list of segments (pivots) that the original query was broken into.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-118">The `pivotSuggestions` field contains the list of segments (pivots) that the original query was broken into.</span></span> <span data-ttu-id="3b1ce-119">For each pivot, the response contains a list of [Query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query_obj) objects that contain suggested queries.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-119">For each pivot, the response contains a list of [Query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query_obj) objects that contain suggested queries.</span></span> <span data-ttu-id="3b1ce-120">The `text` field contains the suggested query.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-120">The `text` field contains the suggested query.</span></span> <span data-ttu-id="3b1ce-121">The `displayText` field contains the term that replaces the pivot in the original query.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-121">The `displayText` field contains the term that replaces the pivot in the original query.</span></span> <span data-ttu-id="3b1ce-122">An example is Release Date of Surface.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-122">An example is Release Date of Surface.</span></span>

<span data-ttu-id="3b1ce-123">If the pivot query string is what the user is looking for, use the `text` and `thumbnail` fields to display the pivot query strings.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-123">If the pivot query string is what the user is looking for, use the `text` and `thumbnail` fields to display the pivot query strings.</span></span> <span data-ttu-id="3b1ce-124">Make the thumbnail and text clickable by using the `webSearchUrl` URL or the `searchLink` URL.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-124">Make the thumbnail and text clickable by using the `webSearchUrl` URL or the `searchLink` URL.</span></span> <span data-ttu-id="3b1ce-125">Use `webSearchUrl` to send the user to the Bing search results.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-125">Use `webSearchUrl` to send the user to the Bing search results.</span></span> <span data-ttu-id="3b1ce-126">If you provide your own results page, use `searchLink`.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-126">If you provide your own results page, use `searchLink`.</span></span>

<!-- Need a sanitized version of the image
The following shows an example of the pivot queries.

![Pivot suggestions](./media/cognitive-services-bing-images-api/bing-image-pivotsuggestion.GIF)
-->

## <a name="expand-the-query"></a><span data-ttu-id="3b1ce-127">Expand the query</span><span class="sxs-lookup"><span data-stu-id="3b1ce-127">Expand the query</span></span>

<span data-ttu-id="3b1ce-128">If Bing can expand the query to narrow the original search, the [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) object contains the `queryExpansions` field.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-128">If Bing can expand the query to narrow the original search, the [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) object contains the `queryExpansions` field.</span></span> <span data-ttu-id="3b1ce-129">For example, if the query was *Microsoft Surface*, the expanded queries might be:</span><span class="sxs-lookup"><span data-stu-id="3b1ce-129">For example, if the query was *Microsoft Surface*, the expanded queries might be:</span></span> 
- <span data-ttu-id="3b1ce-130">Microsoft Surface **Pro 3**.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-130">Microsoft Surface **Pro 3**.</span></span>
- <span data-ttu-id="3b1ce-131">Microsoft Surface **RT**.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-131">Microsoft Surface **RT**.</span></span>
- <span data-ttu-id="3b1ce-132">Microsoft Surface **Phone**.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-132">Microsoft Surface **Phone**.</span></span>
- <span data-ttu-id="3b1ce-133">Microsoft Surface **Hub**.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-133">Microsoft Surface **Hub**.</span></span>

<span data-ttu-id="3b1ce-134">The following example shows the expanded queries for *Microsoft Surface*.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-134">The following example shows the expanded queries for *Microsoft Surface*.</span></span>

```json
{
    "_type": "Images",
    "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=microsoft%20surface...",
    "totalEstimatedMatches": 1000,
    "value": [...],
    "queryExpansions":  [{
        "text": "Microsoft Surface Pro 3",
        "displayText": "Pro 3",
        "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Surface+Pro+3...",
        "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=Microsoft...",
        "thumbnail": {
            "thumbnailUrl": "https:\/\/tse4.mm.bing.net\/th?q=Microsoft+Surface+Pro+3..."
        }
    },
    {
        "text": "Microsoft Surface RT",
        "displayText": "RT",
        "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Surface+RT...",
        "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=...",
        "thumbnail": {
            "thumbnailUrl": "https:\/\/tse4.mm.bing.net\/th?q=Microsoft+Surface+RT..."
        }
    },
    {
        "text": "Microsoft Surface Phone",
        "displayText": "Phone",
        "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Surface+Phone",
        "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=...",
        "thumbnail": {
            "thumbnailUrl": "https:\/\/tse4.mm.bing.net\/th?q=Microsoft+Surface+Phone..."
        }
    }],
    "pivotSuggestions": [...],
    "nextOffsetAddCount": 0
}
```

<span data-ttu-id="3b1ce-135">The `queryExpansions` field contains a list of [Query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query_obj) objects.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-135">The `queryExpansions` field contains a list of [Query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query_obj) objects.</span></span> <span data-ttu-id="3b1ce-136">The `text` field contains the expanded query.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-136">The `text` field contains the expanded query.</span></span> <span data-ttu-id="3b1ce-137">The `displayText` field contains the expansion term.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-137">The `displayText` field contains the expansion term.</span></span> <span data-ttu-id="3b1ce-138">If the expanded query string is what the user is looking for, use the `text` and `thumbnail` fields to display the expanded query strings.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-138">If the expanded query string is what the user is looking for, use the `text` and `thumbnail` fields to display the expanded query strings.</span></span> <span data-ttu-id="3b1ce-139">Make the thumbnail and text clickable by using the `webSearchUrl` URL or the `searchLink` URL.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-139">Make the thumbnail and text clickable by using the `webSearchUrl` URL or the `searchLink` URL.</span></span> <span data-ttu-id="3b1ce-140">Use `webSearchUrl` to send the user to the Bing search results.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-140">Use `webSearchUrl` to send the user to the Bing search results.</span></span> <span data-ttu-id="3b1ce-141">if you provide your own results page, use `searchLink`.</span><span class="sxs-lookup"><span data-stu-id="3b1ce-141">if you provide your own results page, use `searchLink`.</span></span>

<!-- Removing until we can replace with a sanitized image.
The following shows an example Bing implementation that uses expanded queries. If the user clicks the Microsoft Surface Pro 3 link, they're taken to the Bing search results page, which shows them images of the Pro 3.

![Query expansion suggestions](./media/cognitive-services-bing-images-api/bing-image-queryexpansion.GIF)
-->


## <a name="throttling-requests"></a><span data-ttu-id="3b1ce-142">Throttling requests</span><span class="sxs-lookup"><span data-stu-id="3b1ce-142">Throttling requests</span></span>

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../../includes/cognitive-services-bing-throttling-requests.md)]

## <a name="next-steps"></a><span data-ttu-id="3b1ce-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b1ce-143">Next steps</span></span>

<span data-ttu-id="3b1ce-144">If you haven't tried the Bing Image Search API before, try a [quickstart](../quickstarts/csharp.md).</span><span class="sxs-lookup"><span data-stu-id="3b1ce-144">If you haven't tried the Bing Image Search API before, try a [quickstart](../quickstarts/csharp.md).</span></span> <span data-ttu-id="3b1ce-145">If you're looking for something more complex, try the tutorial to create a [single-page web app](../tutorial-bing-image-search-single-page-app.md).</span><span class="sxs-lookup"><span data-stu-id="3b1ce-145">If you're looking for something more complex, try the tutorial to create a [single-page web app](../tutorial-bing-image-search-single-page-app.md).</span></span>
