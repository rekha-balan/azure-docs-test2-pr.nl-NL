---
title: Translator Text get sentence lengths with Ruby | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you find the lengths of sentences in text using the Translator Text API with Ruby in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: 3a4fc999961e06b084a0d7da42ed5576962e5722
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867179"
---
# <a name="quickstart-get-sentence-lengths-with-ruby"></a><span data-ttu-id="776a8-103">Quickstart: Get sentence lengths with Ruby</span><span class="sxs-lookup"><span data-stu-id="776a8-103">Quickstart: Get sentence lengths with Ruby</span></span>

<span data-ttu-id="776a8-104">In this quickstart, you find the lengths of sentences in text using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="776a8-104">In this quickstart, you find the lengths of sentences in text using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="776a8-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="776a8-105">Prerequisites</span></span>

<span data-ttu-id="776a8-106">You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span><span class="sxs-lookup"><span data-stu-id="776a8-106">You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span></span>

<span data-ttu-id="776a8-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="776a8-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="breaksentence-request"></a><span data-ttu-id="776a8-108">BreakSentence request</span><span class="sxs-lookup"><span data-stu-id="776a8-108">BreakSentence request</span></span>

<span data-ttu-id="776a8-109">The following code breaks the source text into sentences using the [BreakSentence](./reference/v3-0-break-sentence.md) method.</span><span class="sxs-lookup"><span data-stu-id="776a8-109">The following code breaks the source text into sentences using the [BreakSentence](./reference/v3-0-break-sentence.md) method.</span></span>

1. <span data-ttu-id="776a8-110">Create a new Ruby project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="776a8-110">Create a new Ruby project in your favorite code editor.</span></span>
2. <span data-ttu-id="776a8-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="776a8-111">Add the code provided below.</span></span>
3. <span data-ttu-id="776a8-112">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="776a8-112">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="776a8-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="776a8-113">Run the program.</span></span>

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
path = '/breaksentence?api-version=3.0'

uri = URI (host + path)

text = 'How are you? I am fine. What did you do today?'

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

## <a name="breaksentence-response"></a><span data-ttu-id="776a8-114">BreakSentence response</span><span class="sxs-lookup"><span data-stu-id="776a8-114">BreakSentence response</span></span>

<span data-ttu-id="776a8-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="776a8-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "detectedLanguage": {
      "language": "en",
      "score": 1.0
    },
    "sentLen": [
      13,
      11,
      22
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="776a8-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="776a8-116">Next steps</span></span>

<span data-ttu-id="776a8-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="776a8-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="776a8-118">Explore Ruby examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="776a8-118">Explore Ruby examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=ruby)
