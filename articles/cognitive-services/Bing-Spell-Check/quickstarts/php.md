---
title: PHP Quickstart for Bing Spell Check API - Azure Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Spell Check API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: quickstart
ms.date: 09/14/2017
ms.author: v-jaswel
ms.openlocfilehash: b0eefcfc834bfc408d38fa9c697087a40f96da45
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864935"
---
# <a name="quickstart-for-bing-spell-check-api-with-php"></a><span data-ttu-id="8157a-103">Quickstart for Bing Spell Check API with PHP</span><span class="sxs-lookup"><span data-stu-id="8157a-103">Quickstart for Bing Spell Check API with PHP</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="8157a-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with PHP.</span><span class="sxs-lookup"><span data-stu-id="8157a-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with PHP.</span></span> <span data-ttu-id="8157a-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span><span class="sxs-lookup"><span data-stu-id="8157a-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span></span> <span data-ttu-id="8157a-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span><span class="sxs-lookup"><span data-stu-id="8157a-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span></span> <span data-ttu-id="8157a-107">This article shows how to send a request that contains the text "Hollo, wrld!"</span><span class="sxs-lookup"><span data-stu-id="8157a-107">This article shows how to send a request that contains the text "Hollo, wrld!"</span></span> <span data-ttu-id="8157a-108">The suggested replacements are "Hello" and "world."</span><span class="sxs-lookup"><span data-stu-id="8157a-108">The suggested replacements are "Hello" and "world."</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8157a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8157a-109">Prerequisites</span></span>

<span data-ttu-id="8157a-110">You will need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span><span class="sxs-lookup"><span data-stu-id="8157a-110">You will need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span></span>

<span data-ttu-id="8157a-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span><span class="sxs-lookup"><span data-stu-id="8157a-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span></span> <span data-ttu-id="8157a-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="8157a-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span></span> <span data-ttu-id="8157a-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="8157a-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="get-spell-check-results"></a><span data-ttu-id="8157a-114">Get Spell Check results</span><span class="sxs-lookup"><span data-stu-id="8157a-114">Get Spell Check results</span></span>

1. <span data-ttu-id="8157a-115">Create a new PHP project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8157a-115">Create a new PHP project in your favorite IDE.</span></span>
2. <span data-ttu-id="8157a-116">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8157a-116">Add the code provided below.</span></span>
3. <span data-ttu-id="8157a-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8157a-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8157a-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8157a-118">Run the program.</span></span>

```php
<?php

// NOTE: Be sure to uncomment the following line in your php.ini file.
// ;extension=php_openssl.dll

// These properties are used for optional headers (see below).
// define("CLIENT_ID", "<Client ID from Previous Response Goes Here>");
// define("CLIENT_IP", "999.999.999.999");
// define("CLIENT_LOCATION", "+90.0000000000000;long: 00.0000000000000;re:100.000000000000");

$host = 'https://api.cognitive.microsoft.com';
$path = '/bing/v7.0/spellcheck?';
$params = 'mkt=en-us&mode=proof';

$input = "Hollo, wrld!";

$data = array (
    'text' => urlencode ($input)
);

// NOTE: Replace this example key with a valid subscription key.
$key = 'ENTER KEY HERE';

// The following headers are optional, but it is recommended
// that they are treated as required. These headers will assist the service
// with returning more accurate results.
//'X-Search-Location' => CLIENT_LOCATION
//'X-MSEdge-ClientID' => CLIENT_ID
//'X-MSEdge-ClientIP' => CLIENT_IP

$headers = "Content-type: application/x-www-form-urlencoded\r\n" .
    "Ocp-Apim-Subscription-Key: $key\r\n";

// NOTE: Use the key 'http' even if you are making an HTTPS request. See:
// http://php.net/manual/en/function.stream-context-create.php
$options = array (
    'http' => array (
        'header' => $headers,
        'method' => 'POST',
        'content' => http_build_query ($data)
    )
);
$context  = stream_context_create ($options);
$result = file_get_contents ($host . $path . $params, false, $context);

if ($result === FALSE) {
    /* Handle error */
}

$json = json_encode(json_decode($result), JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT);
echo $json;
?>
```

<span data-ttu-id="8157a-119">**Response**</span><span class="sxs-lookup"><span data-stu-id="8157a-119">**Response**</span></span>

<span data-ttu-id="8157a-120">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8157a-120">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="8157a-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="8157a-121">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8157a-122">Bing Spell Check tutorial</span><span class="sxs-lookup"><span data-stu-id="8157a-122">Bing Spell Check tutorial</span></span>](../tutorials/spellcheck.md)

## <a name="see-also"></a><span data-ttu-id="8157a-123">See also</span><span class="sxs-lookup"><span data-stu-id="8157a-123">See also</span></span>

- [<span data-ttu-id="8157a-124">Bing Spell Check overview</span><span class="sxs-lookup"><span data-stu-id="8157a-124">Bing Spell Check overview</span></span>](../proof-text.md)
- [<span data-ttu-id="8157a-125">Bing Spell Check API v7 Reference</span><span class="sxs-lookup"><span data-stu-id="8157a-125">Bing Spell Check API v7 Reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference)
