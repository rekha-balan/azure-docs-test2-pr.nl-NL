---
title: Translator Text get supported languages with Python | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API with Java in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: 3ae3c6be814f79541e39eddd3be137b71cc1a494
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868845"
---
# <a name="quickstart-get-supported-languages-with-python"></a><span data-ttu-id="59897-103">Quickstart: Get supported languages with Python</span><span class="sxs-lookup"><span data-stu-id="59897-103">Quickstart: Get supported languages with Python</span></span>

<span data-ttu-id="59897-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="59897-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59897-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59897-105">Prerequisites</span></span>

<span data-ttu-id="59897-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="59897-106">You'll need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="59897-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="59897-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="languages-request"></a><span data-ttu-id="59897-108">Languages request</span><span class="sxs-lookup"><span data-stu-id="59897-108">Languages request</span></span>

<span data-ttu-id="59897-109">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span><span class="sxs-lookup"><span data-stu-id="59897-109">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span></span>

1. <span data-ttu-id="59897-110">Create a new Python project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="59897-110">Create a new Python project in your favorite code editor.</span></span>
2. <span data-ttu-id="59897-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="59897-111">Add the code provided below.</span></span>
3. <span data-ttu-id="59897-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="59897-112">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="59897-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="59897-113">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'api.cognitive.microsofttranslator.com'
path = '/languages?api-version=3.0'

output_path = 'output.txt'

def get_languages ():

    headers = {'Ocp-Apim-Subscription-Key': subscriptionKey}

    conn = http.client.HTTPSConnection(host)
    conn.request ("GET", path, None, headers)
    response = conn.getresponse ()
    return response.read ()

result = get_languages ()

# Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
# We want to avoid escaping any Unicode characters that result contains. See:
# https://stackoverflow.com/questions/18337407/saving-utf-8-texts-in-json-dumps-as-utf8-not-as-u-escape-sequence
json = json.dumps(json.loads(result), indent=4, ensure_ascii=False).encode('utf-8')

f = open(output_path, 'wb')
f.write (json)
f.close
```

## <a name="languages-response"></a><span data-ttu-id="59897-114">Languages response</span><span class="sxs-lookup"><span data-stu-id="59897-114">Languages response</span></span>

<span data-ttu-id="59897-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="59897-115">A successful response is returned in JSON as shown in the following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="59897-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="59897-116">Next steps</span></span>

<span data-ttu-id="59897-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="59897-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59897-118">Explore Python examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="59897-118">Explore Python examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=python)
