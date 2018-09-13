---
title: 'Quickstart: Send search queries using the REST API for the Bing Image Search API using Node.js'
description: In this quickstart, you send search queries to the Bing Search API to get a list of relevant images using Node.js.
services: cognitive-services
documentationcenter: ''
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: 975275bea61a5903c06da394b762b1aceb18023f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966870"
---
# <a name="quickstart-send-search-queries-using-the-rest-api-and-nodejs"></a><span data-ttu-id="55b6a-103">Quickstart: Send search queries using the REST API and Node.js</span><span class="sxs-lookup"><span data-stu-id="55b6a-103">Quickstart: Send search queries using the REST API and Node.js</span></span>

<span data-ttu-id="55b6a-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span><span class="sxs-lookup"><span data-stu-id="55b6a-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span></span>

<span data-ttu-id="55b6a-105">This article includes a simple console application that performs a Bing Image Search API query and displays the returned raw search results, which are in JSON format.</span><span class="sxs-lookup"><span data-stu-id="55b6a-105">This article includes a simple console application that performs a Bing Image Search API query and displays the returned raw search results, which are in JSON format.</span></span> <span data-ttu-id="55b6a-106">While this application is written in JavaScript and runs under Node.js, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="55b6a-106">While this application is written in JavaScript and runs under Node.js, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="55b6a-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="55b6a-107">Prerequisites</span></span>

<span data-ttu-id="55b6a-108">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="55b6a-108">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

[!INCLUDE [cognitive-services-bing-image-search-signup-requirements](../../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

## <a name="running-the-application"></a><span data-ttu-id="55b6a-109">Running the application</span><span class="sxs-lookup"><span data-stu-id="55b6a-109">Running the application</span></span>

<span data-ttu-id="55b6a-110">To run this application, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="55b6a-110">To run this application, follow these steps.</span></span>

1. <span data-ttu-id="55b6a-111">Create a new Node.js project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="55b6a-111">Create a new Node.js project in your favorite IDE or editor.</span></span>
2. <span data-ttu-id="55b6a-112">Add the provided code.</span><span class="sxs-lookup"><span data-stu-id="55b6a-112">Add the provided code.</span></span>
3. <span data-ttu-id="55b6a-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="55b6a-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="55b6a-114">Run the program.</span><span class="sxs-lookup"><span data-stu-id="55b6a-114">Run the program.</span></span>

```javascript
'use strict';

let https = require('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'enter key here';

// Verify the endpoint URI.  At this writing, only one endpoint is used for Bing
// search APIs.  In the future, regional endpoints may be available.  If you
// encounter unexpected authorization errors, double-check this host against
// the endpoint for your Bing Search instance in your Azure dashboard.
let host = 'api.cognitive.microsoft.com';
let path = '/bing/v7.0/images/search';

let term = 'puppies';

let response_handler = function (response) {
    let body = '';
    response.on('data', function (d) {
        body += d;
    });
    response.on('end', function () {
        console.log('\nRelevant Headers:\n');
        for (var header in response.headers)
            // header keys are lower-cased by Node.js
            if (header.startsWith("bingapis-") || header.startsWith("x-msedge-"))
                 console.log(header + ": " + response.headers[header]);
        body = JSON.stringify(JSON.parse(body), null, '  ');
        console.log('\nJSON Response:\n');
        console.log(body);
    });
    response.on('error', function (e) {
        console.log('Error: ' + e.message);
    });
};

let bing_image_search = function (search) {
  console.log('Searching images for: ' + term);
  let request_params = {
        method : 'GET',
        hostname : host,
        path : path + '?q=' + encodeURIComponent(search),
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

    let req = https.request(request_params, response_handler);
    req.end();
}

if (subscriptionKey.length === 32) {
    bing_image_search(term);
} else {
    console.log('Invalid Bing Search API subscription key!');
    console.log('Please paste yours into the source code.');
}
```

## <a name="json-response"></a><span data-ttu-id="55b6a-115">JSON response</span><span class="sxs-lookup"><span data-stu-id="55b6a-115">JSON response</span></span>

<span data-ttu-id="55b6a-116">A sample response follows.</span><span class="sxs-lookup"><span data-stu-id="55b6a-116">A sample response follows.</span></span> <span data-ttu-id="55b6a-117">To limit the length of the JSON, only a single result is shown, and other parts of the response have been truncated.</span><span class="sxs-lookup"><span data-stu-id="55b6a-117">To limit the length of the JSON, only a single result is shown, and other parts of the response have been truncated.</span></span> 

```json
{
  "_type": "Images",
  "instrumentation": {},
  "readLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=puppies",
  "webSearchUrl": "https://www.bing.com/images/search?q=puppies&FORM=OIIARP",
  "totalEstimatedMatches": 955,
  "nextOffset": 1,
  "value": [
    {
      "webSearchUrl": "https://www.bing.com/images/search?view=detailv...",
      "name": "So cute - Puppies Wallpaper",
      "thumbnailUrl": "https://tse3.mm.bing.net/th?id=OIP.jHrihoDNkXGS1t...",
      "datePublished": "2014-02-01T21:55:00.0000000Z",
      "contentUrl": "http://images4.contoso.com/image/photos/14700000/So-cute-puppies...",
      "hostPageUrl": "http://www.contoso.com/clubs/puppies/images/14749028/...",
      "contentSize": "394455 B",
      "encodingFormat": "jpeg",
      "hostPageDisplayUrl": "www.contoso.com/clubs/puppies/images/14749...",
      "width": 1600,
      "height": 1200,
      "thumbnail": {
        "width": 300,
        "height": 225
      },
      "imageInsightsToken": "ccid_jHrihoDN*mid_F68CC526226E163FD1EA659747AD...",
      "insightsMetadata": {
        "recipeSourcesCount": 0
      },
      "imageId": "F68CC526226E163FD1EA659747ADCB8F9FA36",
      "accentColor": "8D613E"
    }
  ],
  "queryExpansions": [
    {
      "text": "Shih Tzu Puppies",
      "displayText": "Shih Tzu",
      "webSearchUrl": "https://www.bing.com/images/search?q=Shih+Tzu+Puppies...",
      "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=Shih...",
      "thumbnail": {
        "thumbnailUrl": "https://tse2.mm.bing.net/th?q=Shih+Tzu+Puppies&pid=Api..."
      }
    }
  ],
  "pivotSuggestions": [
    {
      "pivot": "puppies",
      "suggestions": [
        {
          "text": "Dog",
          "displayText": "Dog",
          "webSearchUrl": "https://www.bing.com/images/search?q=Dog&tq=%7b%22pq%...",
          "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=Dog...",
          "thumbnail": {
            "thumbnailUrl": "https://tse1.mm.bing.net/th?q=Dog&pid=Api&mkt=en-US..."
          }
        }
      ]
    }
  ],
  "similarTerms": [
    {
      "text": "cute",
      "displayText": "cute",
      "webSearchUrl": "https://www.bing.com/images/search?q=cute&FORM=...",
      "thumbnail": {
        "url": "https://tse2.mm.bing.net/th?q=cute&pid=Api&mkt=en-US..."
      }
    }
  ],
  "relatedSearches": [
    {
      "text": "Cute Puppies",
      "displayText": "Cute Puppies",
      "webSearchUrl": "https://www.bing.com/images/search?q=Cute+Puppies",
      "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/sear...",
      "thumbnail": {
        "thumbnailUrl": "https://tse4.mm.bing.net/th?q=Cute+Puppies&pid=..."
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="55b6a-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="55b6a-118">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55b6a-119">Bing Image Search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="55b6a-119">Bing Image Search single-page app tutorial</span></span>](../tutorial-bing-image-search-single-page-app.md)

## <a name="see-also"></a><span data-ttu-id="55b6a-120">See also</span><span class="sxs-lookup"><span data-stu-id="55b6a-120">See also</span></span> 

[<span data-ttu-id="55b6a-121">Bing Image Search overview</span><span class="sxs-lookup"><span data-stu-id="55b6a-121">Bing Image Search overview</span></span>](../overview.md)  
[<span data-ttu-id="55b6a-122">Try it</span><span class="sxs-lookup"><span data-stu-id="55b6a-122">Try it</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/)  
[<span data-ttu-id="55b6a-123">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="55b6a-123">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api)  
[<span data-ttu-id="55b6a-124">Bing Image Search API reference</span><span class="sxs-lookup"><span data-stu-id="55b6a-124">Bing Image Search API reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)
