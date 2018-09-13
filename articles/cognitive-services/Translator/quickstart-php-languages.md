---
title: Translator Text get supported languages with PHP | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API with PHP in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: 95b48f15ffe8cea14f9ffb7612193b819e03f5f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869009"
---
# <a name="quickstart-get-supported-languages-with-php"></a><span data-ttu-id="7afb6-103">Quickstart: Get supported languages with PHP</span><span class="sxs-lookup"><span data-stu-id="7afb6-103">Quickstart: Get supported languages with PHP</span></span>

<span data-ttu-id="7afb6-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="7afb6-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7afb6-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7afb6-105">Prerequisites</span></span>

<span data-ttu-id="7afb6-106">You'll need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span><span class="sxs-lookup"><span data-stu-id="7afb6-106">You'll need [PHP 5.6.x](http://php.net/downloads.php) to run this code.</span></span>

<span data-ttu-id="7afb6-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="7afb6-107">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="languages-request"></a><span data-ttu-id="7afb6-108">Languages request</span><span class="sxs-lookup"><span data-stu-id="7afb6-108">Languages request</span></span>

<span data-ttu-id="7afb6-109">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span><span class="sxs-lookup"><span data-stu-id="7afb6-109">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span></span>

1. <span data-ttu-id="7afb6-110">Create a new PHP project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="7afb6-110">Create a new PHP project in your favorite code editor.</span></span>
2. <span data-ttu-id="7afb6-111">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="7afb6-111">Add the code provided below.</span></span>
3. <span data-ttu-id="7afb6-112">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="7afb6-112">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="7afb6-113">Run the program.</span><span class="sxs-lookup"><span data-stu-id="7afb6-113">Run the program.</span></span>

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
$path = "/languages?api-version=3.0";

$output_path = "output.txt";

function GetLanguages ($host, $path, $key) {

    $headers = "Content-type: text/xml\r\n" .
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
    $result = file_get_contents ($host . $path, false, $context);
    return $result;
}

$result = GetLanguages ($host, $path, $key);

// Note: We convert result, which is JSON, to and from an object so we can pretty-print it.
// We want to avoid escaping any Unicode characters that result contains. See:
// http://php.net/manual/en/function.json-encode.php
$json = json_encode(json_decode($result), JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT);
$out = fopen($output_path, 'w');
fwrite($out, $json);
fclose($out);
?>
```

## <a name="languages-response"></a><span data-ttu-id="7afb6-114">Languages response</span><span class="sxs-lookup"><span data-stu-id="7afb6-114">Languages response</span></span>

<span data-ttu-id="7afb6-115">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7afb6-115">A successful response is returned in JSON as shown in the following example:</span></span>

```json
{
  "translation": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr"
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl"
    },
...
  },
  "transliteration": {
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "scripts": [
        {
          "code": "Arab",
          "name": "Arabic",
          "nativeName": "العربية",
          "dir": "rtl",
          "toScripts": [
            {
              "code": "Latn",
              "name": "Latin",
              "nativeName": "اللاتينية",
              "dir": "ltr"
            }
          ]
        },
        {
          "code": "Latn",
          "name": "Latin",
          "nativeName": "اللاتينية",
          "dir": "ltr",
          "toScripts": [
            {
              "code": "Arab",
              "name": "Arabic",
              "nativeName": "العربية",
              "dir": "rtl"
            }
          ]
        }
      ]
    },
...
  },
  "dictionary": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
...
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="7afb6-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="7afb6-116">Next steps</span></span>

<span data-ttu-id="7afb6-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="7afb6-117">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7afb6-118">Explore PHP examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="7afb6-118">Explore PHP examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=php)
