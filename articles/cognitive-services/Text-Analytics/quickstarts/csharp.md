---
title: 'Quickstart: Using C# to call the Text Analytics API | Microsoft Docs'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started with using the Text Analytics API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: luiscabrer
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 08/30/2018
ms.author: ashmaka
ms.openlocfilehash: b4d945b7495897caf1f4edd1e909581614798a23
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868723"
---
# <a name="quickstart-using-c-to-call-the-text-analytics-cognitive-service"></a><span data-ttu-id="5495e-103">Quickstart: Using C# to call the Text Analytics Cognitive Service</span><span class="sxs-lookup"><span data-stu-id="5495e-103">Quickstart: Using C# to call the Text Analytics Cognitive Service</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="5495e-104">This article shows you how to detect language, analyze sentiment, and extract key phrases by using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with C#.</span><span class="sxs-lookup"><span data-stu-id="5495e-104">This article shows you how to detect language, analyze sentiment, and extract key phrases by using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with C#.</span></span> <span data-ttu-id="5495e-105">The code was written to work on a .NET Core application, with minimal references to external libraries, so you can also run it on Linux or MacOS.</span><span class="sxs-lookup"><span data-stu-id="5495e-105">The code was written to work on a .NET Core application, with minimal references to external libraries, so you can also run it on Linux or MacOS.</span></span>

<span data-ttu-id="5495e-106">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span><span class="sxs-lookup"><span data-stu-id="5495e-106">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5495e-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5495e-107">Prerequisites</span></span>

<span data-ttu-id="5495e-108">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with the Text Analytics API.</span><span class="sxs-lookup"><span data-stu-id="5495e-108">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with the Text Analytics API.</span></span> <span data-ttu-id="5495e-109">You can use the *free tier for 5,000 transactions/month* to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="5495e-109">You can use the *free tier for 5,000 transactions/month* to complete this quickstart.</span></span>

<span data-ttu-id="5495e-110">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that were generated for you during sign-up.</span><span class="sxs-lookup"><span data-stu-id="5495e-110">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that were generated for you during sign-up.</span></span> 


## <a name="install-the-nuget-sdk-package"></a><span data-ttu-id="5495e-111">Install the NuGet SDK package</span><span class="sxs-lookup"><span data-stu-id="5495e-111">Install the NuGet SDK package</span></span>
1. <span data-ttu-id="5495e-112">Create a new console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5495e-112">Create a new console solution in Visual Studio.</span></span>
1. <span data-ttu-id="5495e-113">Right-click the solution and select **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="5495e-113">Right-click the solution and select **Manage NuGet Packages for Solution**.</span></span>
1. <span data-ttu-id="5495e-114">Select the **Include Prerelease** check box.</span><span class="sxs-lookup"><span data-stu-id="5495e-114">Select the **Include Prerelease** check box.</span></span>
1. <span data-ttu-id="5495e-115">Select the **Browse** tab, and search for **Microsoft.Azure.CognitiveServices.Language**.</span><span class="sxs-lookup"><span data-stu-id="5495e-115">Select the **Browse** tab, and search for **Microsoft.Azure.CognitiveServices.Language**.</span></span>
1. <span data-ttu-id="5495e-116">Select the **Microsoft.Azure.CognitiveServices.Language.TextAnalytics** NuGet package and install it.</span><span class="sxs-lookup"><span data-stu-id="5495e-116">Select the **Microsoft.Azure.CognitiveServices.Language.TextAnalytics** NuGet package and install it.</span></span>

> [!Tip]
> <span data-ttu-id="5495e-117">Although you can call the [HTTP endpoints](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) directly from C#, the Microsoft.Azure.CognitiveServices.Language SDK makes it much easier to call the service without having to worry about serializing and deserializing JSON.</span><span class="sxs-lookup"><span data-stu-id="5495e-117">Although you can call the [HTTP endpoints](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) directly from C#, the Microsoft.Azure.CognitiveServices.Language SDK makes it much easier to call the service without having to worry about serializing and deserializing JSON.</span></span>
>
> <span data-ttu-id="5495e-118">Here are useful links:</span><span class="sxs-lookup"><span data-stu-id="5495e-118">Here are useful links:</span></span>
> - [<span data-ttu-id="5495e-119">SDK NuGet page</span><span class="sxs-lookup"><span data-stu-id="5495e-119">SDK NuGet page</span></span>](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Language.TextAnalytics)
> - [<span data-ttu-id="5495e-120">SDK code</span><span class="sxs-lookup"><span data-stu-id="5495e-120">SDK code</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/CognitiveServices/dataPlane/Language/TextAnalytics)


## <a name="call-the-text-analytics-api-by-using-the-sdk"></a><span data-ttu-id="5495e-121">Call the Text Analytics API by using the SDK</span><span class="sxs-lookup"><span data-stu-id="5495e-121">Call the Text Analytics API by using the SDK</span></span>
1. <span data-ttu-id="5495e-122">Replace Program.cs with the following code.</span><span class="sxs-lookup"><span data-stu-id="5495e-122">Replace Program.cs with the following code.</span></span> <span data-ttu-id="5495e-123">This program demonstrates the capabilities of the Text Analytics API in three sections (language extraction, key-phrase extraction, and sentiment analysis).</span><span class="sxs-lookup"><span data-stu-id="5495e-123">This program demonstrates the capabilities of the Text Analytics API in three sections (language extraction, key-phrase extraction, and sentiment analysis).</span></span>
1. <span data-ttu-id="5495e-124">Replace the `Ocp-Apim-Subscription-Key` header value with an access key that's valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="5495e-124">Replace the `Ocp-Apim-Subscription-Key` header value with an access key that's valid for your subscription.</span></span>
1. <span data-ttu-id="5495e-125">Replace the location in `Endpoint` to the endpoint that you signed up for.</span><span class="sxs-lookup"><span data-stu-id="5495e-125">Replace the location in `Endpoint` to the endpoint that you signed up for.</span></span> <span data-ttu-id="5495e-126">You can find the endpoint on the Azure portal resource.</span><span class="sxs-lookup"><span data-stu-id="5495e-126">You can find the endpoint on the Azure portal resource.</span></span> <span data-ttu-id="5495e-127">The endpoint typically starts with "https://[region].api.cognitive.microsoft.com."</span><span class="sxs-lookup"><span data-stu-id="5495e-127">The endpoint typically starts with "https://[region].api.cognitive.microsoft.com."</span></span> <span data-ttu-id="5495e-128">Include only the protocol and host name.</span><span class="sxs-lookup"><span data-stu-id="5495e-128">Include only the protocol and host name.</span></span>
1. <span data-ttu-id="5495e-129">Run the program.</span><span class="sxs-lookup"><span data-stu-id="5495e-129">Run the program.</span></span>

```csharp
using System;
using Microsoft.Azure.CognitiveServices.Language.TextAnalytics;
using Microsoft.Azure.CognitiveServices.Language.TextAnalytics.Models;
using System.Collections.Generic;
using Microsoft.Rest;
using System.Linq;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;

namespace ConsoleApp1
{
    class Program
    {
        /// <summary>
        /// Container for subscription credentials. Make sure to enter your valid key.
        /// </summary>
        class ApiKeyServiceClientCredentials : ServiceClientCredentials
        {
            public override Task ProcessHttpRequestAsync(HttpRequestMessage request, CancellationToken cancellationToken)
            {
                request.Headers.Add("Ocp-Apim-Subscription-Key", "ENTER KEY HERE");
                return base.ProcessHttpRequestAsync(request, cancellationToken);
            }
        }

        static void Main(string[] args)
        {

            // Create a client.
            ITextAnalyticsClient client = new TextAnalyticsClient(new ApiKeyServiceClientCredentials())
            {
                Endpoint = "https://westus.api.cognitive.microsoft.com"
            };

            Console.OutputEncoding = System.Text.Encoding.UTF8;
```

## <a name="detect-language"></a><span data-ttu-id="5495e-130">Detect language</span><span class="sxs-lookup"><span data-stu-id="5495e-130">Detect language</span></span>

<span data-ttu-id="5495e-131">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span><span class="sxs-lookup"><span data-stu-id="5495e-131">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span></span>

```csharp
            // Extracting language.
            Console.WriteLine("===== LANGUAGE EXTRACTION ======");

            var result =  client.DetectLanguageAsync(new BatchInput(
                    new List<Input>()
                        {
                          new Input("1", "This is a document written in English."),
                          new Input("2", "Este es un document escrito en Español."),
                          new Input("3", "这是一个用中文写的文件")
                    })).Result;

            // Printing language results.
            foreach (var document in result.Documents)
            {
                Console.WriteLine("Document ID: {0} , Language: {1}", document.Id, document.DetectedLanguages[0].Name);
            }
```

## <a name="extract-key-phrases"></a><span data-ttu-id="5495e-132">Extract key phrases</span><span class="sxs-lookup"><span data-stu-id="5495e-132">Extract key phrases</span></span>

<span data-ttu-id="5495e-133">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span><span class="sxs-lookup"><span data-stu-id="5495e-133">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span></span>

```csharp
            // Getting key phrases.
            Console.WriteLine("\n\n===== KEY-PHRASE EXTRACTION ======");

            KeyPhraseBatchResult result2 = client.KeyPhrasesAsync(new MultiLanguageBatchInput(
                        new List<MultiLanguageInput>()
                        {
                          new MultiLanguageInput("ja", "1", "猫は幸せ"),
                          new MultiLanguageInput("de", "2", "Fahrt nach Stuttgart und dann zum Hotel zu Fu."),
                          new MultiLanguageInput("en", "3", "My cat is stiff as a rock."),
                          new MultiLanguageInput("es", "4", "A mi me encanta el fútbol!")
                        })).Result;

            // Printing key phrases.
            foreach (var document in result2.Documents)
            {
                Console.WriteLine("Document ID: {0} ", document.Id);

                Console.WriteLine("\t Key phrases:");

                foreach (string keyphrase in document.KeyPhrases)
                {
                    Console.WriteLine("\t\t" + keyphrase);
                }
            }
```

## <a name="analyze-sentiment"></a><span data-ttu-id="5495e-134">Analyze sentiment</span><span class="sxs-lookup"><span data-stu-id="5495e-134">Analyze sentiment</span></span>

<span data-ttu-id="5495e-135">The Sentiment Analysis API detects the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span><span class="sxs-lookup"><span data-stu-id="5495e-135">The Sentiment Analysis API detects the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span></span>

```csharp
            // Analyzing sentiment.
            Console.WriteLine("\n\n===== SENTIMENT ANALYSIS ======");

            SentimentBatchResult result3 = client.SentimentAsync(
                    new MultiLanguageBatchInput(
                        new List<MultiLanguageInput>()
                        {
                          new MultiLanguageInput("en", "0", "I had the best day of my life."),
                          new MultiLanguageInput("en", "1", "This was a waste of my time. The speaker put me to sleep."),
                          new MultiLanguageInput("es", "2", "No tengo dinero ni nada que dar..."),
                          new MultiLanguageInput("it", "3", "L'hotel veneziano era meraviglioso. È un bellissimo pezzo di architettura."),
                        })).Result;


            // Printing sentiment results.
            foreach (var document in result3.Documents)
            {
                Console.WriteLine("Document ID: {0} , Sentiment Score: {1:0.00}", document.Id, document.Score);
            }
```

## <a name="identify-linked-entities"></a><span data-ttu-id="5495e-136">Identify linked entities</span><span class="sxs-lookup"><span data-stu-id="5495e-136">Identify linked entities</span></span>

<span data-ttu-id="5495e-137">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span><span class="sxs-lookup"><span data-stu-id="5495e-137">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span></span>

```csharp
            // Linking entities
            Console.WriteLine("\n\n===== ENTITY LINKING ======");

            EntitiesBatchResult result4 = client.EntitiesAsync(
                    new MultiLanguageBatchInput(
                        new List<MultiLanguageInput>()
                        {
                            new MultiLanguageInput("en", "0", "I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable."),
                            new MultiLanguageInput("en", "1", "The Seattle Seahawks won the Super Bowl in 2014."),
                        })).Result;

            // Printing entity results.
            foreach (var document in result4.Documents)
            {
                Console.WriteLine("Document ID: {0} , Entities: {1}", document.Id, String.Join(", ", document.Entities.Select(entity => entity.Name)));
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5495e-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="5495e-138">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5495e-139">Text Analytics with Power BI</span><span class="sxs-lookup"><span data-stu-id="5495e-139">Text Analytics with Power BI</span></span>](../tutorials/tutorial-power-bi-key-phrases.md)

## <a name="see-also"></a><span data-ttu-id="5495e-140">See also</span><span class="sxs-lookup"><span data-stu-id="5495e-140">See also</span></span> 

 [<span data-ttu-id="5495e-141">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="5495e-141">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="5495e-142">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="5495e-142">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)
