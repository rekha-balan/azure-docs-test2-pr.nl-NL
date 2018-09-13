---
title: 'Quickstart: Send search queries using the REST API for the Bing Image Search API using PHP'
description: In this quickstart, you send search queries to the Bing Search API to get a list of relevant images using PHP.
services: cognitive-services
documentationcenter: ''
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: d91021c4bd5e0f78e518811f3794055b397c1a39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865414"
---
# <a name="quickstart-send-search-queries-using-the-rest-api-and-php"></a><span data-ttu-id="6c8fb-103">Quickstart: Send search queries using the REST API and PHP</span><span class="sxs-lookup"><span data-stu-id="6c8fb-103">Quickstart: Send search queries using the REST API and PHP</span></span>

<span data-ttu-id="6c8fb-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span></span>

<span data-ttu-id="6c8fb-105">This article includes a simple console application that performs a Bing Image Search API query and displays the returned raw search results, which are in JSON format.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-105">This article includes a simple console application that performs a Bing Image Search API query and displays the returned raw search results, which are in JSON format.</span></span> <span data-ttu-id="6c8fb-106">While this application is written in PHP, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-106">While this application is written in PHP, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6c8fb-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c8fb-107">Prerequisites</span></span>

<span data-ttu-id="6c8fb-108">You need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-108">You need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span></span>

[!INCLUDE [cognitive-services-bing-image-search-signup-requirements](../../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

## <a name="running-the-application"></a><span data-ttu-id="6c8fb-109">Running the application</span><span class="sxs-lookup"><span data-stu-id="6c8fb-109">Running the application</span></span>

<span data-ttu-id="6c8fb-110">To run this application, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-110">To run this application, follow these steps.</span></span>

1. <span data-ttu-id="6c8fb-111">Make sure secure HTTP support is enabled in your `php.ini` as described in the code comment.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-111">Make sure secure HTTP support is enabled in your `php.ini` as described in the code comment.</span></span> <span data-ttu-id="6c8fb-112">On Windows, this file is in `C:\windows`.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-112">On Windows, this file is in `C:\windows`.</span></span>
2. <span data-ttu-id="6c8fb-113">Create a new PHP project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-113">Create a new PHP project in your favorite IDE or editor.</span></span>
3. <span data-ttu-id="6c8fb-114">Add the provided code.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-114">Add the provided code.</span></span>
4. <span data-ttu-id="6c8fb-115">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-115">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
5. <span data-ttu-id="6c8fb-116">Run the program.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-116">Run the program.</span></span>

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
$endpoint = 'https://api.cognitive.microsoft.com/bing/v7.0/images/search';

$term = 'puppies';

function BingImageSearch ($url, $key, $query) {
    // Prepare HTTP request
    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $headers = "Ocp-Apim-Subscription-Key: $key\r\n";
    $options = array ( 'http' => array (
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

if (strlen($accessKey) == 32) {

    print "Searching images for: " . $term . "\n";
    
    list($headers, $json) = BingImageSearch($endpoint, $accessKey, $term);
    
    print "\nRelevant Headers:\n\n";
    foreach ($headers as $k => $v) {
        print $k . ": " . $v . "\n";
    }
    
    print "\nJSON Response:\n\n";
    echo json_encode(json_decode($json), JSON_PRETTY_PRINT);

} else {

    print("Invalid Bing Search API subscription key!\n");
    print("Please paste yours into the source code.\n");

}
?>
```

## <a name="json-response"></a><span data-ttu-id="6c8fb-117">JSON response</span><span class="sxs-lookup"><span data-stu-id="6c8fb-117">JSON response</span></span>

<span data-ttu-id="6c8fb-118">A sample response follows.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-118">A sample response follows.</span></span> <span data-ttu-id="6c8fb-119">To limit the length of the JSON, only a single result is shown, and other parts of the response have been truncated.</span><span class="sxs-lookup"><span data-stu-id="6c8fb-119">To limit the length of the JSON, only a single result is shown, and other parts of the response have been truncated.</span></span> 

```json
{
  "_type": "Images",
  "instrumentation": {},
  "readLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=puppies",
  "webSearchUrl": "https://www.bing.com/images/search?q=puppies&FORM=OIIARP",
  "totalEstimatedMatches": 955,
  "nextOffset": 1,
  "value": [
    {
      "webSearchUrl": "https://www.bing.com/images/search?view=detailv...",
      "name": "So cute - Puppies Wallpaper",
      "thumbnailUrl": "https://tse3.mm.bing.net/th?id=OIP.jHrihoDNkXGS1t...",
      "datePublished": "2014-02-01T21:55:00.0000000Z",
      "contentUrl": "http://images4.contoso.com/image/photos/14700000/So-cute-puppies...",
      "hostPageUrl": "http://www.contoso.com/clubs/puppies/images/14749028/...",
      "contentSize": "394455 B",
      "encodingFormat": "jpeg",
      "hostPageDisplayUrl": "www.contoso.com/clubs/puppies/images/14749...",
      "width": 1600,
      "height": 1200,
      "thumbnail": {
        "width": 300,
        "height": 225
      },
      "imageInsightsToken": "ccid_jHrihoDN*mid_F68CC526226E163FD1EA659747AD...",
      "insightsMetadata": {
        "recipeSourcesCount": 0
      },
      "imageId": "F68CC526226E163FD1EA659747ADCB8F9FA36",
      "accentColor": "8D613E"
    }
  ],
  "queryExpansions": [
    {
      "text": "Shih Tzu Puppies",
      "displayText": "Shih Tzu",
      "webSearchUrl": "https://www.bing.com/images/search?q=Shih+Tzu+Puppies...",
      "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=Shih...",
      "thumbnail": {
        "thumbnailUrl": "https://tse2.mm.bing.net/th?q=Shih+Tzu+Puppies&pid=Api..."
      }
    }
  ],
  "pivotSuggestions": [
    {
      "pivot": "puppies",
      "suggestions": [
        {
          "text": "Dog",
          "displayText": "Dog",
          "webSearchUrl": "https://www.bing.com/images/search?q=Dog&tq=%7b%22pq%...",
          "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=Dog...",
          "thumbnail": {
            "thumbnailUrl": "https://tse1.mm.bing.net/th?q=Dog&pid=Api&mkt=en-US..."
          }
        }
      ]
    }
  ],
  "similarTerms": [
    {
      "text": "cute",
      "displayText": "cute",
      "webSearchUrl": "https://www.bing.com/images/search?q=cute&FORM=...",
      "thumbnail": {
        "url": "https://tse2.mm.bing.net/th?q=cute&pid=Api&mkt=en-US..."
      }
    }
  ],
  "relatedSearches": [
    {
      "text": "Cute Puppies",
      "displayText": "Cute Puppies",
      "webSearchUrl": "https://www.bing.com/images/search?q=Cute+Puppies",
      "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/sear...",
      "thumbnail": {
        "thumbnailUrl": "https://tse4.mm.bing.net/th?q=Cute+Puppies&pid=..."
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="6c8fb-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c8fb-120">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6c8fb-121">Bing Image Search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="6c8fb-121">Bing Image Search single-page app tutorial</span></span>](../tutorial-bing-image-search-single-page-app.md)

## <a name="see-also"></a><span data-ttu-id="6c8fb-122">See also</span><span class="sxs-lookup"><span data-stu-id="6c8fb-122">See also</span></span> 

[<span data-ttu-id="6c8fb-123">Bing Image Search overview</span><span class="sxs-lookup"><span data-stu-id="6c8fb-123">Bing Image Search overview</span></span>](../overview.md)  
[<span data-ttu-id="6c8fb-124">Try it</span><span class="sxs-lookup"><span data-stu-id="6c8fb-124">Try it</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/)  
[<span data-ttu-id="6c8fb-125">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="6c8fb-125">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api)  
[<span data-ttu-id="6c8fb-126">Bing Image Search API reference</span><span class="sxs-lookup"><span data-stu-id="6c8fb-126">Bing Image Search API reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)
