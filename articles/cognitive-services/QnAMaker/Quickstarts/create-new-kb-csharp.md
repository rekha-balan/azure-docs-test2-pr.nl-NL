---
title: Create a new knowledge base - quickstart C# - for Microsoft QnA Maker API (V4) - Azure Cognitive Services | Microsoft Docs
description: Create a knowledge base in C# to hold your FAQs or product manuals, so you can get started with QnA Maker.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: quickstart
ms.date: 06/15/2018
ms.author: nolachar
ms.openlocfilehash: 16d17a335bb84212497010b3eeb930582fa86dc4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868495"
---
# <a name="create-a-new-knowledge-base-in-c"></a><span data-ttu-id="945e8-103">Create a new knowledge base in C#</span><span class="sxs-lookup"><span data-stu-id="945e8-103">Create a new knowledge base in C#</span></span>

<span data-ttu-id="945e8-104">This quickstart walks you through creating a sample QnA maker knowledge base, programmatically, that will appear in your Azure Dashboard of your Cognitive Services API account.</span><span class="sxs-lookup"><span data-stu-id="945e8-104">This quickstart walks you through creating a sample QnA maker knowledge base, programmatically, that will appear in your Azure Dashboard of your Cognitive Services API account.</span></span>

<span data-ttu-id="945e8-105">Two sample FAQ URLs are given below ('urls' in the string kb).</span><span class="sxs-lookup"><span data-stu-id="945e8-105">Two sample FAQ URLs are given below ('urls' in the string kb).</span></span> <span data-ttu-id="945e8-106">QnA Maker automatically extracts questions and answers from semi-structured content, like FAQs, as explained more in this [data sources](../Concepts/data-sources-supported.md) document.</span><span class="sxs-lookup"><span data-stu-id="945e8-106">QnA Maker automatically extracts questions and answers from semi-structured content, like FAQs, as explained more in this [data sources](../Concepts/data-sources-supported.md) document.</span></span> <span data-ttu-id="945e8-107">You may also use your own FAQ URLs in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="945e8-107">You may also use your own FAQ URLs in this quickstart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="945e8-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="945e8-108">Prerequisites</span></span>

<span data-ttu-id="945e8-109">If your preferred IDE is Visual Studio, you'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code sample on Windows.</span><span class="sxs-lookup"><span data-stu-id="945e8-109">If your preferred IDE is Visual Studio, you'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code sample on Windows.</span></span> <span data-ttu-id="945e8-110">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="945e8-110">(The free Community Edition will work.)</span></span>

<span data-ttu-id="945e8-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **QnA Maker** chosen as your resource.</span><span class="sxs-lookup"><span data-stu-id="945e8-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **QnA Maker** chosen as your resource.</span></span> <span data-ttu-id="945e8-112">You'll need a paid subscription key from your new API account in your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="945e8-112">You'll need a paid subscription key from your new API account in your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span> <span data-ttu-id="945e8-113">To retrieve your key, select **Keys** under **Resource Management** in your dashboard.</span><span class="sxs-lookup"><span data-stu-id="945e8-113">To retrieve your key, select **Keys** under **Resource Management** in your dashboard.</span></span> <span data-ttu-id="945e8-114">Either key will work for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="945e8-114">Either key will work for this quickstart.</span></span>

![Azure dashboard service key](../media/sub-key.png)

## <a name="create-knowledge-base"></a><span data-ttu-id="945e8-116">Create knowledge base</span><span class="sxs-lookup"><span data-stu-id="945e8-116">Create knowledge base</span></span>

<span data-ttu-id="945e8-117">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span><span class="sxs-lookup"><span data-stu-id="945e8-117">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span></span>

1. <span data-ttu-id="945e8-118">Create a new .NET Framework C# console application in your preferred IDE.</span><span class="sxs-lookup"><span data-stu-id="945e8-118">Create a new .NET Framework C# console application in your preferred IDE.</span></span>
2. <span data-ttu-id="945e8-119">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="945e8-119">Add the code provided below.</span></span>
3. <span data-ttu-id="945e8-120">Replace the `key` value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="945e8-120">Replace the `key` value with your valid subscription key.</span></span>
4. <span data-ttu-id="945e8-121">Run the program.</span><span class="sxs-lookup"><span data-stu-id="945e8-121">Run the program.</span></span>

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
        // Represents the various elements used to create HTTP request URIs
        // for QnA Maker operations.
        static string host = "https://westus.api.cognitive.microsoft.com";
        static string service = "/qnamaker/v4.0";
        static string method = "/knowledgebases/create";

        // NOTE: Replace this value with a valid QnA Maker subscription key.
        static string key = "YOUR SUBSCRIPTION KEY HERE";

        /// <summary>
        /// Defines the data source used to create the knowledge base.
        /// The data source includes a QnA pair, with metadata, 
        /// the URL for the QnA Maker FAQ article, and 
        /// the URL for the Azure Bot Service FAQ article.
        /// </summary>
        static string kb = @"
{
  'name': 'QnA Maker FAQ',
  'qnaList': [
    {
      'id': 0,
      'answer': 'You can use our REST APIs to manage your knowledge base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/58994a073d9e04097c7ba6fe/operations/58994a073d9e041ad42d9baa',
      'source': 'Custom Editorial',
      'questions': [
        'How do I programmatically update my knowledge base?'
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

        /// <summary>
        /// Represents the HTTP response returned by an HTTP request.
        /// </summary>
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

        /// <summary>
        /// Formats and indents JSON for display.
        /// </summary>
        /// <param name="s">The JSON to format and indent.</param>
        /// <returns>A string containing formatted and indented JSON.</returns>
        static string PrettyPrint(string s)
        {
            return JsonConvert.SerializeObject(JsonConvert.DeserializeObject(s), Formatting.Indented);
        }

        /// <summary>
        /// Asynchronously sends a POST HTTP request.
        /// </summary>
        /// <param name="uri">The URI of the HTTP request.</param>
        /// <param name="body">The body of the HTTP request.</param>
        /// <returns>A <see cref="System.Threading.Tasks.Task{TResult}(QnAMaker.Program.Response)"/> 
        /// object that represents the HTTP response."</returns>
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

        /// <summary>
        /// Asynchronously sends a GET HTTP request.
        /// </summary>
        /// <param name="uri">The URI of the HTTP request.</param>
        /// <returns>A <see cref="System.Threading.Tasks.Task{TResult}(QnAMaker.Program.Response)"/> 
        /// object that represents the HTTP response."</returns>
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

        /// <summary>
        /// Creates a knowledge base.
        /// </summary>
        /// <param name="kb">The data source for the knowledge base.</param>
        /// <returns>A <see cref="System.Threading.Tasks.Task{TResult}(QnAMaker.Program.Response)"/> 
        /// object that represents the HTTP response."</returns>
        /// <remarks>The method constructs the URI to create a knowledge base in QnA Maker, and then
        /// asynchronously invokes the <see cref="QnAMaker.Program.Post(string, string)"/> method
        /// to send the HTTP request.</remarks>
        async static Task<Response> PostCreateKB(string kb)
        {
            // Builds the HTTP request URI.
            string uri = host + service + method;
            
            // Writes the HTTP request URI to the console, for display purposes.
            Console.WriteLine("Calling " + uri + ".");

            // Asynchronously invokes the Post(string, string) method, using the
            // HTTP request URI and the specified data source.
            return await Post(uri, kb);
        }

        /// <summary>
        /// Gets the status of the specified QnA Maker operation.
        /// </summary>
        /// <param name="operation">The QnA Maker operation to check.</param>
        /// <returns>A <see cref="System.Threading.Tasks.Task{TResult}(QnAMaker.Program.Response)"/> 
        /// object that represents the HTTP response."</returns>
        /// <remarks>The method constructs the URI to get the status of a QnA Maker operation, and
        /// then asynchronously invokes the <see cref="QnAMaker.Program.Get(string)"/> method
        /// to send the HTTP request.</remarks>
        async static Task<Response> GetStatus(string operation)
        {
            // Builds the HTTP request URI.
            string uri = host + service + operation;

            // Writes the HTTP request URI to the console, for display purposes.
            Console.WriteLine("Calling " + uri + ".");

            // Asynchronously invokes the Get(string) method, using the
            // HTTP request URI.
            return await Get(uri);
        }

        /// <summary>
        /// Creates a knowledge base, periodically checking status 
        /// until the knowledge base is created.
        /// </summary>
        async static void CreateKB()
        {
            try
            {
                // Starts the QnA Maker operation to create the knowledge base.
                var response = await PostCreateKB(kb);

                // Retrieves the operation ID, so the operation's status can be
                // checked periodically.
                var operation = response.headers.GetValues("Location").First();

                // Displays the JSON in the HTTP response returned by the 
                // PostCreateKB(string) method.
                Console.WriteLine(PrettyPrint(response.response));

                // Iteratively gets the state of the operation creating the
                // knowledge base. Once the operation state is set to something other
                // than "Running" or "NotStarted", the loop ends.
                var done = false;
                while (true != done)
                {
                    // Gets the status of the operation.
                    response = await GetStatus(operation);

                    // Displays the JSON in the HTTP response returned by the
                    // GetStatus(string) method.
                    Console.WriteLine(PrettyPrint(response.response));

                    // Deserialize the JSON into key-value pairs, to retrieve the
                    // state of the operation.
                    var fields = JsonConvert.DeserializeObject<Dictionary<string, string>>(response.response);

                    // Gets and checks the state of the operation.
                    String state = fields["operationState"];
                    if (state.CompareTo("Running") == 0 || state.CompareTo("NotStarted") == 0)
                    {
                        // QnA Maker is still creating the knowledge base. The thread is 
                        // paused for a number of seconds equal to the Retry-After header value,
                        // and then the loop continues.
                        var wait = response.headers.GetValues("Retry-After").First();
                        Console.WriteLine("Waiting " + wait + " seconds...");
                        Thread.Sleep(Int32.Parse(wait) * 1000);
                    }
                    else
                    {
                        // QnA Maker has completed creating the knowledge base. 
                        done = true;
                    }
                }
            }
            catch
            {
                // An error occurred while creating the knowledge base. Ensure that
                // you included your QnA Maker subscription key where directed in the sample.
                Console.WriteLine("An error occurred while creating the knowledge base.");
            }
            finally
            {
                Console.WriteLine("Press any key to continue.");
            }

        }

        static void Main(string[] args)
        {
            // Invoke the CreateKB() method to create a knowledge base, periodically 
            // checking the status of the QnA Maker operation until the 
            // knowledge base is created.
            CreateKB();

            // The console waits for a key to be pressed before closing.
            Console.ReadLine();
        }
    }
}
  
```

## <a name="understand-what-qna-maker-returns"></a><span data-ttu-id="945e8-122">Understand what QnA Maker returns</span><span class="sxs-lookup"><span data-stu-id="945e8-122">Understand what QnA Maker returns</span></span>

<span data-ttu-id="945e8-123">A successful response is returned in JSON, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="945e8-123">A successful response is returned in JSON, as shown in the following example.</span></span> <span data-ttu-id="945e8-124">Your results may differ slightly.</span><span class="sxs-lookup"><span data-stu-id="945e8-124">Your results may differ slightly.</span></span> <span data-ttu-id="945e8-125">If the final call returns a "Succeeded" state... your knowledge base was created successfully.</span><span class="sxs-lookup"><span data-stu-id="945e8-125">If the final call returns a "Succeeded" state... your knowledge base was created successfully.</span></span> <span data-ttu-id="945e8-126">To troubleshoot refer to the [Get Operation Details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) of the QnA Maker API.</span><span class="sxs-lookup"><span data-stu-id="945e8-126">To troubleshoot refer to the [Get Operation Details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) of the QnA Maker API.</span></span>

```json
Calling https://westus.api.cognitive.microsoft.com/qnamaker/v4.0/knowledgebases/create.
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-06-25T10:30:15Z",
  "lastActionTimestamp": "2018-06-25T10:30:15Z",
  "userId": "0d85ec291c204197a70cfec51725cd22",
  "operationId": "d9d40918-01bd-49f4-88b4-129fbc434c94"
}
Calling https://westus.api.cognitive.microsoft.com/qnamaker/v4.0/operations/d9d40918-01bd-49f4-88b4-129fbc434c94.
{
  "operationState": "Running",
  "createdTimestamp": "2018-06-25T10:30:15Z",
  "lastActionTimestamp": "2018-06-25T10:30:15Z",
  "userId": "0d85ec291c184197a70cfeb51025cd22",
  "operationId": "d9d40918-01bd-49f4-88b4-129fbc434c94"
}
Waiting 30 seconds...
Calling https://westus.api.cognitive.microsoft.com/qnamaker/v4.0/operations/d9d40918-01bd-49f4-88b4-129fbc434c94.
{
  "operationState": "Running",
  "createdTimestamp": "2018-06-25T10:30:15Z",
  "lastActionTimestamp": "2018-06-25T10:30:15Z",
  "userId": "0d85ec221c284197a70gfeb51725cd22",
  "operationId": "d9d40918-01bd-49f4-88b4-129fbc434c94"
}
Waiting 30 seconds...
Calling https://westus.api.cognitive.microsoft.com/qnamaker/v4.0/operations/d9d40918-01bd-49f4-88b4-129fbc434c94.
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-06-25T10:30:15Z",
  "lastActionTimestamp": "2018-06-25T10:30:51Z",
  "resourceLocation": "/knowledgebases/1d9eb2a1-de2a-4709-91b2-f6ea8afb6fb9",
  "userId": "0d85ec294c284197a70cfeb51775cd22",
  "operationId": "d9d40918-01bd-49f4-88b4-129fbc434c94"
}
Press any key to continue.
```

<span data-ttu-id="945e8-127">Once your knowledge base is created, you can view it in your QnA Maker Portal, [My knowledge bases](https://www.qnamaker.ai/Home/MyServices) page.</span><span class="sxs-lookup"><span data-stu-id="945e8-127">Once your knowledge base is created, you can view it in your QnA Maker Portal, [My knowledge bases](https://www.qnamaker.ai/Home/MyServices) page.</span></span> <span data-ttu-id="945e8-128">Select your knowledge base name, for example QnA Maker FAQ, to view.</span><span class="sxs-lookup"><span data-stu-id="945e8-128">Select your knowledge base name, for example QnA Maker FAQ, to view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="945e8-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="945e8-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="945e8-130">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="945e8-130">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)
