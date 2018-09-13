---
title: C# Quickstart for Bing Spell Check API - Azure Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Spell Check API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: quickstart
ms.date: 09/14/2017
ms.author: v-jaswel
ms.openlocfilehash: e655963df4756accc52aa7d5f57e74658cb9edc9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870673"
---
# <a name="quickstart-for-bing-spell-check-api-with-c"></a><span data-ttu-id="0277f-103">Quickstart for Bing Spell Check API with C#</span><span class="sxs-lookup"><span data-stu-id="0277f-103">Quickstart for Bing Spell Check API with C#</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="0277f-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with C#.</span><span class="sxs-lookup"><span data-stu-id="0277f-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with C#.</span></span> <span data-ttu-id="0277f-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span><span class="sxs-lookup"><span data-stu-id="0277f-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span></span> <span data-ttu-id="0277f-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span><span class="sxs-lookup"><span data-stu-id="0277f-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span></span> <span data-ttu-id="0277f-107">This article shows how to send a request that contains the text "Hollo, wrld!"</span><span class="sxs-lookup"><span data-stu-id="0277f-107">This article shows how to send a request that contains the text "Hollo, wrld!"</span></span> <span data-ttu-id="0277f-108">The suggested replacements are "Hello" and "world."</span><span class="sxs-lookup"><span data-stu-id="0277f-108">The suggested replacements are "Hello" and "world."</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0277f-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0277f-109">Prerequisites</span></span>

<span data-ttu-id="0277f-110">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="0277f-110">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="0277f-111">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="0277f-111">(The free Community Edition will work.)</span></span>

<span data-ttu-id="0277f-112">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span><span class="sxs-lookup"><span data-stu-id="0277f-112">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span></span> <span data-ttu-id="0277f-113">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="0277f-113">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span></span> <span data-ttu-id="0277f-114">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="0277f-114">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="get-spell-check-results"></a><span data-ttu-id="0277f-115">Get Spell Check results</span><span class="sxs-lookup"><span data-stu-id="0277f-115">Get Spell Check results</span></span>

1. <span data-ttu-id="0277f-116">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="0277f-116">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="0277f-117">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="0277f-117">Add the code provided below.</span></span>
3. <span data-ttu-id="0277f-118">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="0277f-118">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="0277f-119">Run the program.</span><span class="sxs-lookup"><span data-stu-id="0277f-119">Run the program.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;

namespace SpellCheckSample1
{
    class Program
    {
        static string host = "https://api.cognitive.microsoft.com";
        static string path = "/bing/v7.0/spellcheck?";

        // For a list of available markets, go to:
        // https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference#market-codes
        static string params_ = "mkt=en-US&mode=proof";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string text = "Hollo, wrld!";

        // These properties are used for optional headers (see below).
        // static string ClientId = "<Client ID from Previous Response Goes Here>";
        //static string ClientId = "2325577A61966D252A475CD760C96C03";
        // static string ClientIp = "999.999.999.999";
        // static string ClientLocation = "+90.0000000000000;long: 00.0000000000000;re:100.000000000000";

        async static void SpellCheck()
        {
            HttpClient client = new HttpClient();
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", key);

            // The following headers are optional, but it is recommended they be treated as required.
            // These headers help the service return more accurate results.
            //client.DefaultRequestHeaders.Add("X-Search-Location", ClientLocation);
            //client.DefaultRequestHeaders.Add("X-MSEdge-ClientID", ClientId);
            //client.DefaultRequestHeaders.Add("X-MSEdge-ClientIP", ClientIp);

            HttpResponseMessage response = new HttpResponseMessage();
            string uri = host + path + params_;

            List<KeyValuePair<string, string>> values = new List<KeyValuePair<string, string>>();
            values.Add(new KeyValuePair<string, string>("text", text));

            using (FormUrlEncodedContent content = new FormUrlEncodedContent(values))
            {
                content.Headers.ContentType = new MediaTypeHeaderValue("application/x-www-form-urlencoded");
                response = await client.PostAsync(uri, content);
            }

            string client_id;
            if (response.Headers.TryGetValues("X-MSEdge-ClientID", out IEnumerable<string> header_values))
            {
                client_id = header_values.First();
                Console.WriteLine("Client ID: " + client_id);
            }

            string contentString = await response.Content.ReadAsStringAsync();
            Console.WriteLine(JsonPrettyPrint(contentString));

        }

        static void Main(string[] args)
        {
            SpellCheck();
            Console.ReadLine();
        }

        static string JsonPrettyPrint(string json)
        {
            if (string.IsNullOrEmpty(json))
            {
                return string.Empty;
            }

            json = json.Replace(Environment.NewLine, "").Replace("\t", "");

            StringBuilder sb = new StringBuilder();
            bool quote = false;
            bool ignore = false;
            char last = ' ';
            int offset = 0;
            int indentLength = 3;

            foreach (char ch in json)
            {
                switch (ch)
                {
                    case '"':
                        if (!ignore) quote = !quote;
                        break;
                    case '\\':
                        if (quote && last != '\\') ignore = true;
                        break;
                }

                if (quote)
                {
                    sb.Append(ch);
                    if (last == '\\' && ignore) ignore = false;
                }
                else
                {
                    switch (ch)
                    {
                        case '{':
                        case '[':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', ++offset * indentLength));
                            break;
                        case '}':
                        case ']':
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', --offset * indentLength));
                            sb.Append(ch);
                            break;
                        case ',':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', offset * indentLength));
                            break;
                        case ':':
                            sb.Append(ch);
                            sb.Append(' ');
                            break;
                        default:
                            if (quote || ch != ' ') sb.Append(ch);
                            break;
                    }
                }
                last = ch;
            }

            return sb.ToString().Trim();
        }
    }
}
```

<span data-ttu-id="0277f-120">**Response**</span><span class="sxs-lookup"><span data-stu-id="0277f-120">**Response**</span></span>

<span data-ttu-id="0277f-121">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="0277f-121">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="0277f-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="0277f-122">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0277f-123">Bing Spell Check tutorial</span><span class="sxs-lookup"><span data-stu-id="0277f-123">Bing Spell Check tutorial</span></span>](../tutorials/spellcheck.md)

## <a name="see-also"></a><span data-ttu-id="0277f-124">See also</span><span class="sxs-lookup"><span data-stu-id="0277f-124">See also</span></span>

- [<span data-ttu-id="0277f-125">Bing Spell Check overview</span><span class="sxs-lookup"><span data-stu-id="0277f-125">Bing Spell Check overview</span></span>](../proof-text.md)
- [<span data-ttu-id="0277f-126">Bing Spell Check API v7 Reference</span><span class="sxs-lookup"><span data-stu-id="0277f-126">Bing Spell Check API v7 Reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference)
