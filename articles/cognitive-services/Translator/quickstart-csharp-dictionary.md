---
title: Translator Text find alternate translations with C# | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you find alternate translations and examples of terms in context using the Translator Text API with C# in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/15/2018
ms.author: nolachar
ms.openlocfilehash: 3f45e7281456f9ae09912a2ee665cb480dc5052f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868580"
---
# <a name="quickstart-find-alternate-translations-and-usage-with-c35"></a><span data-ttu-id="3c4a2-103">Quickstart: Find alternate translations and usage with C&#35;</span><span class="sxs-lookup"><span data-stu-id="3c4a2-103">Quickstart: Find alternate translations and usage with C&#35;</span></span>

<span data-ttu-id="3c4a2-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c4a2-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3c4a2-105">Prerequisites</span></span>

<span data-ttu-id="3c4a2-106">You'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-106">You'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="3c4a2-107">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="3c4a2-107">(The free Community Edition will work.)</span></span>

<span data-ttu-id="3c4a2-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="3c4a2-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="dictionary-lookup-request"></a><span data-ttu-id="3c4a2-109">Dictionary Lookup request</span><span class="sxs-lookup"><span data-stu-id="3c4a2-109">Dictionary Lookup request</span></span>

<span data-ttu-id="3c4a2-110">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-110">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span></span>

1. <span data-ttu-id="3c4a2-111">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-111">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="3c4a2-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-112">Add the code provided below.</span></span>
3. <span data-ttu-id="3c4a2-113">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-113">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="3c4a2-114">Run the program.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-114">Run the program.</span></span>

```csharp
using System;
using System.Net.Http;
using System.Text;
// NOTE: Install the Newtonsoft.Json NuGet package.
using Newtonsoft.Json;

namespace TranslatorTextQuickStart
{
    class Program
    {
        static string host = "https://api.cognitive.microsofttranslator.com";
        static string path = "/dictionary/lookup?api-version=3.0";
        // Translate from English to French.
        static string params_ = "&from=en&to=fr";

        static string uri = host + path + params_;

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string text = "great";

        async static void Lookup()
        {
            System.Object[] body = new System.Object[] { new { Text = text } };
            var requestBody = JsonConvert.SerializeObject(body);

            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(requestBody, Encoding.UTF8, "application/json");
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();
                var result = JsonConvert.SerializeObject(JsonConvert.DeserializeObject(responseBody), Formatting.Indented);

                Console.OutputEncoding = UnicodeEncoding.UTF8;
                Console.WriteLine(result);
            }
        }

        static void Main(string[] args)
        {
            Lookup();
            Console.ReadLine();
        }
    }
}
```

## <a name="dictionary-lookup-response"></a><span data-ttu-id="3c4a2-115">Dictionary Lookup response</span><span class="sxs-lookup"><span data-stu-id="3c4a2-115">Dictionary Lookup response</span></span>

<span data-ttu-id="3c4a2-116">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="3c4a2-116">A successful response is returned in JSON as shown in the following example:</span></span>

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

## <a name="dictionary-examples-request"></a><span data-ttu-id="3c4a2-117">Dictionary Examples request</span><span class="sxs-lookup"><span data-stu-id="3c4a2-117">Dictionary Examples request</span></span>

<span data-ttu-id="3c4a2-118">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-118">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span></span>

1. <span data-ttu-id="3c4a2-119">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-119">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="3c4a2-120">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-120">Add the code provided below.</span></span>
3. <span data-ttu-id="3c4a2-121">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-121">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="3c4a2-122">Run the program.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-122">Run the program.</span></span>

```csharp
using System;
using System.Net.Http;
using System.Text;
// NOTE: Install the Newtonsoft.Json NuGet package.
using Newtonsoft.Json;

namespace TranslatorTextQuickStart
{
    class Program
    {
        static string host = "https://api.cognitive.microsofttranslator.com";
        static string path = "/dictionary/examples?api-version=3.0";
        // Translate from English to French.
        static string params_ = "&from=en&to=fr";

        static string uri = host + path + params_;

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string text = "great";
        static string translation = "formidable";

        async static void Examples()
        {
            System.Object[] body = new System.Object[] { new { Text = text, Translation = translation } };
            var requestBody = JsonConvert.SerializeObject(body);

            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(requestBody, Encoding.UTF8, "application/json");
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();
                var result = JsonConvert.SerializeObject(JsonConvert.DeserializeObject(responseBody), Formatting.Indented);

                Console.OutputEncoding = UnicodeEncoding.UTF8;
                Console.WriteLine(result);
            }
        }

        static void Main(string[] args)
        {
            Examples();
            Console.ReadLine();
        }
    }
}
```

## <a name="dictionary-examples-response"></a><span data-ttu-id="3c4a2-123">Dictionary Examples response</span><span class="sxs-lookup"><span data-stu-id="3c4a2-123">Dictionary Examples response</span></span>

<span data-ttu-id="3c4a2-124">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="3c4a2-124">A successful response is returned in JSON as shown in the following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3c4a2-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c4a2-125">Next steps</span></span>

<span data-ttu-id="3c4a2-126">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-126">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c4a2-127">Explore C# examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="3c4a2-127">Explore C# examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=c%23)
