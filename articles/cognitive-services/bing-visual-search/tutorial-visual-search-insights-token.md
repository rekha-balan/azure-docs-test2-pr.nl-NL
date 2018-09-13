---
title: Bing Visual Search SDK ImageInsightsToken tutorial | Microsoft Docs
description: How to use the Bing Visual Search SDK to get URLs of images specified by ImageInsightsToken.
services: cognitive-services
author: mikedodaro
manager: ronakshah
ms.service: cognitive-services
ms.component: bing-visual-search
ms.topic: article
ms.date: 06/21/2018
ms.author: rosh
ms.openlocfilehash: 8f6e7f7e88ae78fe7e8a9be4adefd689dd26d0f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965936"
---
# <a name="tutorial-bing-visual-search-sdk-imageinsightstoken-and-results"></a><span data-ttu-id="3fe13-103">Tutorial: Bing Visual Search SDK ImageInsightsToken and results</span><span class="sxs-lookup"><span data-stu-id="3fe13-103">Tutorial: Bing Visual Search SDK ImageInsightsToken and results</span></span>
<span data-ttu-id="3fe13-104">The Visual Search SDK includes an option to find images online from a previous search that returns an `ImageInsightsToken`.</span><span class="sxs-lookup"><span data-stu-id="3fe13-104">The Visual Search SDK includes an option to find images online from a previous search that returns an `ImageInsightsToken`.</span></span>  <span data-ttu-id="3fe13-105">This example gets an `ImageInsightsToken` and uses the token in a subsequent search.</span><span class="sxs-lookup"><span data-stu-id="3fe13-105">This example gets an `ImageInsightsToken` and uses the token in a subsequent search.</span></span>  <span data-ttu-id="3fe13-106">The code sends the `ImageInsightsToken` to Bing and returns results that include Bing Search URLs and URLs of similar images found online.</span><span class="sxs-lookup"><span data-stu-id="3fe13-106">The code sends the `ImageInsightsToken` to Bing and returns results that include Bing Search URLs and URLs of similar images found online.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fe13-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3fe13-107">Prerequisites</span></span>
<span data-ttu-id="3fe13-108">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3fe13-108">Visual Studio 2017.</span></span> <span data-ttu-id="3fe13-109">If necessary, you can download free community version from here: https://www.visualstudio.com/vs/community/.</span><span class="sxs-lookup"><span data-stu-id="3fe13-109">If necessary, you can download free community version from here: https://www.visualstudio.com/vs/community/.</span></span>
<span data-ttu-id="3fe13-110">A cognitive services API key is required to authenticate SDK calls.</span><span class="sxs-lookup"><span data-stu-id="3fe13-110">A cognitive services API key is required to authenticate SDK calls.</span></span> <span data-ttu-id="3fe13-111">Sign up for a free trial key.</span><span class="sxs-lookup"><span data-stu-id="3fe13-111">Sign up for a free trial key.</span></span> <span data-ttu-id="3fe13-112">The trial key is good for seven days with one call per second.</span><span class="sxs-lookup"><span data-stu-id="3fe13-112">The trial key is good for seven days with one call per second.</span></span> <span data-ttu-id="3fe13-113">For production scenarios, buy an access key.</span><span class="sxs-lookup"><span data-stu-id="3fe13-113">For production scenarios, buy an access key.</span></span> <span data-ttu-id="3fe13-114">See also pricing information.</span><span class="sxs-lookup"><span data-stu-id="3fe13-114">See also pricing information.</span></span>
<span data-ttu-id="3fe13-115">The ability to run .NET core SDK, .net core 1.1 apps.</span><span class="sxs-lookup"><span data-stu-id="3fe13-115">The ability to run .NET core SDK, .net core 1.1 apps.</span></span> <span data-ttu-id="3fe13-116">You can get CORE, Framework, and Runtime from here: https://www.microsoft.com/net/download/.</span><span class="sxs-lookup"><span data-stu-id="3fe13-116">You can get CORE, Framework, and Runtime from here: https://www.microsoft.com/net/download/.</span></span>

##<a name="application-dependencies"></a><span data-ttu-id="3fe13-117">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="3fe13-117">Application dependencies</span></span>
<span data-ttu-id="3fe13-118">To set up a console application using the Bing Web Search SDK, browse to the Manage NuGet Packages option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fe13-118">To set up a console application using the Bing Web Search SDK, browse to the Manage NuGet Packages option from the Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="3fe13-119">Add:</span><span class="sxs-lookup"><span data-stu-id="3fe13-119">Add:</span></span>
* <span data-ttu-id="3fe13-120">Microsoft.Azure.CognitiveServices.Search.VisualSearch</span><span class="sxs-lookup"><span data-stu-id="3fe13-120">Microsoft.Azure.CognitiveServices.Search.VisualSearch</span></span>
* <span data-ttu-id="3fe13-121">Microsoft.Azure.CognitiveServices.Search.ImageSearchpackage packages.</span><span class="sxs-lookup"><span data-stu-id="3fe13-121">Microsoft.Azure.CognitiveServices.Search.ImageSearchpackage packages.</span></span>

<span data-ttu-id="3fe13-122">Installing the NuGet Web Search SDK package also installs dependencies, including:</span><span class="sxs-lookup"><span data-stu-id="3fe13-122">Installing the NuGet Web Search SDK package also installs dependencies, including:</span></span>

* <span data-ttu-id="3fe13-123">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="3fe13-123">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="3fe13-124">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="3fe13-124">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="3fe13-125">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="3fe13-125">Newtonsoft.Json</span></span>

## <a name="get-the-imageinsightstoken-from-image-search"></a><span data-ttu-id="3fe13-126">Get the ImageInsightsToken from Image Search</span><span class="sxs-lookup"><span data-stu-id="3fe13-126">Get the ImageInsightsToken from Image Search</span></span>
<span data-ttu-id="3fe13-127">This example uses an `ImageInsightsToken` obtained by the following method.</span><span class="sxs-lookup"><span data-stu-id="3fe13-127">This example uses an `ImageInsightsToken` obtained by the following method.</span></span>  <span data-ttu-id="3fe13-128">For more information about this call, see [Image Search SDK C# quickstart](https://docs.microsoft.com/en-us/azure/cognitive-services/bing-image-search/image-search-sdk-quickstart).</span><span class="sxs-lookup"><span data-stu-id="3fe13-128">For more information about this call, see [Image Search SDK C# quickstart](https://docs.microsoft.com/en-us/azure/cognitive-services/bing-image-search/image-search-sdk-quickstart).</span></span>

<span data-ttu-id="3fe13-129">The code searches for results on a query for 'Canadian Rockies' and gets an ImageInsightsToken.</span><span class="sxs-lookup"><span data-stu-id="3fe13-129">The code searches for results on a query for 'Canadian Rockies' and gets an ImageInsightsToken.</span></span> <span data-ttu-id="3fe13-130">It prints the first image's insights token, thumbnail url, and image content url.</span><span class="sxs-lookup"><span data-stu-id="3fe13-130">It prints the first image's insights token, thumbnail url, and image content url.</span></span>  <span data-ttu-id="3fe13-131">The method returns the `ImageInsightsToken`for use in a subsequent Visual Search request.</span><span class="sxs-lookup"><span data-stu-id="3fe13-131">The method returns the `ImageInsightsToken`for use in a subsequent Visual Search request.</span></span>

```
        private static String ImageResults(String subKey)
        {
            String insightTok = "None";
            try
            {
                var client = new ImageSearchAPI(new Microsoft.Azure.CognitiveServices.Search.ImageSearch.ApiKeyServiceClientCredentials(subKey)); //
                var imageResults = client.Images.SearchAsync(query: "canadian rockies").Result;
                Console.WriteLine("Search images for query \"canadian rockies\"");

                if (imageResults == null)
                {
                    Console.WriteLine("No image result data.");
                }
                else
                {
                    // Image results
                    if (imageResults.Value.Count > 0)
                    {
                        var firstImageResult = imageResults.Value.First();

                        Console.WriteLine($"\r\nImage result count: {imageResults.Value.Count}");
                        insightTok = firstImageResult.ImageInsightsToken;
                        Console.WriteLine($"First image insights token: {firstImageResult.ImageInsightsToken}");  
                        Console.WriteLine($"First image thumbnail url: {firstImageResult.ThumbnailUrl}");
                        Console.WriteLine($"First image content url: {firstImageResult.ContentUrl}");
                    }
                    else
                    {
                        insightTok = "None found";
                        Console.WriteLine("Couldn't find image results!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("\r\nEncountered exception. " + ex.Message);
            }

            return insightTok;
        }
```

## <a name="specify-the-imageinsightstoken-for-visual-search-request"></a><span data-ttu-id="3fe13-132">Specify the ImageInsightsToken for Visual Search request</span><span class="sxs-lookup"><span data-stu-id="3fe13-132">Specify the ImageInsightsToken for Visual Search request</span></span>
<span data-ttu-id="3fe13-133">This example uses the insights token returned by the previous method.</span><span class="sxs-lookup"><span data-stu-id="3fe13-133">This example uses the insights token returned by the previous method.</span></span> <span data-ttu-id="3fe13-134">The following code creates an `ImageInfo` object from the `ImageInsightsToken` and loads the ImageInfo object into a `VisualSearchRequest`.</span><span class="sxs-lookup"><span data-stu-id="3fe13-134">The following code creates an `ImageInfo` object from the `ImageInsightsToken` and loads the ImageInfo object into a `VisualSearchRequest`.</span></span> <span data-ttu-id="3fe13-135">Specify `ImageInsightsToken` in an `ImageInfo` for the `VisualSearchRequest`</span><span class="sxs-lookup"><span data-stu-id="3fe13-135">Specify `ImageInsightsToken` in an `ImageInfo` for the `VisualSearchRequest`</span></span>

```
ImageInfo ImageInfo = new ImageInfo(imageInsightsToken: insightsTok);
```
## <a name="use-visual-search-to-find-images-from-an-imageinsightstoken"></a><span data-ttu-id="3fe13-136">Use Visual Search to find images from an ImageInsightsToken</span><span class="sxs-lookup"><span data-stu-id="3fe13-136">Use Visual Search to find images from an ImageInsightsToken</span></span>
<span data-ttu-id="3fe13-137">The `VisualSearchRequest` contains information about the image to search for in the `ImageInfo` object.</span><span class="sxs-lookup"><span data-stu-id="3fe13-137">The `VisualSearchRequest` contains information about the image to search for in the `ImageInfo` object.</span></span>  <span data-ttu-id="3fe13-138">The `VisualSearchMethodAsync` method gets the results.</span><span class="sxs-lookup"><span data-stu-id="3fe13-138">The `VisualSearchMethodAsync` method gets the results.</span></span>
```
// An image binary is not necessary here, as the image is specified by insights token.
VisualSearchRequest VisualSearchRequest = new VisualSearchRequest(ImageInfo);

var visualSearchResults = client.Images.VisualSearchMethodAsync(knowledgeRequest: VisualSearchRequest).Result;
Console.WriteLine("\r\nVisual search request with knowledgeRequest");

```

## <a name="get-the-url-data-from-imagemoduleaction"></a><span data-ttu-id="3fe13-139">Get the URL data from ImageModuleAction</span><span class="sxs-lookup"><span data-stu-id="3fe13-139">Get the URL data from ImageModuleAction</span></span>
<span data-ttu-id="3fe13-140">Visual Search results are `ImageTag` objects.</span><span class="sxs-lookup"><span data-stu-id="3fe13-140">Visual Search results are `ImageTag` objects.</span></span>  <span data-ttu-id="3fe13-141">Each tag contains a list of `ImageAction` objects.</span><span class="sxs-lookup"><span data-stu-id="3fe13-141">Each tag contains a list of `ImageAction` objects.</span></span>  <span data-ttu-id="3fe13-142">Each `ImageAction` contains a `Data` field which is a list of values that depend on the type of action:</span><span class="sxs-lookup"><span data-stu-id="3fe13-142">Each `ImageAction` contains a `Data` field which is a list of values that depend on the type of action:</span></span>

<span data-ttu-id="3fe13-143">You can get the various types with the following code:</span><span class="sxs-lookup"><span data-stu-id="3fe13-143">You can get the various types with the following code:</span></span>
```
Console.WriteLine("\r\n" + "ActionType: " + i.ActionType + " -> WebSearchUrl: " + i.WebSearchUrl);

```
<span data-ttu-id="3fe13-144">The complete application returns:</span><span class="sxs-lookup"><span data-stu-id="3fe13-144">The complete application returns:</span></span>

* <span data-ttu-id="3fe13-145">ActionType: MoreSizes -> WebSearchUrl:</span><span class="sxs-lookup"><span data-stu-id="3fe13-145">ActionType: MoreSizes -> WebSearchUrl:</span></span>
* <span data-ttu-id="3fe13-146">ActionType: VisualSearch -> WebSearchUrl:</span><span class="sxs-lookup"><span data-stu-id="3fe13-146">ActionType: VisualSearch -> WebSearchUrl:</span></span>
* <span data-ttu-id="3fe13-147">ActionType: ImageById -> WebSearchUrl:</span><span class="sxs-lookup"><span data-stu-id="3fe13-147">ActionType: ImageById -> WebSearchUrl:</span></span>
* <span data-ttu-id="3fe13-148">ActionType: RelatedSearches -> WebSearchUrl:</span><span class="sxs-lookup"><span data-stu-id="3fe13-148">ActionType: RelatedSearches -> WebSearchUrl:</span></span>
* <span data-ttu-id="3fe13-149">ActionType: DocumentLevelSuggestions -> WebSearchUrl:</span><span class="sxs-lookup"><span data-stu-id="3fe13-149">ActionType: DocumentLevelSuggestions -> WebSearchUrl:</span></span>
* <span data-ttu-id="3fe13-150">ActionType: TopicResults -> WebSearchUrl: https://www.bing.com/cr?IG=3E32CC6CA5934FBBA14ABC3B2E4651F9&CID=1BA795A21EAF6A63175699B71FC36B7C&rd=1&h=BcQifmzdKFyyBusjLxxgO42kzq1Geh7RucVVqvH-900&v=1&r=https%3a%2f%2fwww.bing.com%2fdiscover%2fcanadian%2brocky&p=DevEx,5823.1</span><span class="sxs-lookup"><span data-stu-id="3fe13-150">ActionType: TopicResults -> WebSearchUrl: https://www.bing.com/cr?IG=3E32CC6CA5934FBBA14ABC3B2E4651F9&CID=1BA795A21EAF6A63175699B71FC36B7C&rd=1&h=BcQifmzdKFyyBusjLxxgO42kzq1Geh7RucVVqvH-900&v=1&r=https%3a%2f%2fwww.bing.com%2fdiscover%2fcanadian%2brocky&p=DevEx,5823.1</span></span>
* <span data-ttu-id="3fe13-151">ActionType: ImageResults -> WebSearchUrl: https://www.bing.com/cr?IG=3E32CC6CA5934FBBA14ABC3B2E4651F9&CID=1BA795A21EAF6A63175699B71FC36B7C&rd=1&h=PV9GzMFOI0AHZp2gKeWJ8DcveSDRE3fP2jHDKMpJSU8&v=1&r=https%3a%2f%2fwww.bing.com%2fimages%2fsearch%3fq%3doutdoor&p=DevEx,5831.1</span><span class="sxs-lookup"><span data-stu-id="3fe13-151">ActionType: ImageResults -> WebSearchUrl: https://www.bing.com/cr?IG=3E32CC6CA5934FBBA14ABC3B2E4651F9&CID=1BA795A21EAF6A63175699B71FC36B7C&rd=1&h=PV9GzMFOI0AHZp2gKeWJ8DcveSDRE3fP2jHDKMpJSU8&v=1&r=https%3a%2f%2fwww.bing.com%2fimages%2fsearch%3fq%3doutdoor&p=DevEx,5831.1</span></span>

<span data-ttu-id="3fe13-152">As shown in preceding list, the `TopicResults` and `ImageResults` types contain queries for related images.</span><span class="sxs-lookup"><span data-stu-id="3fe13-152">As shown in preceding list, the `TopicResults` and `ImageResults` types contain queries for related images.</span></span> <span data-ttu-id="3fe13-153">The URLs in the list link  to Bing search results.</span><span class="sxs-lookup"><span data-stu-id="3fe13-153">The URLs in the list link  to Bing search results.</span></span>


## <a name="pagesincluding-actiontype-urls-of-images-found-by-visual-search"></a><span data-ttu-id="3fe13-154">PagesIncluding ActionType URLs of images found by Visual Search</span><span class="sxs-lookup"><span data-stu-id="3fe13-154">PagesIncluding ActionType URLs of images found by Visual Search</span></span>

<span data-ttu-id="3fe13-155">Getting the actual image URLs requires a cast that reads an `ActionType` as `ImageModuleAction`, which contains a `Data` element with a list of values.</span><span class="sxs-lookup"><span data-stu-id="3fe13-155">Getting the actual image URLs requires a cast that reads an `ActionType` as `ImageModuleAction`, which contains a `Data` element with a list of values.</span></span>  <span data-ttu-id="3fe13-156">Each value is the URL of an image.</span><span class="sxs-lookup"><span data-stu-id="3fe13-156">Each value is the URL of an image.</span></span>  <span data-ttu-id="3fe13-157">The following casts the `PagesIncluding` action type to `ImageModuleAction` and reads the values.</span><span class="sxs-lookup"><span data-stu-id="3fe13-157">The following casts the `PagesIncluding` action type to `ImageModuleAction` and reads the values.</span></span>
```
    if (i.ActionType == "PagesIncluding")
    {
        foreach(ImageObject o in (i as ImageModuleAction).Data.Value)
        {
            Console.WriteLine("ContentURL: " + o.ContentUrl);
        }
    }
```
<span data-ttu-id="3fe13-158">For more information about these data types, see [Images - Visual Search](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bingvisualsearch/images/visualsearch).</span><span class="sxs-lookup"><span data-stu-id="3fe13-158">For more information about these data types, see [Images - Visual Search](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bingvisualsearch/images/visualsearch).</span></span>
## <a name="complete-code"></a><span data-ttu-id="3fe13-159">Complete code</span><span class="sxs-lookup"><span data-stu-id="3fe13-159">Complete code</span></span>

<span data-ttu-id="3fe13-160">The following code runs previous examples.</span><span class="sxs-lookup"><span data-stu-id="3fe13-160">The following code runs previous examples.</span></span> <span data-ttu-id="3fe13-161">It sends the `ImageInsightsToken` in a post request.</span><span class="sxs-lookup"><span data-stu-id="3fe13-161">It sends the `ImageInsightsToken` in a post request.</span></span> <span data-ttu-id="3fe13-162">Then it prints the Bing search URLs for each ActionType.</span><span class="sxs-lookup"><span data-stu-id="3fe13-162">Then it prints the Bing search URLs for each ActionType.</span></span> <span data-ttu-id="3fe13-163">If the ActionType is `PagesIncluding`, the code gets the `ImageObject` items in `Data`.</span><span class="sxs-lookup"><span data-stu-id="3fe13-163">If the ActionType is `PagesIncluding`, the code gets the `ImageObject` items in `Data`.</span></span>  <span data-ttu-id="3fe13-164">The `Data` contains a list of values, which are the URLs of images on Web pages.</span><span class="sxs-lookup"><span data-stu-id="3fe13-164">The `Data` contains a list of values, which are the URLs of images on Web pages.</span></span>  <span data-ttu-id="3fe13-165">Copy and paste resulting Visual Search URLs to browser to show results.</span><span class="sxs-lookup"><span data-stu-id="3fe13-165">Copy and paste resulting Visual Search URLs to browser to show results.</span></span> <span data-ttu-id="3fe13-166">Copy and paste ContentUrl items to browser to show images.</span><span class="sxs-lookup"><span data-stu-id="3fe13-166">Copy and paste ContentUrl items to browser to show images.</span></span>

```
using System;
using System.IO;
using System.Linq;
using Microsoft.Azure.CognitiveServices.Search.VisualSearch;
using Microsoft.Azure.CognitiveServices.Search.VisualSearch.Models;
using Microsoft.Azure.CognitiveServices.Search.ImageSearch;

namespace VisualSearchFeatures
{
    class Program
    {
        static void Main(string[] args)
        {
            String subscriptionKey = "YOUR-ACCESS-KEY";

            insightsToken = ImageResults(subscriptionKey);

            VisualSearchInsightsToken(subscriptionKey, insightsToken);

            Console.WriteLine("Any key to quit...");
            Console.ReadKey();

        }

        // Searches for results on query (Canadian Rockies) and gets an ImageInsightsToken.
        // Also prints first image insights token, thumbnail url, and image content url.
        private static String ImageResults(String subKey)
        {
            String insightTok = "None";
            try
            {
                var client = new ImageSearchAPI(new Microsoft.Azure.CognitiveServices.Search.ImageSearch.ApiKeyServiceClientCredentials(subKey)); //
                var imageResults = client.Images.SearchAsync(query: "canadian rockies").Result;
                Console.WriteLine("Search images for query \"canadian rockies\"");

                if (imageResults == null)
                {
                    Console.WriteLine("No image result data.");
                }
                else
                {
                    // Image results
                    if (imageResults.Value.Count > 0)
                    {
                        var firstImageResult = imageResults.Value.First();

                        Console.WriteLine($"\r\nImage result count: {imageResults.Value.Count}");
                        insightTok = firstImageResult.ImageInsightsToken;
                        Console.WriteLine($"First image insights token: {firstImageResult.ImageInsightsToken}");  
                        Console.WriteLine($"First image thumbnail url: {firstImageResult.ThumbnailUrl}");
                        Console.WriteLine($"First image content url: {firstImageResult.ContentUrl}");
                    }
                    else
                    {
                        insightTok = "None found";
                        Console.WriteLine("Couldn't find image results!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("\r\nEncountered exception. " + ex.Message);
            }

            return insightTok;
        }


        // This method will get Visual Search results from an imageInsightsToken obtained from the return value of the ImageResults method.
        // The method includes imageInsightsToken the in a knowledgeRequest parameter, along with a cropArea object. 
        // It prints out the imageInsightsToken uploaded in the request.
        // Finally the example prints URLs of images found using the imageInsightsToken.

        public static void VisualSearchInsightsToken(string subscriptionKey, string insightsTok)
        {
            var client = new VisualSearchAPI(new Microsoft.Azure.CognitiveServices.Search.VisualSearch.ApiKeyServiceClientCredentials(subscriptionKey));

            try
            {
                // The image can be specified via an insights token, in the ImageInfo object.
                ImageInfo ImageInfo = new ImageInfo(imageInsightsToken: insightsTok);

                // An image binary is not necessary here, as the image is specified by insights token.
                VisualSearchRequest VisualSearchRequest = new VisualSearchRequest(ImageInfo);

                var visualSearchResults = client.Images.VisualSearchMethodAsync(knowledgeRequest: VisualSearchRequest).Result;
                Console.WriteLine("\r\nVisual search request with imageInsightsToken and knowledgeRequest");

                if (visualSearchResults == null)
                {
                    Console.WriteLine("No visual search result data.");
                }
                else
                {
                    // Visual Search results
                    if (visualSearchResults.Image?.ImageInsightsToken != null)
                    {
                        Console.WriteLine($"Uploaded image insights token: {insightsTok}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find image insights token!");
                    }

                    if (visualSearchResults.Tags.Count > 0)
                    {
                        // List of tags
                        foreach (ImageTag t in visualSearchResults.Tags)
                        {
                            foreach (ImageAction i in t.Actions)
                            {
                                Console.WriteLine("\r\n" + "ActionType: " + i.ActionType + " WebSearchURL: " + i.WebSearchUrl);

                                if (i.ActionType == "PagesIncluding")
                                {
                                    foreach (ImageObject o in (i as ImageModuleAction).Data.Value)
                                    {
                                        Console.WriteLine("ContentURL: " + o.ContentUrl);
                                    }
                                }
                            }
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
    }
}

```
## <a name="next-steps"></a><span data-ttu-id="3fe13-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fe13-167">Next steps</span></span>
[<span data-ttu-id="3fe13-168">Visual Search response</span><span class="sxs-lookup"><span data-stu-id="3fe13-168">Visual Search response</span></span>](https://docs.microsoft.com/azure/cognitive-services/bing-visual-search/overview#the-response)
