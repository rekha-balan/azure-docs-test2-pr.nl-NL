---
title: PHP Quickstart for Azure Cognitive Services, Bing News Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing News Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: a1e62a63ec926b77bca290767ee453cde83de3df
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866461"
---
# <a name="quickstart-for-bing-news-search-api-with-php"></a><span data-ttu-id="a8f91-103">Quickstart for Bing News Search API with PHP</span><span class="sxs-lookup"><span data-stu-id="a8f91-103">Quickstart for Bing News Search API with PHP</span></span>

<span data-ttu-id="a8f91-104">This article shows you how use the Bing News Search API, part of Microsoft Cognitive Services on Azure.</span><span class="sxs-lookup"><span data-stu-id="a8f91-104">This article shows you how use the Bing News Search API, part of Microsoft Cognitive Services on Azure.</span></span> <span data-ttu-id="a8f91-105">While this article employs PHP, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="a8f91-105">While this article employs PHP, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

<span data-ttu-id="a8f91-106">The example code was written to work under PHP 5.6.</span><span class="sxs-lookup"><span data-stu-id="a8f91-106">The example code was written to work under PHP 5.6.</span></span>

<span data-ttu-id="a8f91-107">Refer to the [API reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference) for technical details about the APIs.</span><span class="sxs-lookup"><span data-stu-id="a8f91-107">Refer to the [API reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference) for technical details about the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8f91-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8f91-108">Prerequisites</span></span>

<span data-ttu-id="a8f91-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="a8f91-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="a8f91-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a8f91-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="a8f91-111">You will need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="a8f91-111">You will need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="bing-news-search"></a><span data-ttu-id="a8f91-112">Bing News search</span><span class="sxs-lookup"><span data-stu-id="a8f91-112">Bing News search</span></span>

<span data-ttu-id="a8f91-113">The [Bing News Search API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference) returns news results from the Bing search engine.</span><span class="sxs-lookup"><span data-stu-id="a8f91-113">The [Bing News Search API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference) returns news results from the Bing search engine.</span></span>

1. <span data-ttu-id="a8f91-114">Make sure secure HTTP support is enabled in your `php.ini` as described in the code comment.</span><span class="sxs-lookup"><span data-stu-id="a8f91-114">Make sure secure HTTP support is enabled in your `php.ini` as described in the code comment.</span></span>
2. <span data-ttu-id="a8f91-115">Create a new PHP project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="a8f91-115">Create a new PHP project in your favorite IDE or editor.</span></span>
3. <span data-ttu-id="a8f91-116">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a8f91-116">Add the code provided below.</span></span>
4. <span data-ttu-id="a8f91-117">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a8f91-117">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
5. <span data-ttu-id="a8f91-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a8f91-118">Run the program.</span></span>

```php
<?php

// NOTE: Be sure to uncomment the following line in your php.ini file.
// ;extension=php_openssl.dll

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the accessKey string value with your valid access key.
$accessKey = 'enter key here';

// Verify the endpoint URI.  At this writing, only one endpoint is used for Bing
// search APIs.  In the future, regional endpoints may be available.  If you
// encounter unexpected authorization errors, double-check this value against
// the endpoint for your Bing Search instance in your Azure dashboard.
$endpoint = 'https://api.cognitive.microsoft.com/bing/v7.0/news/search';

$term = 'Microsoft';

function BingNewsSearch ($url, $key, $query) {
    // Prepare HTTP request
    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $headers = "Ocp-Apim-Subscription-Key: $key\r\n";
    $options = array ('http' => array (
                          'header' => $headers,
                          'method' => 'GET' ));

    // Perform the Web request and get the JSON response
    $context = stream_context_create($options);
    $result = file_get_contents($url . "?q=" . urlencode($query), false, $context);

    // Extract Bing HTTP headers
    $headers = array();
    foreach ($http_response_header as $k => $v) {
        $h = explode(":", $v, 2);
        if (isset($h[1]))
            if (preg_match("/^BingAPIs-/", $h[0]) || preg_match("/^X-MSEdge-/", $h[0]))
                $headers[trim($h[0])] = trim($h[1]);
    }

    return array($headers, $result);
}

print "Searching news for: " . $term . "\n";

list($headers, $json) = BingNewsSearch($endpoint, $accessKey, $term);

print "\nRelevant Headers:\n\n";
foreach ($headers as $k => $v) {
    print $k . ": " . $v . "\n";
}

print "\nJSON Response:\n\n";
echo json_encode(json_decode($json), JSON_PRETTY_PRINT);
?>
```

<span data-ttu-id="a8f91-119">**Response**</span><span class="sxs-lookup"><span data-stu-id="a8f91-119">**Response**</span></span>

<span data-ttu-id="a8f91-120">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a8f91-120">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "_type": "News",
   "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft",
   "totalEstimatedMatches": 36,
   "sort": [
      {
         "name": "Best match",
         "id": "relevance",
         "isSelected": true,
         "url": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft"
      },
      {
         "name": "Most recent",
         "id": "date",
         "isSelected": false,
         "url": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft&sortby=date"
      }
   ],
   "value": [
      {
         "name": "Microsoft to open flagship London brick-and-mortar retail store",
         "url": "http:\/\/www.contoso.com\/article\/microsoft-to-open-flagshi...",
         "image": {
            "thumbnail": {
               "contentUrl": "https:\/\/www.bing.com\/th?id=ON.F9E4A49EC010417...",
               "width": 220,
               "height": 146
            }
         },
         "description": "After years of rumors about Microsoft opening a brick-and-mortar...", 
         "about": [
           {
             "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entiti...", 
             "name": "Microsoft"
           }, 
           {
             "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entit...", 
             "name": "London"
           }
         ], 
         "provider": [
           {
             "_type": "Organization", 
             "name": "Contoso"
           }
         ], 
          "datePublished": "2017-09-21T21:16:00.0000000Z", 
          "category": "ScienceAndTechnology"
      }, 

      . . .
      
      {
         "name": "Microsoft adds Availability Zones to its Azure cloud platform",
         "url": "https:\/\/contoso.com\/2017\/09\/21\/microsoft-adds-availability...",
         "image": {
            "thumbnail": {
               "contentUrl": "https:\/\/www.bing.com\/th?id=ON.0AE7595B9720...",
               "width": 700,
               "height": 466
            }
         },
         "description": "Microsoft has begun adding Availability Zones to its...",
         "about": [
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/a093e9b...",
               "name": "Microsoft"
            },
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/cf3abf7d-e379-...",
               "name": "Windows Azure"
            },
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/9cdd061c-1fae-d0...",
               "name": "Cloud"
            }
         ],
         "provider": [
            {
               "_type": "Organization",
               "name": "Contoso"
            }
         ],
         "datePublished": "2017-09-21T09:01:00.0000000Z",
         "category": "ScienceAndTechnology"
      }
   ]
}
```

## <a name="next-steps"></a><span data-ttu-id="a8f91-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8f91-121">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="a8f91-122">[Paging news](paging-news.md)
> [Using decoration markers to highlight text](hit-highlighting.md)
> [Searching the web for news](search-the-web.md)</span><span class="sxs-lookup"><span data-stu-id="a8f91-122">[Paging news](paging-news.md)
> [Using decoration markers to highlight text](hit-highlighting.md)
[Searching the web for news](search-the-web.md)</span></span>  
[<span data-ttu-id="a8f91-123">Try it</span><span class="sxs-lookup"><span data-stu-id="a8f91-123">Try it</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/)

