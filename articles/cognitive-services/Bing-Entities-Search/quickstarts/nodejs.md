---
title: Node.JS Quickstart for Azure Cognitive Services, Bing Entity Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Entity Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 11/28/2017
ms.author: v-jaswel
ms.openlocfilehash: 7396976453c240d5ea9a767f8c26ac96d10d1e1f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864560"
---
# <a name="quickstart-for-microsoft-bing-entity-search-api-with-nodejs"></a><span data-ttu-id="6800c-103">Quickstart for Microsoft Bing Entity Search API with Node.JS</span><span class="sxs-lookup"><span data-stu-id="6800c-103">Quickstart for Microsoft Bing Entity Search API with Node.JS</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="6800c-104">This article shows you how to use the [Bing Entity Search](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web) API with Node.JS.</span><span class="sxs-lookup"><span data-stu-id="6800c-104">This article shows you how to use the [Bing Entity Search](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web) API with Node.JS.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6800c-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6800c-105">Prerequisites</span></span>

<span data-ttu-id="6800c-106">You will need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="6800c-106">You will need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

<span data-ttu-id="6800c-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Entity Search API**.</span><span class="sxs-lookup"><span data-stu-id="6800c-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Entity Search API**.</span></span> <span data-ttu-id="6800c-108">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-entity-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="6800c-108">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-entity-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="6800c-109">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="6800c-109">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="search-entities"></a><span data-ttu-id="6800c-110">Search entities</span><span class="sxs-lookup"><span data-stu-id="6800c-110">Search entities</span></span>

<span data-ttu-id="6800c-111">To run this application, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="6800c-111">To run this application, follow these steps.</span></span>

1. <span data-ttu-id="6800c-112">Create a new Node.JS project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="6800c-112">Create a new Node.JS project in your favorite IDE.</span></span>
2. <span data-ttu-id="6800c-113">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="6800c-113">Add the code provided below.</span></span>
3. <span data-ttu-id="6800c-114">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="6800c-114">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="6800c-115">Run the program.</span><span class="sxs-lookup"><span data-stu-id="6800c-115">Run the program.</span></span>

```nodejs
'use strict';

let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'api.cognitive.microsoft.com';
let path = '/bing/v7.0/entities';

let mkt = 'en-US';
let q = 'italian restaurant near me';

let params = '?mkt=' + mkt + '&q=' + encodeURI(q);

let response_handler = function (response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
        let body_ = JSON.parse (body);
        let body__ = JSON.stringify (body_, null, '  ');
        console.log (body__);
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

let Search = function () {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path + params,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

    let req = https.request (request_params, response_handler);
    req.end ();
}

Search ();
```

<span data-ttu-id="6800c-116">**Response**</span><span class="sxs-lookup"><span data-stu-id="6800c-116">**Response**</span></span>

<span data-ttu-id="6800c-117">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="6800c-117">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

[<span data-ttu-id="6800c-118">Back to top</span><span class="sxs-lookup"><span data-stu-id="6800c-118">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="6800c-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="6800c-119">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="6800c-120">[Bing Entity Search tutorial](../tutorial-bing-entities-search-single-page-app.md)
> [Bing Entity Search overview](../search-the-web.md )
> [API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)</span><span class="sxs-lookup"><span data-stu-id="6800c-120">[Bing Entity Search tutorial](../tutorial-bing-entities-search-single-page-app.md)
[Bing Entity Search overview](../search-the-web.md )
[API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)</span></span>
