---
title: Translator Text identify language from text with Python | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you identify the language of the source text using the Translator Text API with Python in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: 07a16e419bfdd4d73108fcdaa12695e99fecabee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857417"
---
# <a name="quickstart-identify-language-from-text-with-python"></a><span data-ttu-id="3bd9a-103">Quickstart: Identify language from text with Python</span><span class="sxs-lookup"><span data-stu-id="3bd9a-103">Quickstart: Identify language from text with Python</span></span>

<span data-ttu-id="3bd9a-104">In this quickstart, you identify the language of the source text using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="3bd9a-104">In this quickstart, you identify the language of the source text using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bd9a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3bd9a-105">Prerequisites</span></span>

<span data-ttu-id="3bd9a-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="3bd9a-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="3bd9a-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="3bd9a-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="detect-request"></a><span data-ttu-id="3bd9a-108">Detect request</span><span class="sxs-lookup"><span data-stu-id="3bd9a-108">Detect request</span></span>

<span data-ttu-id="3bd9a-109">The following code identifies the language of the source text using the [Detect](./reference/v3-0-detect.md) method.</span><span class="sxs-lookup"><span data-stu-id="3bd9a-109">The following code identifies the language of the source text using the [Detect](./reference/v3-0-detect.md) method.</span></span>

1. <span data-ttu-id="3bd9a-110">Create a new Python project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="3bd9a-110">Create a new Python project in your favorite code editor.</span></span>
2. <span data-ttu-id="3bd9a-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="3bd9a-111">Add the code provided below.</span></span>
3. <span data-ttu-id="3bd9a-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="3bd9a-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="3bd9a-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="3bd9a-113">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, uuid, json

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'api.cognitive.microsofttranslator.com'
path = '/detect?api-version=3.0'

params = ''

text = 'Salve, mondo!'

def detect (content):

    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-type': 'application/json',
        'X-ClientTraceId': str(uuid.uuid4())
    }

    conn = http.client.HTTPSConnection(host)
    conn.request ("POST", path, content, headers)
    response = conn.getresponse ()
    return response.read ()

requestBody = [{
    'Text' : text,
}]
content = json.dumps(requestBody, ensure_ascii=False).encode('utf-8')
result = detect (content)

# Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
# We want to avoid escaping any Unicode characters that result contains. See:
# https://stackoverflow.com/questions/18337407/saving-utf-8-texts-in-json-dumps-as-utf8-not-as-u-escape-sequence
output = json.dumps(json.loads(result), indent=4, ensure_ascii=False)

print (output)
```

## <a name="detect-response"></a><span data-ttu-id="3bd9a-114">Detect response</span><span class="sxs-lookup"><span data-stu-id="3bd9a-114">Detect response</span></span>

<span data-ttu-id="3bd9a-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="3bd9a-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "language": "it",
    "score": 1.0,
    "isTranslationSupported": true,
    "isTransliterationSupported": false,
    "alternatives": [
      {
        "language": "pt",
        "score": 1.0,
        "isTranslationSupported": true,
        "isTransliterationSupported": false
      },
      {
        "language": "en",
        "score": 1.0,
        "isTranslationSupported": true,
        "isTransliterationSupported": false
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="3bd9a-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="3bd9a-116">Next steps</span></span>

<span data-ttu-id="3bd9a-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="3bd9a-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3bd9a-118">Explore Python examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="3bd9a-118">Explore Python examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=python)
