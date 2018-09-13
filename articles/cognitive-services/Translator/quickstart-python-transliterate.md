---
title: Translator Text convert text script with Python | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you convert text in one language from one script to another using the Translator Text API with Python in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: 41fb0f72c5974a1ab034680a820dca6aa7bbdc6d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869586"
---
# <a name="quickstart-transliterate-text-with-python"></a><span data-ttu-id="d0934-103">Quickstart: Transliterate text with Python</span><span class="sxs-lookup"><span data-stu-id="d0934-103">Quickstart: Transliterate text with Python</span></span>

<span data-ttu-id="d0934-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="d0934-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0934-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d0934-105">Prerequisites</span></span>

<span data-ttu-id="d0934-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="d0934-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="d0934-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="d0934-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="transliterate-request"></a><span data-ttu-id="d0934-108">Transliterate request</span><span class="sxs-lookup"><span data-stu-id="d0934-108">Transliterate request</span></span>

<span data-ttu-id="d0934-109">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span><span class="sxs-lookup"><span data-stu-id="d0934-109">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span></span>

1. <span data-ttu-id="d0934-110">Create a new Python project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="d0934-110">Create a new Python project in your favorite code editor.</span></span>
2. <span data-ttu-id="d0934-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="d0934-111">Add the code provided below.</span></span>
3. <span data-ttu-id="d0934-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="d0934-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="d0934-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="d0934-113">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, uuid, json

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'api.cognitive.microsofttranslator.com'
path = '/transliterate?api-version=3.0'

# Transliterate text in Japanese from Japanese script (i.e. Hiragana/Katakana/Kanji) to Latin script.
params = '&language=ja&fromScript=jpan&toScript=latn';

# Transliterate "good afternoon".
text = 'こんにちは'

def transliterate (content):

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
result = transliterate (content)

# Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
# We want to avoid escaping any Unicode characters that result contains. See:
# https://stackoverflow.com/questions/18337407/saving-utf-8-texts-in-json-dumps-as-utf8-not-as-u-escape-sequence
output = json.dumps(json.loads(result), indent=4, ensure_ascii=False)

print (output)
```

## <a name="transliterate-response"></a><span data-ttu-id="d0934-114">Transliterate response</span><span class="sxs-lookup"><span data-stu-id="d0934-114">Transliterate response</span></span>

<span data-ttu-id="d0934-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="d0934-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "text": "konnnichiha",
    "script": "latn"
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="d0934-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0934-116">Next steps</span></span>

<span data-ttu-id="d0934-117">Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="d0934-117">Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0934-118">Explore Python examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="d0934-118">Explore Python examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=python)
