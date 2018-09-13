---
title: Translator Text identify language from text with Ruby | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you identify the language of the source text using the Translator Text API with Ruby in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: b692b66454cc86e6d81aec9c3139b39a905d0d66
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868491"
---
# <a name="quickstart-identify-language-from-text-with-ruby"></a><span data-ttu-id="b5329-103">Quickstart: Identify language from text with Ruby</span><span class="sxs-lookup"><span data-stu-id="b5329-103">Quickstart: Identify language from text with Ruby</span></span>

<span data-ttu-id="b5329-104">In this quickstart, you identify the language of the source text using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="b5329-104">In this quickstart, you identify the language of the source text using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5329-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b5329-105">Prerequisites</span></span>

<span data-ttu-id="b5329-106">You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span><span class="sxs-lookup"><span data-stu-id="b5329-106">You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span></span>

<span data-ttu-id="b5329-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="b5329-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="detect-request"></a><span data-ttu-id="b5329-108">Detect request</span><span class="sxs-lookup"><span data-stu-id="b5329-108">Detect request</span></span>

<span data-ttu-id="b5329-109">The following code identifies the language of the source text using the [Detect](./reference/v3-0-detect.md) method.</span><span class="sxs-lookup"><span data-stu-id="b5329-109">The following code identifies the language of the source text using the [Detect](./reference/v3-0-detect.md) method.</span></span>

1. <span data-ttu-id="b5329-110">Create a new Ruby project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="b5329-110">Create a new Ruby project in your favorite code editor.</span></span>
2. <span data-ttu-id="b5329-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="b5329-111">Add the code provided below.</span></span>
3. <span data-ttu-id="b5329-112">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="b5329-112">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="b5329-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="b5329-113">Run the program.</span></span>

```ruby
require 'net/https'
require 'uri'
require 'cgi'
require 'json'
require 'securerandom'

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the key string value with your valid subscription key.
key = 'ENTER KEY HERE'

host = 'https://api.cognitive.microsofttranslator.com'
path = '/detect?api-version=3.0'

uri = URI (host + path)

text = 'Salve, mondo!'

content = '[{"Text" : "' + text + '"}]'

request = Net::HTTP::Post.new(uri)
request['Content-type'] = 'application/json'
request['Content-length'] = content.length
request['Ocp-Apim-Subscription-Key'] = key
request['X-ClientTraceId'] = SecureRandom.uuid
request.body = content

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request (request)
end

result = response.body.force_encoding("utf-8")

json = JSON.pretty_generate(JSON.parse(result))
puts json
```

## <a name="detect-response"></a><span data-ttu-id="b5329-114">Detect response</span><span class="sxs-lookup"><span data-stu-id="b5329-114">Detect response</span></span>

<span data-ttu-id="b5329-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="b5329-115">A successful response is returned in JSON as shown in the following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b5329-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5329-116">Next steps</span></span>

<span data-ttu-id="b5329-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5329-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5329-118">Explore Ruby examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="b5329-118">Explore Ruby examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=ruby)
