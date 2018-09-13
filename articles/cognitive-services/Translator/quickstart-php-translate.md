---
title: Translator Text translate text with PHP | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you translate text from one language to another using the Translator Text API with PHP in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: e7d86e36c6137980ba379371548de6f5e6721302
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855900"
---
# <a name="quickstart-translate-text-with-php"></a><span data-ttu-id="7edd1-103">Quickstart: Translate text with PHP</span><span class="sxs-lookup"><span data-stu-id="7edd1-103">Quickstart: Translate text with PHP</span></span>

<span data-ttu-id="7edd1-104">In this quickstart, you translate text from one language to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="7edd1-104">In this quickstart, you translate text from one language to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7edd1-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7edd1-105">Prerequisites</span></span>

<span data-ttu-id="7edd1-106">You'll need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span><span class="sxs-lookup"><span data-stu-id="7edd1-106">You'll need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span></span>

<span data-ttu-id="7edd1-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="7edd1-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="translate-request"></a><span data-ttu-id="7edd1-108">Translate request</span><span class="sxs-lookup"><span data-stu-id="7edd1-108">Translate request</span></span>

<span data-ttu-id="7edd1-109">The following code translates source text from one language to another using the [Translate](./reference/v3-0-translate.md) method.</span><span class="sxs-lookup"><span data-stu-id="7edd1-109">The following code translates source text from one language to another using the [Translate](./reference/v3-0-translate.md) method.</span></span>

1. <span data-ttu-id="7edd1-110">Create a new PHP project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="7edd1-110">Create a new PHP project in your favorite code editor.</span></span>
2. <span data-ttu-id="7edd1-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="7edd1-111">Add the code provided below.</span></span>
3. <span data-ttu-id="7edd1-112">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="7edd1-112">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="7edd1-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="7edd1-113">Run the program.</span></span>

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
$path = "/translate?api-version=3.0";

// Translate to German and Italian.
$params = "&to=de&to=it";

$text = "Hello, world!";

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

function Translate ($host, $path, $key, $params, $content) {

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

$result = Translate ($host, $path, $key, $params, $content);

// Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
// We want to avoid escaping any Unicode characters that result contains. See:
// http://php.net/manual/en/function.json-encode.php
$json = json_encode(json_decode($result), JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT);
echo $json;
?>
```

## <a name="translate-response"></a><span data-ttu-id="7edd1-114">Translate response</span><span class="sxs-lookup"><span data-stu-id="7edd1-114">Translate response</span></span>

<span data-ttu-id="7edd1-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7edd1-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "detectedLanguage": {
      "language": "en",
      "score": 1.0
    },
    "translations": [
      {
        "text": "Hallo Welt!",
        "to": "de"
      },
      {
        "text": "Salve, mondo!",
        "to": "it"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="7edd1-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="7edd1-116">Next steps</span></span>

<span data-ttu-id="7edd1-117">Explore the sample code for this quickstart and others, including transliteration and language identification, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="7edd1-117">Explore the sample code for this quickstart and others, including transliteration and language identification, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7edd1-118">Explore PHP examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="7edd1-118">Explore PHP examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=php)