---
title: 'Quickstart: C# Publish Knowledge Base - Qna Maker'
titleSuffix: Azure Cognitive Services
description: How to publish a knowledge base in C# for QnA Maker.
services: cognitive-services
author: nitinme
manager: cgronlun
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: quickstart
ms.date: 06/18/2018
ms.author: nolachar
ms.openlocfilehash: ac7015ab4b039d7e5e79ca4274bd8a5d4a080b9e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867033"
---
# <a name="publish-a-knowledge-base-in-c"></a><span data-ttu-id="80b6c-103">Publish a knowledge base in C#</span><span class="sxs-lookup"><span data-stu-id="80b6c-103">Publish a knowledge base in C#</span></span>

<span data-ttu-id="80b6c-104">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span><span class="sxs-lookup"><span data-stu-id="80b6c-104">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span></span>

1. <span data-ttu-id="80b6c-105">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="80b6c-105">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="80b6c-106">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="80b6c-106">Add the code provided below.</span></span>
3. <span data-ttu-id="80b6c-107">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="80b6c-107">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="80b6c-108">Run the program.</span><span class="sxs-lookup"><span data-stu-id="80b6c-108">Run the program.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

// NOTE: Install the Newtonsoft.Json NuGet package.
using Newtonsoft.Json;

namespace QnAMaker
{
    class Program
    {
        static string host = "https://westus.api.cognitive.microsoft.com";
        static string service = "/qnamaker/v4.0";
        static string method = "/knowledgebases/";

        // NOTE: Replace this with a valid subscription key.
        static string key = "ENTER KEY HERE";

        // NOTE: Replace this with a valid knowledge base ID.
        static string kb = "ENTER ID HERE";

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<string> Post(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                if (response.IsSuccessStatusCode)
                {
                    return "{'result' : 'Success.'}";
                }
                else
                {
                    return await response.Content.ReadAsStringAsync();
                }
            }
        }

        async static void PublishKB()
        {
            var uri = host + service + method + kb;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Post(uri);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            PublishKB();
            Console.ReadLine();
        }
    }
}

```

## <a name="the-publish-a-knowledge-base-response"></a><span data-ttu-id="80b6c-109">The publish a knowledge base response</span><span class="sxs-lookup"><span data-stu-id="80b6c-109">The publish a knowledge base response</span></span>

<span data-ttu-id="80b6c-110">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="80b6c-110">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

## <a name="next-steps"></a><span data-ttu-id="80b6c-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="80b6c-111">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="80b6c-112">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="80b6c-112">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)