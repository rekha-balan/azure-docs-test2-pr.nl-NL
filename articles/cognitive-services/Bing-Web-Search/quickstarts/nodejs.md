---
title: 'Quickstart: Use Node.js to call the Bing Web Search API'
description: In this quickstart, you will learn how to make your first call to the Bing Web Search API using Node.js and receive a JSON response.
services: cognitive-services
author: erhopf
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 8/16/2018
ms.author: erhopf
ms.openlocfilehash: 7a46500f7cbf319c788761bccfaa92197ef67490
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868965"
---
# <a name="quickstart-use-nodejs-to-call-the-bing-web-search-api"></a><span data-ttu-id="ae5d9-103">Quickstart: Use Node.js to call the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="ae5d9-103">Quickstart: Use Node.js to call the Bing Web Search API</span></span>  

<span data-ttu-id="ae5d9-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response in less than 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response in less than 10 minutes.</span></span>  

[!INCLUDE [bing-web-search-quickstart-signup](../../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="ae5d9-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae5d9-105">Prerequisites</span></span>

<span data-ttu-id="ae5d9-106">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="ae5d9-106">Here are a few things that you'll need before running this quickstart:</span></span>

* <span data-ttu-id="ae5d9-107">[Node.js 6](https://nodejs.org/en/download/) or later</span><span class="sxs-lookup"><span data-stu-id="ae5d9-107">[Node.js 6](https://nodejs.org/en/download/) or later</span></span>
* <span data-ttu-id="ae5d9-108">A subscription key</span><span class="sxs-lookup"><span data-stu-id="ae5d9-108">A subscription key</span></span>  

## <a name="create-a-project-and-declare-required-modules"></a><span data-ttu-id="ae5d9-109">Create a project and declare required modules</span><span class="sxs-lookup"><span data-stu-id="ae5d9-109">Create a project and declare required modules</span></span>

<span data-ttu-id="ae5d9-110">Create a new Node.js project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-110">Create a new Node.js project in your favorite IDE or editor.</span></span> <span data-ttu-id="ae5d9-111">Then copy the code snippet below into your project.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-111">Then copy the code snippet below into your project.</span></span> <span data-ttu-id="ae5d9-112">This quickstart uses strict mode and requires the `https` module to send and receive data.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-112">This quickstart uses strict mode and requires the `https` module to send and receive data.</span></span>

```javascript
// Use strict mode.
'use strict';

// Require the https module.
let https = require('https');
```

## <a name="define-variables"></a><span data-ttu-id="ae5d9-113">Define variables</span><span class="sxs-lookup"><span data-stu-id="ae5d9-113">Define variables</span></span>

<span data-ttu-id="ae5d9-114">A few variables must be set before we can continue.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-114">A few variables must be set before we can continue.</span></span> <span data-ttu-id="ae5d9-115">Confirm that the `host` and `path` are valid and replace the `subscriptionKey` value with a valid subscription key from your Azure account.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-115">Confirm that the `host` and `path` are valid and replace the `subscriptionKey` value with a valid subscription key from your Azure account.</span></span> <span data-ttu-id="ae5d9-116">Feel free to customize the search query by replacing the value for `term`.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-116">Feel free to customize the search query by replacing the value for `term`.</span></span>

```javascript
// Replace with a valid subscription key.
let subscriptionKey = 'enter key here';

/*
 * Verify the endpoint URI. If you
 * encounter unexpected authorization errors, double-check this host against
 * the endpoint for your Bing Web search instance in your Azure dashboard.  
 */
let host = 'api.cognitive.microsoft.com';
let path = '/bing/v7.0/search';
let term = 'Microsoft Cognitive Services';

// Validate the subscription key.
if (subscriptionKey.length === 32) {
    bing_web_search(term);
} else {
    console.log('Invalid Bing Search API subscription key!');
    console.log('Please paste yours into the source code.');
}
```

## <a name="create-a-response-handler"></a><span data-ttu-id="ae5d9-117">Create a response handler</span><span class="sxs-lookup"><span data-stu-id="ae5d9-117">Create a response handler</span></span>

<span data-ttu-id="ae5d9-118">Create a handler to stringify and parse the response.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-118">Create a handler to stringify and parse the response.</span></span> <span data-ttu-id="ae5d9-119">The `response_handler` is called each time a request is made to the Bing Web Search API, as you'll see in the next section.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-119">The `response_handler` is called each time a request is made to the Bing Web Search API, as you'll see in the next section.</span></span>

```javascript
let response_handler = function (response) {
    let body = '';
    response.on('data', function (d) {
        body += d;
    });
    response.on('end', function () {
        console.log('\nRelevant Headers:\n');
        for (var header in response.headers)
            // Headers are lowercased by Node.js.
            if (header.startsWith("bingapis-") || header.startsWith("x-msedge-"))
                 console.log(header + ": " + response.headers[header]);
        // Stringify and parse the response body.
        body = JSON.stringify(JSON.parse(body), null, '  ');
        console.log('\nJSON Response:\n');
        console.log(body);
    });
    response.on('error', function (e) {
        console.log('Error: ' + e.message);
    });
};
```

## <a name="make-a-request-and-print-the-response"></a><span data-ttu-id="ae5d9-120">Make a request and print the response</span><span class="sxs-lookup"><span data-stu-id="ae5d9-120">Make a request and print the response</span></span>

<span data-ttu-id="ae5d9-121">Construct the request and make a call to the Bing Web Search API.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-121">Construct the request and make a call to the Bing Web Search API.</span></span> <span data-ttu-id="ae5d9-122">After the request is made, the `response_handler` function is called and the response is printed.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-122">After the request is made, the `response_handler` function is called and the response is printed.</span></span>

```javascript
let bing_web_search = function (search) {
    console.log('Searching the Web for: ' + term);
        // Declare the method, hostname, path, and headers.
        let request_params = {
            method : 'GET',
            hostname : host,
            path : path + '?q=' + encodeURIComponent(search),
            headers : {
                'Ocp-Apim-Subscription-Key' : subscriptionKey,
            }
        };
    // Request to the Bing Web Search API.
    let req = https.request(request_params, response_handler);
    req.end();
}
```

## <a name="put-it-all-together"></a><span data-ttu-id="ae5d9-123">Put it all together</span><span class="sxs-lookup"><span data-stu-id="ae5d9-123">Put it all together</span></span>

<span data-ttu-id="ae5d9-124">The last step is to run your code!</span><span class="sxs-lookup"><span data-stu-id="ae5d9-124">The last step is to run your code!</span></span> <span data-ttu-id="ae5d9-125">If you'd like to compare your code with ours, [sample code is available on GitHub](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/blob/master/nodejs/Search/BingWebSearchv7.js).</span><span class="sxs-lookup"><span data-stu-id="ae5d9-125">If you'd like to compare your code with ours, [sample code is available on GitHub](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/blob/master/nodejs/Search/BingWebSearchv7.js).</span></span>

## <a name="sample-response"></a><span data-ttu-id="ae5d9-126">Sample response</span><span class="sxs-lookup"><span data-stu-id="ae5d9-126">Sample response</span></span>

<span data-ttu-id="ae5d9-127">Responses from the Bing Web Search API are returned as JSON.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-127">Responses from the Bing Web Search API are returned as JSON.</span></span> <span data-ttu-id="ae5d9-128">This sample response has been truncated to show a single result.</span><span class="sxs-lookup"><span data-stu-id="ae5d9-128">This sample response has been truncated to show a single result.</span></span>  

```json
{
  "_type": "SearchResponse",
  "queryContext": {
    "originalQuery": "Microsoft Cognitive Services"
  },
  "webPages": {
    "webSearchUrl": "https://www.bing.com/search?q=Microsoft+cognitive+services",
    "totalEstimatedMatches": 22300000,
    "value": [
      {
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.0",
        "name": "Microsoft Cognitive Services",
        "url": "https://www.microsoft.com/cognitive-services",
        "displayUrl": "https://www.microsoft.com/cognitive-services",
        "snippet": "Knock down barriers between you and your ideas. Enable natural and contextual interaction with tools that augment users' experiences via the power of machine-based AI. Plug them in and bring your ideas to life.",
        "deepLinks": [
          {
            "name": "Face API",
            "url": "https://azure.microsoft.com/services/cognitive-services/face/",
            "snippet": "Add facial recognition to your applications to detect, identify, and verify faces using a Face API from Microsoft Azure. ... Cognitive Services; Face API;"
          },
          {
            "name": "Text Analytics",
            "url": "https://azure.microsoft.com/services/cognitive-services/text-analytics/",
            "snippet": "Cognitive Services; Text Analytics API; Text Analytics API . Detect sentiment, ... you agree that Microsoft may store it and use it to improve Microsoft services, ..."
          },
          {
            "name": "Computer Vision API",
            "url": "https://azure.microsoft.com/services/cognitive-services/computer-vision/",
            "snippet": "Extract the data you need from images using optical character recognition and image analytics with Computer Vision APIs from Microsoft Azure."
          },
          {
            "name": "Emotion",
            "url": "https://www.microsoft.com/cognitive-services/en-us/emotion-api",
            "snippet": "Cognitive Services Emotion API - microsoft.com"
          },
          {
            "name": "Bing Speech API",
            "url": "https://azure.microsoft.com/services/cognitive-services/speech/",
            "snippet": "Add speech recognition to your applications, including text to speech, with a speech API from Microsoft Azure. ... Cognitive Services; Bing Speech API;"
          },
          {
            "name": "Get Started for Free",
            "url": "https://azure.microsoft.com/services/cognitive-services/",
            "snippet": "Add vision, speech, language, and knowledge capabilities to your applications using intelligence APIs and SDKs from Cognitive Services."
          }
        ]
      }
    ]
  },
  "relatedSearches": {
    "id": "https://api.cognitive.microsoft.com/api/v7/#RelatedSearches",
    "value": [
      {
        "text": "microsoft bot framework",
        "displayText": "microsoft bot framework",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+bot+framework"
      },
      {
        "text": "microsoft cognitive services youtube",
        "displayText": "microsoft cognitive services youtube",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+youtube"
      },
      {
        "text": "microsoft cognitive services search api",
        "displayText": "microsoft cognitive services search api",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+search+api"
      },
      {
        "text": "microsoft cognitive services news",
        "displayText": "microsoft cognitive services news",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+news"
      },
      {
        "text": "ms cognitive service",
        "displayText": "ms cognitive service",
        "webSearchUrl": "https://www.bing.com/search?q=ms+cognitive+service"
      },
      {
        "text": "microsoft cognitive services text analytics",
        "displayText": "microsoft cognitive services text analytics",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+text+analytics"
      },
      {
        "text": "microsoft cognitive services toolkit",
        "displayText": "microsoft cognitive services toolkit",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+toolkit"
      },
      {
        "text": "microsoft cognitive services api",
        "displayText": "microsoft cognitive services api",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+api"
      }
    ]
  },
  "rankingResponse": {
    "mainline": {
      "items": [
        {
          "answerType": "WebPages",
          "resultIndex": 0,
          "value": {
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.0"
          }
        }
      ]
    },
    "sidebar": {
      "items": [
        {
          "answerType": "RelatedSearches",
          "value": {
            "id": "https://api.cognitive.microsoft.com/api/v7/#RelatedSearches"
          }
        }
      ]
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="ae5d9-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae5d9-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae5d9-130">Bing Web search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="ae5d9-130">Bing Web search single-page app tutorial</span></span>](../tutorial-bing-web-search-single-page-app.md)

[!INCLUDE [bing-web-search-quickstart-see-also](../../../../includes/bing-web-search-quickstart-see-also.md)]
