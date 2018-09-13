---
title: Visual search SDK C# Quickstart | Microsoft Docs
description: Setup for Visual search SDK C# console application.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 05/16/2018
ms.author: v-gedod
ms.openlocfilehash: e9b93c46cf0702dc58398e247fef79c3f31bb50c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866012"
---
# <a name="visual-search-sdk-c-quickstart"></a><span data-ttu-id="69c69-103">Visual Search SDK C# Quickstart</span><span class="sxs-lookup"><span data-stu-id="69c69-103">Visual Search SDK C# Quickstart</span></span>

<span data-ttu-id="69c69-104">The Bing Visual Search SDK uses the functionality of the REST API for web requests and parsing results.</span><span class="sxs-lookup"><span data-stu-id="69c69-104">The Bing Visual Search SDK uses the functionality of the REST API for web requests and parsing results.</span></span>
<span data-ttu-id="69c69-105">The [source code for C# Bing Visual Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingVisualSearch) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="69c69-105">The [source code for C# Bing Visual Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingVisualSearch) is available on Git Hub.</span></span>

<span data-ttu-id="69c69-106">Code scenarios are documented under the following headings:</span><span class="sxs-lookup"><span data-stu-id="69c69-106">Code scenarios are documented under the following headings:</span></span>
* [<span data-ttu-id="69c69-107">Visual Search Client</span><span class="sxs-lookup"><span data-stu-id="69c69-107">Visual Search Client</span></span>](#client)
* [<span data-ttu-id="69c69-108">Complete console application</span><span class="sxs-lookup"><span data-stu-id="69c69-108">Complete console application</span></span>](#complete)
* [<span data-ttu-id="69c69-109">Image binary post with cropArea</span><span class="sxs-lookup"><span data-stu-id="69c69-109">Image binary post with cropArea</span></span>](#binary-crop)
* [<span data-ttu-id="69c69-110">KnowledgeRequest parameter</span><span class="sxs-lookup"><span data-stu-id="69c69-110">KnowledgeRequest parameter</span></span>](#knowledge-req)
* [<span data-ttu-id="69c69-111">Tags, actions, and actionType</span><span class="sxs-lookup"><span data-stu-id="69c69-111">Tags, actions, and actionType</span></span>](#tags-actions)
* [<span data-ttu-id="69c69-112">Number of tags, number of actions, and first actionType</span><span class="sxs-lookup"><span data-stu-id="69c69-112">Number of tags, number of actions, and first actionType</span></span>](#num-tags-actions)

## <a name="prerequisites"></a><span data-ttu-id="69c69-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="69c69-113">Prerequisites</span></span>

* <span data-ttu-id="69c69-114">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="69c69-114">Visual Studio 2017.</span></span> <span data-ttu-id="69c69-115">If necessary, you can download free community version from here: https://www.visualstudio.com/vs/community/.</span><span class="sxs-lookup"><span data-stu-id="69c69-115">If necessary, you can download free community version from here: https://www.visualstudio.com/vs/community/.</span></span>
* <span data-ttu-id="69c69-116">A Cognitive Services API key is required to authenticate SDK calls.</span><span class="sxs-lookup"><span data-stu-id="69c69-116">A Cognitive Services API key is required to authenticate SDK calls.</span></span> <span data-ttu-id="69c69-117">Sign up for a [free trial key](https://azure.microsoft.com/try/cognitive-services/?api=search-api-v7).</span><span class="sxs-lookup"><span data-stu-id="69c69-117">Sign up for a [free trial key](https://azure.microsoft.com/try/cognitive-services/?api=search-api-v7).</span></span> <span data-ttu-id="69c69-118">The trial key is good for seven days with one call per second.</span><span class="sxs-lookup"><span data-stu-id="69c69-118">The trial key is good for seven days with one call per second.</span></span> <span data-ttu-id="69c69-119">For production scenario, [buy access key](https://portal.azure.com/#create/Microsoft.CognitiveServicesBingSearch-v7).</span><span class="sxs-lookup"><span data-stu-id="69c69-119">For production scenario, [buy access key](https://portal.azure.com/#create/Microsoft.CognitiveServicesBingSearch-v7).</span></span> <span data-ttu-id="69c69-120">See also [pricing information](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/visual/).</span><span class="sxs-lookup"><span data-stu-id="69c69-120">See also [pricing information](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/visual/).</span></span>
* <span data-ttu-id="69c69-121">The ability to run .NET core SDK, .net core 1.1 apps.</span><span class="sxs-lookup"><span data-stu-id="69c69-121">The ability to run .NET core SDK, .net core 1.1 apps.</span></span> <span data-ttu-id="69c69-122">You can get CORE, Framework, and Runtime from here: https://www.microsoft.com/net/download/.</span><span class="sxs-lookup"><span data-stu-id="69c69-122">You can get CORE, Framework, and Runtime from here: https://www.microsoft.com/net/download/.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="69c69-123">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="69c69-123">Application dependencies</span></span>

<span data-ttu-id="69c69-124">To set up a console application using the Bing Web Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69c69-124">To set up a console application using the Bing Web Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span></span>  <span data-ttu-id="69c69-125">Add the `Microsoft.Azure.CognitiveServices.Search.VisualSearch` package.</span><span class="sxs-lookup"><span data-stu-id="69c69-125">Add the `Microsoft.Azure.CognitiveServices.Search.VisualSearch` package.</span></span>

<span data-ttu-id="69c69-126">Installing the [NuGet Web Search SDK package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.VisualSearch/1.0) also installs dependencies, including:</span><span class="sxs-lookup"><span data-stu-id="69c69-126">Installing the [NuGet Web Search SDK package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.VisualSearch/1.0) also installs dependencies, including:</span></span>
* <span data-ttu-id="69c69-127">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="69c69-127">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="69c69-128">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="69c69-128">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="69c69-129">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="69c69-129">Newtonsoft.Json</span></span>

<a name="client"></a>

## <a name="visual-search-client"></a><span data-ttu-id="69c69-130">Visual Search client</span><span class="sxs-lookup"><span data-stu-id="69c69-130">Visual Search client</span></span>
<span data-ttu-id="69c69-131">To create an instance of the `VisualSearchAPI` client, add using directives:</span><span class="sxs-lookup"><span data-stu-id="69c69-131">To create an instance of the `VisualSearchAPI` client, add using directives:</span></span>

```csharp
using Microsoft.Azure.CognitiveServices.Search.VisualSearch;
using Microsoft.Azure.CognitiveServices.Search.VisualSearch.Models;
```

<span data-ttu-id="69c69-132">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="69c69-132">Then, instantiate the client:</span></span>

```csharp
var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));
```

<span data-ttu-id="69c69-133">Use the client to search images:</span><span class="sxs-lookup"><span data-stu-id="69c69-133">Use the client to search images:</span></span>

```csharp
 System.IO.FileStream stream = new FileStream(Path.Combine("TestImages", "image.jpg"), FileMode.Open;
 // The knowledgeRequest parameter is not required if an image binary is passed in the request body
 var visualSearchResults = client.Images.VisualSearchMethodAsync(image: stream, knowledgeRequest: (string)null).Result;
```

<span data-ttu-id="69c69-134">Parse the results of the previous query:</span><span class="sxs-lookup"><span data-stu-id="69c69-134">Parse the results of the previous query:</span></span>

```csharp
// Visual Search results
if (visualSearchResults.Image?.ImageInsightsToken != null)
{
    Console.WriteLine($"Uploaded image insights token: {visualSearchResults.Image.ImageInsightsToken}");
}
else
{
    Console.WriteLine("Couldn't find image insights token!");
}

// List of tags
if (visualSearchResults.Tags.Count > 0)
{
    var firstTagResult = visualSearchResults.Tags.First();
    Console.WriteLine($"Visual search tag count: {visualSearchResults.Tags.Count}");

    // List of actions in first tag
    if (firstTagResult.Actions.Count > 0)
    {
        var firstActionResult = firstTagResult.Actions.First();
        Console.WriteLine($"First tag action count: {firstTagResult.Actions.Count}");
        Console.WriteLine($"First tag action type: {firstActionResult.ActionType}");
    }
    else
    {
        Console.WriteLine("Couldn't find tag actions!");
    }
```

<a name="complete"></a> 

## <a name="complete-console-application"></a><span data-ttu-id="69c69-135">Complete console application</span><span class="sxs-lookup"><span data-stu-id="69c69-135">Complete console application</span></span>

<span data-ttu-id="69c69-136">The following console application executes the previously defined query and parses the results:</span><span class="sxs-lookup"><span data-stu-id="69c69-136">The following console application executes the previously defined query and parses the results:</span></span>

```csharp
using Microsoft.Azure.CognitiveServices.Search.VisualSearch;
using Microsoft.Azure.CognitiveServices.Search.VisualSearch.Models;
using System;
using System.IO;
using System.Linq;

namespace VisualSrchSDK
{
    class Program
    {
        static void Main(string[] args)
        {
            String subKey = "YOUR-SUBSCRIPTION-KEY";

            VisualSearchImageBinary(subKey);
            //VisualSearchImageBinaryWithCropArea(subKey);
            //VisualSearchUrlWithFilters(subKey);
            //VisualSearchInsightsTokenWithCropArea(subKey);
            //VisualSearchUrlWithJson(subKey);

            Console.WriteLine("\r\nAny key to quit...");
            Console.ReadKey();
        }


        // This will send an image binary in the body of the post request and print out the imageInsightsToken, 
        //  the number of tags, the number of actions, and the first actionType.

        public static void VisualSearchImageBinary(string subscriptionKey)
        {
            var client = new VisualSearchAPI(new ApiKeyServiceClientCredentials(subscriptionKey));

            try
            {
                using (System.IO.FileStream stream = new FileStream(Path.Combine("TestImages", "image.jpg"), FileMode.Open))
                {
                    // The knowledgeRequest parameter is not required if an image binary is passed in the request body
                    var visualSearchResults = client.Images.VisualSearchMethodAsync(image: stream, knowledgeRequest: (string)null).Result;
                    Console.WriteLine("\r\nVisual search request with binary of image");

                    if (visualSearchResults == null)
                    {
                        Console.WriteLine("No visual search result data.");
                    }
                    else
                    {
                        // Visual Search results
                        if (visualSearchResults.Image?.ImageInsightsToken != null)
                        {
                            Console.WriteLine($"Uploaded image insights token: {visualSearchResults.Image.ImageInsightsToken}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find image insights token!");
                        }

                        // List of tags
                        if (visualSearchResults.Tags.Count > 0)
                        {
                            var firstTagResult = visualSearchResults.Tags.First();
                            Console.WriteLine($"Visual search tag count: {visualSearchResults.Tags.Count}");

                            // List of actions in first tag
                            if (firstTagResult.Actions.Count > 0)
                            {
                                var firstActionResult = firstTagResult.Actions.First();
                                Console.WriteLine($"First tag action count: {firstTagResult.Actions.Count}");
                                Console.WriteLine($"First tag action type: {firstActionResult.ActionType}");
                            }
                            else
                            {
                                Console.WriteLine("Couldn't find tag actions!");
                            }

                        }
                        else
                        {
                            Console.WriteLine("Couldn't find image tags!");
                        }
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }
    }
}
```

<span data-ttu-id="69c69-137">The Bing search samples demonstrate various features of the SDK.</span><span class="sxs-lookup"><span data-stu-id="69c69-137">The Bing search samples demonstrate various features of the SDK.</span></span>  <span data-ttu-id="69c69-138">Add the following functions to the previously defined `VisualSrchSDK` class.</span><span class="sxs-lookup"><span data-stu-id="69c69-138">Add the following functions to the previously defined `VisualSrchSDK` class.</span></span>

<a name="binary-crop"></a>

## <a name="image-binary-post-with-croparea"></a><span data-ttu-id="69c69-139">Image binary post with cropArea</span><span class="sxs-lookup"><span data-stu-id="69c69-139">Image binary post with cropArea</span></span>

<span data-ttu-id="69c69-140">The following code sends an image binary in the body of the post request, along with a cropArea object.</span><span class="sxs-lookup"><span data-stu-id="69c69-140">The following code sends an image binary in the body of the post request, along with a cropArea object.</span></span>  <span data-ttu-id="69c69-141">Then it prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span><span class="sxs-lookup"><span data-stu-id="69c69-141">Then it prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span></span>

```csharp
public static void VisualSearchImageBinaryWithCropArea(string subscriptionKey)
{
    var client = new VisualSearchAPI(new ApiKeyServiceClientCredentials(subscriptionKey));

    try
    {
        using (FileStream stream = new FileStream(Path.Combine("TestImages", "image.jpg"), FileMode.Open))
        {
            // The ImageInfo struct contains a crop area specifying a region to crop in the uploaded image
            CropArea CropArea = new CropArea(top: (float)0.1, bottom: (float)0.5, left: (float)0.1, right: (float)0.9);
            ImageInfo ImageInfo = new ImageInfo(cropArea: CropArea);
            VisualSearchRequest VisualSearchRequest = new VisualSearchRequest(imageInfo: ImageInfo);

            // The knowledgeRequest here holds additional information about the image, which is passed in in binary form
            var visualSearchResults = client.Images.VisualSearchMethodAsync(image: stream, knowledgeRequest: VisualSearchRequest).Result;
            Console.WriteLine("\r\nVisual search request with binary of image with knowledgeRequest of CropArea");

            if (visualSearchResults == null)
            {
                Console.WriteLine("No visual search result data.");
            }
            else
            {
                // Visual Search results
                if (visualSearchResults.Image?.ImageInsightsToken != null)
                {
                    Console.WriteLine($"Uploaded image insights token: {visualSearchResults.Image.ImageInsightsToken}");
                }
                else
                {
                    Console.WriteLine("Couldn't find image insights token!");
                }

                // List of tags
                if (visualSearchResults.Tags.Count > 0)
                {
                    var firstTagResult = visualSearchResults.Tags.First();
                    Console.WriteLine($"Visual search tag count: {visualSearchResults.Tags.Count}");

                    // List of actions in first tag
                    if (firstTagResult.Actions.Count > 0)
                    {
                        var firstActionResult = firstTagResult.Actions.First();
                        Console.WriteLine($"First tag action count: {firstTagResult.Actions.Count}");
                        Console.WriteLine($"First tag action type: {firstActionResult.ActionType}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find tag actions!");
                    }

                }
                else
                {
                    Console.WriteLine("Couldn't find image tags!");
                }
            }
        }
    }

    catch (Exception ex)
    {
        Console.WriteLine("Encountered exception. " + ex.Message);
    }
}
```

<a name="knowledge-req"></a>

## <a name="knowledgerequest-parameter"></a><span data-ttu-id="69c69-142">KnowledgeRequest parameter</span><span class="sxs-lookup"><span data-stu-id="69c69-142">KnowledgeRequest parameter</span></span>

<span data-ttu-id="69c69-143">The following code sends an image url in the `knowledgeRequest` parameter, along with a \"site:www.bing.com\" filter.</span><span class="sxs-lookup"><span data-stu-id="69c69-143">The following code sends an image url in the `knowledgeRequest` parameter, along with a \"site:www.bing.com\" filter.</span></span>  <span data-ttu-id="69c69-144">Then it prints the `imageInsightsToken`, the number of tags, the number of actions, and the first actionType.</span><span class="sxs-lookup"><span data-stu-id="69c69-144">Then it prints the `imageInsightsToken`, the number of tags, the number of actions, and the first actionType.</span></span>

```csharp
public static void VisualSearchUrlWithFilters(string subscriptionKey)
{
    var client = new VisualSearchAPI(new ApiKeyServiceClientCredentials(subscriptionKey));

    try
    {
        // The image can be specified via URL, in the ImageInfo object
        var ImageUrl = "https://images.unsplash.com/photo-1512546148165-e50d714a565a?w=600&q=80";
        ImageInfo ImageInfo = new ImageInfo(url: ImageUrl);

        // Optional filters inside the knowledgeRequest will restrict similar products and images to certain domains
        Filters Filters = new Filters(site: "www.bing.com");
        KnowledgeRequest KnowledgeRequest = new KnowledgeRequest(filters: Filters);

        // An image binary is not necessary here, as the image is specified via URL
        VisualSearchRequest VisualSearchRequest = new VisualSearchRequest(imageInfo: ImageInfo, knowledgeRequest: KnowledgeRequest);
        var visualSearchResults = client.Images.VisualSearchMethodAsync(knowledgeRequest: VisualSearchRequest).Result;
        Console.WriteLine("\r\nVisual search request with url of image and knowledgeRequest based on filters");

        if (visualSearchResults == null)
        {
            Console.WriteLine("No visual search result data.");
        }
        else
        {
            // Visual Search results
            if (visualSearchResults.Image?.ImageInsightsToken != null)
            {
                Console.WriteLine($"Uploaded image insights token: {visualSearchResults.Image.ImageInsightsToken}");
            }
            else
            {
                Console.WriteLine("Couldn't find image insights token!");
            }

            // List of tags
            if (visualSearchResults.Tags.Count > 0)
            {
                var firstTagResult = visualSearchResults.Tags.First();
                Console.WriteLine($"Visual search tag count: {visualSearchResults.Tags.Count}");

                // List of actions in first tag
                if (firstTagResult.Actions.Count > 0)
                {
                    var firstActionResult = firstTagResult.Actions.First();
                    Console.WriteLine($"First tag action count: {firstTagResult.Actions.Count}");
                    Console.WriteLine($"First tag action type: {firstActionResult.ActionType}");
                }
                else
                {
                    Console.WriteLine("Couldn't find tag actions!");
                }

            }
            else
            {
                Console.WriteLine("Couldn't find image tags!");
            }
        }
    }

    catch (Exception ex)
    {
        Console.WriteLine("Encountered exception. " + ex.Message);
    }
}
```

<a name="tags-actions"></a>

## <a name="tags-actions-and-actiontype"></a><span data-ttu-id="69c69-145">Tags, actions, and actionType</span><span class="sxs-lookup"><span data-stu-id="69c69-145">Tags, actions, and actionType</span></span>

<span data-ttu-id="69c69-146">The following code sends an image insights token in the knowledgeRequest parameter, along with a cropArea object.</span><span class="sxs-lookup"><span data-stu-id="69c69-146">The following code sends an image insights token in the knowledgeRequest parameter, along with a cropArea object.</span></span>  <span data-ttu-id="69c69-147">Then it prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span><span class="sxs-lookup"><span data-stu-id="69c69-147">Then it prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span></span>

```csharp
public static void VisualSearchInsightsTokenWithCropArea(string subscriptionKey)
{
    var client = new VisualSearchAPI(new ApiKeyServiceClientCredentials(subscriptionKey));

    try
    {
        // The image can be specified via an insights token, in the ImageInfo object
        var ImageInsightsToken = "bcid_113F29C079F18F385732D8046EC80145*ccid_oV/QcH95*mid_687689FAFA449B35BC11A1AE6CEAB6F9A9B53708*thid_R.113F29C079F18F385732D8046EC80145";

        // An optional crop area can be passed in to define a region of interest in the image
        CropArea CropArea = new CropArea(top: (float)0.1, bottom: (float)0.5, left: (float)0.1, right: (float)0.9);
        ImageInfo ImageInfo = new ImageInfo(imageInsightsToken: ImageInsightsToken, cropArea: CropArea);

        // An image binary is not necessary here, as the image is specified via insights token
        VisualSearchRequest VisualSearchRequest = new VisualSearchRequest(imageInfo: ImageInfo);
        var visualSearchResults = client.Images.VisualSearchMethodAsync(knowledgeRequest: VisualSearchRequest).Result;
        Console.WriteLine("\r\nVisual search request with ImageInsightsToken and knowledgeRequest based on imageInfo of cropArea");

        if (visualSearchResults == null)
        {
            Console.WriteLine("No visual search result data.");
        }
        else
        {
            // Visual Search results
            if (visualSearchResults.Image?.ImageInsightsToken != null)
            {
                Console.WriteLine($"Uploaded image insights token: {visualSearchResults.Image.ImageInsightsToken}");
            }
            else
            {
                Console.WriteLine("Couldn't find image insights token!");
            }

            // List of tags
            if (visualSearchResults.Tags.Count > 0)
            {
                var firstTagResult = visualSearchResults.Tags.First();
                Console.WriteLine($"Visual search tag count: {visualSearchResults.Tags.Count}");

                // List of actions in first tag
                if (firstTagResult.Actions.Count > 0)
                {
                    var firstActionResult = firstTagResult.Actions.First();
                    Console.WriteLine($"First tag action count: {firstTagResult.Actions.Count}");
                    Console.WriteLine($"First tag action type: {firstActionResult.ActionType}");
                }
                else
                {
                    Console.WriteLine("Couldn't find tag actions!");
                }

            }
            else
            {
                Console.WriteLine("Couldn't find image tags!");
            }
        }
    }

    catch (Exception ex)
    {
        Console.WriteLine("Encountered exception. " + ex.Message);
    }
}
```

<a name="num-tags-actions"></a>

## <a name="number-of-tags-number-of-actions-and-first-actiontype"></a><span data-ttu-id="69c69-148">Number of tags, number of actions, and first actionType</span><span class="sxs-lookup"><span data-stu-id="69c69-148">Number of tags, number of actions, and first actionType</span></span>

<span data-ttu-id="69c69-149">The following code sends an image url in the knowledgeRequest parameter, along with a crop area.</span><span class="sxs-lookup"><span data-stu-id="69c69-149">The following code sends an image url in the knowledgeRequest parameter, along with a crop area.</span></span>  <span data-ttu-id="69c69-150">Then prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span><span class="sxs-lookup"><span data-stu-id="69c69-150">Then prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span></span>

```csharp
public static void VisualSearchUrlWithJson(string subscriptionKey)
{
    var client = new VisualSearchAPI(new ApiKeyServiceClientCredentials(subscriptionKey));

    try
    {

        //The visual search request can be passed in as a JSON string
        //The image is specified via URL in the ImageInfo object, along with a crop area as shown below:
        
        //     "imageInfo": {
        //         "url": "https://images.unsplash.com/photo-1512546148165-e50d714a565a?w=600&q=80",
        //     "cropArea": {
        //           "top": 0.1,
        //           "bottom": 0.5,
        //           "left": 0.1,
        //           "right": 0.9
        //         }
        //     },
        //     "knowledgeRequest": {
        //        "filters": {
        //            "site": "www.bing.com"
        //        }              
        //     }

        var VisualSearchRequestJSON = "{\"imageInfo\":{\"url\":\"https://images.unsplash.com/photo-1512546148165-e50d714a565a?w=600&q=80\",\"cropArea\":{\"top\":0.1,\"bottom\":0.5,\"left\":0.1,\"right\":0.9}},\"knowledgeRequest\":{\"filters\":{\"site\":\"www.bing.com\"}}}";

        // An image binary is not necessary here, as the image is specified by URL in JSON text
        var visualSearchResults = client.Images.VisualSearchMethodAsync(knowledgeRequest: VisualSearchRequestJSON).Result;
        Console.WriteLine("\r\nVisual search request with image url specified by JSON text");

        if (visualSearchResults == null)
        {
            Console.WriteLine("No visual search result data.");
        }
        else
        {
            // Visual Search results
            if (visualSearchResults.Image?.ImageInsightsToken != null)
            {
                Console.WriteLine($"Uploaded image insights token: {visualSearchResults.Image.ImageInsightsToken}");
            }
            else
            {
                Console.WriteLine("Couldn't find image insights token!");
            }

            // List of tags
            if (visualSearchResults.Tags.Count > 0)
            {
                var firstTagResult = visualSearchResults.Tags.First();
                Console.WriteLine($"Visual search tag count: {visualSearchResults.Tags.Count}");

                // List of actions in first tag
                if (firstTagResult.Actions.Count > 0)
                {
                    var firstActionResult = firstTagResult.Actions.First();
                    Console.WriteLine($"First tag action count: {firstTagResult.Actions.Count}");
                    Console.WriteLine($"First tag action type: {firstActionResult.ActionType}");
                }
                else
                {
                    Console.WriteLine("Couldn't find tag actions!");
                }

            }
            else
            {
                Console.WriteLine("Couldn't find image tags!");
            }
        }
    }

    catch (Exception ex)
    {
        Console.WriteLine("Encountered exception. " + ex.Message);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="69c69-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="69c69-151">Next steps</span></span>

<span data-ttu-id="69c69-152">[Cognitive Services .NET SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7).</span><span class="sxs-lookup"><span data-stu-id="69c69-152">[Cognitive Services .NET SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7).</span></span>
