---
title: Autosuggest Bing search terms
titleSuffix: Microsoft Cognitive Services
description: Pair the Bing Web Search API with the Bing Autosuggest API to provide users with an improved search experience.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 8/13/2018
ms.author: erhopf
ms.openlocfilehash: df8a57b3136abfacce971f4d01ccb2296dfa784c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865577"
---
# <a name="autosuggest-bing-search-terms"></a><span data-ttu-id="6aea1-103">Autosuggest Bing search terms</span><span class="sxs-lookup"><span data-stu-id="6aea1-103">Autosuggest Bing search terms</span></span>

<span data-ttu-id="6aea1-104">If you provide a search box where the user enters their search term, use the [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span><span class="sxs-lookup"><span data-stu-id="6aea1-104">If you provide a search box where the user enters their search term, use the [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span></span> <span data-ttu-id="6aea1-105">The API returns suggested query strings based on partial search terms as the user types.</span><span class="sxs-lookup"><span data-stu-id="6aea1-105">The API returns suggested query strings based on partial search terms as the user types.</span></span>

<span data-ttu-id="6aea1-106">After the user enters a search term, it must be URL encoded before the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#query) query parameter is set.</span><span class="sxs-lookup"><span data-stu-id="6aea1-106">After the user enters a search term, it must be URL encoded before the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#query) query parameter is set.</span></span> <span data-ttu-id="6aea1-107">For example, if the user enters *sailing dinghies*, set `q` to `sailing+dinghies` or `sailing%20dinghies`.</span><span class="sxs-lookup"><span data-stu-id="6aea1-107">For example, if the user enters *sailing dinghies*, set `q` to `sailing+dinghies` or `sailing%20dinghies`.</span></span>

<span data-ttu-id="6aea1-108">If the query term contains a spelling mistake, the search response includes a [QueryContext](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#querycontext) object.</span><span class="sxs-lookup"><span data-stu-id="6aea1-108">If the query term contains a spelling mistake, the search response includes a [QueryContext](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#querycontext) object.</span></span> <span data-ttu-id="6aea1-109">The object shows the original spelling and the corrected spelling that Bing used for the search.</span><span class="sxs-lookup"><span data-stu-id="6aea1-109">The object shows the original spelling and the corrected spelling that Bing used for the search.</span></span>

```json
"queryContext": {
    "originalQuery": "sialing dingy for sale",
    "alteredQuery": "sailing dinghy for sale",
    "alterationOverrideQuery": "+sialing +dingy for sale"
}
```

<span data-ttu-id="6aea1-110">You can use this information to let the user know that you modified their query string when you display the search results.</span><span class="sxs-lookup"><span data-stu-id="6aea1-110">You can use this information to let the user know that you modified their query string when you display the search results.</span></span>

![Query context UX example](./media/cognitive-services-bing-web-api/bing-query-context.PNG)  

## <a name="next-steps"></a><span data-ttu-id="6aea1-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="6aea1-112">Next steps</span></span>  

* <span data-ttu-id="6aea1-113">Review sample [Bing Web Search API responses](search-responses.md).</span><span class="sxs-lookup"><span data-stu-id="6aea1-113">Review sample [Bing Web Search API responses](search-responses.md).</span></span>  

## <a name="see-also"></a><span data-ttu-id="6aea1-114">See also</span><span class="sxs-lookup"><span data-stu-id="6aea1-114">See also</span></span>  

* [<span data-ttu-id="6aea1-115">Bing Web Search API reference</span><span class="sxs-lookup"><span data-stu-id="6aea1-115">Bing Web Search API reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference)
