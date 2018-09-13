---
title: PHP Quickstart for Azure Cognitive Services, Bing Entity Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Entity Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 11/28/2017
ms.author: v-jaswel
ms.openlocfilehash: 448064de764775c497de467b235837d66ef7093b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968667"
---
# <a name="quickstart-for-microsoft-bing-entity-search-api-with-php"></a><span data-ttu-id="c3220-103">Quickstart for Microsoft Bing Entity Search API with PHP</span><span class="sxs-lookup"><span data-stu-id="c3220-103">Quickstart for Microsoft Bing Entity Search API with PHP</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="c3220-104">This article shows you how to use the [Bing Entity Search](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web) API with PHP.</span><span class="sxs-lookup"><span data-stu-id="c3220-104">This article shows you how to use the [Bing Entity Search](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web) API with PHP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3220-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c3220-105">Prerequisites</span></span>

<span data-ttu-id="c3220-106">You will need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span><span class="sxs-lookup"><span data-stu-id="c3220-106">You will need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span></span>

<span data-ttu-id="c3220-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Entity Search API**.</span><span class="sxs-lookup"><span data-stu-id="c3220-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Entity Search API**.</span></span> <span data-ttu-id="c3220-108">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-entity-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="c3220-108">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-entity-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="c3220-109">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="c3220-109">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="search-entities"></a><span data-ttu-id="c3220-110">Search entities</span><span class="sxs-lookup"><span data-stu-id="c3220-110">Search entities</span></span>

<span data-ttu-id="c3220-111">To run this application, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="c3220-111">To run this application, follow these steps.</span></span>

1. <span data-ttu-id="c3220-112">Create a new PHP project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="c3220-112">Create a new PHP project in your favorite IDE.</span></span>
2. <span data-ttu-id="c3220-113">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="c3220-113">Add the code provided below.</span></span>
3. <span data-ttu-id="c3220-114">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="c3220-114">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="c3220-115">Run the program.</span><span class="sxs-lookup"><span data-stu-id="c3220-115">Run the program.</span></span>

```php
<?php

// NOTE: Be sure to uncomment the following line in your php.ini file.
// ;extension=php_openssl.dll

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
$subscriptionKey = 'ENTER KEY HERE';

$host = "https://api.cognitive.microsoft.com";
$path = "/bing/v7.0/entities";

$mkt = "en-US";
$query = "italian restaurants near me";

function search ($host, $path, $key, $mkt, $query) {

    $params = '?mkt=' . $mkt . '&q=' . urlencode ($query);

    $headers = "Ocp-Apim-Subscription-Key: $key\r\n";

    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $options = array (
        'http' => array (
            'header' => $headers,
            'method' => 'GET'
        )
    );
    $context  = stream_context_create ($options);
    $result = file_get_contents ($host . $path . $params, false, $context);
    return $result;
}

$result = search ($host, $path, $subscriptionKey, $mkt, $query);

echo json_encode (json_decode ($result), JSON_PRETTY_PRINT);
?>
```

<span data-ttu-id="c3220-116">**Response**</span><span class="sxs-lookup"><span data-stu-id="c3220-116">**Response**</span></span>

<span data-ttu-id="c3220-117">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c3220-117">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "_type": "SearchResponse",
  "queryContext": {
    "originalQuery": "italian restaurant near me",
    "askUserForLocation": true
  },
  "places": {
    "value": [
      {
        "_type": "LocalBusiness",
        "webSearchUrl": "https://www.bing.com/search?q=sinful+bakery&filters=local...",
        "name": "Liberty's Delightful Sinful Bakery & Cafe",
        "url": "https://www.contoso.com/",
        "entityPresentationInfo": {
          "entityScenario": "ListItem",
          "entityTypeHints": [
            "Place",
            "LocalBusiness"
          ]
        },
        "address": {
          "addressLocality": "Seattle",
          "addressRegion": "WA",
          "postalCode": "98112",
          "addressCountry": "US",
          "neighborhood": "Madison Park"
        },
        "telephone": "(800) 555-1212"
      },

      . . .
      {
        "_type": "Restaurant",
        "webSearchUrl": "https://www.bing.com/search?q=Pickles+and+Preserves...",
        "name": "Munson's Pickles and Preserves Farm",
        "url": "http://www.princi.com/",
        "entityPresentationInfo": {
          "entityScenario": "ListItem",
          "entityTypeHints": [
            "Place",
            "LocalBusiness",
            "Restaurant"
          ]
        },
        "address": {
          "addressLocality": "Seattle",
          "addressRegion": "WA",
          "postalCode": "98101",
          "addressCountry": "US",
          "neighborhood": "Capitol Hill"
        },
        "telephone": "(800) 555-1212"
      },
      
      . . .
    ]
  }
}
```

[<span data-ttu-id="c3220-118">Back to top</span><span class="sxs-lookup"><span data-stu-id="c3220-118">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="c3220-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3220-119">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="c3220-120">[Bing Entity Search tutorial](../tutorial-bing-entities-search-single-page-app.md)
> [Bing Entity Search overview](../search-the-web.md )
> [API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)</span><span class="sxs-lookup"><span data-stu-id="c3220-120">[Bing Entity Search tutorial](../tutorial-bing-entities-search-single-page-app.md)
[Bing Entity Search overview](../search-the-web.md )
[API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)</span></span>
