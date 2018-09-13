---
title: Quickstart for Bing Autosuggest API with PHP | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Autosuggest API in Azure Cognitive Services.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-autosuggest
ms.topic: article
ms.date: 09/14/2017
ms.author: v-jaswel
ms.openlocfilehash: 2a1a79d9868c577fa13fe8299421e7fbc99952af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856679"
---
# <a name="quickstart-for-bing-autosuggest-api-with-php"></a><span data-ttu-id="2d2f7-103">Quickstart for Bing Autosuggest API with PHP</span><span class="sxs-lookup"><span data-stu-id="2d2f7-103">Quickstart for Bing Autosuggest API with PHP</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="2d2f7-104">This article shows you how to use the [Bing Autosuggest API](https://azure.microsoft.com/services/cognitive-services/autosuggest/) with PHP.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-104">This article shows you how to use the [Bing Autosuggest API](https://azure.microsoft.com/services/cognitive-services/autosuggest/) with PHP.</span></span> <span data-ttu-id="2d2f7-105">The Bing Autosuggest API returns a list of suggested queries based on the partial query string the user enters in the search box.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-105">The Bing Autosuggest API returns a list of suggested queries based on the partial query string the user enters in the search box.</span></span> <span data-ttu-id="2d2f7-106">Typically, you would call this API each time the user types a new character in the search box, and then display the suggestions in the search box's drop down list.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-106">Typically, you would call this API each time the user types a new character in the search box, and then display the suggestions in the search box's drop down list.</span></span> <span data-ttu-id="2d2f7-107">This article shows how to send a request that returns the suggested query strings for *sail*.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-107">This article shows how to send a request that returns the suggested query strings for *sail*.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d2f7-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d2f7-108">Prerequisites</span></span>

<span data-ttu-id="2d2f7-109">You will need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-109">You will need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span></span>

<span data-ttu-id="2d2f7-110">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Autosuggest API v7**.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-110">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Autosuggest API v7**.</span></span> <span data-ttu-id="2d2f7-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/#search) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/#search) is sufficient for this quickstart.</span></span> <span data-ttu-id="2d2f7-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="get-autosuggest-results"></a><span data-ttu-id="2d2f7-113">Get Autosuggest results</span><span class="sxs-lookup"><span data-stu-id="2d2f7-113">Get Autosuggest results</span></span>

1. <span data-ttu-id="2d2f7-114">Create a new PHP project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-114">Create a new PHP project in your favorite IDE.</span></span>
2. <span data-ttu-id="2d2f7-115">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-115">Add the code provided below.</span></span>
3. <span data-ttu-id="2d2f7-116">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-116">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="2d2f7-117">Run the program.</span><span class="sxs-lookup"><span data-stu-id="2d2f7-117">Run the program.</span></span>

```php
<?php

// NOTE: Be sure to uncomment the following line in your php.ini file.
// ;extension=php_openssl.dll

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
$subscriptionKey = 'enter key here';

$host = "https://api.cognitive.microsoft.com";
$path = "/bing/v7.0/Suggestions";

$mkt = "en-US";
$query = "sail";

function get_suggestions ($host, $path, $key, $mkt, $query) {

  $params = '?mkt=' . $mkt . '&q=' . $query;

  $headers = "Content-type: text/json\r\n" .
    "Ocp-Apim-Subscription-Key: $key\r\n";

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

$result = get_suggestions ($host, $path, $subscriptionKey, $mkt, $query);

echo json_encode (json_decode ($result), JSON_PRETTY_PRINT);
?>
```

### <a name="response"></a><span data-ttu-id="2d2f7-118">Response</span><span class="sxs-lookup"><span data-stu-id="2d2f7-118">Response</span></span>

<span data-ttu-id="2d2f7-119">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2d2f7-119">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "_type": "Suggestions",
  "queryContext": {
    "originalQuery": "sail"
  },
  "suggestionGroups": [
    {
      "name": "Web",
      "searchSuggestions": [
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dgvtP9TS9NwhajSapY2Se6y1eCbP2fq_GiP2n-cxi6OY\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailrite%26FORM%3dUSBAPI\u0026p\u003dDevEx,5003.1",
          "displayText": "sailrite",
          "query": "sailrite",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dBTS0G6AakxntIl9rmbDXtk1n6rQpsZZ99aQ7ClE7dTY\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsail%2bsand%2bpoint%26FORM%3dUSBAPI\u0026p\u003dDevEx,5004.1",
          "displayText": "sail sand point",
          "query": "sail sand point",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dc0QOA_j6swCZJy9FxqOwke2KslJE7ZRmMooGClAuCpY\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailboats%2bfor%2bsale%26FORM%3dUSBAPI\u0026p\u003dDevEx,5005.1",
          "displayText": "sailboats for sale",
          "query": "sailboats for sale",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dmnMdREUH20SepmHQH1zlh9Hy_w7jpOlZFm3KG2R_BoA\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailing%2banarchy%26FORM%3dUSBAPI\u0026p\u003dDevEx,5006.1",
          "displayText": "sailing anarchy",
          "query": "sailing anarchy",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dWLFO-B1GG5qtBGnoU1Bizz02YKkg5fgAQtHwhXn4z8I\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailpoint%26FORM%3dUSBAPI\u0026p\u003dDevEx,5007.1",
          "displayText": "sailpoint",
          "query": "sailpoint",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dquBMwmKlGwqC5wAU0K7n416plhWcR8zQCi7r-Fw9Y0w\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailflow%26FORM%3dUSBAPI\u0026p\u003dDevEx,5008.1",
          "displayText": "sailflow",
          "query": "sailflow",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003d0udadFl0gCTKCp0QmzQTXS3_y08iO8FpwsoKPHPS6kw\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailboatdata%26FORM%3dUSBAPI\u0026p\u003dDevEx,5009.1",
          "displayText": "sailboatdata",
          "query": "sailboatdata",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003deSSt0MRSbl2V0RFPSuVd-gC7fGOT4717pz55EBUgPec\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailor%2b2025%26FORM%3dUSBAPI\u0026p\u003dDevEx,5010.1",
          "displayText": "sailor 2025",
          "query": "sailor 2025",
          "searchKind": "WebSearch"
        }
      ]
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="2d2f7-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="2d2f7-120">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d2f7-121">Bing Autosuggest tutorial</span><span class="sxs-lookup"><span data-stu-id="2d2f7-121">Bing Autosuggest tutorial</span></span>](../tutorials/autosuggest.md)

## <a name="see-also"></a><span data-ttu-id="2d2f7-122">See also</span><span class="sxs-lookup"><span data-stu-id="2d2f7-122">See also</span></span>

- [<span data-ttu-id="2d2f7-123">What is Bing Autosuggest?</span><span class="sxs-lookup"><span data-stu-id="2d2f7-123">What is Bing Autosuggest?</span></span>](../get-suggested-search-terms.md)
- [<span data-ttu-id="2d2f7-124">Bing Autosuggest API v7 reference</span><span class="sxs-lookup"><span data-stu-id="2d2f7-124">Bing Autosuggest API v7 reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference)