---
title: Translator Text find alternate translations with Ruby | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you find alternate translations and examples of terms in context using the Translator Text API with Ruby in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: 6462a48c2f15c8ac4a6b9bce49d23ea3d38dcbd5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857341"
---
# <a name="quickstart-find-alternate-translations-and-usage-with-ruby"></a><span data-ttu-id="2aedd-103">Quickstart: Find alternate translations and usage with Ruby</span><span class="sxs-lookup"><span data-stu-id="2aedd-103">Quickstart: Find alternate translations and usage with Ruby</span></span>

<span data-ttu-id="2aedd-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="2aedd-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2aedd-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2aedd-105">Prerequisites</span></span>

<span data-ttu-id="2aedd-106">You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span><span class="sxs-lookup"><span data-stu-id="2aedd-106">You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span></span>

<span data-ttu-id="2aedd-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="2aedd-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="dictionary-lookup-request"></a><span data-ttu-id="2aedd-108">Dictionary Lookup request</span><span class="sxs-lookup"><span data-stu-id="2aedd-108">Dictionary Lookup request</span></span>

<span data-ttu-id="2aedd-109">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span><span class="sxs-lookup"><span data-stu-id="2aedd-109">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span></span>

1. <span data-ttu-id="2aedd-110">Create a new Ruby project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="2aedd-110">Create a new Ruby project in your favorite code editor.</span></span>
2. <span data-ttu-id="2aedd-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="2aedd-111">Add the code provided below.</span></span>
3. <span data-ttu-id="2aedd-112">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="2aedd-112">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="2aedd-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="2aedd-113">Run the program.</span></span>

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
path = '/dictionary/lookup?api-version=3.0'

params = '&from=en&to=fr'

uri = URI (host + path + params)

text = 'great'

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

## <a name="dictionary-lookup-response"></a><span data-ttu-id="2aedd-114">Dictionary Lookup response</span><span class="sxs-lookup"><span data-stu-id="2aedd-114">Dictionary Lookup response</span></span>

<span data-ttu-id="2aedd-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2aedd-115">A successful response is returned in JSON as shown in the following example:</span></span>

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

## <a name="dictionary-examples-request"></a><span data-ttu-id="2aedd-116">Dictionary Examples request</span><span class="sxs-lookup"><span data-stu-id="2aedd-116">Dictionary Examples request</span></span>

<span data-ttu-id="2aedd-117">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span><span class="sxs-lookup"><span data-stu-id="2aedd-117">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span></span>

1. <span data-ttu-id="2aedd-118">Create a new Ruby project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="2aedd-118">Create a new Ruby project in your favorite code editor.</span></span>
2. <span data-ttu-id="2aedd-119">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="2aedd-119">Add the code provided below.</span></span>
3. <span data-ttu-id="2aedd-120">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="2aedd-120">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="2aedd-121">Run the program.</span><span class="sxs-lookup"><span data-stu-id="2aedd-121">Run the program.</span></span>

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
path = '/dictionary/examples?api-version=3.0'

params = '&from=en&to=fr'

uri = URI (host + path + params)

text = 'great'
translation = 'formidable'

content = '[{"Text" : "' + text + '", "Translation" : "' + translation + '"}]'

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

## <a name="dictionary-examples-response"></a><span data-ttu-id="2aedd-122">Dictionary Examples response</span><span class="sxs-lookup"><span data-stu-id="2aedd-122">Dictionary Examples response</span></span>

<span data-ttu-id="2aedd-123">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2aedd-123">A successful response is returned in JSON as shown in the following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2aedd-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="2aedd-124">Next steps</span></span>

<span data-ttu-id="2aedd-125">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="2aedd-125">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2aedd-126">Explore Ruby examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="2aedd-126">Explore Ruby examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=ruby)
