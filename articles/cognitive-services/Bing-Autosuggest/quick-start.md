---
title: Autosuggest API quickstart | Microsoft Docs
description: Shows how to get started using the Bing Autosuggest API.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 1482E781-7352-4A3F-B1D5-B896381348C4
ms.service: cognitive-services
ms.component: bing-autosuggest
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: a7b54a1fb0b7c76eb72097357a6b51aa02e6e2fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968750"
---
# <a name="making-your-first-autosuggest-query"></a><span data-ttu-id="ab068-103">Making your first Autosuggest query</span><span class="sxs-lookup"><span data-stu-id="ab068-103">Making your first Autosuggest query</span></span>

<span data-ttu-id="ab068-104">Before you can make your first call, you need to get a Cognitive Services subscription key.</span><span class="sxs-lookup"><span data-stu-id="ab068-104">Before you can make your first call, you need to get a Cognitive Services subscription key.</span></span> <span data-ttu-id="ab068-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=autosuggest-api).</span><span class="sxs-lookup"><span data-stu-id="ab068-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=autosuggest-api).</span></span>

<span data-ttu-id="ab068-106">To get Web search results, you'd send a GET request to the following endpoint:</span><span class="sxs-lookup"><span data-stu-id="ab068-106">To get Web search results, you'd send a GET request to the following endpoint:</span></span>

```http
https://api.cognitive.microsoft.com/bing/v5.0/Suggestions
```

> [!NOTE]
> <span data-ttu-id="ab068-107">V7 Preview endpoint:</span><span class="sxs-lookup"><span data-stu-id="ab068-107">V7 Preview endpoint:</span></span>
>
> ```http
> https://api.cognitive.microsoft.com/bing/v7.0/Suggestions
> ```

<span data-ttu-id="ab068-108">The request must use the HTTPS protocol.</span><span class="sxs-lookup"><span data-stu-id="ab068-108">The request must use the HTTPS protocol.</span></span>

<span data-ttu-id="ab068-109">We recommend that all requests originate from a server.</span><span class="sxs-lookup"><span data-stu-id="ab068-109">We recommend that all requests originate from a server.</span></span> <span data-ttu-id="ab068-110">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span><span class="sxs-lookup"><span data-stu-id="ab068-110">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span></span> <span data-ttu-id="ab068-111">Also, making calls from a server provides a single upgrade point for future versions of the API.</span><span class="sxs-lookup"><span data-stu-id="ab068-111">Also, making calls from a server provides a single upgrade point for future versions of the API.</span></span>

<span data-ttu-id="ab068-112">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#query) query parameter, which contains the user's partial search term.</span><span class="sxs-lookup"><span data-stu-id="ab068-112">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#query) query parameter, which contains the user's partial search term.</span></span> <span data-ttu-id="ab068-113">Although it's optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span><span class="sxs-lookup"><span data-stu-id="ab068-113">Although it's optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span></span> <span data-ttu-id="ab068-114">For a list of optional query parameters, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#query-parameters).</span><span class="sxs-lookup"><span data-stu-id="ab068-114">For a list of optional query parameters, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#query-parameters).</span></span> <span data-ttu-id="ab068-115">All query parameter values must be URL encoded.</span><span class="sxs-lookup"><span data-stu-id="ab068-115">All query parameter values must be URL encoded.</span></span>

<span data-ttu-id="ab068-116">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#subscriptionkey) header.</span><span class="sxs-lookup"><span data-stu-id="ab068-116">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#subscriptionkey) header.</span></span> <span data-ttu-id="ab068-117">Although optional, you are encouraged to also specify the following headers:</span><span class="sxs-lookup"><span data-stu-id="ab068-117">Although optional, you are encouraged to also specify the following headers:</span></span>

- [<span data-ttu-id="ab068-118">User-Agent</span><span class="sxs-lookup"><span data-stu-id="ab068-118">User-Agent</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#useragent)
- [<span data-ttu-id="ab068-119">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="ab068-119">X-MSEdge-ClientID</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#clientid)
- [<span data-ttu-id="ab068-120">X-Search-ClientIP</span><span class="sxs-lookup"><span data-stu-id="ab068-120">X-Search-ClientIP</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#clientip)
- [<span data-ttu-id="ab068-121">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="ab068-121">X-Search-Location</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#location)

<span data-ttu-id="ab068-122">The client IP and location headers are important for returning location aware content.</span><span class="sxs-lookup"><span data-stu-id="ab068-122">The client IP and location headers are important for returning location aware content.</span></span>

<span data-ttu-id="ab068-123">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#headers).</span><span class="sxs-lookup"><span data-stu-id="ab068-123">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v5-reference#headers).</span></span>

## <a name="the-request"></a><span data-ttu-id="ab068-124">The request</span><span class="sxs-lookup"><span data-stu-id="ab068-124">The request</span></span>

<span data-ttu-id="ab068-125">The request should include all the suggested query parameters and headers.</span><span class="sxs-lookup"><span data-stu-id="ab068-125">The request should include all the suggested query parameters and headers.</span></span> <span data-ttu-id="ab068-126">You'd call this API each time the user types a new character in the search box.</span><span class="sxs-lookup"><span data-stu-id="ab068-126">You'd call this API each time the user types a new character in the search box.</span></span> <span data-ttu-id="ab068-127">The completeness of the query string impacts the relevance of the suggested query terms that the API returns.</span><span class="sxs-lookup"><span data-stu-id="ab068-127">The completeness of the query string impacts the relevance of the suggested query terms that the API returns.</span></span> <span data-ttu-id="ab068-128">The more complete the query string, the more relevant that the list of suggested query terms are.</span><span class="sxs-lookup"><span data-stu-id="ab068-128">The more complete the query string, the more relevant that the list of suggested query terms are.</span></span> <span data-ttu-id="ab068-129">For example, the suggestions that the API may return for *s* are likely to be less relevant than the queries it returns for *sailing dinghies*.</span><span class="sxs-lookup"><span data-stu-id="ab068-129">For example, the suggestions that the API may return for *s* are likely to be less relevant than the queries it returns for *sailing dinghies*.</span></span> 

<span data-ttu-id="ab068-130">The following example shows a request that returns the suggested query strings for *sail*.</span><span class="sxs-lookup"><span data-stu-id="ab068-130">The following example shows a request that returns the suggested query strings for *sail*.</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v5.0/suggestions?q=sail&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```

> [!NOTE]
> <span data-ttu-id="ab068-131">V7 Preview request:</span><span class="sxs-lookup"><span data-stu-id="ab068-131">V7 Preview request:</span></span>

> ```http
> GET https://api.cognitive.microsoft.com/bing/v7.0/suggestions?q=sail&mkt=en-us HTTP/1.1
> Ocp-Apim-Subscription-Key: 123456789ABCDE
> X-MSEdge-ClientIP: 999.999.999.999
> X-Search-Location: lat:47.60357;long:-122.3295;re:100
> X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
> Host: api.cognitive.microsoft.com
> ```

<span data-ttu-id="ab068-132">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="ab068-132">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span></span> <span data-ttu-id="ab068-133">Only include the client ID header if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="ab068-133">Only include the client ID header if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span></span>

<span data-ttu-id="ab068-134">The following shows the response to the preceding request.</span><span class="sxs-lookup"><span data-stu-id="ab068-134">The following shows the response to the preceding request.</span></span> <span data-ttu-id="ab068-135">The response includes a web suggestion group that contains a list of search query suggestions.</span><span class="sxs-lookup"><span data-stu-id="ab068-135">The response includes a web suggestion group that contains a list of search query suggestions.</span></span> <span data-ttu-id="ab068-136">Each suggestion includes a `displayText`, `query`, and `url` field.</span><span class="sxs-lookup"><span data-stu-id="ab068-136">Each suggestion includes a `displayText`, `query`, and `url` field.</span></span>

<span data-ttu-id="ab068-137">The `displayText` field contains the suggested query that you'd use to populate your search box's drop-down list.</span><span class="sxs-lookup"><span data-stu-id="ab068-137">The `displayText` field contains the suggested query that you'd use to populate your search box's drop-down list.</span></span> <span data-ttu-id="ab068-138">You must display all suggestions that the response includes, and in the given order.</span><span class="sxs-lookup"><span data-stu-id="ab068-138">You must display all suggestions that the response includes, and in the given order.</span></span>  

<span data-ttu-id="ab068-139">If the user selects a query from the drop-down list, you may use the query string in the `query` field to call the [Bing Search API](../bing-web-search/search-the-web.md) and display the results yourself.</span><span class="sxs-lookup"><span data-stu-id="ab068-139">If the user selects a query from the drop-down list, you may use the query string in the `query` field to call the [Bing Search API](../bing-web-search/search-the-web.md) and display the results yourself.</span></span> <span data-ttu-id="ab068-140">Or, you could use the URL in the `url` field to send the user to the Bing search results page.</span><span class="sxs-lookup"><span data-stu-id="ab068-140">Or, you could use the URL in the `url` field to send the user to the Bing search results page.</span></span>

```  
BingAPIs-TraceId: 76DD2C2549B94F9FB55B4BD6FEB6AC
X-MSEdge-ClientID: 1C3352B306E669780D58D607B96869
BingAPIs-Market: en-US

{
    "_type" : "Suggestions",
    "queryContext" : {
        "originalQuery" : "sail"
    },
    "suggestionGroups" : [{
        "name" : "Web",
        "searchSuggestions" : [{
            "url" : "https:\/\/www.bing.com\/search?q=sailing+lessons+seattle&FORM=USBAPI",
            "displayText" : "sailing lessons seattle",
            "query" : "sailing lessons seattle",
            "searchKind" : "WebSearch"
        },
        {
            "url" : "https:\/\/www.bing.com\/search?q=sailor+moon+news&FORM=USBAPI",
            "displayText" : "sailor moon news",
            "query" : "sailor moon news",
            "searchKind" : "WebSearch"
        },
        {
            "url" : "https:\/\/www.bing.com\/search?q=sailor+jack%27s+lincoln+city&FORM=USBAPI",
            "displayText" : "sailor jack's lincoln city",
            "query" : "sailor jack's lincoln city",
            "searchKind" : "WebSearch"
        },
        {
            "url" : "https:\/\/www.bing.com\/search?q=sailing+anarchy&FORM=USBAPI",
            "displayText" : "sailing anarchy",
            "query" : "sailing anarchy",
            "searchKind" : "WebSearch"
        },
        {
            "url" : "https:\/\/www.bing.com\/search?q=sailboats+for+sale&FORM=USBAPI",
            "displayText" : "sailboats for sale",
            "query" : "sailboats for sale",
            "searchKind" : "WebSearch"
        },
        {
            "url" : "https:\/\/www.bing.com\/search?q=sailstn.mylabsplus.com&FORM=USBAPI",
            "displayText" : "sailstn.mylabsplus.com",
            "query" : "sailstn.mylabsplus.com",
            "searchKind" : "WebSearch"
        },
        {
            "url" : "https:\/\/www.bing.com\/search?q=sailusfood&FORM=USBAPI",
            "displayText" : "sailusfood",
            "query" : "sailusfood",
            "searchKind" : "WebSearch"
        },
        {
            "url" : "https:\/\/www.bing.com\/search?q=sailboats+for+sale+seattle&FORM=USBAPI",
            "displayText" : "sailboats for sale seattle",
            "query" : "sailboats for sale seattle",
            "searchKind" : "WebSearch"
        }]
    }]
}
```

## <a name="next-steps"></a><span data-ttu-id="ab068-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab068-141">Next steps</span></span>

<span data-ttu-id="ab068-142">Try out the API.</span><span class="sxs-lookup"><span data-stu-id="ab068-142">Try out the API.</span></span> <span data-ttu-id="ab068-143">Go to [Autosuggest API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56c7694ecf5ff801a090fbd1/operations/56c769a2cf5ff801a090fbd2).</span><span class="sxs-lookup"><span data-stu-id="ab068-143">Go to [Autosuggest API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56c7694ecf5ff801a090fbd1/operations/56c769a2cf5ff801a090fbd2).</span></span>

<span data-ttu-id="ab068-144">For details about consuming the response objects, see [Getting Suggested Search Terms](./get-suggested-search-terms.md).</span><span class="sxs-lookup"><span data-stu-id="ab068-144">For details about consuming the response objects, see [Getting Suggested Search Terms](./get-suggested-search-terms.md).</span></span>
