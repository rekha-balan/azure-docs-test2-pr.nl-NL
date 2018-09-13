---
title: 'Quickstart: Using PHP to call the Text Analytics API | Microsoft Docs'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Text Analytics API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: ashmaka
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 08/30/2018
ms.author: ashmaka
ms.openlocfilehash: 602988747f54c3dbdfa933986d47b631b757db65
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855984"
---
# <a name="quickstart-using-php-to-call-the-text-analytics-cognitive-service"></a><span data-ttu-id="64998-103">Quickstart: Using PHP to call the Text Analytics Cognitive Service</span><span class="sxs-lookup"><span data-stu-id="64998-103">Quickstart: Using PHP to call the Text Analytics Cognitive Service</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="64998-104">This article shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), [extract key phrases](#KeyPhraseExtraction), and [identify linked entities](#Entities) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with PHP.</span><span class="sxs-lookup"><span data-stu-id="64998-104">This article shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), [extract key phrases](#KeyPhraseExtraction), and [identify linked entities](#Entities) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with PHP.</span></span>

<span data-ttu-id="64998-105">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span><span class="sxs-lookup"><span data-stu-id="64998-105">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64998-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="64998-106">Prerequisites</span></span>

<span data-ttu-id="64998-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="64998-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span></span> <span data-ttu-id="64998-108">You can use the **free tier for 5,000 transactions/month** to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="64998-108">You can use the **free tier for 5,000 transactions/month** to complete this quickstart.</span></span>

<span data-ttu-id="64998-109">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign up.</span><span class="sxs-lookup"><span data-stu-id="64998-109">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign up.</span></span> 

<a name="Detect"></a>

## <a name="detect-language"></a><span data-ttu-id="64998-110">Detect language</span><span class="sxs-lookup"><span data-stu-id="64998-110">Detect language</span></span>

<span data-ttu-id="64998-111">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span><span class="sxs-lookup"><span data-stu-id="64998-111">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span></span>

1. <span data-ttu-id="64998-112">Create a new PHP project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="64998-112">Create a new PHP project in your favorite IDE.</span></span>
2. <span data-ttu-id="64998-113">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="64998-113">Add the code provided below.</span></span>
3. <span data-ttu-id="64998-114">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="64998-114">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="64998-115">Replace the location in `host` (currently `westus`) to the region you signed up for.</span><span class="sxs-lookup"><span data-stu-id="64998-115">Replace the location in `host` (currently `westus`) to the region you signed up for.</span></span>
5. <span data-ttu-id="64998-116">Run the program.</span><span class="sxs-lookup"><span data-stu-id="64998-116">Run the program.</span></span>

```php
<?php

// NOTE: Be sure to uncomment the following line in your php.ini file.
// ;extension=php_openssl.dll

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the accessKey string value with your valid access key.
$accessKey = 'ENTER KEY HERE';

// Replace or verify the region.

// You must use the same region in your REST API call as you used to obtain your access keys.
// For example, if you obtained your access keys from the westus region, replace 
// "westcentralus" in the URI below with "westus".

// NOTE: Free trial access keys are generated in the westcentralus region, so if you are using
// a free trial access key, you should not need to change this region.
$host = 'https://westus.api.cognitive.microsoft.com';
$path = '/text/analytics/v2.0/';

function DetectLanguage ($host, $path, $key, $data) {

    $headers = "Content-type: text/json\r\n" .
        "Ocp-Apim-Subscription-Key: $key\r\n";

    $data = json_encode ($data);

    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $options = array (
        'http' => array (
            'header' => $headers,
            'method' => 'POST',
            'content' => $data
        )
    );
    $context  = stream_context_create ($options);
    $result = file_get_contents ($host . $path . 'languages', false, $context);
    return $result;
}

$data = array (
    'documents' => array (
        array ( 'id' => '1', 'text' => 'This is a document written in English.' ),
        array ( 'id' => '2', 'text' => 'Este es un document escrito en Español.' ),
        array ( 'id' => '3', 'text' => '这是一个用中文写的文件')
    )
);

print "Please wait a moment for the results to appear.\n\n";

$result = DetectLanguage ($host, $path, $accessKey, $data);

echo json_encode (json_decode ($result), JSON_PRETTY_PRINT) . "\n\n";
```

<span data-ttu-id="64998-117">**Language detection response**</span><span class="sxs-lookup"><span data-stu-id="64998-117">**Language detection response**</span></span>

<span data-ttu-id="64998-118">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="64998-118">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "id": "1",
         "detectedLanguages": [
            {
               "name": "English",
               "iso6391Name": "en",
               "score": 1.0
            }
         ]
      },
      {
         "id": "2",
         "detectedLanguages": [
            {
               "name": "Spanish",
               "iso6391Name": "es",
               "score": 1.0
            }
         ]
      },
      {
         "id": "3",
         "detectedLanguages": [
            {
               "name": "Chinese_Simplified",
               "iso6391Name": "zh_chs",
               "score": 1.0
            }
         ]
      }
   ],
   "errors": [

   ]
}
```
<a name="SentimentAnalysis"></a>

## <a name="analyze-sentiment"></a><span data-ttu-id="64998-119">Analyze sentiment</span><span class="sxs-lookup"><span data-stu-id="64998-119">Analyze sentiment</span></span>

<span data-ttu-id="64998-120">The Sentiment Analysis API detexts the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span><span class="sxs-lookup"><span data-stu-id="64998-120">The Sentiment Analysis API detexts the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span></span> <span data-ttu-id="64998-121">The following example scores two documents, one in English and another in Spanish.</span><span class="sxs-lookup"><span data-stu-id="64998-121">The following example scores two documents, one in English and another in Spanish.</span></span>

<span data-ttu-id="64998-122">Add the following code to the code from the [previous section](#Detect).</span><span class="sxs-lookup"><span data-stu-id="64998-122">Add the following code to the code from the [previous section](#Detect).</span></span>

```php
function GetSentiment ($host, $path, $key, $data) {

    $headers = "Content-type: text/json\r\n" .
        "Ocp-Apim-Subscription-Key: $key\r\n";

    $data = json_encode ($data);

    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $options = array (
        'http' => array (
            'header' => $headers,
            'method' => 'POST',
            'content' => $data
        )
    );
    $context  = stream_context_create ($options);
    $result = file_get_contents ($host . $path . 'sentiment', false, $context);
    return $result;
}

$data = array (
    'documents' => array (
        array ( 'id' => '1', 'language' => 'en', 'text' => 'I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.' ),
        array ( 'id' => '2', 'language' => 'es', 'text' => 'Este ha sido un dia terrible, llegué tarde al trabajo debido a un accidente automobilistico.' )
    )
);

print "Please wait a moment for the results to appear.\n\n";

$result = GetSentiment ($host, $path, $accessKey, $data);

echo json_encode (json_decode ($result), JSON_PRETTY_PRINT) . "\n\n";
```

<span data-ttu-id="64998-123">**Sentiment analysis response**</span><span class="sxs-lookup"><span data-stu-id="64998-123">**Sentiment analysis response**</span></span>

<span data-ttu-id="64998-124">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="64998-124">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "score": 0.99984133243560791,
         "id": "1"
      },
      {
         "score": 0.024017512798309326,
         "id": "2"
      },
   ],
   "errors": [   ]
}
```

<a name="KeyPhraseExtraction"></a>

## <a name="extract-key-phrases"></a><span data-ttu-id="64998-125">Extract key phrases</span><span class="sxs-lookup"><span data-stu-id="64998-125">Extract key phrases</span></span>

<span data-ttu-id="64998-126">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span><span class="sxs-lookup"><span data-stu-id="64998-126">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span></span> <span data-ttu-id="64998-127">The following example extracts key phrases for both English and Spanish documents.</span><span class="sxs-lookup"><span data-stu-id="64998-127">The following example extracts key phrases for both English and Spanish documents.</span></span>

<span data-ttu-id="64998-128">Add the following code to the code from the [previous section](#SentimentAnalysis).</span><span class="sxs-lookup"><span data-stu-id="64998-128">Add the following code to the code from the [previous section](#SentimentAnalysis).</span></span>

```php
function GetKeyPhrases ($host, $path, $key, $data) {

    $headers = "Content-type: text/json\r\n" .
        "Ocp-Apim-Subscription-Key: $key\r\n";

    $data = json_encode ($data);

    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $options = array (
        'http' => array (
            'header' => $headers,
            'method' => 'POST',
            'content' => $data
        )
    );
    $context  = stream_context_create ($options);
    $result = file_get_contents ($host . $path . 'keyPhrases', false, $context);
    return $result;
}

$data = array (
    'documents' => array (
        array ( 'id' => '1', 'language' => 'en', 'text' => 'I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.' ),
        array ( 'id' => '2', 'language' => 'es', 'text' => 'Si usted quiere comunicarse con Carlos, usted debe de llamarlo a su telefono movil. Carlos es muy responsable, pero necesita recibir una notificacion si hay algun problema.' ),
        array ( 'id' => '3', 'language' => 'en', 'text' => 'The Grand Hotel is a new hotel in the center of Seattle. It earned 5 stars in my review, and has the classiest decor I\'ve ever seen.' )
    )
);

print "Please wait a moment for the results to appear.\n\n";

$result = GetKeyPhrases ($host, $path, $accessKey, $data);

echo json_encode (json_decode ($result), JSON_PRETTY_PRINT) . "\n\n";
```

<span data-ttu-id="64998-129">**Key phrase extraction response**</span><span class="sxs-lookup"><span data-stu-id="64998-129">**Key phrase extraction response**</span></span>

<span data-ttu-id="64998-130">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="64998-130">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "keyPhrases": [
            "HDR resolution",
            "new XBox",
            "clean look"
         ],
         "id": "1"
      },
      {
         "keyPhrases": [
            "Carlos",
            "notificacion",
            "algun problema",
            "telefono movil"
         ],
         "id": "2"
      },
      {
         "keyPhrases": [
            "new hotel",
            "Grand Hotel",
            "review",
            "center of Seattle",
            "classiest decor",
            "stars"
         ],
         "id": "3"
      }
   ],
   "errors": [  ]
}
```

<a name="Entities"></a>

## <a name="identify-linked-entities"></a><span data-ttu-id="64998-131">Identify linked entities</span><span class="sxs-lookup"><span data-stu-id="64998-131">Identify linked entities</span></span>

<span data-ttu-id="64998-132">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span><span class="sxs-lookup"><span data-stu-id="64998-132">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span></span> <span data-ttu-id="64998-133">The following example identifies entities for English documents.</span><span class="sxs-lookup"><span data-stu-id="64998-133">The following example identifies entities for English documents.</span></span>

<span data-ttu-id="64998-134">Add the following code to the code from the [previous section](#KeyPhraseExtraction).</span><span class="sxs-lookup"><span data-stu-id="64998-134">Add the following code to the code from the [previous section](#KeyPhraseExtraction).</span></span>

```php
function GetEntities ($host, $path, $key, $data) {

    $headers = "Content-type: text/json\r\n" .
        "Ocp-Apim-Subscription-Key: $key\r\n";

    $data = json_encode ($data);

    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $options = array (
        'http' => array (
            'header' => $headers,
            'method' => 'POST',
            'content' => $data
        )
    );
    $context  = stream_context_create ($options);
    $result = file_get_contents ($host . $path . 'entities', false, $context);
    return $result;
}

$data = array (
    'documents' => array (
        array ( 'id' => '1', 'language' => 'en', 'text' => 'I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.' ),
        array ( 'id' => '2', 'language' => 'en', 'text' => 'The Seattle Seahawks won the Super Bowl in 2014.' )
    )
);

print "Please wait a moment for the results to appear.\n\n";

$result = GetEntities ($host, $path, $accessKey, $data);

echo json_encode (json_decode ($result), JSON_PRETTY_PRINT) . "\n\n";
?>
```

<span data-ttu-id="64998-135">**Entity linking response**</span><span class="sxs-lookup"><span data-stu-id="64998-135">**Entity linking response**</span></span>

<span data-ttu-id="64998-136">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="64998-136">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
    "documents": [
        {
            "id": "1",
            "entities": [
                {
                    "name": "Xbox One",
                    "matches": [
                        {
                            "text": "XBox One",
                            "offset": 23,
                            "length": 8
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Xbox One",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Xbox_One",
                    "bingId": "446bb4df-4999-4243-84c0-74e0f6c60e75"
                },
                {
                    "name": "Ultra-high-definition television",
                    "matches": [
                        {
                            "text": "4K",
                            "offset": 63,
                            "length": 2
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Ultra-high-definition television",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Ultra-high-definition_television",
                    "bingId": "7ee02026-b6ec-878b-f4de-f0bc7b0ab8c4"
                }
            ]
        },
        {
            "id": "2",
            "entities": [
                {
                    "name": "2013 Seattle Seahawks season",
                    "matches": [
                        {
                            "text": "Seattle Seahawks",
                            "offset": 4,
                            "length": 16
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "2013 Seattle Seahawks season",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/2013_Seattle_Seahawks_season",
                    "bingId": "eb637865-4722-4eca-be9e-0ac0c376d361"
                }
            ]
        }
    ],
    "errors": []
}
```

## <a name="next-steps"></a><span data-ttu-id="64998-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="64998-137">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64998-138">Text Analytics With Power BI</span><span class="sxs-lookup"><span data-stu-id="64998-138">Text Analytics With Power BI</span></span>](../tutorials/tutorial-power-bi-key-phrases.md)

## <a name="see-also"></a><span data-ttu-id="64998-139">See also</span><span class="sxs-lookup"><span data-stu-id="64998-139">See also</span></span> 

 [<span data-ttu-id="64998-140">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="64998-140">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="64998-141">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="64998-141">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)
