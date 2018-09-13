---
title: Azure Content Moderator - Moderate images using .NET | Microsoft Docs
description: How to moderate images using Azure Content Moderator SDK for .NET
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 09/10/2018
ms.author: sajagtap
ms.openlocfilehash: 1cccd12b7a0676da8db61ba1f02e199f2a086ee0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965577"
---
# <a name="moderate-images-using-net"></a><span data-ttu-id="a9091-103">Moderate images using .NET</span><span class="sxs-lookup"><span data-stu-id="a9091-103">Moderate images using .NET</span></span>

<span data-ttu-id="a9091-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span><span class="sxs-lookup"><span data-stu-id="a9091-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span></span> 
- <span data-ttu-id="a9091-105">Check an image for adult or racy content</span><span class="sxs-lookup"><span data-stu-id="a9091-105">Check an image for adult or racy content</span></span>
- <span data-ttu-id="a9091-106">Detect and extract text from an image</span><span class="sxs-lookup"><span data-stu-id="a9091-106">Detect and extract text from an image</span></span>
- <span data-ttu-id="a9091-107">Detect faces in an image</span><span class="sxs-lookup"><span data-stu-id="a9091-107">Detect faces in an image</span></span>

<span data-ttu-id="a9091-108">This article assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="a9091-108">This article assumes that you are already familiar with Visual Studio and C#.</span></span>

## <a name="sign-up-for-content-moderator-services"></a><span data-ttu-id="a9091-109">Sign up for Content Moderator services</span><span class="sxs-lookup"><span data-stu-id="a9091-109">Sign up for Content Moderator services</span></span>

<span data-ttu-id="a9091-110">Before you can use Content Moderator services through the REST API or the SDK, you need an API key and the region of your API account.</span><span class="sxs-lookup"><span data-stu-id="a9091-110">Before you can use Content Moderator services through the REST API or the SDK, you need an API key and the region of your API account.</span></span>
<span data-ttu-id="a9091-111">Refer to the [Quickstart](quick-start.md) to learn how to sign up for Content Moderator to obtain both.</span><span class="sxs-lookup"><span data-stu-id="a9091-111">Refer to the [Quickstart](quick-start.md) to learn how to sign up for Content Moderator to obtain both.</span></span>

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="a9091-112">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="a9091-112">Create your Visual Studio project</span></span>

1. <span data-ttu-id="a9091-113">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="a9091-113">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

   <span data-ttu-id="a9091-114">In the sample code, name the project **ImageModeration**.</span><span class="sxs-lookup"><span data-stu-id="a9091-114">In the sample code, name the project **ImageModeration**.</span></span>

1. <span data-ttu-id="a9091-115">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="a9091-115">Select this project as the single startup project for the solution.</span></span>


### <a name="install-required-packages"></a><span data-ttu-id="a9091-116">Install required packages</span><span class="sxs-lookup"><span data-stu-id="a9091-116">Install required packages</span></span>

<span data-ttu-id="a9091-117">Install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="a9091-117">Install the following NuGet packages:</span></span>

- <span data-ttu-id="a9091-118">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="a9091-118">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="a9091-119">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="a9091-119">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="a9091-120">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="a9091-120">Newtonsoft.Json</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="a9091-121">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="a9091-121">Update the program's using statements</span></span>

<span data-ttu-id="a9091-122">Modify the program's using statements.</span><span class="sxs-lookup"><span data-stu-id="a9091-122">Modify the program's using statements.</span></span>

    using Microsoft.Azure.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator.Models;
    using Newtonsoft.Json;
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Threading;

### <a name="create-the-content-moderator-client"></a><span data-ttu-id="a9091-123">Create the Content Moderator client</span><span class="sxs-lookup"><span data-stu-id="a9091-123">Create the Content Moderator client</span></span>

<span data-ttu-id="a9091-124">Add the following code to create a Content Moderator client for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a9091-124">Add the following code to create a Content Moderator client for your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9091-125">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span><span class="sxs-lookup"><span data-stu-id="a9091-125">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span></span>

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

### <a name="initialize-application-specific-settings"></a><span data-ttu-id="a9091-126">Initialize application-specific settings</span><span class="sxs-lookup"><span data-stu-id="a9091-126">Initialize application-specific settings</span></span>

<span data-ttu-id="a9091-127">Add the following static fields to the **Program** class in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="a9091-127">Add the following static fields to the **Program** class in Program.cs.</span></span>

    ///<summary>
    ///The name of the file that contains the image URLs to evaluate.
    ///</summary>
    ///<remarks>You will need to create an input file and update 
    ///this path accordingly. Paths are relative to the execution directory.
    ///</remarks>
    private static string ImageUrlFile = "ImageFiles.txt";

    ///<summary>
    ///The name of the file to contain the output from the evaluation.
    ///</summary>
    ///<remarks>Paths are relative to the execution directory.
    ///</remarks>
    private static string OutputFile = "ModerationOutput.json";


> [!NOTE]
> <span data-ttu-id="a9091-128">The sample uses the following images to generate the output for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a9091-128">The sample uses the following images to generate the output for this quickstart.</span></span>
> - https://moderatorsampleimages.blob.core.windows.net/samples/sample2.jpg
> - https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png

## <a name="store-the-analysis-results"></a><span data-ttu-id="a9091-129">Store the analysis results</span><span class="sxs-lookup"><span data-stu-id="a9091-129">Store the analysis results</span></span>

<span data-ttu-id="a9091-130">Add the following class to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="a9091-130">Add the following class to the **Program** class.</span></span> <span data-ttu-id="a9091-131">Use an instance of this class to record the moderation results for the reviewed images.</span><span class="sxs-lookup"><span data-stu-id="a9091-131">Use an instance of this class to record the moderation results for the reviewed images.</span></span>

    /// <summary>
    /// Contains the image moderation results for an image, 
    /// including text and face detection results.
    /// </summary>
    public class EvaluationData
    {
        /// <summary>
        /// The URL of the evaluated image.
        /// </summary>
        public string ImageUrl;

        /// <summary>
        /// The image moderation results.
        /// </summary>
        public Evaluate ImageModeration;

        /// <summary>
        /// The text detection results.
        /// </summary>
        public OCR TextDetection;

        /// <summary>
        /// The face detection results;
        /// </summary>
        public FoundFaces FaceDetection;
    }

## <a name="evaluate-an-individual-image"></a><span data-ttu-id="a9091-132">Evaluate an individual image</span><span class="sxs-lookup"><span data-stu-id="a9091-132">Evaluate an individual image</span></span>

<span data-ttu-id="a9091-133">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="a9091-133">Add the following method to the **Program** class.</span></span> <span data-ttu-id="a9091-134">This method evaluates a single image and returns the evaluation results.</span><span class="sxs-lookup"><span data-stu-id="a9091-134">This method evaluates a single image and returns the evaluation results.</span></span>

> [!NOTE]
> <span data-ttu-id="a9091-135">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="a9091-135">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span></span> 
>
> <span data-ttu-id="a9091-136">A free tier key has a one RPS rate limit.</span><span class="sxs-lookup"><span data-stu-id="a9091-136">A free tier key has a one RPS rate limit.</span></span>


    /// <summary>
    /// Evaluates an image using the Image Moderation APIs.
    /// </summary>
    /// <param name="client">The Content Moderator API wrapper to use.</param>
    /// <param name="imageUrl">The URL of the image to evaluate.</param>
    /// <returns>Aggregated image moderation results for the image.</returns>
    /// <remarks>This method throttles calls to the API.
    /// Your Content Moderator service key will have a requests per second (RPS)
    /// rate limit, and the SDK will throw an exception with a 429 error code 
    /// if you exceed that limit. A free tier key has a 1 RPS rate limit.
    /// </remarks>
    private static EvaluationData EvaluateImage(
    ContentModeratorClient client, string imageUrl)
    {
        var url = new ImageUrl("URL", imageUrl.Trim());

        var imageData = new EvaluationData();

        imageData.ImageUrl = url.Value;

        // Evaluate for adult and racy content.
        imageData.ImageModeration =
            client.ImageModeration.EvaluateUrlInput("application/json", url, true);
        Thread.Sleep(1000);

        // Detect and extract text.
        imageData.TextDetection =
            client.ImageModeration.OCRUrlInput("eng", "application/json", url, true);
        Thread.Sleep(1000);

        // Detect faces.
        imageData.FaceDetection =
            client.ImageModeration.FindFacesUrlInput("application/json", url, true);
        Thread.Sleep(1000);

        return imageData;
    }

<span data-ttu-id="a9091-137">The **EvaluateUrlInput** method is a wrapper for the Image Moderation REST API.</span><span class="sxs-lookup"><span data-stu-id="a9091-137">The **EvaluateUrlInput** method is a wrapper for the Image Moderation REST API.</span></span>
<span data-ttu-id="a9091-138">The return value contains the object returned from the API call.</span><span class="sxs-lookup"><span data-stu-id="a9091-138">The return value contains the object returned from the API call.</span></span>

<span data-ttu-id="a9091-139">The **OCRUrlInput** method is a wrapper for the Image OCR REST API.</span><span class="sxs-lookup"><span data-stu-id="a9091-139">The **OCRUrlInput** method is a wrapper for the Image OCR REST API.</span></span>
<span data-ttu-id="a9091-140">The return value contains the object returned from the API call.</span><span class="sxs-lookup"><span data-stu-id="a9091-140">The return value contains the object returned from the API call.</span></span>

<span data-ttu-id="a9091-141">The **FindFacesUrlInput** method is a wrapper for the Image Find Faces REST API.</span><span class="sxs-lookup"><span data-stu-id="a9091-141">The **FindFacesUrlInput** method is a wrapper for the Image Find Faces REST API.</span></span>
<span data-ttu-id="a9091-142">The return value contains the object returned from the API call.</span><span class="sxs-lookup"><span data-stu-id="a9091-142">The return value contains the object returned from the API call.</span></span>

## <a name="process-the-image-urls-in-your-code"></a><span data-ttu-id="a9091-143">Process the image URLs in your code</span><span class="sxs-lookup"><span data-stu-id="a9091-143">Process the image URLs in your code</span></span>

<span data-ttu-id="a9091-144">Add the following code to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="a9091-144">Add the following code to the **Main** method.</span></span>

    // Create an object to store the image moderation results.
    List<EvaluationData> evaluationData = new List<EvaluationData>();

    // Create an instance of the Content Moderator API wrapper.
    using (var client = Clients.NewClient())
    {
        // Read image URLs from the input file and evaluate each one.
        using (StreamReader inputReader = new StreamReader(ImageUrlFile))
        {
            while (!inputReader.EndOfStream)
            {
                string line = inputReader.ReadLine().Trim();
                if (line != String.Empty)
                {
                    EvaluationData imageData = EvaluateImage(client, line);
                    evaluationData.Add(imageData);
                }
            }
        }
    }

    // Save the moderation results to a file.
    using (StreamWriter outputWriter = new StreamWriter(OutputFile, false))
    {
        outputWriter.WriteLine(JsonConvert.SerializeObject(
            evaluationData, Formatting.Indented));

        outputWriter.Flush();
        outputWriter.Close();
    }

## <a name="run-the-program-and-review-the-output"></a><span data-ttu-id="a9091-145">Run the program and review the output</span><span class="sxs-lookup"><span data-stu-id="a9091-145">Run the program and review the output</span></span>

<span data-ttu-id="a9091-146">The following JSON object contains output for the program.</span><span class="sxs-lookup"><span data-stu-id="a9091-146">The following JSON object contains output for the program.</span></span>

> [!NOTE]
> <span data-ttu-id="a9091-147">`isImageAdultClassified` represents the potential presence of images that may be considered sexually explicit or adult in certain situations.</span><span class="sxs-lookup"><span data-stu-id="a9091-147">`isImageAdultClassified` represents the potential presence of images that may be considered sexually explicit or adult in certain situations.</span></span>
> <span data-ttu-id="a9091-148">`isImageRacyClassified` represents the potential presence of images that may be considered sexually suggestive or mature in certain situations.</span><span class="sxs-lookup"><span data-stu-id="a9091-148">`isImageRacyClassified` represents the potential presence of images that may be considered sexually suggestive or mature in certain situations.</span></span>
>

    [
    {
    "ImageUrl": "https://moderatorsampleimages.blob.core.windows.net/samples/sample2.jpg",
    "ImageModeration": {
      "cacheID": "7733c303-3b95-4710-a41e-7a322ae81a15_636488005858745661",
      "result": false,
      "trackingId": "WE_e1f20803b4ed471fb5de7df551f5bd9f_ContentModerator.Preview_687c356d-0f00-4aeb-ae5f-c7555af80247",
      "adultClassificationScore": 0.019196987152099609,
      "isImageAdultClassified": false,
      "racyClassificationScore": 0.032390203326940536,
      "isImageRacyClassified": false,
      "advancedInfo": [
        {
          "key": "ImageDownloadTimeInMs",
          "value": "116"
        },
        {
          "key": "ImageSizeInBytes",
          "value": "273405"
        }
      ],
      "status": {
        "code": 3000.0,
        "description": "OK",
        "exception": null
      }
    },
    "TextDetection": {
      "status": {
        "code": 3000.0,
        "description": "OK",
        "exception": null
      },
      "metadata": [
        {
          "key": "ImageDownloadTimeInMs",
          "value": "12"
        },
        {
          "key": "ImageSizeInBytes",
          "value": "273405"
        }
      ],
      "trackingId": "WE_e1f20803b4ed471fb5de7df551f5bd9f_ContentModerator.Preview_814fa162-c5d6-4ca6-997b-30ed0686ca83",
      "cacheId": "3fb69496-c64b-4de9-affd-6dd6d23f3e78_636488005876558920",
      "language": "eng",
      "text": "IF WE DID \r\nALL \r\nTHE THINGS \r\nWE ARE \r\nCAPABLE \r\nOF DOING, \r\nWE WOULD \r\nLITERALLY \r\nASTOUND \r\nOURSELVE \r\n",
      "candidates": []
    },
    "FaceDetection": {
      "status": {
        "code": 3000.0,
        "description": "OK",
        "exception": null
      },
      "trackingId": "WE_e1f20803b4ed471fb5de7df551f5bd9f_ContentModerator.Preview_a2c40dbe-609d-4eb8-b01c-9988388804ea",
      "cacheId": "e4c0b500-ea8e-4a31-8fb3-35f98c4fbd65_636488005889528303",
      "result": false,
      "count": 0,
      "advancedInfo": [
        {
          "key": "ImageDownloadTimeInMs",
          "value": "11"
        },
        {
          "key": "ImageSizeInBytes",
          "value": "273405"
        }
      ],
      "faces": []
    }
    },
    {
    "ImageUrl": "https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png",
    "ImageModeration": {
      "cacheID": "b4866aa2-5e69-44ed-806a-f9a5d618c8ae_636488005930693926",
      "result": false,
      "trackingId": "WE_e1f20803b4ed471fb5de7df551f5bd9f_ContentModerator.Preview_fdce5510-f689-4791-b081-c2ad54dcfe78",
      "adultClassificationScore": 0.0035635426174849272,
      "isImageAdultClassified": false,
      "racyClassificationScore": 0.021369094029068947,
      "isImageRacyClassified": false,
      "advancedInfo": [
        {
          "key": "ImageDownloadTimeInMs",
          "value": "109"
        },
        {
          "key": "ImageSizeInBytes",
          "value": "2278902"
        }
      ],
      "status": {
        "code": 3000.0,
        "description": "OK",
        "exception": null
      }
    },
    "TextDetection": {
      "status": {
        "code": 3000.0,
        "description": "OK",
        "exception": null
      },
      "metadata": [
        {
          "key": "ImageDownloadTimeInMs",
          "value": "46"
        },
        {
          "key": "ImageSizeInBytes",
          "value": "2278902"
        }
      ],
      "trackingId": "WE_e1f20803b4ed471fb5de7df551f5bd9f_ContentModerator.Preview_08a4bc19-6010-41bb-a440-a77278e167d8",
      "cacheId": "28b37471-41b3-4f79-bd23-965498bcff51_636488005950851288",
      "language": "eng",
      "text": "",
      "candidates": []
    },
    "FaceDetection": {
      "status": {
        "code": 3000.0,
        "description": "OK",
        "exception": null
      },
      "trackingId": "WE_e1f20803b4ed471fb5de7df551f5bd9f_ContentModerator.Preview_40f2ce07-14ba-47cd-ba09-58b557a89854",
      "cacheId": "ec9c1be3-99b7-4bd9-8bc4-dc958c74459f_636488005964914299",
      "result": true,
      "count": 6,
      "advancedInfo": [
        {
          "key": "ImageDownloadTimeInMs",
          "value": "60"
        },
        {
          "key": "ImageSizeInBytes",
          "value": "2278902"
        }
      ],
      "faces": [
        {
          "bottom": 598,
          "left": 44,
          "right": 268,
          "top": 374
        },
        {
          "bottom": 620,
          "left": 308,
          "right": 532,
          "top": 396
        },
        {
          "bottom": 575,
          "left": 594,
          "right": 773,
          "top": 396
        },
        {
          "bottom": 563,
          "left": 812,
          "right": 955,
          "top": 420
        },
        {
          "bottom": 611,
          "left": 972,
          "right": 1151,
          "top": 432
        },
        {
          "bottom": 510,
          "left": 1232,
          "right": 1456,
          "top": 286
        }
      ]
    }
    }
    ]


## <a name="next-steps---get-the-source-code"></a><span data-ttu-id="a9091-149">Next steps - get the source code</span><span class="sxs-lookup"><span data-stu-id="a9091-149">Next steps - get the source code</span></span>

<span data-ttu-id="a9091-150">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span><span class="sxs-lookup"><span data-stu-id="a9091-150">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span></span>
