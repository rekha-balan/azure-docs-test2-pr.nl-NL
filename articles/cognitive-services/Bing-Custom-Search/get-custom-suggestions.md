---
title: 'Bing Custom Search: Get Custom Autosuggest suggestions | Microsoft Docs'
description: Describes how to retrieve custom Autosuggest suggestions
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.technology: bing-custom-search
ms.topic: article
ms.date: 09/28/2017
ms.author: v-brapel
ms.openlocfilehash: 73059038018602f7aa76377bf7c98d4658576576
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856471"
---
# <a name="get-custom-suggestions"></a><span data-ttu-id="32cab-103">Get custom suggestions</span><span class="sxs-lookup"><span data-stu-id="32cab-103">Get custom suggestions</span></span>
<span data-ttu-id="32cab-104">Before sending queries to Bing Custom Search, call the Custom Autosuggest API to make search term suggestions and enhance the search experience.</span><span class="sxs-lookup"><span data-stu-id="32cab-104">Before sending queries to Bing Custom Search, call the Custom Autosuggest API to make search term suggestions and enhance the search experience.</span></span> <span data-ttu-id="32cab-105">The Custom Autosuggest API returns a list of suggested queries based on a partial query string that the user provides.</span><span class="sxs-lookup"><span data-stu-id="32cab-105">The Custom Autosuggest API returns a list of suggested queries based on a partial query string that the user provides.</span></span> <span data-ttu-id="32cab-106">Any relevant custom query terms that you specify appear before the suggestions that Autosuggest generates.</span><span class="sxs-lookup"><span data-stu-id="32cab-106">Any relevant custom query terms that you specify appear before the suggestions that Autosuggest generates.</span></span> <span data-ttu-id="32cab-107">For more information, see [Define custom search suggestions](define-custom-suggestions.md).</span><span class="sxs-lookup"><span data-stu-id="32cab-107">For more information, see [Define custom search suggestions](define-custom-suggestions.md).</span></span>

## <a name="endpoint"></a><span data-ttu-id="32cab-108">Endpoint</span><span class="sxs-lookup"><span data-stu-id="32cab-108">Endpoint</span></span>
<span data-ttu-id="32cab-109">To get suggested queries using the Bing Custom Search API, send a `GET` request to the following endpoint.</span><span class="sxs-lookup"><span data-stu-id="32cab-109">To get suggested queries using the Bing Custom Search API, send a `GET` request to the following endpoint.</span></span>

```
GET https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/Suggestions 
```

## <a name="response-json"></a><span data-ttu-id="32cab-110">Response JSON</span><span class="sxs-lookup"><span data-stu-id="32cab-110">Response JSON</span></span>
<span data-ttu-id="32cab-111">The response contains a list of SearchAction objects that contain the suggested query terms.</span><span class="sxs-lookup"><span data-stu-id="32cab-111">The response contains a list of SearchAction objects that contain the suggested query terms.</span></span>

```
        {  
            "displayText" : "sailing lessons seattle",  
            "query" : "sailing lessons seattle",  
            "searchKind" : "CustomSearch"  
        },  
```

<span data-ttu-id="32cab-112">Each suggestion includes a `displayText` and `query` field.</span><span class="sxs-lookup"><span data-stu-id="32cab-112">Each suggestion includes a `displayText` and `query` field.</span></span> <span data-ttu-id="32cab-113">The `displayText` field contains the suggested query that you use to populate your search box's drop-down list.</span><span class="sxs-lookup"><span data-stu-id="32cab-113">The `displayText` field contains the suggested query that you use to populate your search box's drop-down list.</span></span>

<span data-ttu-id="32cab-114">If the user selects a suggested query from the drop-down list, use the query term in the `query` field when calling the [Bing Custom Search API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="32cab-114">If the user selects a suggested query from the drop-down list, use the query term in the `query` field when calling the [Bing Custom Search API](overview.md).</span></span>

## <a name="throttling-requests"></a><span data-ttu-id="32cab-115">Throttling requests</span><span class="sxs-lookup"><span data-stu-id="32cab-115">Throttling requests</span></span>

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../includes/cognitive-services-bing-throttling-requests.md)]

## <a name="next-steps"></a><span data-ttu-id="32cab-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="32cab-116">Next steps</span></span>

- [<span data-ttu-id="32cab-117">Call your custom search</span><span class="sxs-lookup"><span data-stu-id="32cab-117">Call your custom search</span></span>](./search-your-custom-view.md)
- [<span data-ttu-id="32cab-118">Configure your hosted UI experience</span><span class="sxs-lookup"><span data-stu-id="32cab-118">Configure your hosted UI experience</span></span>](./hosted-ui.md)