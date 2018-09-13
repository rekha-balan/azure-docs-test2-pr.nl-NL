---
title: Azure Content Moderator - Moderate text using .NET | Microsoft Docs
description: How to moderate text using Azure Content Moderator SDK for .NET
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 09/10/2018
ms.author: sajagtap
ms.openlocfilehash: 7b7bba256b87be95d72d2bddbd10f11c097f1022
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968751"
---
# <a name="moderate-text-using-net"></a><span data-ttu-id="340b8-103">Moderate text using .NET</span><span class="sxs-lookup"><span data-stu-id="340b8-103">Moderate text using .NET</span></span>

<span data-ttu-id="340b8-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span><span class="sxs-lookup"><span data-stu-id="340b8-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span></span>
- <span data-ttu-id="340b8-105">Detect potential profanity in text with term-based filtering</span><span class="sxs-lookup"><span data-stu-id="340b8-105">Detect potential profanity in text with term-based filtering</span></span>
- <span data-ttu-id="340b8-106">Use machine-learning-based models to [classify the text](text-moderation-api.md#classification) into three categories.</span><span class="sxs-lookup"><span data-stu-id="340b8-106">Use machine-learning-based models to [classify the text](text-moderation-api.md#classification) into three categories.</span></span>
- <span data-ttu-id="340b8-107">Detect personally identifiable information (PII) such as US and UK phone numbers, email addresses, and US mailing addresses.</span><span class="sxs-lookup"><span data-stu-id="340b8-107">Detect personally identifiable information (PII) such as US and UK phone numbers, email addresses, and US mailing addresses.</span></span>
- <span data-ttu-id="340b8-108">Normalize text and autocorrect typos</span><span class="sxs-lookup"><span data-stu-id="340b8-108">Normalize text and autocorrect typos</span></span>

<span data-ttu-id="340b8-109">This article assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="340b8-109">This article assumes that you are already familiar with Visual Studio and C#.</span></span>

## <a name="sign-up-for-content-moderator-services"></a><span data-ttu-id="340b8-110">Sign up for Content Moderator services</span><span class="sxs-lookup"><span data-stu-id="340b8-110">Sign up for Content Moderator services</span></span>

<span data-ttu-id="340b8-111">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="340b8-111">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span></span>
<span data-ttu-id="340b8-112">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span><span class="sxs-lookup"><span data-stu-id="340b8-112">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span></span>

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="340b8-113">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="340b8-113">Create your Visual Studio project</span></span>

1. <span data-ttu-id="340b8-114">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="340b8-114">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

   <span data-ttu-id="340b8-115">In the sample code, name the project **TextModeration**.</span><span class="sxs-lookup"><span data-stu-id="340b8-115">In the sample code, name the project **TextModeration**.</span></span>

1. <span data-ttu-id="340b8-116">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="340b8-116">Select this project as the single startup project for the solution.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="340b8-117">Install required packages</span><span class="sxs-lookup"><span data-stu-id="340b8-117">Install required packages</span></span>

<span data-ttu-id="340b8-118">Install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="340b8-118">Install the following NuGet packages:</span></span>

- <span data-ttu-id="340b8-119">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="340b8-119">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="340b8-120">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="340b8-120">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="340b8-121">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="340b8-121">Newtonsoft.Json</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="340b8-122">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="340b8-122">Update the program's using statements</span></span>

<span data-ttu-id="340b8-123">Modify the program's using statements.</span><span class="sxs-lookup"><span data-stu-id="340b8-123">Modify the program's using statements.</span></span>

    using Microsoft.Azure.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator.Models;
    using Newtonsoft.Json;
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Threading;

### <a name="create-the-content-moderator-client"></a><span data-ttu-id="340b8-124">Create the Content Moderator client</span><span class="sxs-lookup"><span data-stu-id="340b8-124">Create the Content Moderator client</span></span>

<span data-ttu-id="340b8-125">Add the following code to create a Content Moderator client for your subscription.</span><span class="sxs-lookup"><span data-stu-id="340b8-125">Add the following code to create a Content Moderator client for your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="340b8-126">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span><span class="sxs-lookup"><span data-stu-id="340b8-126">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span></span>


    /// <summary>
    /// Wraps the creation and configuration of a Content Moderator client.
    /// </summary>
    /// <remarks>This class library contains insecure code. If you adapt this 
    /// code for use in production, use a secure method of storing and using
    /// your Content Moderator subscription key.</remarks>
    public static class Clients
    {
        /// <summary>
        /// The region/location for your Content Moderator account, 
        /// for example, westus.
        /// </summary>
        private static readonly string AzureRegion = "YOUR API REGION";

        /// <summary>
        /// The base URL fragment for Content Moderator calls.
        /// </summary>
        private static readonly string AzureBaseURL =
            $"https://{AzureRegion}.api.cognitive.microsoft.com";

        /// <summary>
        /// Your Content Moderator subscription key.
        /// </summary>
        private static readonly string CMSubscriptionKey = "YOUR API KEY";

        /// <summary>
        /// Returns a new Content Moderator client for your subscription.
        /// </summary>
        /// <returns>The new client.</returns>
        /// <remarks>The <see cref="ContentModeratorClient"/> is disposable.
        /// When you have finished using the client,
        /// you should dispose of it either directly or indirectly. </remarks>
        public static ContentModeratorClient NewClient()
        {
            // Create and initialize an instance of the Content Moderator API wrapper.
            ContentModeratorClient client = new ContentModeratorClient(new ApiKeyServiceClientCredentials(CMSubscriptionKey));

            client.BaseUrl = AzureBaseURL;
            return client;
        }
    }

### <a name="initialize-application-specific-settings"></a><span data-ttu-id="340b8-127">Initialize application-specific settings</span><span class="sxs-lookup"><span data-stu-id="340b8-127">Initialize application-specific settings</span></span>

<span data-ttu-id="340b8-128">Add the following static fields to the **Program** class in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="340b8-128">Add the following static fields to the **Program** class in Program.cs.</span></span>

    /// <summary>
    /// The name of the file that contains the text to evaluate.
    /// </summary>
    /// <remarks>You will need to create an input file and update this path
    /// accordingly. Relative paths are ralative the execution directory.</remarks>
    private static string TextFile = "TextFile.txt";

    /// <summary>
    /// The name of the file to contain the output from the evaluation.
    /// </summary>
    /// <remarks>Relative paths are ralative the execution directory.</remarks>
    private static string OutputFile = "TextModerationOutput.txt";

<span data-ttu-id="340b8-129">We used the following text to generate the output for this quickstart:</span><span class="sxs-lookup"><span data-stu-id="340b8-129">We used the following text to generate the output for this quickstart:</span></span>

> [!NOTE]
> <span data-ttu-id="340b8-130">The invalid social security number in the following sample text is intentional.</span><span class="sxs-lookup"><span data-stu-id="340b8-130">The invalid social security number in the following sample text is intentional.</span></span> <span data-ttu-id="340b8-131">The purpose is to convey the sample input and output format.</span><span class="sxs-lookup"><span data-stu-id="340b8-131">The purpose is to convey the sample input and output format.</span></span>

    Is this a grabage or crap email abcdef@abcd.com, phone: 6657789887, IP: 255.255.255.255, 1 Microsoft Way, Redmond, WA 98052.
    These are all UK phone numbers, the last two being Microsoft UK support numbers: +44 870 608 4000 or 0344 800 2400 or 
    0800 820 3300. Also, 999-99-9999 looks like a social security number (SSN).

## <a name="add-code-to-load-and-evaluate-the-input-text"></a><span data-ttu-id="340b8-132">Add code to load and evaluate the input text</span><span class="sxs-lookup"><span data-stu-id="340b8-132">Add code to load and evaluate the input text</span></span>

<span data-ttu-id="340b8-133">Add the following code to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="340b8-133">Add the following code to the **Main** method.</span></span>

    // Load the input text.
    string text = File.ReadAllText(TextFile);
    text = text.Replace(System.Environment.NewLine, " ");

    // Save the moderation results to a file.
    using (StreamWriter outputWriter = new StreamWriter(OutputFile, false))
    {
        // Create a Content Moderator client and evaluate the text.
        using (var client = Clients.NewClient())
        {
            // Screen the input text: check for profanity, classify the text into three categories
                // do autocorrect text, and check for personally identifying 
                // information (PII)
                outputWriter.WriteLine("Autocorrect typos, check for matching terms, PII, and classify.");
                var screenResult =
                    client.TextModeration.ScreenText("eng", "text/plain", text, true, true, null, true);
                outputWriter.WriteLine(
                        JsonConvert.SerializeObject(screenResult, Formatting.Indented));
        }
        outputWriter.Flush();
        outputWriter.Close();
    }

> [!NOTE]
> <span data-ttu-id="340b8-134">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="340b8-134">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span></span>
>
> <span data-ttu-id="340b8-135">When using a free tier key, the rate of requests is limited to one request per second.</span><span class="sxs-lookup"><span data-stu-id="340b8-135">When using a free tier key, the rate of requests is limited to one request per second.</span></span>

## <a name="run-the-program-and-review-the-output"></a><span data-ttu-id="340b8-136">Run the program and review the output</span><span class="sxs-lookup"><span data-stu-id="340b8-136">Run the program and review the output</span></span>

<span data-ttu-id="340b8-137">The sample output for the program, as written to the log file, is:</span><span class="sxs-lookup"><span data-stu-id="340b8-137">The sample output for the program, as written to the log file, is:</span></span>

    Autocorrect typos, check for matching terms, PII, and classify.
    {
    "OriginalText": "\"Is this a grabage or crap email abcdef@abcd.com, phone: 6657789887, IP: 255.255.255.255, 1 Microsoft Way, Redmond, WA 98052. These are all UK phone numbers, the last two being Microsoft UK support numbers: +44 870 608 4000 or 0344 800 2400 or 0800 820 3300. Also, 999-99-9999 looks like a social security number (SSN).\"",
    "NormalizedText": "\" Is this a garbage or crap email abide@ abed. com, phone: 6657789887, IP: 255. 255. 255. 255, 1 Microsoft Way, Redmond, WA 98052. These are all UK phone numbers, the last two being Microsoft UK support numbers: +44 870 608 4000 or 0344 800 2400 or 0800 820 3300. Also, 999-99-9999 looks like a social security number ( SSN) . \"",
    "AutoCorrectedText": "\" Is this a garbage or crap email abide@ abed. com, phone: 6657789887, IP: 255. 255. 255. 255, 1 Microsoft Way, Redmond, WA 98052. These are all UK phone numbers, the last two being Microsoft UK support numbers: +44 870 608 4000 or 0344 800 2400 or 0800 820 3300. Also, 999-99-9999 looks like a social security number ( SSN) . \"",
    "Misrepresentation": null,
    
    "Classification": {
            "Category1": {
            "Score": 1.5113095059859916E-06
            },
            "Category2": {
            "Score": 0.12747249007225037
            },
            "Category3": {
            "Score": 0.98799997568130493
            },
            "ReviewRecommended": true
    },
    "Status": {
        "Code": 3000,
        "Description": "OK",
        "Exception": null
    },
    "PII": {
            "Email": [
                {
                "Detected": "abcdef@abcd.com",
                "SubType": "Regular",
                "Text": "abcdef@abcd.com",
                "Index": 33
                }
                ],
            "IPA": [
                {
                "SubType": "IPV4",
                "Text": "255.255.255.255",
                "Index": 73
                }
                ],
            "Phone": [
                {
                "CountryCode": "US",
                "Text": "6657789887",
                "Index": 57
                },
                {
                "CountryCode": "US",
                "Text": "870 608 4000",
                "Index": 211
                },
                {
                "CountryCode": "UK",
                "Text": "+44 870 608 4000",
                "Index": 207
                },
                {
                "CountryCode": "UK",
                "Text": "0344 800 2400",
                "Index": 227
                },
                {
            "   CountryCode": "UK",
                "Text": "0800 820 3300",
                "Index": 244
                }
                ],
             "Address": [{
                 "Text": "1 Microsoft Way, Redmond, WA 98052",
                 "Index": 89
                    }]
        },
    "Language": "eng",
    "Terms": [
        {
            "Index": 22,
            "OriginalIndex": 22,
            "ListId": 0,
            "Term": "crap"
        }
    ],
    "TrackingId": "9392c53c-d11a-441d-a874-eb2b93d978d3"
    }

## <a name="next-steps"></a><span data-ttu-id="340b8-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="340b8-138">Next steps</span></span>

<span data-ttu-id="340b8-139">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span><span class="sxs-lookup"><span data-stu-id="340b8-139">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span></span>
