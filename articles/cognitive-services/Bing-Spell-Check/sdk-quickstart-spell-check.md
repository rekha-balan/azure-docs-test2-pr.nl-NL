---
title: Spell Check SDK C# quickstart - Azure Cognitive Services | Microsoft Docs
description: Setup for Spell Check SDK console application
titleSuffix: Azure cognitive services setup Spell check search SDK C# console application
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: quickstart
ms.date: 01/30/2018
ms.author: v-gedod
ms.openlocfilehash: b64c1be49a26e1fadb504bed3ff8eb78d791539f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968271"
---
# <a name="spell-check-sdk-c-quickstart"></a><span data-ttu-id="65168-103">Spell Check SDK C# Quickstart</span><span class="sxs-lookup"><span data-stu-id="65168-103">Spell Check SDK C# Quickstart</span></span>

<span data-ttu-id="65168-104">The Bing Spell Check SDK contains the functionality of the REST API for spell check.</span><span class="sxs-lookup"><span data-stu-id="65168-104">The Bing Spell Check SDK contains the functionality of the REST API for spell check.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="65168-105">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="65168-105">Application dependencies</span></span>

<span data-ttu-id="65168-106">To set up a console application using the Bing Spell Check SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65168-106">To set up a console application using the Bing Spell Check SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="65168-107">Add the `Microsoft.Azure.CognitiveServices.SpellCheck` package.</span><span class="sxs-lookup"><span data-stu-id="65168-107">Add the `Microsoft.Azure.CognitiveServices.SpellCheck` package.</span></span>

<span data-ttu-id="65168-108">Installing the [SpellCheck SDK package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.SpellCheck/1.2.0) also installs dependencies, including:</span><span class="sxs-lookup"><span data-stu-id="65168-108">Installing the [SpellCheck SDK package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.SpellCheck/1.2.0) also installs dependencies, including:</span></span>

* <span data-ttu-id="65168-109">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="65168-109">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="65168-110">Microsoft.Rest.ClientRuntime.AZure</span><span class="sxs-lookup"><span data-stu-id="65168-110">Microsoft.Rest.ClientRuntime.AZure</span></span>
* <span data-ttu-id="65168-111">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="65168-111">Newtonsoft.Json</span></span>

## <a name="spell-check-client"></a><span data-ttu-id="65168-112">Spell check client</span><span class="sxs-lookup"><span data-stu-id="65168-112">Spell check client</span></span>

<span data-ttu-id="65168-113">To create an instance of the `SpellCheckAPI` client, add using directive:</span><span class="sxs-lookup"><span data-stu-id="65168-113">To create an instance of the `SpellCheckAPI` client, add using directive:</span></span>

```cs
using Microsoft.Azure.CognitiveServices.SpellCheck;
```

<span data-ttu-id="65168-114">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="65168-114">Then, instantiate the client:</span></span>

```cs
var client = new SpellCheckAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));
```

<span data-ttu-id="65168-115">Use the client to check spelling:</span><span class="sxs-lookup"><span data-stu-id="65168-115">Use the client to check spelling:</span></span>

```cs
var result = client.SpellCheckerWithHttpMessagesAsync(text: "Bill Gatas", mode: "proof", acceptLanguage: "en-US").Result;
Console.WriteLine("Correction for Query# \"bill gatas\"");
```

<span data-ttu-id="65168-116">Parse the results:</span><span class="sxs-lookup"><span data-stu-id="65168-116">Parse the results:</span></span>

```cs
// SpellCheck Results
if (result?.Body.FlaggedTokens?.Count > 0)
{
    // find the first spellcheck result
    var firstspellCheckResult = result.Body.FlaggedTokens.FirstOrDefault();

    if (firstspellCheckResult != null)
    {
        Console.WriteLine("SpellCheck Results#{0}", result.Body.FlaggedTokens.Count);
        Console.WriteLine("First SpellCheck Result token: {0} ", firstspellCheckResult.Token);
        Console.WriteLine("First SpellCheck Result Type: {0} ", firstspellCheckResult.Type);
        Console.WriteLine("First SpellCheck Result Suggestion Count: {0} ", firstspellCheckResult.Suggestions.Count);

        var suggestions = firstspellCheckResult.Suggestions;
        if (suggestions?.Count > 0)
        {
            var firstSuggestion = suggestions.FirstOrDefault();
            Console.WriteLine("First SpellCheck Suggestion Score: {0} ", firstSuggestion.Score);
            Console.WriteLine("First SpellCheck Suggestion : {0} ", firstSuggestion.Suggestion);
        }
        }
        else
        {
            Console.WriteLine("Couldn't get any Spell check results!");
        }
    }
    else
    {
        Console.WriteLine("Didn't see any SpellCheck results..");
    }
```

## <a name="complete-console-application"></a><span data-ttu-id="65168-117">Complete console application</span><span class="sxs-lookup"><span data-stu-id="65168-117">Complete console application</span></span>

<span data-ttu-id="65168-118">The following console application executes the previous code:</span><span class="sxs-lookup"><span data-stu-id="65168-118">The following console application executes the previous code:</span></span>

```cs
using System;
using System.Linq;
using Microsoft.Azure.CognitiveServices.SpellCheck;

namespace SpellCheckSDK
{
    class Program
    {
        static void Main(string[] args)
        {
            var client = new SpellCheckAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));

            try
            {
                var result = client.SpellCheckerWithHttpMessagesAsync(text: "Bill Gatas", mode: "proof", acceptLanguage: "en-US").Result;
                Console.WriteLine("Correction for Query# \"bill gatas\"");

                // SpellCheck Results
                if (result?.Body.FlaggedTokens?.Count > 0)
                {
                    // find the first spellcheck result
                    var firstspellCheckResult = result.Body.FlaggedTokens.FirstOrDefault();

                    if (firstspellCheckResult != null)
                    {
                        Console.WriteLine("SpellCheck Results#{0}", result.Body.FlaggedTokens.Count);
                        Console.WriteLine("First SpellCheck Result token: {0} ", firstspellCheckResult.Token);
                        Console.WriteLine("First SpellCheck Result Type: {0} ", firstspellCheckResult.Type);
                        Console.WriteLine("First SpellCheck Result Suggestion Count: {0} ", firstspellCheckResult.Suggestions.Count);

                        var suggestions = firstspellCheckResult.Suggestions;
                        if (suggestions?.Count > 0)
                        {
                            var firstSuggestion = suggestions.FirstOrDefault();
                            Console.WriteLine("First SpellCheck Suggestion Score: {0} ", firstSuggestion.Score);
                            Console.WriteLine("First SpellCheck Suggestion : {0} ", firstSuggestion.Suggestion);
                        }
                    }
                    else
                    {
                        Console.WriteLine("Couldn't get any Spell check results!");
                    }
                }
                else
                {
                    Console.WriteLine("Didn't see any SpellCheck results..");
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }

            Console.WriteLine("Any key to exit...");
            Console.ReadKey();
        }

        // This will trigger an error response from the API.
        public static void SpellCheckError(string subscriptionKey)
        {
            var client = new SpellCheckAPI(new ApiKeyServiceClientCredentials(subscriptionKey));

            try
            {
                var result = client.SpellCheckerAsync(mode: "proof").Result;
                Console.WriteLine("Correction for Query# \"empty text field\"");
            }
            catch (Exception ex)
            {
                if (ex.GetBaseException().GetType() == typeof(Exception) )
                {
                    Console.WriteLine("Encountered exception. " + ex.Message);
                }
            }
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="65168-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="65168-119">Next steps</span></span>

[<span data-ttu-id="65168-120">Cognitive services .NET SDK samples</span><span class="sxs-lookup"><span data-stu-id="65168-120">Cognitive services .NET SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)
