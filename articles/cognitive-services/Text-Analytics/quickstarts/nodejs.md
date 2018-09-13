---
title: 'Quickstart: Using Node.js to call the Text Analytics API | Microsoft Docs'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Text Analytics API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: ashmaka
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 08/30/2018
ms.author: ashmaka
ms.openlocfilehash: 6cb02ea6c886b3c784826f41f6c3cb638e7104e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871344"
---
# <a name="quickstart-using-nodejs-to-call-the-text-analytics-cognitive-service"></a><span data-ttu-id="cc746-103">Quickstart: Using Node.js to call the Text Analytics Cognitive Service</span><span class="sxs-lookup"><span data-stu-id="cc746-103">Quickstart: Using Node.js to call the Text Analytics Cognitive Service</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="cc746-104">This article shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), [extract key phrases](#KeyPhraseExtraction), and [identify linked entities](#Entities) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with Node.JS.</span><span class="sxs-lookup"><span data-stu-id="cc746-104">This article shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), [extract key phrases](#KeyPhraseExtraction), and [identify linked entities](#Entities) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with Node.JS.</span></span>

<span data-ttu-id="cc746-105">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span><span class="sxs-lookup"><span data-stu-id="cc746-105">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc746-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc746-106">Prerequisites</span></span>

<span data-ttu-id="cc746-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="cc746-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span></span> <span data-ttu-id="cc746-108">You can use the **free tier for 5,000 transactions/month** to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="cc746-108">You can use the **free tier for 5,000 transactions/month** to complete this quickstart.</span></span>

<span data-ttu-id="cc746-109">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign up.</span><span class="sxs-lookup"><span data-stu-id="cc746-109">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign up.</span></span> 

<a name="Detect"></a>

## <a name="detect-language"></a><span data-ttu-id="cc746-110">Detect language</span><span class="sxs-lookup"><span data-stu-id="cc746-110">Detect language</span></span>

<span data-ttu-id="cc746-111">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span><span class="sxs-lookup"><span data-stu-id="cc746-111">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span></span>

1. <span data-ttu-id="cc746-112">Create a new Node.JS project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="cc746-112">Create a new Node.JS project in your favorite IDE.</span></span>
2. <span data-ttu-id="cc746-113">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="cc746-113">Add the code provided below.</span></span>
3. <span data-ttu-id="cc746-114">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="cc746-114">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="cc746-115">Replace the location in `uri` (currently `westus`) to the region you signed up for.</span><span class="sxs-lookup"><span data-stu-id="cc746-115">Replace the location in `uri` (currently `westus`) to the region you signed up for.</span></span>
5. <span data-ttu-id="cc746-116">Run the program.</span><span class="sxs-lookup"><span data-stu-id="cc746-116">Run the program.</span></span>

```javascript
'use strict';

let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the accessKey string value with your valid access key.
let accessKey = 'ENTER KEY HERE';

// Replace or verify the region.

// You must use the same region in your REST API call as you used to obtain your access keys.
// For example, if you obtained your access keys from the westus region, replace 
// "westcentralus" in the URI below with "westus".

// NOTE: Free trial access keys are generated in the westcentralus region, so if you are using
// a free trial access key, you should not need to change this region.
let uri = 'westus.api.cognitive.microsoft.com';
let path = '/text/analytics/v2.0/';

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

let get_language = function (documents) {
    let body = JSON.stringify (documents);

    let request_params = {
        method : 'POST',
        hostname : uri,
        path : path + 'languages',
        headers : {
            'Ocp-Apim-Subscription-Key' : accessKey,
        }
    };

    let req = https.request (request_params, response_handler);
    req.write (body);
    req.end ();
}

var documents = { 'documents': [
    { 'id': '1', 'text': 'This is a document written in English.' },
    { 'id': '2', 'text': 'Este es un document escrito en Español.' },
    { 'id': '3', 'text': '这是一个用中文写的文件' }
]};

get_language (documents);
```

<span data-ttu-id="cc746-117">**Language detection response**</span><span class="sxs-lookup"><span data-stu-id="cc746-117">**Language detection response**</span></span>

<span data-ttu-id="cc746-118">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="cc746-118">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "id": "1",
         "detectedLanguages": [
            {
               "name": "English",
               "iso6391Name": "en",
               "score": 1.0
            }
         ]
      },
      {
         "id": "2",
         "detectedLanguages": [
            {
               "name": "Spanish",
               "iso6391Name": "es",
               "score": 1.0
            }
         ]
      },
      {
         "id": "3",
         "detectedLanguages": [
            {
               "name": "Chinese_Simplified",
               "iso6391Name": "zh_chs",
               "score": 1.0
            }
         ]
      }
   ],
   "errors": [

   ]
}


```
<a name="SentimentAnalysis"></a>

## <a name="analyze-sentiment"></a><span data-ttu-id="cc746-119">Analyze sentiment</span><span class="sxs-lookup"><span data-stu-id="cc746-119">Analyze sentiment</span></span>

<span data-ttu-id="cc746-120">The Sentiment Analysis API detexts the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span><span class="sxs-lookup"><span data-stu-id="cc746-120">The Sentiment Analysis API detexts the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span></span> <span data-ttu-id="cc746-121">The following example scores two documents, one in English and another in Spanish.</span><span class="sxs-lookup"><span data-stu-id="cc746-121">The following example scores two documents, one in English and another in Spanish.</span></span>

<span data-ttu-id="cc746-122">Add the following code to the code from the [previous section](#Detect).</span><span class="sxs-lookup"><span data-stu-id="cc746-122">Add the following code to the code from the [previous section](#Detect).</span></span>

```javascript
let get_sentiments = function (documents) {
    let body = JSON.stringify (documents);

    let request_params = {
        method : 'POST',
        hostname : uri,
        path : path + 'sentiment',
        headers : {
            'Ocp-Apim-Subscription-Key' : accessKey,
        }
    };

    let req = https.request (request_params, response_handler);
    req.write (body);
    req.end ();
}

documents = { 'documents': [
    { 'id': '1', 'language': 'en', 'text': 'I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.' },
    { 'id': '2', 'language': 'es', 'text': 'Este ha sido un dia terrible, llegué tarde al trabajo debido a un accidente automobilistico.' },
]};

get_sentiments (documents);
```

<span data-ttu-id="cc746-123">**Sentiment analysis response**</span><span class="sxs-lookup"><span data-stu-id="cc746-123">**Sentiment analysis response**</span></span>

<span data-ttu-id="cc746-124">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="cc746-124">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "score": 0.99984133243560791,
         "id": "1"
      },
      {
         "score": 0.024017512798309326,
         "id": "2"
      },
   ],
   "errors": [   ]
}
```

<a name="KeyPhraseExtraction"></a>

## <a name="extract-key-phrases"></a><span data-ttu-id="cc746-125">Extract key phrases</span><span class="sxs-lookup"><span data-stu-id="cc746-125">Extract key phrases</span></span>

<span data-ttu-id="cc746-126">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span><span class="sxs-lookup"><span data-stu-id="cc746-126">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span></span> <span data-ttu-id="cc746-127">The following example extracts key phrases for both English and Spanish documents.</span><span class="sxs-lookup"><span data-stu-id="cc746-127">The following example extracts key phrases for both English and Spanish documents.</span></span>

<span data-ttu-id="cc746-128">Add the following code to the code from the [previous section](#SentimentAnalysis).</span><span class="sxs-lookup"><span data-stu-id="cc746-128">Add the following code to the code from the [previous section](#SentimentAnalysis).</span></span>

```javascript
let get_key_phrases = function (documents) {
    let body = JSON.stringify (documents);

    let request_params = {
        method : 'POST',
        hostname : uri,
        path : path + 'keyPhrases',
        headers : {
            'Ocp-Apim-Subscription-Key' : accessKey,
        }
    };

    let req = https.request (request_params, response_handler);
    req.write (body);
    req.end ();
}

documents = { 'documents': [
    { 'id': '1', 'language': 'en', 'text': 'I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.' },
    { 'id': '2', 'language': 'es', 'text': 'Si usted quiere comunicarse con Carlos, usted debe de llamarlo a su telefono movil. Carlos es muy responsable, pero necesita recibir una notificacion si hay algun problema.' },
    { 'id': '3', 'language': 'en', 'text': 'The Grand Hotel is a new hotel in the center of Seattle. It earned 5 stars in my review, and has the classiest decor I\'ve ever seen.' }
]};

get_key_phrases (documents);
```

<span data-ttu-id="cc746-129">**Key phrase extraction response**</span><span class="sxs-lookup"><span data-stu-id="cc746-129">**Key phrase extraction response**</span></span>

<span data-ttu-id="cc746-130">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="cc746-130">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "keyPhrases": [
            "HDR resolution",
            "new XBox",
            "clean look"
         ],
         "id": "1"
      },
      {
         "keyPhrases": [
            "Carlos",
            "notificacion",
            "algun problema",
            "telefono movil"
         ],
         "id": "2"
      },
      {
         "keyPhrases": [
            "new hotel",
            "Grand Hotel",
            "review",
            "center of Seattle",
            "classiest decor",
            "stars"
         ],
         "id": "3"
      }
   ],
   "errors": [  ]
}
```

<a name="Entities"></a>

## <a name="identify-linked-entities"></a><span data-ttu-id="cc746-131">Identify linked entities</span><span class="sxs-lookup"><span data-stu-id="cc746-131">Identify linked entities</span></span>

<span data-ttu-id="cc746-132">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span><span class="sxs-lookup"><span data-stu-id="cc746-132">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span></span> <span data-ttu-id="cc746-133">The following example identifies entities for English documents.</span><span class="sxs-lookup"><span data-stu-id="cc746-133">The following example identifies entities for English documents.</span></span>

<span data-ttu-id="cc746-134">Add the following code to the code from the [previous section](#KeyPhraseExtraction).</span><span class="sxs-lookup"><span data-stu-id="cc746-134">Add the following code to the code from the [previous section](#KeyPhraseExtraction).</span></span>

```javascript
let get_entities = function (documents) {
    let body = JSON.stringify (documents);

    let request_params = {
        method : 'POST',
        hostname : uri,
        path : path + 'entities',
        headers : {
            'Ocp-Apim-Subscription-Key' : accessKey,
        }
    };

    let req = https.request (request_params, response_handler);
    req.write (body);
    req.end ();
}

documents = { 'documents': [
    { 'id': '1', 'language': 'en', 'text': 'I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.' },
    { 'id': '2', 'language': 'en', 'text': 'The Seattle Seahawks won the Super Bowl in 2014.' }
]};

get_entities (documents);
```

<span data-ttu-id="cc746-135">**Entity linking response**</span><span class="sxs-lookup"><span data-stu-id="cc746-135">**Entity linking response**</span></span>

<span data-ttu-id="cc746-136">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="cc746-136">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
    "documents": [
        {
            "id": "1",
            "entities": [
                {
                    "name": "Xbox One",
                    "matches": [
                        {
                            "text": "XBox One",
                            "offset": 23,
                            "length": 8
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Xbox One",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Xbox_One",
                    "bingId": "446bb4df-4999-4243-84c0-74e0f6c60e75"
                },
                {
                    "name": "Ultra-high-definition television",
                    "matches": [
                        {
                            "text": "4K",
                            "offset": 63,
                            "length": 2
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Ultra-high-definition television",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Ultra-high-definition_television",
                    "bingId": "7ee02026-b6ec-878b-f4de-f0bc7b0ab8c4"
                }
            ]
        },
        {
            "id": "2",
            "entities": [
                {
                    "name": "2013 Seattle Seahawks season",
                    "matches": [
                        {
                            "text": "Seattle Seahawks",
                            "offset": 4,
                            "length": 16
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "2013 Seattle Seahawks season",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/2013_Seattle_Seahawks_season",
                    "bingId": "eb637865-4722-4eca-be9e-0ac0c376d361"
                }
            ]
        }
    ],
    "errors": []
}
```

## <a name="next-steps"></a><span data-ttu-id="cc746-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc746-137">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc746-138">Text Analytics With Power BI</span><span class="sxs-lookup"><span data-stu-id="cc746-138">Text Analytics With Power BI</span></span>](../tutorials/tutorial-power-bi-key-phrases.md)

## <a name="see-also"></a><span data-ttu-id="cc746-139">See also</span><span class="sxs-lookup"><span data-stu-id="cc746-139">See also</span></span> 

 [<span data-ttu-id="cc746-140">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="cc746-140">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="cc746-141">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="cc746-141">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)
