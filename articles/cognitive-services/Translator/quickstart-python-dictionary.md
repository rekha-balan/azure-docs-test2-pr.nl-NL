---
title: Translator Text find alternate translations with Python | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you find alternate translations and examples of terms in context using the Translator Text API with Python in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: 4f7c91bfa6fe82f19e84e13b4b7442b59b126cb9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869458"
---
# <a name="quickstart-find-alternate-translations-and-usage-with-python"></a><span data-ttu-id="72c0c-103">Quickstart: Find alternate translations and usage with Python</span><span class="sxs-lookup"><span data-stu-id="72c0c-103">Quickstart: Find alternate translations and usage with Python</span></span>

<span data-ttu-id="72c0c-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="72c0c-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72c0c-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="72c0c-105">Prerequisites</span></span>

<span data-ttu-id="72c0c-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="72c0c-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="72c0c-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="72c0c-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="dictionary-lookup-request"></a><span data-ttu-id="72c0c-108">Dictionary Lookup request</span><span class="sxs-lookup"><span data-stu-id="72c0c-108">Dictionary Lookup request</span></span>

<span data-ttu-id="72c0c-109">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span><span class="sxs-lookup"><span data-stu-id="72c0c-109">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span></span>

1. <span data-ttu-id="72c0c-110">Create a new Python project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="72c0c-110">Create a new Python project in your favorite code editor.</span></span>
2. <span data-ttu-id="72c0c-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="72c0c-111">Add the code provided below.</span></span>
3. <span data-ttu-id="72c0c-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="72c0c-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="72c0c-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="72c0c-113">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, uuid, json

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'api.cognitive.microsofttranslator.com'
path = '/dictionary/lookup?api-version=3.0'

params = '&from=en&to=fr';

text = 'great'

def lookup (content):

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
result = lookup (content)

# Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
# We want to avoid escaping any Unicode characters that result contains. See:
# https://stackoverflow.com/questions/18337407/saving-utf-8-texts-in-json-dumps-as-utf8-not-as-u-escape-sequence
output = json.dumps(json.loads(result), indent=4, ensure_ascii=False)

print (output)
```

## <a name="dictionary-lookup-response"></a><span data-ttu-id="72c0c-114">Dictionary Lookup response</span><span class="sxs-lookup"><span data-stu-id="72c0c-114">Dictionary Lookup response</span></span>

<span data-ttu-id="72c0c-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="72c0c-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "normalizedSource": "great",
    "displaySource": "great",
    "translations": [
      {
        "normalizedTarget": "grand",
        "displayTarget": "grand",
        "posTag": "ADJ",
        "confidence": 0.2783,
        "prefixWord": "",
        "backTranslations": [
          {
            "normalizedText": "great",
            "displayText": "great",
            "numExamples": 15,
            "frequencyCount": 34358
          },
          {
            "normalizedText": "big",
            "displayText": "big",
            "numExamples": 15,
            "frequencyCount": 21770
          },
...
        ]
      },
      {
        "normalizedTarget": "super",
        "displayTarget": "super",
        "posTag": "ADJ",
        "confidence": 0.1514,
        "prefixWord": "",
        "backTranslations": [
          {
            "normalizedText": "super",
            "displayText": "super",
            "numExamples": 15,
            "frequencyCount": 12023
          },
          {
            "normalizedText": "great",
            "displayText": "great",
            "numExamples": 15,
            "frequencyCount": 10931
          },
...
        ]
      },
...
    ]
  }
]
```

## <a name="dictionary-examples-request"></a><span data-ttu-id="72c0c-116">Dictionary Examples request</span><span class="sxs-lookup"><span data-stu-id="72c0c-116">Dictionary Examples request</span></span>

<span data-ttu-id="72c0c-117">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span><span class="sxs-lookup"><span data-stu-id="72c0c-117">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span></span>

1. <span data-ttu-id="72c0c-118">Create a new Python project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="72c0c-118">Create a new Python project in your favorite code editor.</span></span>
2. <span data-ttu-id="72c0c-119">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="72c0c-119">Add the code provided below.</span></span>
3. <span data-ttu-id="72c0c-120">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="72c0c-120">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="72c0c-121">Run the program.</span><span class="sxs-lookup"><span data-stu-id="72c0c-121">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, uuid, json

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'api.cognitive.microsofttranslator.com'
path = '/dictionary/examples?api-version=3.0'

params = '&from=en&to=fr';

text = 'great'
translation = 'formidable'

def examples (content):

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
    'Translation' : translation,
}]
content = json.dumps(requestBody, ensure_ascii=False).encode('utf-8')
result = examples (content)

# Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
# We want to avoid escaping any Unicode characters that result contains. See:
# https://stackoverflow.com/questions/18337407/saving-utf-8-texts-in-json-dumps-as-utf8-not-as-u-escape-sequence
output = json.dumps(json.loads(result), indent=4, ensure_ascii=False)

print (output)
```

## <a name="dictionary-examples-response"></a><span data-ttu-id="72c0c-122">Dictionary Examples response</span><span class="sxs-lookup"><span data-stu-id="72c0c-122">Dictionary Examples response</span></span>

<span data-ttu-id="72c0c-123">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="72c0c-123">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "normalizedSource": "great",
    "normalizedTarget": "formidable",
    "examples": [
      {
        "sourcePrefix": "You have a ",
        "sourceTerm": "great",
        "sourceSuffix": " expression there.",
        "targetPrefix": "Vous avez une expression ",
        "targetTerm": "formidable",
        "targetSuffix": "."
      },
      {
        "sourcePrefix": "You played a ",
        "sourceTerm": "great",
        "sourceSuffix": " game today.",
        "targetPrefix": "Vous avez été ",
        "targetTerm": "formidable",
        "targetSuffix": "."
      },
...
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="72c0c-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="72c0c-124">Next steps</span></span>

<span data-ttu-id="72c0c-125">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="72c0c-125">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="72c0c-126">Explore Python examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="72c0c-126">Explore Python examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=python)
