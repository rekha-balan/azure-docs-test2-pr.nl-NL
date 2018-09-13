---
title: Translator Text translate text with C# | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you translate text from one language to another using the Translator Text API with C# in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/15/2018
ms.author: nolachar
ms.openlocfilehash: 7923cf3249beaf713b91ba0e5ea4f70f34841b3c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866459"
---
# <a name="quickstart-translate-text-with-c35"></a><span data-ttu-id="1ca65-103">Quickstart: Translate text with C&#35;</span><span class="sxs-lookup"><span data-stu-id="1ca65-103">Quickstart: Translate text with C&#35;</span></span>

<span data-ttu-id="1ca65-104">In this quickstart, you translate text from one language to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="1ca65-104">In this quickstart, you translate text from one language to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ca65-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1ca65-105">Prerequisites</span></span>

<span data-ttu-id="1ca65-106">You'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="1ca65-106">You'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="1ca65-107">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="1ca65-107">(The free Community Edition will work.)</span></span>

<span data-ttu-id="1ca65-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="1ca65-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="translate-request"></a><span data-ttu-id="1ca65-109">Translate request</span><span class="sxs-lookup"><span data-stu-id="1ca65-109">Translate request</span></span>

<span data-ttu-id="1ca65-110">The following code translates source text from one language to another using the [Translate](./reference/v3-0-translate.md) method.</span><span class="sxs-lookup"><span data-stu-id="1ca65-110">The following code translates source text from one language to another using the [Translate](./reference/v3-0-translate.md) method.</span></span>

1. <span data-ttu-id="1ca65-111">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1ca65-111">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="1ca65-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1ca65-112">Add the code provided below.</span></span>
3. <span data-ttu-id="1ca65-113">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1ca65-113">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1ca65-114">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1ca65-114">Run the program.</span></span>

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
        static string path = "/translate?api-version=3.0";
        // Translate to German and Italian.
        static string params_ = "&to=de&to=it";

        static string uri = host + path + params_;

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string text = "Hello world!";

        async static void Translate()
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
            Translate();
            Console.ReadLine();
        }
    }
}
```

## <a name="translate-response"></a><span data-ttu-id="1ca65-115">Translate response</span><span class="sxs-lookup"><span data-stu-id="1ca65-115">Translate response</span></span>

<span data-ttu-id="1ca65-116">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1ca65-116">A successful response is returned in JSON as shown in the following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1ca65-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ca65-117">Next steps</span></span>

<span data-ttu-id="1ca65-118">Explore the sample code for this quickstart and others, including transliteration and language identification, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="1ca65-118">Explore the sample code for this quickstart and others, including transliteration and language identification, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ca65-119">Explore C# examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="1ca65-119">Explore C# examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=c%23)
