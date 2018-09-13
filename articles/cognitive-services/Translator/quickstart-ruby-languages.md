---
title: Translator Text get supported languages with Ruby | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API with Ruby in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: 1080d79f6dddfd57816989b7d1c4f95348493ad6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856234"
---
# <a name="quickstart-get-supported-languages-with-ruby"></a><span data-ttu-id="7a255-103">Quickstart: Get supported languages with Ruby</span><span class="sxs-lookup"><span data-stu-id="7a255-103">Quickstart: Get supported languages with Ruby</span></span>

<span data-ttu-id="7a255-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="7a255-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a255-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a255-105">Prerequisites</span></span>

<span data-ttu-id="7a255-106">You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span><span class="sxs-lookup"><span data-stu-id="7a255-106">You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span></span>

<span data-ttu-id="7a255-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="7a255-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="languages-request"></a><span data-ttu-id="7a255-108">Languages request</span><span class="sxs-lookup"><span data-stu-id="7a255-108">Languages request</span></span>

<span data-ttu-id="7a255-109">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span><span class="sxs-lookup"><span data-stu-id="7a255-109">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span></span>

1. <span data-ttu-id="7a255-110">Create a new Ruby project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="7a255-110">Create a new Ruby project in your favorite code editor.</span></span>
2. <span data-ttu-id="7a255-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="7a255-111">Add the code provided below.</span></span>
3. <span data-ttu-id="7a255-112">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="7a255-112">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="7a255-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="7a255-113">Run the program.</span></span>

```ruby
require 'net/https'
require 'uri'
require 'cgi'
require 'json'

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the key string value with your valid subscription key.
key = 'ENTER KEY HERE'

host = 'https://api.cognitive.microsofttranslator.com'
path = '/languages?api-version=3.0'

uri = URI (host + path)

request = Net::HTTP::Get.new(uri)
request['Ocp-Apim-Subscription-Key'] = key

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request (request)
end

result = response.body.force_encoding("utf-8")

json = JSON.pretty_generate(JSON.parse(result))

output_path = 'output.txt'

File.open(output_path, 'w' ) do |output|
    output.print json
end
```

## <a name="languages-response"></a><span data-ttu-id="7a255-114">Languages response</span><span class="sxs-lookup"><span data-stu-id="7a255-114">Languages response</span></span>

<span data-ttu-id="7a255-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7a255-115">A successful response is returned in JSON as shown in the following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7a255-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a255-116">Next steps</span></span>

<span data-ttu-id="7a255-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a255-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a255-118">Explore Ruby examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="7a255-118">Explore Ruby examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=ruby)
