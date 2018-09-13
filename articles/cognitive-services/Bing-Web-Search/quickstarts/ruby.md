---
title: 'Quickstart: Use Ruby to call the Bing Web Search API'
description: In this quickstart, you will learn how to make your first call to the Bing Web Search API using Ruby and receive a JSON response.
services: cognitive-services
author: erhopf
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 8/16/2018
ms.author: erhopf
ms.openlocfilehash: a60bf0ef12272be3b224fdbf9f9819057fe4aa55
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870812"
---
# <a name="quickstart-use-ruby-to-call-the-bing-web-search-api"></a><span data-ttu-id="f05a5-103">Quickstart: Use Ruby to call the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="f05a5-103">Quickstart: Use Ruby to call the Bing Web Search API</span></span>  

<span data-ttu-id="f05a5-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response in less than 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="f05a5-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response in less than 10 minutes.</span></span>  

[!INCLUDE [bing-web-search-quickstart-signup](../../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="f05a5-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f05a5-105">Prerequisites</span></span>

<span data-ttu-id="f05a5-106">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="f05a5-106">Here are a few things that you'll need before running this quickstart:</span></span>

* [<span data-ttu-id="f05a5-107">Ruby 2.4 or later</span><span class="sxs-lookup"><span data-stu-id="f05a5-107">Ruby 2.4 or later</span></span>](https://www.ruby-lang.org/en/downloads/)
* <span data-ttu-id="f05a5-108">A subscription key</span><span class="sxs-lookup"><span data-stu-id="f05a5-108">A subscription key</span></span>

## <a name="create-a-project-and-declare-required-modules"></a><span data-ttu-id="f05a5-109">Create a project and declare required modules</span><span class="sxs-lookup"><span data-stu-id="f05a5-109">Create a project and declare required modules</span></span>

<span data-ttu-id="f05a5-110">Create a new Ruby project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="f05a5-110">Create a new Ruby project in your favorite IDE or editor.</span></span> <span data-ttu-id="f05a5-111">Then require `net/https` for requests, `uri` for URI handling, and `json` to parse the response.</span><span class="sxs-lookup"><span data-stu-id="f05a5-111">Then require `net/https` for requests, `uri` for URI handling, and `json` to parse the response.</span></span>

```ruby
require 'net/https'
require 'uri'
require 'json'
```

## <a name="define-variables"></a><span data-ttu-id="f05a5-112">Define variables</span><span class="sxs-lookup"><span data-stu-id="f05a5-112">Define variables</span></span>

<span data-ttu-id="f05a5-113">A few variables must be set before we can continue.</span><span class="sxs-lookup"><span data-stu-id="f05a5-113">A few variables must be set before we can continue.</span></span> <span data-ttu-id="f05a5-114">Confirm that the `$uri` and `path` are valid and replace the `accessKey` value with a valid subscription key from your Azure account.</span><span class="sxs-lookup"><span data-stu-id="f05a5-114">Confirm that the `$uri` and `path` are valid and replace the `accessKey` value with a valid subscription key from your Azure account.</span></span> <span data-ttu-id="f05a5-115">Feel free to customize the search query by replacing the value for `term`.</span><span class="sxs-lookup"><span data-stu-id="f05a5-115">Feel free to customize the search query by replacing the value for `term`.</span></span>

```ruby
accessKey = "YOUR_SUBSCRIPTION_KEY"
uri  = "https://api.cognitive.microsoft.com"
path = "/bing/v7.0/search"
term = "Microsoft Cognitive Services"

if accessKey.length != 32 then
    puts "Invalid Bing Search API subscription key!"
    puts "Please paste yours into the source code."
    abort
end
```

## <a name="make-a-request"></a><span data-ttu-id="f05a5-116">Make a request</span><span class="sxs-lookup"><span data-stu-id="f05a5-116">Make a request</span></span>

<span data-ttu-id="f05a5-117">Use this code to make a request and handle the response.</span><span class="sxs-lookup"><span data-stu-id="f05a5-117">Use this code to make a request and handle the response.</span></span>

```ruby
# Construct the endpoint uri.
uri = URI(uri + path + "?q=" + URI.escape(term))
puts "Searching the Web for: " + term

# Create the request.
request = Net::HTTP::Get.new(uri)
request['Ocp-Apim-Subscription-Key'] = accessKey

# Get the response.
response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end
```

## <a name="print-the-response"></a><span data-ttu-id="f05a5-118">Print the response</span><span class="sxs-lookup"><span data-stu-id="f05a5-118">Print the response</span></span>

<span data-ttu-id="f05a5-119">Validate the headers, format the response data as JSON, and print the results.</span><span class="sxs-lookup"><span data-stu-id="f05a5-119">Validate the headers, format the response data as JSON, and print the results.</span></span>

```ruby
puts "\nRelevant Headers:\n\n"
response.each_header do |key, value|
    # Header names are lower-cased.
    if key.start_with?("bingapis-") or key.start_with?("x-msedge-") then
        puts key + ": " + value
    end
end

puts "\nJSON Response:\n\n"
puts JSON::pretty_generate(JSON(response.body))
```

## <a name="put-it-all-together"></a><span data-ttu-id="f05a5-120">Put it all together</span><span class="sxs-lookup"><span data-stu-id="f05a5-120">Put it all together</span></span>

<span data-ttu-id="f05a5-121">The last step is to validate your code and run it!</span><span class="sxs-lookup"><span data-stu-id="f05a5-121">The last step is to validate your code and run it!</span></span> <span data-ttu-id="f05a5-122">If you'd like to compare your code with ours, here's the complete program:</span><span class="sxs-lookup"><span data-stu-id="f05a5-122">If you'd like to compare your code with ours, here's the complete program:</span></span>

```ruby
require 'net/https'
require 'uri'
require 'json'

accessKey = "enter key here"
uri  = "https://api.cognitive.microsoft.com"
path = "/bing/v7.0/search"
term = "Microsoft Cognitive Services"

if accessKey.length != 32 then
    puts "Invalid Bing Search API subscription key!"
    puts "Please paste yours into the source code."
    abort
end

uri = URI(uri + path + "?q=" + URI.escape(term))
puts "Searching the Web for: " + term

request = Net::HTTP::Get.new(uri)
request['Ocp-Apim-Subscription-Key'] = accessKey

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end

puts "\nRelevant Headers:\n\n"
response.each_header do |key, value|
    if key.start_with?("bingapis-") or key.start_with?("x-msedge-") then
        puts key + ": " + value
    end
end

puts "\nJSON Response:\n\n"
puts JSON::pretty_generate(JSON(response.body))
```

## <a name="sample-response"></a><span data-ttu-id="f05a5-123">Sample response</span><span class="sxs-lookup"><span data-stu-id="f05a5-123">Sample response</span></span>

<span data-ttu-id="f05a5-124">Responses from the Bing Web Search API are returned as JSON.</span><span class="sxs-lookup"><span data-stu-id="f05a5-124">Responses from the Bing Web Search API are returned as JSON.</span></span> <span data-ttu-id="f05a5-125">This sample response has been truncated to show a single result.</span><span class="sxs-lookup"><span data-stu-id="f05a5-125">This sample response has been truncated to show a single result.</span></span>

```json
{
  "_type": "SearchResponse",
  "queryContext": {
    "originalQuery": "Microsoft Cognitive Services"
  },
  "webPages": {
    "webSearchUrl": "https://www.bing.com/search?q=Microsoft+cognitive+services",
    "totalEstimatedMatches": 22300000,
    "value": [
      {
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.0",
        "name": "Microsoft Cognitive Services",
        "url": "https://www.microsoft.com/cognitive-services",
        "displayUrl": "https://www.microsoft.com/cognitive-services",
        "snippet": "Knock down barriers between you and your ideas. Enable natural and contextual interaction with tools that augment users' experiences via the power of machine-based AI. Plug them in and bring your ideas to life.",
        "deepLinks": [
          {
            "name": "Face API",
            "url": "https://azure.microsoft.com/services/cognitive-services/face/",
            "snippet": "Add facial recognition to your applications to detect, identify, and verify faces using a Face API from Microsoft Azure. ... Cognitive Services; Face API;"
          },
          {
            "name": "Text Analytics",
            "url": "https://azure.microsoft.com/services/cognitive-services/text-analytics/",
            "snippet": "Cognitive Services; Text Analytics API; Text Analytics API . Detect sentiment, ... you agree that Microsoft may store it and use it to improve Microsoft services, ..."
          },
          {
            "name": "Computer Vision API",
            "url": "https://azure.microsoft.com/services/cognitive-services/computer-vision/",
            "snippet": "Extract the data you need from images using optical character recognition and image analytics with Computer Vision APIs from Microsoft Azure."
          },
          {
            "name": "Emotion",
            "url": "https://www.microsoft.com/cognitive-services/en-us/emotion-api",
            "snippet": "Cognitive Services Emotion API - microsoft.com"
          },
          {
            "name": "Bing Speech API",
            "url": "https://azure.microsoft.com/services/cognitive-services/speech/",
            "snippet": "Add speech recognition to your applications, including text to speech, with a speech API from Microsoft Azure. ... Cognitive Services; Bing Speech API;"
          },
          {
            "name": "Get Started for Free",
            "url": "https://azure.microsoft.com/services/cognitive-services/",
            "snippet": "Add vision, speech, language, and knowledge capabilities to your applications using intelligence APIs and SDKs from Cognitive Services."
          }
        ]
      }
    ]
  },
  "relatedSearches": {
    "id": "https://api.cognitive.microsoft.com/api/v7/#RelatedSearches",
    "value": [
      {
        "text": "microsoft bot framework",
        "displayText": "microsoft bot framework",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+bot+framework"
      },
      {
        "text": "microsoft cognitive services youtube",
        "displayText": "microsoft cognitive services youtube",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+youtube"
      },
      {
        "text": "microsoft cognitive services search api",
        "displayText": "microsoft cognitive services search api",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+search+api"
      },
      {
        "text": "microsoft cognitive services news",
        "displayText": "microsoft cognitive services news",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+news"
      },
      {
        "text": "ms cognitive service",
        "displayText": "ms cognitive service",
        "webSearchUrl": "https://www.bing.com/search?q=ms+cognitive+service"
      },
      {
        "text": "microsoft cognitive services text analytics",
        "displayText": "microsoft cognitive services text analytics",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+text+analytics"
      },
      {
        "text": "microsoft cognitive services toolkit",
        "displayText": "microsoft cognitive services toolkit",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+toolkit"
      },
      {
        "text": "microsoft cognitive services api",
        "displayText": "microsoft cognitive services api",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+api"
      }
    ]
  },
  "rankingResponse": {
    "mainline": {
      "items": [
        {
          "answerType": "WebPages",
          "resultIndex": 0,
          "value": {
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.0"
          }
        }
      ]
    },
    "sidebar": {
      "items": [
        {
          "answerType": "RelatedSearches",
          "value": {
            "id": "https://api.cognitive.microsoft.com/api/v7/#RelatedSearches"
          }
        }
      ]
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="f05a5-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="f05a5-126">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f05a5-127">Bing Web search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="f05a5-127">Bing Web search single-page app tutorial</span></span>](../tutorial-bing-web-search-single-page-app.md)

[!INCLUDE [bing-web-search-quickstart-see-also](../../../../includes/bing-web-search-quickstart-see-also.md)]
