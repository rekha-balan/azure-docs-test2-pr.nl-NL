---
title: Translator Text convert text script with C# | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you convert text in one language from one script to another using the Translator Text API with C# in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/15/2018
ms.author: nolachar
ms.openlocfilehash: 66d649c0015be8c6a74e9925af68297334bfdb30
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870031"
---
# <a name="quickstart-transliterate-text-with-c35"></a><span data-ttu-id="8b97d-103">Quickstart: Transliterate text with C&#35;</span><span class="sxs-lookup"><span data-stu-id="8b97d-103">Quickstart: Transliterate text with C&#35;</span></span>

<span data-ttu-id="8b97d-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="8b97d-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b97d-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8b97d-105">Prerequisites</span></span>

<span data-ttu-id="8b97d-106">You'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="8b97d-106">You'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="8b97d-107">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="8b97d-107">(The free Community Edition will work.)</span></span>

<span data-ttu-id="8b97d-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="8b97d-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="transliterate-request"></a><span data-ttu-id="8b97d-109">Transliterate request</span><span class="sxs-lookup"><span data-stu-id="8b97d-109">Transliterate request</span></span>

<span data-ttu-id="8b97d-110">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span><span class="sxs-lookup"><span data-stu-id="8b97d-110">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span></span>

1. <span data-ttu-id="8b97d-111">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8b97d-111">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8b97d-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8b97d-112">Add the code provided below.</span></span>
3. <span data-ttu-id="8b97d-113">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8b97d-113">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8b97d-114">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8b97d-114">Run the program.</span></span>

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
        static string path = "/transliterate?api-version=3.0";
        // Transliterate text in Japanese from Japanese script (i.e. Hiragana/Katakana/Kanji) to Latin script.
        static string params_ = "&language=ja&fromScript=jpan&toScript=latn";

        static string uri = host + path + params_;

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        // Transliterate "good afternoon".
        static string text = "こんにちは";

        async static void Transliterate()
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
            Transliterate();
            Console.ReadLine();
        }
    }
}
```

## <a name="transliterate-response"></a><span data-ttu-id="8b97d-115">Transliterate response</span><span class="sxs-lookup"><span data-stu-id="8b97d-115">Transliterate response</span></span>

<span data-ttu-id="8b97d-116">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8b97d-116">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "text": "konnnichiha",
    "script": "latn"
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="8b97d-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b97d-117">Next steps</span></span>

<span data-ttu-id="8b97d-118">Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b97d-118">Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8b97d-119">Explore C# examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="8b97d-119">Explore C# examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=c%23)
