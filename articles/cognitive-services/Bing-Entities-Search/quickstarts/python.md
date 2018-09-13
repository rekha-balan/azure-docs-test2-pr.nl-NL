---
title: Python Quickstart for Azure Cognitive Services, Bing Entity Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Entity Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 11/28/2017
ms.author: v-jaswel
ms.openlocfilehash: 88e954af0254b158ea59a88ed4523e3b141a135e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866023"
---
# <a name="quickstart-for-microsoft-bing-entity-search-api-with-python"></a><span data-ttu-id="4b444-103">Quickstart for Microsoft Bing Entity Search API with Python</span><span class="sxs-lookup"><span data-stu-id="4b444-103">Quickstart for Microsoft Bing Entity Search API with Python</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="4b444-104">This article shows you how to use the [Bing Entity Search](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web) API with Python.</span><span class="sxs-lookup"><span data-stu-id="4b444-104">This article shows you how to use the [Bing Entity Search](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web) API with Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b444-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4b444-105">Prerequisites</span></span>

<span data-ttu-id="4b444-106">You will need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="4b444-106">You will need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="4b444-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Entity Search API**.</span><span class="sxs-lookup"><span data-stu-id="4b444-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Entity Search API**.</span></span> <span data-ttu-id="4b444-108">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-entity-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="4b444-108">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-entity-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="4b444-109">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="4b444-109">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="search-entities"></a><span data-ttu-id="4b444-110">Search entities</span><span class="sxs-lookup"><span data-stu-id="4b444-110">Search entities</span></span>

<span data-ttu-id="4b444-111">To run this application, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="4b444-111">To run this application, follow these steps.</span></span>

1. <span data-ttu-id="4b444-112">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="4b444-112">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="4b444-113">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="4b444-113">Add the code provided below.</span></span>
3. <span data-ttu-id="4b444-114">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="4b444-114">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="4b444-115">Run the program.</span><span class="sxs-lookup"><span data-stu-id="4b444-115">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse
import json

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'api.cognitive.microsoft.com'
path = '/bing/v7.0/entities'

mkt = 'en-US'
query = 'italian restaurants near me'

params = '?mkt=' + mkt + '&q=' + urllib.parse.quote (query)

def get_suggestions ():
    headers = {'Ocp-Apim-Subscription-Key': subscriptionKey}
    conn = http.client.HTTPSConnection (host)
    conn.request ("GET", path + params, None, headers)
    response = conn.getresponse ()
    return response.read ()

result = get_suggestions ()
print (json.dumps(json.loads(result), indent=4))
```

<span data-ttu-id="4b444-116">**Response**</span><span class="sxs-lookup"><span data-stu-id="4b444-116">**Response**</span></span>

<span data-ttu-id="4b444-117">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="4b444-117">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "_type": "SearchResponse",
  "queryContext": {
    "originalQuery": "italian restaurant near me",
    "askUserForLocation": true
  },
  "places": {
    "value": [
      {
        "_type": "LocalBusiness",
        "webSearchUrl": "https://www.bing.com/search?q=sinful+bakery&filters=local...",
        "name": "Liberty's Delightful Sinful Bakery & Cafe",
        "url": "https://www.contoso.com/",
        "entityPresentationInfo": {
          "entityScenario": "ListItem",
          "entityTypeHints": [
            "Place",
            "LocalBusiness"
          ]
        },
        "address": {
          "addressLocality": "Seattle",
          "addressRegion": "WA",
          "postalCode": "98112",
          "addressCountry": "US",
          "neighborhood": "Madison Park"
        },
        "telephone": "(800) 555-1212"
      },

      . . .
      {
        "_type": "Restaurant",
        "webSearchUrl": "https://www.bing.com/search?q=Pickles+and+Preserves...",
        "name": "Munson's Pickles and Preserves Farm",
        "url": "http://www.princi.com/",
        "entityPresentationInfo": {
          "entityScenario": "ListItem",
          "entityTypeHints": [
            "Place",
            "LocalBusiness",
            "Restaurant"
          ]
        },
        "address": {
          "addressLocality": "Seattle",
          "addressRegion": "WA",
          "postalCode": "98101",
          "addressCountry": "US",
          "neighborhood": "Capitol Hill"
        },
        "telephone": "(800) 555-1212"
      },
      
      . . .
    ]
  }
}
```

[<span data-ttu-id="4b444-118">Back to top</span><span class="sxs-lookup"><span data-stu-id="4b444-118">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="4b444-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b444-119">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="4b444-120">[Bing Entity Search tutorial](../tutorial-bing-entities-search-single-page-app.md)
> [Bing Entity Search overview](../search-the-web.md )
> [API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)</span><span class="sxs-lookup"><span data-stu-id="4b444-120">[Bing Entity Search tutorial](../tutorial-bing-entities-search-single-page-app.md)
[Bing Entity Search overview](../search-the-web.md )
[API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)</span></span>
