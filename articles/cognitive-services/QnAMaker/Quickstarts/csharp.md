---
title: 'Quickstart: C# for QnA Maker API (V4)'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Microsoft Translator Text API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: nitinme
manager: cgronlun
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jaswel
ms.openlocfilehash: 3c0248b08dbaa1d81843474fcc65590c719e8170
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856461"
---
# <a name="quickstart-for-microsoft-qna-maker-api-with-c"></a><span data-ttu-id="8ff6f-103">Quickstart for Microsoft QnA Maker API with C#</span><span class="sxs-lookup"><span data-stu-id="8ff6f-103">Quickstart for Microsoft QnA Maker API with C#</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="8ff6f-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with C# to do the following.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with C# to do the following.</span></span>

- [<span data-ttu-id="8ff6f-105">Create a new knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-105">Create a new knowledge base.</span></span>](#Create)
- [<span data-ttu-id="8ff6f-106">Update an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-106">Update an existing knowledge base.</span></span>](#Update)
- [<span data-ttu-id="8ff6f-107">Get the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-107">Get the status of a request to create or update a knowledge base.</span></span>](#Status)
- [<span data-ttu-id="8ff6f-108">Publish an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-108">Publish an existing knowledge base.</span></span>](#Publish)
- [<span data-ttu-id="8ff6f-109">Replace the contents of an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-109">Replace the contents of an existing knowledge base.</span></span>](#Replace)
- [<span data-ttu-id="8ff6f-110">Download the contents of a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-110">Download the contents of a knowledge base.</span></span>](#GetQnA)
- [<span data-ttu-id="8ff6f-111">Get answers to a question using a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-111">Get answers to a question using a knowledge base.</span></span>](#GetAnswers)
- [<span data-ttu-id="8ff6f-112">Get information about a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-112">Get information about a knowledge base.</span></span>](#GetKB)
- [<span data-ttu-id="8ff6f-113">Get information about all knowledge bases belonging to the specified user.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-113">Get information about all knowledge bases belonging to the specified user.</span></span>](#GetKBsByUser)
- [<span data-ttu-id="8ff6f-114">Delete a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-114">Delete a knowledge base.</span></span>](#Delete)
- [<span data-ttu-id="8ff6f-115">Get the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-115">Get the current endpoint keys.</span></span>](#GetKeys)
- [<span data-ttu-id="8ff6f-116">Re-generate the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-116">Re-generate the current endpoint keys.</span></span>](#PutKeys)
- [<span data-ttu-id="8ff6f-117">Get the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-117">Get the current set of word alterations.</span></span>](#GetAlterations)
- [<span data-ttu-id="8ff6f-118">Replace the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-118">Replace the current set of word alterations.</span></span>](#PutAlterations)

## <a name="prerequisites"></a><span data-ttu-id="8ff6f-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8ff6f-119">Prerequisites</span></span>

<span data-ttu-id="8ff6f-120">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-120">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="8ff6f-121">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="8ff6f-121">(The free Community Edition will work.)</span></span>

<span data-ttu-id="8ff6f-122">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-122">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span></span> <span data-ttu-id="8ff6f-123">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="8ff6f-123">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

<a name="Create"></a>

## <a name="create-knowledge-base"></a><span data-ttu-id="8ff6f-124">Create knowledge base</span><span class="sxs-lookup"><span data-stu-id="8ff6f-124">Create knowledge base</span></span>

<span data-ttu-id="8ff6f-125">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-125">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span></span>

1. <span data-ttu-id="8ff6f-126">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-126">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-127">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-127">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-128">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-128">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-129">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-129">Run the program.</span></span>

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
        static string method = "/knowledgebases/create";

        // NOTE: Replace this with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string kb = @"
{
  'name': 'QnA Maker FAQ',
  'qnaList': [
    {
      'id': 0,
      'answer': 'You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600',
      'source': 'Custom Editorial',
      'questions': [
        'How do I programmatically update my Knowledge Base?'
      ],
      'metadata': [
        {
          'name': 'category',
          'value': 'api'
        }
      ]
    }
  ],
  'urls': [
    'https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs',
    'https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq'
  ],
  'files': []
}
";

        public struct Response
        {
            public HttpResponseHeaders headers;
            public string response;

            public Response(HttpResponseHeaders headers, string response)
            {
                this.headers = headers;
                this.response = response;
            }
        }

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<Response> Post(string uri, string body)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(body, Encoding.UTF8, "application/json");
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();
                return new Response(response.Headers, responseBody);
            }
        }

        async static Task<Response> Get(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Get;
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();
                return new Response(response.Headers, responseBody);
            }
        }

        async static Task<Response> PostCreateKB(string kb)
        {
            string uri = host + service + method;
            Console.WriteLine("Calling " + uri + ".");
            return await Post(uri, kb);
        }

        async static Task<Response> GetStatus(string operation)
        {
            string uri = host + service + operation;
            Console.WriteLine("Calling " + uri + ".");
            return await Get(uri);
        }

        async static void CreateKB()
        {
            
            var response = await PostCreateKB(kb);
            var operation = response.headers.GetValues("Location").First();
            Console.WriteLine(PrettyPrint(response.response));

            var done = false;
            while (true != done)
            {
                response = await GetStatus(operation);
                Console.WriteLine(PrettyPrint(response.response));

                var fields = JsonConvert.DeserializeObject<Dictionary<string, string>>(response.response);

                String state = fields["operationState"];
                if (state.CompareTo("Running") == 0 || state.CompareTo("NotStarted") == 0)
                {
                    var wait = response.headers.GetValues("Retry-After").First();
                    Console.WriteLine("Waiting " + wait + " seconds...");
                    Thread.Sleep(Int32.Parse(wait) * 1000);
                }
                else
                {
                    Console.WriteLine("Press any key to continue.");
                    done = true;
                }
            }
        }

        static void Main(string[] args)
        {
            CreateKB();
            Console.ReadLine();
        }
    }
}

```

<span data-ttu-id="8ff6f-130">**Create knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-130">**Create knowledge base response**</span></span>

<span data-ttu-id="8ff6f-131">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-131">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
...
{
  "operationState": "Running",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:46Z",
  "resourceLocation": "/knowledgebases/b0288f33-27b9-4258-a304-8b9f63427dad",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
```

[<span data-ttu-id="8ff6f-132">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-132">Back to top</span></span>](#HOLTop)

<a name="Update"></a>

## <a name="update-knowledge-base"></a><span data-ttu-id="8ff6f-133">Update knowledge base</span><span class="sxs-lookup"><span data-stu-id="8ff6f-133">Update knowledge base</span></span>

<span data-ttu-id="8ff6f-134">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-134">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span></span>

1. <span data-ttu-id="8ff6f-135">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-135">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-136">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-136">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-137">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-137">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-138">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-138">Run the program.</span></span>

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

        static string new_kb = @"
{
  'add': {
    'qnaList': [
      {
        'id': 1,
        'answer': 'You can change the default message if you use the QnAMakerDialog. See this for details: https://docs.botframework.com/en-us/azure-bot-service/templates/qnamaker/#navtitle',
        'source': 'Custom Editorial',
        'questions': [
          'How can I change the default message from QnA Maker?'
        ],
        'metadata': []
      }
    ],
    'urls': [
      'https://docs.microsoft.com/en-us/azure/cognitive-services/Emotion/FAQ'
    ]
  },
  'update' : {
    'name' : 'New KB Name'
  },
  'delete': {
    'ids': [
      0
    ]
  }
}
";

        public struct Response
        {
            public HttpResponseHeaders headers;
            public string response;

            public Response(HttpResponseHeaders headers, string response)
            {
                this.headers = headers;
                this.response = response;
            }
        }

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<Response> Patch(string uri, string body)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = new HttpMethod("PATCH");
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(body, Encoding.UTF8, "application/json");
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();
                return new Response(response.Headers, responseBody);
            }
        }

        async static Task<Response> Get(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Get;
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();
                return new Response(response.Headers, responseBody);
            }
        }

        async static Task<Response> PostUpdateKB(string kb, string new_kb)
        {
            string uri = host + service + method + kb;
            Console.WriteLine("Calling " + uri + ".");
            return await Patch(uri, new_kb);
        }

        async static Task<Response> GetStatus(string operation)
        {
            string uri = host + service + operation;
            Console.WriteLine("Calling " + uri + ".");
            return await Get(uri);
        }

        async static void UpdateKB(string kb, string new_kb)
        {
            var response = await PostUpdateKB(kb, new_kb);
            var operation = response.headers.GetValues("Location").First();
            Console.WriteLine(PrettyPrint(response.response));

            var done = false;
            while (true != done)
            {
                response = await GetStatus(operation);
                Console.WriteLine(PrettyPrint(response.response));

                var fields = JsonConvert.DeserializeObject<Dictionary<string, string>>(response.response);

                String state = fields["operationState"];
                if (state.CompareTo("Running") == 0 || state.CompareTo("NotStarted") == 0)
                {
                    var wait = response.headers.GetValues("Retry-After").First();
                    Console.WriteLine("Waiting " + wait + " seconds...");
                    Thread.Sleep(Int32.Parse(wait) * 1000);
                }
                else
                {
                    Console.WriteLine("Press any key to continue.");
                    done = true;
                }
            }
        }

        static void Main(string[] args)
        {
            UpdateKB(kb, new_kb);
            Console.ReadLine();
        }
    }
}

```

<span data-ttu-id="8ff6f-139">**Update knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-139">**Update knowledge base response**</span></span>

<span data-ttu-id="8ff6f-140">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-140">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:48Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:50Z",
  "resourceLocation": "/knowledgebases/140a46f3-b248-4f1b-9349-614bfd6e5563",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
Press any key to continue.
```

[<span data-ttu-id="8ff6f-141">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-141">Back to top</span></span>](#HOLTop)

<a name="Status"></a>

## <a name="get-request-status"></a><span data-ttu-id="8ff6f-142">Get request status</span><span class="sxs-lookup"><span data-stu-id="8ff6f-142">Get request status</span></span>

<span data-ttu-id="8ff6f-143">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-143">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span></span> <span data-ttu-id="8ff6f-144">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-144">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span></span>

[<span data-ttu-id="8ff6f-145">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-145">Back to top</span></span>](#HOLTop)

<a name="Publish"></a>

## <a name="publish-knowledge-base"></a><span data-ttu-id="8ff6f-146">Publish knowledge base</span><span class="sxs-lookup"><span data-stu-id="8ff6f-146">Publish knowledge base</span></span>

<span data-ttu-id="8ff6f-147">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-147">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span></span>

1. <span data-ttu-id="8ff6f-148">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-148">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-149">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-149">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-150">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-150">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-151">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-151">Run the program.</span></span>

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

<span data-ttu-id="8ff6f-152">**Publish knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-152">**Publish knowledge base response**</span></span>

<span data-ttu-id="8ff6f-153">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-153">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="8ff6f-154">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-154">Back to top</span></span>](#HOLTop)

<a name="Replace"></a>

## <a name="replace-knowledge-base"></a><span data-ttu-id="8ff6f-155">Replace knowledge base</span><span class="sxs-lookup"><span data-stu-id="8ff6f-155">Replace knowledge base</span></span>

<span data-ttu-id="8ff6f-156">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-156">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span></span>

1. <span data-ttu-id="8ff6f-157">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-157">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-158">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-158">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-159">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-159">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-160">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-160">Run the program.</span></span>

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

        static string new_kb = @"
{
  'qnaList': [
    {
      'id': 0,
      'answer': 'You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600',
      'source': 'Custom Editorial',
      'questions': [
        'How do I programmatically update my Knowledge Base?'
      ],
      'metadata': [
        {
          'name': 'category',
          'value': 'api'
        }
      ]
    }
  ]
}
";

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<string> Put(string uri, String body)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Put;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(body, Encoding.UTF8, "application/json");
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

        async static void ReplaceKB()
        {
            var uri = host + service + method + kb;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Put(uri, new_kb);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            ReplaceKB();
            Console.ReadLine();
        }
    }
}

```

<span data-ttu-id="8ff6f-161">**Replace knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-161">**Replace knowledge base response**</span></span>

<span data-ttu-id="8ff6f-162">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-162">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
    "result": "Success."
}
```

[<span data-ttu-id="8ff6f-163">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-163">Back to top</span></span>](#HOLTop)

<a name="GetQnA"></a>

## <a name="download-the-contents-of-a-knowledge-base"></a><span data-ttu-id="8ff6f-164">Download the contents of a knowledge base</span><span class="sxs-lookup"><span data-stu-id="8ff6f-164">Download the contents of a knowledge base</span></span>

<span data-ttu-id="8ff6f-165">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-165">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span></span>

1. <span data-ttu-id="8ff6f-166">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-166">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-167">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-167">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-168">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-168">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-169">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-169">Run the program.</span></span>

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
        static string method = "/knowledgebases/{0}/{1}/qna/";

        // NOTE: Replace this with a valid subscription key.
        static string key = "ENTER KEY HERE";

        // NOTE: Replace this with a valid knowledge base ID.
        static string kb = "ENTER ID HERE";

        // NOTE: Replace this with "test" or "prod".
        static string env = "test";

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<string> Get(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Get;
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                return await response.Content.ReadAsStringAsync();
            }
        }

        async static void GetQnA()
        {
            var method_with_id = String.Format(method, kb, env);
            var uri = host + service + method_with_id;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Get(uri);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            GetQnA();
            Console.ReadLine();
        }
    }
}

```

<span data-ttu-id="8ff6f-170">**Download knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-170">**Download knowledge base response**</span></span>

<span data-ttu-id="8ff6f-171">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-171">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "qnaDocuments": [
    {
      "id": 1,
      "answer": "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600",
      "source": "Custom Editorial",
      "questions": [
        "How do I programmatically update my Knowledge Base?"
      ],
      "metadata": [
        {
          "name": "category",
          "value": "api"
        }
      ]
    },
    {
      "id": 2,
      "answer": "QnA Maker provides an FAQ data source that you can query from your bot or application. Although developers will find this useful, content owners will especially benefit from this tool. QnA Maker is a completely no-code way of managing the content that powers your bot or application.",
      "source": "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
      "questions": [
        "Who is the target audience for the QnA Maker tool?"
      ],
      "metadata": []
    },
...
  ]
}
```

[<span data-ttu-id="8ff6f-172">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-172">Back to top</span></span>](#HOLTop)

<a name="GetAnswers"></a>

## <a name="get-answers-to-a-question-by-using-a-knowledge-base"></a><span data-ttu-id="8ff6f-173">Get answers to a question by using a knowledge base</span><span class="sxs-lookup"><span data-stu-id="8ff6f-173">Get answers to a question by using a knowledge base</span></span>

<span data-ttu-id="8ff6f-174">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-174">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span></span>

1. <span data-ttu-id="8ff6f-175">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-175">Create a new C# project in your favorite IDE.</span></span>
1. <span data-ttu-id="8ff6f-176">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-176">Add the code provided below.</span></span>
1. <span data-ttu-id="8ff6f-177">Replace the `host` value with the Website name for your QnA Maker subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-177">Replace the `host` value with the Website name for your QnA Maker subscription.</span></span> <span data-ttu-id="8ff6f-178">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8ff6f-178">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span></span>
1. <span data-ttu-id="8ff6f-179">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-179">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span></span> <span data-ttu-id="8ff6f-180">Note this is not the same as your subscription key.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-180">Note this is not the same as your subscription key.</span></span> <span data-ttu-id="8ff6f-181">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-181">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span></span>
1. <span data-ttu-id="8ff6f-182">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-182">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span></span> <span data-ttu-id="8ff6f-183">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-183">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span></span>
1. <span data-ttu-id="8ff6f-184">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-184">Run the program.</span></span>

```csharp
using System;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

namespace QnAMaker
{
    class Program
    {
        // NOTE: Replace this with a valid host name.
        static string host = "ENTER HOST HERE";

        // NOTE: Replace this with a valid endpoint key.
        // This is not your subscription key.
        // To get your endpoint keys, call the GET /endpointkeys method.
        static string endpoint_key = "ENTER KEY HERE";

        // NOTE: Replace this with a valid knowledge base ID.
        // Make sure you have published the knowledge base with the
        // POST /knowledgebases/{knowledge base ID} method.
        static string kb = "ENTER KB ID HERE";

        static string service = "/qnamaker";
        static string method = "/knowledgebases/" + kb + "/generateAnswer/";

        static string question = @"
{
    'question': 'Is the QnA Maker Service free?',
    'top': 3
}
";

        async static Task<string> Post(string uri, string body)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(body, Encoding.UTF8, "application/json");
                request.Headers.Add("Authorization", "EndpointKey " + endpoint_key);

                var response = await client.SendAsync(request);
                return await response.Content.ReadAsStringAsync();
            }
        }

        async static void GetAnswers()
        {
            var uri = host + service + method;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Post(uri, question);
            Console.WriteLine(response);
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            GetAnswers();
            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="8ff6f-185">**Get answers response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-185">**Get answers response**</span></span>

<span data-ttu-id="8ff6f-186">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-186">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "answers": [
    {
      "questions": [
        "Can I use BitLocker with the Volume Shadow Copy Service?"
      ],
      "answer": "Yes. However, shadow copies made prior to enabling BitLocker will be automatically deleted when BitLocker is enabled on software-encrypted drives. If you are using a hardware encrypted drive, the shadow copies are retained.",
      "score": 17.3,
      "id": 62,
      "source": "https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-frequently-asked-questions",
      "metadata": []
    },
...
  ]
}
```

[<span data-ttu-id="8ff6f-187">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-187">Back to top</span></span>](#HOLTop)

<a name="GetKB"></a>

## <a name="get-information-about-a-knowledge-base"></a><span data-ttu-id="8ff6f-188">Get information about a knowledge base</span><span class="sxs-lookup"><span data-stu-id="8ff6f-188">Get information about a knowledge base</span></span>

<span data-ttu-id="8ff6f-189">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-189">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span></span>

1. <span data-ttu-id="8ff6f-190">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-190">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-191">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-191">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-192">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-192">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-193">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-193">Run the program.</span></span>

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

        async static Task<string> Get(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Get;
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                return await response.Content.ReadAsStringAsync();
            }
        }

        async static void GetKB()
        {
            var uri = host + service + method + kb;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Get(uri);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            GetKB();
            Console.ReadLine();
        }
    }
}

```

<span data-ttu-id="8ff6f-194">**Get knowledge base details response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-194">**Get knowledge base details response**</span></span>

<span data-ttu-id="8ff6f-195">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-195">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "id": "140a46f3-b248-4f1b-9349-614bfd6e5563",
  "hostName": "https://qna-docs.azurewebsites.net",
  "lastAccessedTimestamp": "2018-04-12T22:58:01Z",
  "lastChangedTimestamp": "2018-04-12T22:58:01Z",
  "name": "QnA Maker FAQ",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "urls": [
    "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
    "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
  ],
  "sources": [
    "Custom Editorial"
  ]
}
```

[<span data-ttu-id="8ff6f-196">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-196">Back to top</span></span>](#HOLTop)

<a name="GetKBsByUser"></a>

## <a name="get-all-knowledge-bases-for-a-user"></a><span data-ttu-id="8ff6f-197">Get all knowledge bases for a user</span><span class="sxs-lookup"><span data-stu-id="8ff6f-197">Get all knowledge bases for a user</span></span>

<span data-ttu-id="8ff6f-198">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-198">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span></span>

1. <span data-ttu-id="8ff6f-199">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-199">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-200">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-200">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-201">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-201">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-202">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-202">Run the program.</span></span>

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
        static string method = "/knowledgebases";

        // NOTE: Replace this with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<string> Get(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Get;
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                return await response.Content.ReadAsStringAsync();
            }
        }

        async static void GetKBsByUser()
        {
            var uri = host + service + method;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Get(uri);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            GetKBsByUser();
            Console.ReadLine();
        }
    }
}

```

<span data-ttu-id="8ff6f-203">**Get knowledge bases for user response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-203">**Get knowledge bases for user response**</span></span>

<span data-ttu-id="8ff6f-204">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-204">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "knowledgebases": [
    {
      "id": "081c32a7-bd05-4982-9d74-07ac736df0ac",
      "hostName": "https://qna-docs.azurewebsites.net",
      "lastAccessedTimestamp": "2018-04-12T11:51:58Z",
      "lastChangedTimestamp": "2018-04-12T11:51:58Z",
      "name": "QnA Maker FAQ",
      "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
      "urls": [],
      "sources": []
    },
    {
      "id": "140a46f3-b248-4f1b-9349-614bfd6e5563",
      "hostName": "https://qna-docs.azurewebsites.net",
      "lastAccessedTimestamp": "2018-04-12T22:58:01Z",
      "lastChangedTimestamp": "2018-04-12T22:58:01Z",
      "name": "QnA Maker FAQ",
      "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
      "urls": [
        "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
        "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
      ],
      "sources": [
        "Custom Editorial"
      ]
    },
...
  ]
}
Press any key to continue.
```

[<span data-ttu-id="8ff6f-205">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-205">Back to top</span></span>](#HOLTop)

<a name="Delete"></a>

## <a name="delete-a-knowledge-base"></a><span data-ttu-id="8ff6f-206">Delete a knowledge base</span><span class="sxs-lookup"><span data-stu-id="8ff6f-206">Delete a knowledge base</span></span>

<span data-ttu-id="8ff6f-207">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-207">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span></span>

1. <span data-ttu-id="8ff6f-208">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-208">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-209">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-209">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-210">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-210">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-211">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-211">Run the program.</span></span>

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

        async static Task<string> Delete(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Delete;
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

        async static void DeleteKB()
        {
            var uri = host + service + method + kb;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Delete(uri);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            DeleteKB();
            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="8ff6f-212">**Delete knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-212">**Delete knowledge base response**</span></span>

<span data-ttu-id="8ff6f-213">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-213">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="8ff6f-214">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-214">Back to top</span></span>](#HOLTop)

<a name="GetKeys"></a>

## <a name="get-endpoint-keys"></a><span data-ttu-id="8ff6f-215">Get endpoint keys</span><span class="sxs-lookup"><span data-stu-id="8ff6f-215">Get endpoint keys</span></span>

<span data-ttu-id="8ff6f-216">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-216">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span></span>

1. <span data-ttu-id="8ff6f-217">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-217">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-218">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-218">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-219">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-219">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-220">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-220">Run the program.</span></span>

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
        static string method = "/endpointkeys/";

        // NOTE: Replace this with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<string> Get(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Get;
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                return await response.Content.ReadAsStringAsync();
            }
        }

        async static void GetEndpointKeys()
        {
            var uri = host + service + method;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Get(uri);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            GetEndpointKeys();
            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="8ff6f-221">**Get endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-221">**Get endpoint keys response**</span></span>

<span data-ttu-id="8ff6f-222">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-222">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="8ff6f-223">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-223">Back to top</span></span>](#HOLTop)

<a name="PutKeys"></a>

## <a name="refresh-endpoint-keys"></a><span data-ttu-id="8ff6f-224">Refresh endpoint keys</span><span class="sxs-lookup"><span data-stu-id="8ff6f-224">Refresh endpoint keys</span></span>

<span data-ttu-id="8ff6f-225">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-225">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span></span>

1. <span data-ttu-id="8ff6f-226">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-226">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-227">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-227">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-228">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-228">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-229">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-229">Run the program.</span></span>

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
        static string method = "/endpointkeys/";

        // NOTE: Replace this with a valid subscription key.
        static string key = "ENTER KEY HERE";

        // NOTE: Replace this with "PrimaryKey" or "SecondaryKey."
        static string key_type = "PrimaryKey";

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<string> Patch(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = new HttpMethod("PATCH");
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                return await response.Content.ReadAsStringAsync();
            }
        }

        async static void RefreshEndpoints()
        {
            var uri = host + service + method + key_type;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Patch(uri);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            RefreshEndpoints();
            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="8ff6f-230">**Refresh endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-230">**Refresh endpoint keys response**</span></span>

<span data-ttu-id="8ff6f-231">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-231">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="8ff6f-232">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-232">Back to top</span></span>](#HOLTop)

<a name="GetAlterations"></a>

## <a name="get-word-alterations"></a><span data-ttu-id="8ff6f-233">Get word alterations</span><span class="sxs-lookup"><span data-stu-id="8ff6f-233">Get word alterations</span></span>

<span data-ttu-id="8ff6f-234">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-234">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span></span>

1. <span data-ttu-id="8ff6f-235">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-235">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-236">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-236">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-237">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-237">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-238">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-238">Run the program.</span></span>

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
        static string method = "/alterations/";

        // NOTE: Replace this with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<string> Get(string uri)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Get;
                request.RequestUri = new Uri(uri);
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                return await response.Content.ReadAsStringAsync();
            }
        }

        async static void GetAlterations()
        {
            var uri = host + service + method;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Get(uri);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            GetAlterations();
            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="8ff6f-239">**Get word alterations response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-239">**Get word alterations response**</span></span>

<span data-ttu-id="8ff6f-240">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-240">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "wordAlterations": [
    {
      "alterations": [
        "botframework",
        "bot frame work"
      ]
    }
  ]
}
```

[<span data-ttu-id="8ff6f-241">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-241">Back to top</span></span>](#HOLTop)

<a name="PutAlterations"></a>

## <a name="replace-word-alterations"></a><span data-ttu-id="8ff6f-242">Replace word alterations</span><span class="sxs-lookup"><span data-stu-id="8ff6f-242">Replace word alterations</span></span>

<span data-ttu-id="8ff6f-243">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-243">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span></span>

1. <span data-ttu-id="8ff6f-244">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-244">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8ff6f-245">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-245">Add the code provided below.</span></span>
3. <span data-ttu-id="8ff6f-246">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-246">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8ff6f-247">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8ff6f-247">Run the program.</span></span>

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
        static string method = "/alterations/";

        // NOTE: Replace this with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string alterations = @"
{
  'wordAlterations': [
    {
      'alterations': [
        'botframework',
        'bot frame work'
      ]
    }
  ]
}
";

        public struct Response
        {
            public HttpResponseHeaders headers;
            public string response;

            public Response(HttpResponseHeaders headers, string response)
            {
                this.headers = headers;
                this.response = response;
            }
        }

        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        async static Task<string> Put(string uri, string body)
        {
            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = new HttpMethod("PUT");
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(body, Encoding.UTF8, "application/json");
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

        async static void ReplaceAlterations(string alterations)
        {
            var uri = host + service + method;
            Console.WriteLine("Calling " + uri + ".");
            var response = await Put(uri, alterations);
            Console.WriteLine(PrettyPrint(response));
            Console.WriteLine("Press any key to continue.");
        }

        static void Main(string[] args)
        {
            ReplaceAlterations(alterations);
            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="8ff6f-248">**Replace word alterations response**</span><span class="sxs-lookup"><span data-stu-id="8ff6f-248">**Replace word alterations response**</span></span>

<span data-ttu-id="8ff6f-249">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8ff6f-249">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="8ff6f-250">Back to top</span><span class="sxs-lookup"><span data-stu-id="8ff6f-250">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="8ff6f-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ff6f-251">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ff6f-252">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="8ff6f-252">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)

## <a name="see-also"></a><span data-ttu-id="8ff6f-253">See also</span><span class="sxs-lookup"><span data-stu-id="8ff6f-253">See also</span></span> 

[<span data-ttu-id="8ff6f-254">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="8ff6f-254">QnA Maker overview</span></span>](../Overview/overview.md)
