---
title: Translator Text convert text script with Node.js | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you convert text in one language from one script to another using the Translator Text API with Node.js in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: b16af911e5822deaa7cc7bcfe792245ae154eb26
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866900"
---
# <a name="quickstart-transliterate-text-with-nodejs"></a><span data-ttu-id="01f13-103">Quickstart: Transliterate text with Node.js</span><span class="sxs-lookup"><span data-stu-id="01f13-103">Quickstart: Transliterate text with Node.js</span></span>

<span data-ttu-id="01f13-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="01f13-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01f13-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="01f13-105">Prerequisites</span></span>

<span data-ttu-id="01f13-106">You'll need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="01f13-106">You'll need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

<span data-ttu-id="01f13-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="01f13-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="transliterate-request"></a><span data-ttu-id="01f13-108">Transliterate request</span><span class="sxs-lookup"><span data-stu-id="01f13-108">Transliterate request</span></span>

<span data-ttu-id="01f13-109">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span><span class="sxs-lookup"><span data-stu-id="01f13-109">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span></span>

1. <span data-ttu-id="01f13-110">Create a new Node.js project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="01f13-110">Create a new Node.js project in your favorite code editor.</span></span>
2. <span data-ttu-id="01f13-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="01f13-111">Add the code provided below.</span></span>
3. <span data-ttu-id="01f13-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="01f13-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="01f13-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="01f13-113">Run the program.</span></span>

```javascript
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'api.cognitive.microsofttranslator.com';
let path = '/transliterate?api-version=3.0';

// Transliterate text in Japanese from Japanese script (i.e. Hiragana/Katakana/Kanji) to Latin script.
let params = '&language=ja&fromScript=jpan&toScript=latn';

// Transliterate "good afternoon".
let text = 'こんにちは';

let response_handler = function (response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
        let json = JSON.stringify(JSON.parse(body), null, 4);
        console.log(json);
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

let get_guid = function () {
  return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
    var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
    return v.toString(16);
  });
}

let Transliterate = function (content) {
    let request_params = {
        method : 'POST',
        hostname : host,
        path : path + params,
        headers : {
            'Content-Type' : 'application/json',
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
            'X-ClientTraceId' : get_guid (),
        }
    };

    let req = https.request (request_params, response_handler);
    req.write (content);
    req.end ();
}

let content = JSON.stringify ([{'Text' : text}]);

Transliterate (content);
```

## <a name="transliterate-response"></a><span data-ttu-id="01f13-114">Transliterate response</span><span class="sxs-lookup"><span data-stu-id="01f13-114">Transliterate response</span></span>

<span data-ttu-id="01f13-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="01f13-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "text": "konnnichiha",
    "script": "latn"
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="01f13-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="01f13-116">Next steps</span></span>

<span data-ttu-id="01f13-117">Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="01f13-117">Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01f13-118">Explore Node.js examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="01f13-118">Explore Node.js examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=javascript)
