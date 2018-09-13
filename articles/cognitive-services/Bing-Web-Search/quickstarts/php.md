---
title: 'Quickstart: Use PHP to call the Bing Web Search API'
description: In this quickstart, you will learn how to make your first call to the Bing Web Search API using PHP and receive a JSON response.
services: cognitive-services
author: erhopf
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 8/16/2018
ms.author: erhopf
ms.openlocfilehash: ef5263ce65efccdab0fb461165e66156dd4fce52
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871409"
---
# <a name="quickstart-use-php-to-call-the-bing-web-search-api"></a><span data-ttu-id="328b8-103">Quickstart: Use PHP to call the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="328b8-103">Quickstart: Use PHP to call the Bing Web Search API</span></span>  

<span data-ttu-id="328b8-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response in less than 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="328b8-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response in less than 10 minutes.</span></span>  

[!INCLUDE [bing-web-search-quickstart-signup](../../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="328b8-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="328b8-105">Prerequisites</span></span>

<span data-ttu-id="328b8-106">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="328b8-106">Here are a few things that you'll need before running this quickstart:</span></span>

* <span data-ttu-id="328b8-107">[PHP 5.6.x](http://php.net/downloads.php) or later</span><span class="sxs-lookup"><span data-stu-id="328b8-107">[PHP 5.6.x](http://php.net/downloads.php) or later</span></span>
* <span data-ttu-id="328b8-108">A subscription key</span><span class="sxs-lookup"><span data-stu-id="328b8-108">A subscription key</span></span>  

## <a name="enable-secure-http-support"></a><span data-ttu-id="328b8-109">Enable secure HTTP support</span><span class="sxs-lookup"><span data-stu-id="328b8-109">Enable secure HTTP support</span></span>

<span data-ttu-id="328b8-110">Before we get started, locate `php.ini` and uncomment this line:</span><span class="sxs-lookup"><span data-stu-id="328b8-110">Before we get started, locate `php.ini` and uncomment this line:</span></span>

```
;extension=php_openssl.dll
```

## <a name="create-a-project-and-define-variables"></a><span data-ttu-id="328b8-111">Create a project and define variables</span><span class="sxs-lookup"><span data-stu-id="328b8-111">Create a project and define variables</span></span>  

<span data-ttu-id="328b8-112">Create a new PHP project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="328b8-112">Create a new PHP project in your favorite IDE or editor.</span></span> <span data-ttu-id="328b8-113">Don't forget to add opening and closing tags `<?php` and `?>`.</span><span class="sxs-lookup"><span data-stu-id="328b8-113">Don't forget to add opening and closing tags `<?php` and `?>`.</span></span>

<span data-ttu-id="328b8-114">A few variables must be set before we can continue.</span><span class="sxs-lookup"><span data-stu-id="328b8-114">A few variables must be set before we can continue.</span></span> <span data-ttu-id="328b8-115">Confirm that the `$endpoint` is correct and replace the `$accesskey` value with a valid subscription key from your Azure account.</span><span class="sxs-lookup"><span data-stu-id="328b8-115">Confirm that the `$endpoint` is correct and replace the `$accesskey` value with a valid subscription key from your Azure account.</span></span> <span data-ttu-id="328b8-116">Feel free to customize the search query by replacing the value for `$term`.</span><span class="sxs-lookup"><span data-stu-id="328b8-116">Feel free to customize the search query by replacing the value for `$term`.</span></span>

```php
$accessKey = 'enter key here';
$endpoint = 'https://api.cognitive.microsoft.com/bing/v7.0/search';
$term = 'Microsoft Cognitive Services';
```

## <a name="construct-a-request"></a><span data-ttu-id="328b8-117">Construct a request</span><span class="sxs-lookup"><span data-stu-id="328b8-117">Construct a request</span></span>

<span data-ttu-id="328b8-118">This code declares a function called `BingWebSearch` that is used to construct requests to the Bing Web Search API.</span><span class="sxs-lookup"><span data-stu-id="328b8-118">This code declares a function called `BingWebSearch` that is used to construct requests to the Bing Web Search API.</span></span> <span data-ttu-id="328b8-119">It takes three arguments: `$url`, `$key`, and `$query`.</span><span class="sxs-lookup"><span data-stu-id="328b8-119">It takes three arguments: `$url`, `$key`, and `$query`.</span></span>

```php
function BingWebSearch ($url, $key, $query) {
    /* Prepare the HTTP request.
     * NOTE: Use the key 'http' even if you are making an HTTPS request.
     * See: http://php.net/manual/en/function.stream-context-create.php.
     */
    $headers = "Ocp-Apim-Subscription-Key: $key\r\n";
    $options = array ('http' => array (
                          'header' => $headers,
                           'method' => 'GET'));

    // Perform the request and get a JSON response.
    $context = stream_context_create($options);
    $result = file_get_contents($url . "?q=" . urlencode($query), false, $context);

    // Extract Bing HTTP headers.
    $headers = array();
    foreach ($http_response_header as $k => $v) {
        $h = explode(":", $v, 2);
        if (isset($h[1]))
            if (preg_match("/^BingAPIs-/", $h[0]) || preg_match("/^X-MSEdge-/", $h[0]))
                $headers[trim($h[0])] = trim($h[1]);
    }

    return array($headers, $result);
}
```

## <a name="make-a-request-and-print-the-response"></a><span data-ttu-id="328b8-120">Make a request and print the response</span><span class="sxs-lookup"><span data-stu-id="328b8-120">Make a request and print the response</span></span>

<span data-ttu-id="328b8-121">This code validates the subscription key, makes a request, and prints the response.</span><span class="sxs-lookup"><span data-stu-id="328b8-121">This code validates the subscription key, makes a request, and prints the response.</span></span>

```php
// Validates the subscription key.
if (strlen($accessKey) == 32) {

    print "Searching the Web for: " . $term . "\n";
    // Makes the request.
    list($headers, $json) = BingWebSearch($endpoint, $accessKey, $term);

    print "\nRelevant Headers:\n\n";
    foreach ($headers as $k => $v) {
        print $k . ": " . $v . "\n";
    }
    // Prints JSON encoded response.
    print "\nJSON Response:\n\n";
    echo json_encode(json_decode($json), JSON_PRETTY_PRINT);

} else {

    print("Invalid Bing Search API subscription key!\n");
    print("Please paste yours into the source code.\n");

}
```

## <a name="put-it-all-together"></a><span data-ttu-id="328b8-122">Put it all together</span><span class="sxs-lookup"><span data-stu-id="328b8-122">Put it all together</span></span>

<span data-ttu-id="328b8-123">The last step is to validate your code and run it!</span><span class="sxs-lookup"><span data-stu-id="328b8-123">The last step is to validate your code and run it!</span></span> <span data-ttu-id="328b8-124">If you'd like to compare your code with ours, here's the complete program:</span><span class="sxs-lookup"><span data-stu-id="328b8-124">If you'd like to compare your code with ours, here's the complete program:</span></span>

```php
<?php
$accessKey = 'enter key here';
$endpoint = 'https://api.cognitive.microsoft.com/bing/v7.0/search';
$term = 'Microsoft Cognitive Services';

function BingWebSearch ($url, $key, $query) {
    $headers = "Ocp-Apim-Subscription-Key: $key\r\n";
    $options = array ('http' => array (
                          'header' => $headers,
                           'method' => 'GET'));
    $context = stream_context_create($options);
    $result = file_get_contents($url . "?q=" . urlencode($query), false, $context);
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
    print "Searching the Web for: " . $term . "\n";
    list($headers, $json) = BingWebSearch($endpoint, $accessKey, $term);
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

## <a name="sample-response"></a><span data-ttu-id="328b8-125">Sample response</span><span class="sxs-lookup"><span data-stu-id="328b8-125">Sample response</span></span>

<span data-ttu-id="328b8-126">Responses from the Bing Web Search API are returned as JSON.</span><span class="sxs-lookup"><span data-stu-id="328b8-126">Responses from the Bing Web Search API are returned as JSON.</span></span> <span data-ttu-id="328b8-127">This sample response has been truncated to show a single result.</span><span class="sxs-lookup"><span data-stu-id="328b8-127">This sample response has been truncated to show a single result.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="328b8-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="328b8-128">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="328b8-129">Bing Web search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="328b8-129">Bing Web search single-page app tutorial</span></span>](../tutorial-bing-web-search-single-page-app.md)

[!INCLUDE [bing-web-search-quickstart-see-also](../../../../includes/bing-web-search-quickstart-see-also.md)]
