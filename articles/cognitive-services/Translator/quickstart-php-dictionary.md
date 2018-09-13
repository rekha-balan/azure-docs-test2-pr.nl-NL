---
title: Translator Text find alternate translations with PHP | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you find alternate translations and examples of terms in context using the Translator Text API with PHP in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: 3f3f98d42a327602352735db97ad1844061aa3a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867938"
---
# <a name="quickstart-find-alternate-translations-and-usage-with-php"></a><span data-ttu-id="de054-103">Quickstart: Find alternate translations and usage with PHP</span><span class="sxs-lookup"><span data-stu-id="de054-103">Quickstart: Find alternate translations and usage with PHP</span></span>

<span data-ttu-id="de054-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="de054-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de054-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="de054-105">Prerequisites</span></span>

<span data-ttu-id="de054-106">You'll need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span><span class="sxs-lookup"><span data-stu-id="de054-106">You'll need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span></span>

<span data-ttu-id="de054-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="de054-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="dictionary-lookup-request"></a><span data-ttu-id="de054-108">Dictionary Lookup request</span><span class="sxs-lookup"><span data-stu-id="de054-108">Dictionary Lookup request</span></span>

<span data-ttu-id="de054-109">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span><span class="sxs-lookup"><span data-stu-id="de054-109">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span></span>

1. <span data-ttu-id="de054-110">Create a new PHP project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="de054-110">Create a new PHP project in your favorite code editor.</span></span>
2. <span data-ttu-id="de054-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="de054-111">Add the code provided below.</span></span>
3. <span data-ttu-id="de054-112">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="de054-112">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="de054-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="de054-113">Run the program.</span></span>

```php
<?php

// NOTE: Be sure to uncomment the following line in your php.ini file.
// ;extension=php_openssl.dll

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
$key = 'ENTER KEY HERE';

$host = "https://api.cognitive.microsofttranslator.com";
$path = "/dictionary/lookup?api-version=3.0";

// Translate from English to French.
$params = "&from=en&to=fr";

$text = "great";

if (!function_exists('com_create_guid')) {
  function com_create_guid() {
    return sprintf( '%04x%04x-%04x-%04x-%04x-%04x%04x%04x',
        mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff ),
        mt_rand( 0, 0xffff ),
        mt_rand( 0, 0x0fff ) | 0x4000,
        mt_rand( 0, 0x3fff ) | 0x8000,
        mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff )
    );
  }
}

function DictionaryLookup ($host, $path, $key, $params, $content) {

    $headers = "Content-type: application/json\r\n" .
        "Content-length: " . strlen($content) . "\r\n" .
        "Ocp-Apim-Subscription-Key: $key\r\n" .
        "X-ClientTraceId: " . com_create_guid() . "\r\n";

    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $options = array (
        'http' => array (
            'header' => $headers,
            'method' => 'POST',
            'content' => $content
        )
    );
    $context  = stream_context_create ($options);
    $result = file_get_contents ($host . $path . $params, false, $context);
    return $result;
}

$requestBody = array (
    array (
        'Text' => $text,
    ),
);
$content = json_encode($requestBody);

$result = DictionaryLookup ($host, $path, $key, $params, $content);

// Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
// We want to avoid escaping any Unicode characters that result contains. See:
// http://php.net/manual/en/function.json-encode.php
$json = json_encode(json_decode($result), JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT);
echo $json;
?>
```

## <a name="dictionary-lookup-response"></a><span data-ttu-id="de054-114">Dictionary Lookup response</span><span class="sxs-lookup"><span data-stu-id="de054-114">Dictionary Lookup response</span></span>

<span data-ttu-id="de054-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="de054-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "normalizedSource": "great",
    "displaySource": "great",
    "translations": [
      {
        "normalizedTarget": "grand",
        "displayTarget": "grand",
        "posTag": "ADJ",
        "confidence": 0.2783,
        "prefixWord": "",
        "backTranslations": [
          {
            "normalizedText": "great",
            "displayText": "great",
            "numExamples": 15,
            "frequencyCount": 34358
          },
          {
            "normalizedText": "big",
            "displayText": "big",
            "numExamples": 15,
            "frequencyCount": 21770
          },
...
        ]
      },
      {
        "normalizedTarget": "super",
        "displayTarget": "super",
        "posTag": "ADJ",
        "confidence": 0.1514,
        "prefixWord": "",
        "backTranslations": [
          {
            "normalizedText": "super",
            "displayText": "super",
            "numExamples": 15,
            "frequencyCount": 12023
          },
          {
            "normalizedText": "great",
            "displayText": "great",
            "numExamples": 15,
            "frequencyCount": 10931
          },
...
        ]
      },
...
    ]
  }
]
```

## <a name="dictionary-examples-request"></a><span data-ttu-id="de054-116">Dictionary Examples request</span><span class="sxs-lookup"><span data-stu-id="de054-116">Dictionary Examples request</span></span>

<span data-ttu-id="de054-117">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span><span class="sxs-lookup"><span data-stu-id="de054-117">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span></span>

1. <span data-ttu-id="de054-118">Create a new PHP project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="de054-118">Create a new PHP project in your favorite code editor.</span></span>
2. <span data-ttu-id="de054-119">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="de054-119">Add the code provided below.</span></span>
3. <span data-ttu-id="de054-120">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="de054-120">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="de054-121">Run the program.</span><span class="sxs-lookup"><span data-stu-id="de054-121">Run the program.</span></span>

```php
<?php

// NOTE: Be sure to uncomment the following line in your php.ini file.
// ;extension=php_openssl.dll

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
$key = 'ENTER KEY HERE';

$host = "https://api.cognitive.microsofttranslator.com";
$path = "/dictionary/examples?api-version=3.0";

// Translate from English to French.
$params = "&from=en&to=fr";

$text = "great";
$translation = "formidable";

if (!function_exists('com_create_guid')) {
  function com_create_guid() {
    return sprintf( '%04x%04x-%04x-%04x-%04x-%04x%04x%04x',
        mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff ),
        mt_rand( 0, 0xffff ),
        mt_rand( 0, 0x0fff ) | 0x4000,
        mt_rand( 0, 0x3fff ) | 0x8000,
        mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff )
    );
  }
}

function DictionaryExamples ($host, $path, $key, $params, $content) {

    $headers = "Content-type: application/json\r\n" .
        "Content-length: " . strlen($content) . "\r\n" .
        "Ocp-Apim-Subscription-Key: $key\r\n" .
        "X-ClientTraceId: " . com_create_guid() . "\r\n";

    // NOTE: Use the key 'http' even if you are making an HTTPS request. See:
    // http://php.net/manual/en/function.stream-context-create.php
    $options = array (
        'http' => array (
            'header' => $headers,
            'method' => 'POST',
            'content' => $content
        )
    );
    $context  = stream_context_create ($options);
    $result = file_get_contents ($host . $path . $params, false, $context);
    return $result;
}

$requestBody = array (
    array (
        'Text' => $text,
        'Translation' => $translation,
    ),
);
$content = json_encode($requestBody);

$result = DictionaryExamples ($host, $path, $key, $params, $content);

// Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
// We want to avoid escaping any Unicode characters that result contains. See:
// http://php.net/manual/en/function.json-encode.php
$json = json_encode(json_decode($result), JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT);
echo $json;
?>
```

## <a name="dictionary-examples-response"></a><span data-ttu-id="de054-122">Dictionary Examples response</span><span class="sxs-lookup"><span data-stu-id="de054-122">Dictionary Examples response</span></span>

<span data-ttu-id="de054-123">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="de054-123">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "normalizedSource": "great",
    "normalizedTarget": "formidable",
    "examples": [
      {
        "sourcePrefix": "You have a ",
        "sourceTerm": "great",
        "sourceSuffix": " expression there.",
        "targetPrefix": "Vous avez une expression ",
        "targetTerm": "formidable",
        "targetSuffix": "."
      },
      {
        "sourcePrefix": "You played a ",
        "sourceTerm": "great",
        "sourceSuffix": " game today.",
        "targetPrefix": "Vous avez été ",
        "targetTerm": "formidable",
        "targetSuffix": "."
      },
...
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="de054-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="de054-124">Next steps</span></span>

<span data-ttu-id="de054-125">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="de054-125">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="de054-126">Explore PHP examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="de054-126">Explore PHP examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=php)
