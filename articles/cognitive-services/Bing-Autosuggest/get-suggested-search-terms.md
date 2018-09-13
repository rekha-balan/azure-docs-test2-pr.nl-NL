---
title: What is Bing Autosuggest? | Microsoft Docs
description: Learn how to use the Bing Autosuggest API.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 6F4AFEDA-71A7-48C1-B3E2-D0D430428CDC
ms.service: cognitive-services
ms.component: bing-autosuggest
ms.topic: overview
ms.date: 09/12/2017
ms.author: scottwhi
ms.openlocfilehash: 76e509289f495e09c367af926fd26e0581b6e7c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864825"
---
# <a name="what-is-bing-autosuggest"></a><span data-ttu-id="faca1-104">What is Bing Autosuggest?</span><span class="sxs-lookup"><span data-stu-id="faca1-104">What is Bing Autosuggest?</span></span>

<span data-ttu-id="faca1-105">If you send queries to any of the Bing Search APIs, you can use the Bing Autosuggest API to improve your search box experience.</span><span class="sxs-lookup"><span data-stu-id="faca1-105">If you send queries to any of the Bing Search APIs, you can use the Bing Autosuggest API to improve your search box experience.</span></span> <span data-ttu-id="faca1-106">The Bing Autosuggest API returns a list of suggested queries based on the partial query string the user enters in the search box.</span><span class="sxs-lookup"><span data-stu-id="faca1-106">The Bing Autosuggest API returns a list of suggested queries based on the partial query string the user enters in the search box.</span></span> <span data-ttu-id="faca1-107">Display the suggestions in the search box's drop-down list.</span><span class="sxs-lookup"><span data-stu-id="faca1-107">Display the suggestions in the search box's drop-down list.</span></span> <span data-ttu-id="faca1-108">The suggested terms are based on suggested queries that other users have searched on and user intent.</span><span class="sxs-lookup"><span data-stu-id="faca1-108">The suggested terms are based on suggested queries that other users have searched on and user intent.</span></span>

<span data-ttu-id="faca1-109">Typically, you'd call this API each time the user types a new character in the search box.</span><span class="sxs-lookup"><span data-stu-id="faca1-109">Typically, you'd call this API each time the user types a new character in the search box.</span></span> <span data-ttu-id="faca1-110">The completeness of the query string impacts the relevance of the suggested query terms that the API returns.</span><span class="sxs-lookup"><span data-stu-id="faca1-110">The completeness of the query string impacts the relevance of the suggested query terms that the API returns.</span></span> <span data-ttu-id="faca1-111">The more complete the query string, the more relevant the list of suggested query terms are.</span><span class="sxs-lookup"><span data-stu-id="faca1-111">The more complete the query string, the more relevant the list of suggested query terms are.</span></span> <span data-ttu-id="faca1-112">For example, the suggestions that the API may return for *s* are likely to be less relevant than the queries it returns for *sailing dinghies*.</span><span class="sxs-lookup"><span data-stu-id="faca1-112">For example, the suggestions that the API may return for *s* are likely to be less relevant than the queries it returns for *sailing dinghies*.</span></span>

## <a name="getting-suggested-search-terms"></a><span data-ttu-id="faca1-113">Getting suggested search terms</span><span class="sxs-lookup"><span data-stu-id="faca1-113">Getting suggested search terms</span></span>

<span data-ttu-id="faca1-114">The following example shows a request that returns the suggested query strings for *sail*.</span><span class="sxs-lookup"><span data-stu-id="faca1-114">The following example shows a request that returns the suggested query strings for *sail*.</span></span> <span data-ttu-id="faca1-115">Remember to URL encode the user's partial query term when you set the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference#query) query parameter.</span><span class="sxs-lookup"><span data-stu-id="faca1-115">Remember to URL encode the user's partial query term when you set the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference#query) query parameter.</span></span> <span data-ttu-id="faca1-116">For example, if the user entered *sailing les*, set `q` to `sailing+les` or `sailing%20les`.</span><span class="sxs-lookup"><span data-stu-id="faca1-116">For example, if the user entered *sailing les*, set `q` to `sailing+les` or `sailing%20les`.</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/suggestions?q=sail&mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
X-MSEdge-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="faca1-117">The following response contains a list of [SearchAction](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference#searchaction) objects that contain the suggested query terms.</span><span class="sxs-lookup"><span data-stu-id="faca1-117">The following response contains a list of [SearchAction](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference#searchaction) objects that contain the suggested query terms.</span></span>

```json
{
    "url" : "https:\/\/www.bing.com\/search?q=sailing+lessons+seattle&FORM=USBAPI",
    "displayText" : "sailing lessons seattle",
    "query" : "sailing lessons seattle",
    "searchKind" : "WebSearch"
}, ...
```

<span data-ttu-id="faca1-118">Each suggestion includes a `displayText`, `query` and, `url` field.</span><span class="sxs-lookup"><span data-stu-id="faca1-118">Each suggestion includes a `displayText`, `query` and, `url` field.</span></span> <span data-ttu-id="faca1-119">The `displayText` field contains the suggested query that you use to populate your search box's drop-down list.</span><span class="sxs-lookup"><span data-stu-id="faca1-119">The `displayText` field contains the suggested query that you use to populate your search box's drop-down list.</span></span> <span data-ttu-id="faca1-120">You must display all suggestions that the response includes, and in the given order.</span><span class="sxs-lookup"><span data-stu-id="faca1-120">You must display all suggestions that the response includes, and in the given order.</span></span>

<span data-ttu-id="faca1-121">The following shows an example of drop-down search box with suggested query terms.</span><span class="sxs-lookup"><span data-stu-id="faca1-121">The following shows an example of drop-down search box with suggested query terms.</span></span>

![Autosuggest drop-down search box list](./media/cognitive-services-bing-autosuggest-api/bing-autosuggest-drop-down-list.PNG)

<span data-ttu-id="faca1-123">If the user selects a suggested query from the drop-down list, you'd use the query term in the `query` field to call the [Bing Web Search API](../bing-web-search/search-the-web.md) and display the results yourself.</span><span class="sxs-lookup"><span data-stu-id="faca1-123">If the user selects a suggested query from the drop-down list, you'd use the query term in the `query` field to call the [Bing Web Search API](../bing-web-search/search-the-web.md) and display the results yourself.</span></span> <span data-ttu-id="faca1-124">Or, you could use the URL in the `url` field to send the user to the Bing search results page instead.</span><span class="sxs-lookup"><span data-stu-id="faca1-124">Or, you could use the URL in the `url` field to send the user to the Bing search results page instead.</span></span>

## <a name="throttling-requests"></a><span data-ttu-id="faca1-125">Throttling requests</span><span class="sxs-lookup"><span data-stu-id="faca1-125">Throttling requests</span></span>

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../includes/cognitive-services-bing-throttling-requests.md)]

## <a name="next-steps"></a><span data-ttu-id="faca1-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="faca1-126">Next steps</span></span>

<span data-ttu-id="faca1-127">To get started quickly with your first request, see [Making Your First Query](quickstarts/csharp.md).</span><span class="sxs-lookup"><span data-stu-id="faca1-127">To get started quickly with your first request, see [Making Your First Query](quickstarts/csharp.md).</span></span>

<span data-ttu-id="faca1-128">Familiarize yourself with the [Bing Autosuggest API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="faca1-128">Familiarize yourself with the [Bing Autosuggest API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference) reference.</span></span> <span data-ttu-id="faca1-129">The reference contains the list of endpoints, headers, and query parameters that you'd use to request suggested query terms, and the definitions of the response objects.</span><span class="sxs-lookup"><span data-stu-id="faca1-129">The reference contains the list of endpoints, headers, and query parameters that you'd use to request suggested query terms, and the definitions of the response objects.</span></span>

<span data-ttu-id="faca1-130">Learn how to search the web by using the [Bing Web Search API](../bing-web-search/search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="faca1-130">Learn how to search the web by using the [Bing Web Search API](../bing-web-search/search-the-web.md).</span></span>

<span data-ttu-id="faca1-131">Be sure to read [Bing Use and Display Requirements](./useanddisplayrequirements.md) so you don't break any of the rules about using the search results.</span><span class="sxs-lookup"><span data-stu-id="faca1-131">Be sure to read [Bing Use and Display Requirements](./useanddisplayrequirements.md) so you don't break any of the rules about using the search results.</span></span>