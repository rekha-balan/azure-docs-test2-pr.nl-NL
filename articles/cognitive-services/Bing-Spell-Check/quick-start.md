---
title: Bing Spell Check API quick start | Microsoft Docs
description: Shows how to get started using the Bing Spell Check API.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: AF8EB1F0-386D-4555-9354-735611435F04
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: article
ms.date: 06/21/2016
ms.author: scottwhi
ms.openlocfilehash: cae8353e5be6e70eca90e5995b29b6774fc7d6a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864385"
---
# <a name="your-first-spell-check-request"></a><span data-ttu-id="53f05-103">Your first spell check request</span><span class="sxs-lookup"><span data-stu-id="53f05-103">Your first spell check request</span></span>

<span data-ttu-id="53f05-104">Before you can make your first call, you need to get a Cognitive Services subscription key.</span><span class="sxs-lookup"><span data-stu-id="53f05-104">Before you can make your first call, you need to get a Cognitive Services subscription key.</span></span> <span data-ttu-id="53f05-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=spellcheck-api).</span><span class="sxs-lookup"><span data-stu-id="53f05-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=spellcheck-api).</span></span>

<span data-ttu-id="53f05-106">To check a text string for spelling and grammar errors, you'd send a GET request to the following endpoint:</span><span class="sxs-lookup"><span data-stu-id="53f05-106">To check a text string for spelling and grammar errors, you'd send a GET request to the following endpoint:</span></span>  
  
```
https://api.cognitive.microsoft.com/bing/v5.0/spellcheck
```

> [!NOTE]
> <span data-ttu-id="53f05-107">V7 Preview endpoint:</span><span class="sxs-lookup"><span data-stu-id="53f05-107">V7 Preview endpoint:</span></span>
> 
> ```
> https://api.cognitive.microsoft.com/bing/v7.0/spellcheck
> ```  
  
<span data-ttu-id="53f05-108">The request must use the HTTPS protocol.</span><span class="sxs-lookup"><span data-stu-id="53f05-108">The request must use the HTTPS protocol.</span></span>

<span data-ttu-id="53f05-109">We recommend that all requests originate from a server.</span><span class="sxs-lookup"><span data-stu-id="53f05-109">We recommend that all requests originate from a server.</span></span> <span data-ttu-id="53f05-110">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span><span class="sxs-lookup"><span data-stu-id="53f05-110">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span></span> <span data-ttu-id="53f05-111">Also, making calls from a server provides a single upgrade point for future versions of the API.</span><span class="sxs-lookup"><span data-stu-id="53f05-111">Also, making calls from a server provides a single upgrade point for future versions of the API.</span></span>

<span data-ttu-id="53f05-112">The request must specify the [text](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#text) query parameter, which contains the text string to proof.</span><span class="sxs-lookup"><span data-stu-id="53f05-112">The request must specify the [text](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#text) query parameter, which contains the text string to proof.</span></span> <span data-ttu-id="53f05-113">Although optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span><span class="sxs-lookup"><span data-stu-id="53f05-113">Although optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span></span> <span data-ttu-id="53f05-114">For a list of optional query parameters such as `mode`, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#query-parameters).</span><span class="sxs-lookup"><span data-stu-id="53f05-114">For a list of optional query parameters such as `mode`, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#query-parameters).</span></span> <span data-ttu-id="53f05-115">All query parameter values must be URL encoded.</span><span class="sxs-lookup"><span data-stu-id="53f05-115">All query parameter values must be URL encoded.</span></span>  
  
<span data-ttu-id="53f05-116">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#subscriptionkey) header.</span><span class="sxs-lookup"><span data-stu-id="53f05-116">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#subscriptionkey) header.</span></span> <span data-ttu-id="53f05-117">Although optional, you are encouraged to also specify the following headers:</span><span class="sxs-lookup"><span data-stu-id="53f05-117">Although optional, you are encouraged to also specify the following headers:</span></span>  
  
-   [<span data-ttu-id="53f05-118">User-Agent</span><span class="sxs-lookup"><span data-stu-id="53f05-118">User-Agent</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#useragent)  
-   [<span data-ttu-id="53f05-119">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="53f05-119">X-MSEdge-ClientID</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#clientid)  
-   [<span data-ttu-id="53f05-120">X-Search-ClientIP</span><span class="sxs-lookup"><span data-stu-id="53f05-120">X-Search-ClientIP</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#clientip)  
-   [<span data-ttu-id="53f05-121">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="53f05-121">X-Search-Location</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#location)  

<span data-ttu-id="53f05-122">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#headers).</span><span class="sxs-lookup"><span data-stu-id="53f05-122">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v5-reference#headers).</span></span>

## <a name="the-request"></a><span data-ttu-id="53f05-123">The request</span><span class="sxs-lookup"><span data-stu-id="53f05-123">The request</span></span>

<span data-ttu-id="53f05-124">The following shows a request that includes all the suggested query parameters and headers.</span><span class="sxs-lookup"><span data-stu-id="53f05-124">The following shows a request that includes all the suggested query parameters and headers.</span></span> <span data-ttu-id="53f05-125">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="53f05-125">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span></span> <span data-ttu-id="53f05-126">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="53f05-126">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span></span> 
  
```  
GET https://api.cognitive.microsoft.com/bing/v5.0/spellcheck?text=when+its+your+turn+turn,+john,+come+runing&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-Search-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```  

> [!NOTE]
> <span data-ttu-id="53f05-127">V7 Preview request:</span><span class="sxs-lookup"><span data-stu-id="53f05-127">V7 Preview request:</span></span>

> ```  
> GET https://api.cognitive.microsoft.com/bing/v7.0/spellcheck?text=when+its+your+turn+turn,+john,+come+runing&mkt=en-us HTTP/1.1
> Ocp-Apim-Subscription-Key: 123456789ABCDE  
> X-MSEdge-ClientIP: 999.999.999.999  
> X-Search-Location: lat:47.60357;long:-122.3295;re:100  
> X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
> Host: api.cognitive.microsoft.com  
> ```  

<span data-ttu-id="53f05-128">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="53f05-128">The following shows the response to the previous request.</span></span> <span data-ttu-id="53f05-129">The example also shows the Bing-specific response headers.</span><span class="sxs-lookup"><span data-stu-id="53f05-129">The example also shows the Bing-specific response headers.</span></span>

```
BingAPIs-TraceId: 76DD2C2549B94F9FB55B4BD6FEB6AC
X-MSEdge-ClientID: 1C3352B306E669780D58D607B96869
BingAPIs-Market: en-US

{  
    "_type" : "SpellCheck",  
    "flaggedTokens" : [{  
        "offset" : 5,  
        "token" : "its",  
        "type" : "UnknownToken",  
        "suggestions" : [{  
            "suggestion" : "it's",  
            "score" : 1  
        }]  
    },  
    {  
        "offset" : 25,  
        "token" : "john",  
        "type" : "UnknownToken",  
        "suggestions" : [{  
            "suggestion" : "John",  
            "score" : 1  
        }]  
    },  
    {  
        "offset" : 19,  
        "token" : "turn",  
        "type" : "RepeatedToken",  
        "suggestions" : [{  
            "suggestion" : "",  
            "score" : 1  
        }]  
    },  
    {  
        "offset" : 35,  
        "token" : "runing",  
        "type" : "UnknownToken",  
        "suggestions" : [{  
            "suggestion" : "running",  
            "score" : 1  
        }]  
    }]  
}  
```  


## <a name="next-steps"></a><span data-ttu-id="53f05-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="53f05-130">Next steps</span></span>

<span data-ttu-id="53f05-131">Try out the API.</span><span class="sxs-lookup"><span data-stu-id="53f05-131">Try out the API.</span></span> <span data-ttu-id="53f05-132">Go to [Spell Check API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56e73033cf5ff80c2008c679/operations/57855119bca1df1c647bc358).</span><span class="sxs-lookup"><span data-stu-id="53f05-132">Go to [Spell Check API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56e73033cf5ff80c2008c679/operations/57855119bca1df1c647bc358).</span></span> 

<span data-ttu-id="53f05-133">For details about consuming the response objects, see [Spell check text strings](./proof-text.md).</span><span class="sxs-lookup"><span data-stu-id="53f05-133">For details about consuming the response objects, see [Spell check text strings](./proof-text.md).</span></span>

