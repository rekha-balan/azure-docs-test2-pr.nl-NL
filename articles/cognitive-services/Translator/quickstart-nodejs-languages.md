---
title: Translator Text get supported languages with Node.js | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API with Node.js in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: dd37aab3707c6f06b8cc2e942366e19746694252
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968135"
---
# <a name="quickstart-get-supported-languages-with-nodejs"></a><span data-ttu-id="1c028-103">Quickstart: Get supported languages with Node.js</span><span class="sxs-lookup"><span data-stu-id="1c028-103">Quickstart: Get supported languages with Node.js</span></span>

<span data-ttu-id="1c028-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="1c028-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c028-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1c028-105">Prerequisites</span></span>

<span data-ttu-id="1c028-106">You'll need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="1c028-106">You'll need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

<span data-ttu-id="1c028-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="1c028-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="languages-request"></a><span data-ttu-id="1c028-108">Languages request</span><span class="sxs-lookup"><span data-stu-id="1c028-108">Languages request</span></span>

<span data-ttu-id="1c028-109">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span><span class="sxs-lookup"><span data-stu-id="1c028-109">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span></span>

1. <span data-ttu-id="1c028-110">Create a new Node.js project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="1c028-110">Create a new Node.js project in your favorite code editor.</span></span>
2. <span data-ttu-id="1c028-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1c028-111">Add the code provided below.</span></span>
3. <span data-ttu-id="1c028-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1c028-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1c028-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1c028-113">Run the program.</span></span>

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
let path = '/languages?api-version=3.0';

let output_path = 'output.txt';
let ws = fs.createWriteStream(output_path);

let response_handler = function (response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
        let json = JSON.stringify(JSON.parse(body), null, 4);
        ws.write (json);
        ws.close ();
        console.log("File written.");

    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

let GetLanguages = function () {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

    let req = https.request (request_params, response_handler);
    req.end ();
}

GetLanguages ();
```

## <a name="languages-response"></a><span data-ttu-id="1c028-114">Languages response</span><span class="sxs-lookup"><span data-stu-id="1c028-114">Languages response</span></span>

<span data-ttu-id="1c028-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1c028-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
{
  "translation": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr"
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl"
    },
...
  },
  "transliteration": {
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "scripts": [
        {
          "code": "Arab",
          "name": "Arabic",
          "nativeName": "العربية",
          "dir": "rtl",
          "toScripts": [
            {
              "code": "Latn",
              "name": "Latin",
              "nativeName": "اللاتينية",
              "dir": "ltr"
            }
          ]
        },
        {
          "code": "Latn",
          "name": "Latin",
          "nativeName": "اللاتينية",
          "dir": "ltr",
          "toScripts": [
            {
              "code": "Arab",
              "name": "Arabic",
              "nativeName": "العربية",
              "dir": "rtl"
            }
          ]
        }
      ]
    },
...
  },
  "dictionary": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
...
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="1c028-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c028-116">Next steps</span></span>

<span data-ttu-id="1c028-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="1c028-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c028-118">Explore Node.js examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="1c028-118">Explore Node.js examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=javascript)
