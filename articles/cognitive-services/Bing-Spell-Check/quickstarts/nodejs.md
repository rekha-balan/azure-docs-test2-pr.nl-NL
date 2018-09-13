---
title: Node.js Quickstart for Bing Spell Check API - Azure Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Spell Check API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: quickstart
ms.date: 09/14/2017
ms.author: v-jaswel
ms.openlocfilehash: 112e75ef15b52d7f010f5f3c18351852cb560e05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870270"
---
# <a name="quickstart-for-bing-spell-check-api-with-nodejs"></a><span data-ttu-id="a7943-103">Quickstart for Bing Spell Check API with Node.js</span><span class="sxs-lookup"><span data-stu-id="a7943-103">Quickstart for Bing Spell Check API with Node.js</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="a7943-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with Node.js.</span><span class="sxs-lookup"><span data-stu-id="a7943-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with Node.js.</span></span> <span data-ttu-id="a7943-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span><span class="sxs-lookup"><span data-stu-id="a7943-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span></span> <span data-ttu-id="a7943-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span><span class="sxs-lookup"><span data-stu-id="a7943-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span></span> <span data-ttu-id="a7943-107">This article shows how to send a request that contains the text "Hollo, wrld!".</span><span class="sxs-lookup"><span data-stu-id="a7943-107">This article shows how to send a request that contains the text "Hollo, wrld!".</span></span> <span data-ttu-id="a7943-108">The suggested replacements will be "Hello" and "world."</span><span class="sxs-lookup"><span data-stu-id="a7943-108">The suggested replacements will be "Hello" and "world."</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7943-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7943-109">Prerequisites</span></span>

<span data-ttu-id="a7943-110">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="a7943-110">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

<span data-ttu-id="a7943-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span><span class="sxs-lookup"><span data-stu-id="a7943-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span></span> <span data-ttu-id="a7943-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a7943-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span></span> <span data-ttu-id="a7943-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7943-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="get-spell-check-results"></a><span data-ttu-id="a7943-114">Get Spell Check results</span><span class="sxs-lookup"><span data-stu-id="a7943-114">Get Spell Check results</span></span>

1. <span data-ttu-id="a7943-115">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a7943-115">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a7943-116">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a7943-116">Add the code provided below.</span></span>
3. <span data-ttu-id="a7943-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a7943-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a7943-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a7943-118">Run the program.</span></span>

```nodejs
'use strict';

let https = require ('https');

let host = 'api.cognitive.microsoft.com';
let path = '/bing/v7.0/spellcheck';

/* NOTE: Replace this example key with a valid subscription key (see the Prequisites section above). Also note v5 and v7 require separate subscription keys. */
let key = 'ENTER KEY HERE';

// These values are used for optional headers (see below).
// let CLIENT_ID = "<Client ID from Previous Response Goes Here>";
// let CLIENT_IP = "999.999.999.999";
// let CLIENT_LOCATION = "+90.0000000000000;long: 00.0000000000000;re:100.000000000000";

let mkt = "en-US";
let mode = "proof";
let text = "Hollo, wrld!";
let query_string = "?mkt=" + mkt + "&mode=" + mode;

let request_params = {
    method : 'POST',
    hostname : host,
    path : path + query_string,
    headers : {
        'Content-Type' : 'application/x-www-form-urlencoded',
        'Content-Length' : text.length + 5,
        'Ocp-Apim-Subscription-Key' : key,
//        'X-Search-Location' : CLIENT_LOCATION,
//        'X-MSEdge-ClientID' : CLIENT_ID,
//        'X-MSEdge-ClientIP' : CLIENT_ID,
    }
};

let response_handler = function (response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
        console.log (body);
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

let req = https.request (request_params, response_handler);
req.write ("text=" + text);
req.end ();
```

<span data-ttu-id="a7943-119">**Response**</span><span class="sxs-lookup"><span data-stu-id="a7943-119">**Response**</span></span>

<span data-ttu-id="a7943-120">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a7943-120">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "_type": "SpellCheck",
   "flaggedTokens": [
      {
         "offset": 0,
         "token": "Hollo",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "Hello",
               "score": 0.9115257530801
            },
            {
               "suggestion": "Hollow",
               "score": 0.858039839213461
            },
            {
               "suggestion": "Hallo",
               "score": 0.597385084464481
            }
         ]
      },
      {
         "offset": 7,
         "token": "wrld",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "world",
               "score": 0.9115257530801
            }
         ]
      }
   ]
}
```

## <a name="next-steps"></a><span data-ttu-id="a7943-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7943-121">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7943-122">Bing Spell Check tutorial</span><span class="sxs-lookup"><span data-stu-id="a7943-122">Bing Spell Check tutorial</span></span>](../tutorials/spellcheck.md)

## <a name="see-also"></a><span data-ttu-id="a7943-123">See also</span><span class="sxs-lookup"><span data-stu-id="a7943-123">See also</span></span>

- [<span data-ttu-id="a7943-124">Bing Spell Check overview</span><span class="sxs-lookup"><span data-stu-id="a7943-124">Bing Spell Check overview</span></span>](../proof-text.md)
- [<span data-ttu-id="a7943-125">Bing Spell Check API v7 Reference</span><span class="sxs-lookup"><span data-stu-id="a7943-125">Bing Spell Check API v7 Reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference)
