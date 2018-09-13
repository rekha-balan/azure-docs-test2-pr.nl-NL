---
title: Ruby Quickstart for Bing Spell Check API - Azure Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Spell Check API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: quickstart
ms.date: 09/14/2017
ms.author: v-jaswel
ms.openlocfilehash: 9787ed058d0207931f8e550bbbc3235e8313d8aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856622"
---
# <a name="quickstart-for-bing-spell-check-api-with-ruby"></a><span data-ttu-id="2f18f-103">Quickstart for Bing Spell Check API with Ruby</span><span class="sxs-lookup"><span data-stu-id="2f18f-103">Quickstart for Bing Spell Check API with Ruby</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="2f18f-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with Ruby.</span><span class="sxs-lookup"><span data-stu-id="2f18f-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with Ruby.</span></span> <span data-ttu-id="2f18f-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span><span class="sxs-lookup"><span data-stu-id="2f18f-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span></span> <span data-ttu-id="2f18f-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span><span class="sxs-lookup"><span data-stu-id="2f18f-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span></span> <span data-ttu-id="2f18f-107">This article shows how to send a request that contains the text "Hollo, wrld!"</span><span class="sxs-lookup"><span data-stu-id="2f18f-107">This article shows how to send a request that contains the text "Hollo, wrld!"</span></span> <span data-ttu-id="2f18f-108">The suggested replacements are "Hello" and "world."</span><span class="sxs-lookup"><span data-stu-id="2f18f-108">The suggested replacements are "Hello" and "world."</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f18f-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f18f-109">Prerequisites</span></span>

<span data-ttu-id="2f18f-110">You will need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span><span class="sxs-lookup"><span data-stu-id="2f18f-110">You will need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.</span></span>

<span data-ttu-id="2f18f-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span><span class="sxs-lookup"><span data-stu-id="2f18f-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span></span> <span data-ttu-id="2f18f-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="2f18f-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span></span> <span data-ttu-id="2f18f-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="2f18f-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="get-spell-check-results"></a><span data-ttu-id="2f18f-114">Get Spell Check results</span><span class="sxs-lookup"><span data-stu-id="2f18f-114">Get Spell Check results</span></span>

1. <span data-ttu-id="2f18f-115">Create a new Ruby project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="2f18f-115">Create a new Ruby project in your favorite IDE.</span></span>
2. <span data-ttu-id="2f18f-116">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="2f18f-116">Add the code provided below.</span></span>
3. <span data-ttu-id="2f18f-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="2f18f-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="2f18f-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="2f18f-118">Run the program.</span></span>

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = 'https://api.cognitive.microsoft.com'
path = '/bing/v7.0/spellcheck?'
params = 'mkt=en-us&mode=proof'

uri = URI(uri + path + params)
uri.query = URI.encode_www_form({
    # Request parameters
    'text' => 'Hollo, wrld!'
})

# NOTE: Replace this example key with a valid subscription key.
key = 'ENTER KEY HERE'

# The headers in the following example 
# are optional but should be considered as required:
#
# X-MSEdge-ClientIP: 999.999.999.999  
# X-Search-Location: lat: +90.0000000000000;long: 00.0000000000000;re:100.000000000000
# X-MSEdge-ClientID: <Client ID from Previous Response Goes Here>
#
# See below for more information.

request = Net::HTTP::Post.new(uri)
request['Content-Type'] = "application/x-www-form-urlencoded"

request['Ocp-Apim-Subscription-Key'] = key

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end

result = JSON.pretty_generate(JSON.parse(response.body))
puts result
```

<span data-ttu-id="2f18f-119">**Response**</span><span class="sxs-lookup"><span data-stu-id="2f18f-119">**Response**</span></span>

<span data-ttu-id="2f18f-120">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2f18f-120">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "_type": "SpellCheck",
   "flaggedTokens": [
      {
         "offset": 0,
         "token": "Hollo",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "Hello",
               "score": 0.9115257530801
            },
            {
               "suggestion": "Hollow",
               "score": 0.858039839213461
            },
            {
               "suggestion": "Hallo",
               "score": 0.597385084464481
            }
         ]
      },
      {
         "offset": 7,
         "token": "wrld",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "world",
               "score": 0.9115257530801
            }
         ]
      }
   ]
}
```

## <a name="next-steps"></a><span data-ttu-id="2f18f-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f18f-121">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f18f-122">Bing Spell Check tutorial</span><span class="sxs-lookup"><span data-stu-id="2f18f-122">Bing Spell Check tutorial</span></span>](../tutorials/spellcheck.md)

## <a name="see-also"></a><span data-ttu-id="2f18f-123">See also</span><span class="sxs-lookup"><span data-stu-id="2f18f-123">See also</span></span>

- [<span data-ttu-id="2f18f-124">Bing Spell Check overview</span><span class="sxs-lookup"><span data-stu-id="2f18f-124">Bing Spell Check overview</span></span>](../proof-text.md)
- [<span data-ttu-id="2f18f-125">Bing Spell Check API v7 Reference</span><span class="sxs-lookup"><span data-stu-id="2f18f-125">Bing Spell Check API v7 Reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference)
