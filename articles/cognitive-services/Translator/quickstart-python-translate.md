---
title: Translator Text translate text with Python | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you translate text from one language to another using the Translator Text API with Python in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: 8f70ffb77e21131990d6b77a1cb13c9d5c054d06
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968986"
---
# <a name="quickstart-translate-text-with-python"></a><span data-ttu-id="f4767-103">Quickstart: Translate text with Python</span><span class="sxs-lookup"><span data-stu-id="f4767-103">Quickstart: Translate text with Python</span></span>

<span data-ttu-id="f4767-104">In this quickstart, you translate text from one language to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="f4767-104">In this quickstart, you translate text from one language to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4767-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f4767-105">Prerequisites</span></span>

<span data-ttu-id="f4767-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="f4767-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="f4767-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="f4767-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="translate-request"></a><span data-ttu-id="f4767-108">Translate request</span><span class="sxs-lookup"><span data-stu-id="f4767-108">Translate request</span></span>

<span data-ttu-id="f4767-109">The following code translates source text from one language to another using the [Translate](./reference/v3-0-translate.md) method.</span><span class="sxs-lookup"><span data-stu-id="f4767-109">The following code translates source text from one language to another using the [Translate](./reference/v3-0-translate.md) method.</span></span>

1. <span data-ttu-id="f4767-110">Create a new Python project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="f4767-110">Create a new Python project in your favorite code editor.</span></span>
2. <span data-ttu-id="f4767-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4767-111">Add the code provided below.</span></span>
3. <span data-ttu-id="f4767-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4767-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4767-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4767-113">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, uuid, json

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'api.cognitive.microsofttranslator.com'
path = '/translate?api-version=3.0'

# Translate to German and Italian.
params = "&to=de&to=it";

text = 'Hello, world!'

def translate (content):

    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-type': 'application/json',
        'X-ClientTraceId': str(uuid.uuid4())
    }

    conn = http.client.HTTPSConnection(host)
    conn.request ("POST", path + params, content, headers)
    response = conn.getresponse ()
    return response.read ()

requestBody = [{
    'Text' : text,
}]
content = json.dumps(requestBody, ensure_ascii=False).encode('utf-8')
result = translate (content)

# Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
# We want to avoid escaping any Unicode characters that result contains. See:
# https://stackoverflow.com/questions/18337407/saving-utf-8-texts-in-json-dumps-as-utf8-not-as-u-escape-sequence
output = json.dumps(json.loads(result), indent=4, ensure_ascii=False)

print (output)
```

## <a name="translate-response"></a><span data-ttu-id="f4767-114">Translate response</span><span class="sxs-lookup"><span data-stu-id="f4767-114">Translate response</span></span>

<span data-ttu-id="f4767-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4767-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "detectedLanguage": {
      "language": "en",
      "score": 1.0
    },
    "translations": [
      {
        "text": "Hallo Welt!",
        "to": "de"
      },
      {
        "text": "Salve, mondo!",
        "to": "it"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="f4767-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4767-116">Next steps</span></span>

<span data-ttu-id="f4767-117">Explore the sample code for this quickstart and others, including transliteration and language identification, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f4767-117">Explore the sample code for this quickstart and others, including transliteration and language identification, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4767-118">Explore Python examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="f4767-118">Explore Python examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=python)
