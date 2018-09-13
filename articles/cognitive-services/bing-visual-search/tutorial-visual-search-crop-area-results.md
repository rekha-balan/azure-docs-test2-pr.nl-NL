---
title: Bing Visual Search SDK crop area results tutorial | Microsoft Docs
description: How to use the Bing Visual Search SDK to get URLs of images similar to crop area of uploaded image.
services: cognitive-services
author: mikedodaro
manager: ronakshah
ms.service: cognitive-services
ms.component: bing-visual-search
ms.topic: article
ms.date: 06/20/2018
ms.author: rosh
ms.openlocfilehash: 9bc3c180f108025f442343d8c5356982a83826a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857579"
---
# <a name="tutorial-bing-visual-search-sdk-image-crop-area-and-results"></a><span data-ttu-id="8fbc8-103">Tutorial: Bing Visual Search SDK image crop area and results</span><span class="sxs-lookup"><span data-stu-id="8fbc8-103">Tutorial: Bing Visual Search SDK image crop area and results</span></span>
<span data-ttu-id="8fbc8-104">The Visual Search SDK includes an option to select an area of an image and find images online that are similar to the crop area of the larger image.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-104">The Visual Search SDK includes an option to select an area of an image and find images online that are similar to the crop area of the larger image.</span></span>  <span data-ttu-id="8fbc8-105">This example specifies crop area showing one person from an image that contains several people.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-105">This example specifies crop area showing one person from an image that contains several people.</span></span>  <span data-ttu-id="8fbc8-106">The code sends the crop area and the URL of the larger image and returns results that include Bing Search URLs and URLs of similar images found online.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-106">The code sends the crop area and the URL of the larger image and returns results that include Bing Search URLs and URLs of similar images found online.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fbc8-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8fbc8-107">Prerequisites</span></span>

<span data-ttu-id="8fbc8-108">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to get this code running on Windows.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-108">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to get this code running on Windows.</span></span> <span data-ttu-id="8fbc8-109">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="8fbc8-109">(The free Community Edition will work.)</span></span>

<span data-ttu-id="8fbc8-110">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with Bing Search APIs.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-110">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with Bing Search APIs.</span></span> <span data-ttu-id="8fbc8-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="8fbc8-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="8fbc8-113">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="8fbc8-113">Application dependencies</span></span>
<span data-ttu-id="8fbc8-114">To set up a console application using the Bing Web Search SDK, browse to the Manage NuGet Packages option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-114">To set up a console application using the Bing Web Search SDK, browse to the Manage NuGet Packages option from the Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="8fbc8-115">Add the Microsoft.Azure.CognitiveServices.Search.VisualSearch package.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-115">Add the Microsoft.Azure.CognitiveServices.Search.VisualSearch package.</span></span>

<span data-ttu-id="8fbc8-116">Installing the NuGet Web Search SDK package also installs dependencies, including:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-116">Installing the NuGet Web Search SDK package also installs dependencies, including:</span></span>

* <span data-ttu-id="8fbc8-117">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="8fbc8-117">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="8fbc8-118">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="8fbc8-118">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="8fbc8-119">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="8fbc8-119">Newtonsoft.Json</span></span>

## <a name="image-and-crop-area"></a><span data-ttu-id="8fbc8-120">Image and crop area</span><span class="sxs-lookup"><span data-stu-id="8fbc8-120">Image and crop area</span></span>
<span data-ttu-id="8fbc8-121">The following image shows the Microsoft senior leadership team.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-121">The following image shows the Microsoft senior leadership team.</span></span>  <span data-ttu-id="8fbc8-122">Using the Visual Search SDK, we upload a crop area of the image and find other images and Web pages that include the entity in the selected area of the larger image.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-122">Using the Visual Search SDK, we upload a crop area of the image and find other images and Web pages that include the entity in the selected area of the larger image.</span></span>  <span data-ttu-id="8fbc8-123">In this case, the entity is a person.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-123">In this case, the entity is a person.</span></span>

![Microsoft Senior Leadership Team](./media/MS_SrLeaders.jpg)

## <a name="specify-the-crop-area-as-imageinfo-in-visualsearchrequest"></a><span data-ttu-id="8fbc8-125">Specify the crop area as ImageInfo in VisualSearchRequest</span><span class="sxs-lookup"><span data-stu-id="8fbc8-125">Specify the crop area as ImageInfo in VisualSearchRequest</span></span>
<span data-ttu-id="8fbc8-126">This example uses a crop area of the previous image that specifies upper left and lower right coordinates by percentage of the whole image.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-126">This example uses a crop area of the previous image that specifies upper left and lower right coordinates by percentage of the whole image.</span></span>  <span data-ttu-id="8fbc8-127">The following code creates an `ImageInfo` object from the crop area and loads the `ImageInfo` object into a `VisualSearchRequest`.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-127">The following code creates an `ImageInfo` object from the crop area and loads the `ImageInfo` object into a `VisualSearchRequest`.</span></span>  <span data-ttu-id="8fbc8-128">The `ImageInfo` object also includes the URL of the image online.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-128">The `ImageInfo` object also includes the URL of the image online.</span></span>

```
CropArea CropArea = new CropArea(top: (float)0.01, bottom: (float)0.30, left: (float)0.01, right: (float)0.20);
string imageURL = "https://docs.microsoft.com/en-us/azure/cognitive-services/bing-visual-search/media/ms_srleaders.jpg;
ImageInfo imageInfo = new ImageInfo(cropArea: CropArea, url: imageURL);

VisualSearchRequest visualSearchRequest = new VisualSearchRequest(imageInfo: imageInfo);
```
## <a name="search-for-images-similar-to-crop-area"></a><span data-ttu-id="8fbc8-129">Search for images similar to crop area</span><span class="sxs-lookup"><span data-stu-id="8fbc8-129">Search for images similar to crop area</span></span>
<span data-ttu-id="8fbc8-130">The `VisualSearchRequest` contains crop area information about the image and its URL.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-130">The `VisualSearchRequest` contains crop area information about the image and its URL.</span></span>  <span data-ttu-id="8fbc8-131">The `VisualSearchMethodAsync` method gets the results.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-131">The `VisualSearchMethodAsync` method gets the results.</span></span>
```
Console.WriteLine("\r\nSending visual search request with knowledgeRequest that contains URL and crop area");
var visualSearchResults = client.Images.VisualSearchMethodAsync(knowledgeRequest: visualSearchRequest).Result; 

```

## <a name="get-the-url-data-from-imagemoduleaction"></a><span data-ttu-id="8fbc8-132">Get the URL data from ImageModuleAction</span><span class="sxs-lookup"><span data-stu-id="8fbc8-132">Get the URL data from ImageModuleAction</span></span>
<span data-ttu-id="8fbc8-133">Visual Search results are `ImageTag` objects.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-133">Visual Search results are `ImageTag` objects.</span></span>  <span data-ttu-id="8fbc8-134">Each tag contains a list of `ImageAction` objects.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-134">Each tag contains a list of `ImageAction` objects.</span></span>  <span data-ttu-id="8fbc8-135">Each `ImageAction` contains a `Data` field which is a list of values that depend on the type of action:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-135">Each `ImageAction` contains a `Data` field which is a list of values that depend on the type of action:</span></span>

<span data-ttu-id="8fbc8-136">You can get the various types with the following code:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-136">You can get the various types with the following code:</span></span>
```
Console.WriteLine("\r\n" + "ActionType: " + i.ActionType + " -> WebSearchUrl: " + i.WebSearchUrl);

```
<span data-ttu-id="8fbc8-137">The complete application returns:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-137">The complete application returns:</span></span>

* <span data-ttu-id="8fbc8-138">ActionType: PagesIncluding WebSearchURL:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-138">ActionType: PagesIncluding WebSearchURL:</span></span>
* <span data-ttu-id="8fbc8-139">ActionType: MoreSizes WebSearchURL:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-139">ActionType: MoreSizes WebSearchURL:</span></span>
* <span data-ttu-id="8fbc8-140">ActionType: VisualSearch WebSearchURL:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-140">ActionType: VisualSearch WebSearchURL:</span></span>
* <span data-ttu-id="8fbc8-141">ActionType: ImageById WebSearchURL:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-141">ActionType: ImageById WebSearchURL:</span></span> 
* <span data-ttu-id="8fbc8-142">ActionType: RelatedSearches  WebSearchURL:</span><span class="sxs-lookup"><span data-stu-id="8fbc8-142">ActionType: RelatedSearches  WebSearchURL:</span></span>
* <span data-ttu-id="8fbc8-143">ActionType: Entity -> WebSearchUrl: https://www.bing.com/cr?IG=E40D0E1A13404994ACB073504BC937A4&CID=03DCF882D7386A442137F49BD6596BEF&rd=1&h=BvvDoRtmZ35Xc_UZE4lZx6_eg7FHgcCkigU1D98NHQo&v=1&r=https%3a%2f%2fwww.bing.com%2fsearch%3fq%3dSatya%2bNadella&p=DevEx,5380.1</span><span class="sxs-lookup"><span data-stu-id="8fbc8-143">ActionType: Entity -> WebSearchUrl: https://www.bing.com/cr?IG=E40D0E1A13404994ACB073504BC937A4&CID=03DCF882D7386A442137F49BD6596BEF&rd=1&h=BvvDoRtmZ35Xc_UZE4lZx6_eg7FHgcCkigU1D98NHQo&v=1&r=https%3a%2f%2fwww.bing.com%2fsearch%3fq%3dSatya%2bNadella&p=DevEx,5380.1</span></span>
* <span data-ttu-id="8fbc8-144">ActionType: TopicResults -> WebSearchUrl: https://www.bing.com/cr?IG=E40D0E1A13404994ACB073504BC937A4&CID=03DCF882D7386A442137F49BD6596BEF&rd=1&h=3QGtxPb3W9LemuHRxAlW4CW7XN4sPkUYCUynxAqI9zQ&v=1&r=https%3a%2f%2fwww.bing.com%2fdiscover%2fnadella%2bsatya&p=DevEx,5382.1</span><span class="sxs-lookup"><span data-stu-id="8fbc8-144">ActionType: TopicResults -> WebSearchUrl: https://www.bing.com/cr?IG=E40D0E1A13404994ACB073504BC937A4&CID=03DCF882D7386A442137F49BD6596BEF&rd=1&h=3QGtxPb3W9LemuHRxAlW4CW7XN4sPkUYCUynxAqI9zQ&v=1&r=https%3a%2f%2fwww.bing.com%2fdiscover%2fnadella%2bsatya&p=DevEx,5382.1</span></span>
* <span data-ttu-id="8fbc8-145">ActionType: ImageResults -> WebSearchUrl: https://www.bing.com/cr?IG=E40D0E1A13404994ACB073504BC937A4&CID=03DCF882D7386A442137F49BD6596BEF&rd=1&h=l-WNHO89Kkw69AmIGe2MhlUp6MxR6YsJszgOuM5sVLs&v=1&r=https%3a%2f%2fwww.bing.com%2fimages%2fsearch%3fq%3dSatya%2bNadella&p=DevEx,5384.1</span><span class="sxs-lookup"><span data-stu-id="8fbc8-145">ActionType: ImageResults -> WebSearchUrl: https://www.bing.com/cr?IG=E40D0E1A13404994ACB073504BC937A4&CID=03DCF882D7386A442137F49BD6596BEF&rd=1&h=l-WNHO89Kkw69AmIGe2MhlUp6MxR6YsJszgOuM5sVLs&v=1&r=https%3a%2f%2fwww.bing.com%2fimages%2fsearch%3fq%3dSatya%2bNadella&p=DevEx,5384.1</span></span>

<span data-ttu-id="8fbc8-146">As shown in preceding list, the `Entity` `ActionType` contains a Bing Search query that returns information about a recognizable person, place, or thing.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-146">As shown in preceding list, the `Entity` `ActionType` contains a Bing Search query that returns information about a recognizable person, place, or thing.</span></span>  <span data-ttu-id="8fbc8-147">The `TopicResults` and `ImageResults` types contain queries for related images.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-147">The `TopicResults` and `ImageResults` types contain queries for related images.</span></span> <span data-ttu-id="8fbc8-148">The URLs in the list link  to Bing search results.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-148">The URLs in the list link  to Bing search results.</span></span>


## <a name="pagesincluding-actiontype-urls-of-images-found-by-visual-search"></a><span data-ttu-id="8fbc8-149">PagesIncluding ActionType URLs of images found by Visual Search</span><span class="sxs-lookup"><span data-stu-id="8fbc8-149">PagesIncluding ActionType URLs of images found by Visual Search</span></span>

<span data-ttu-id="8fbc8-150">Getting the actual image URLs requires a cast that reads an `ActionType` as `ImageModuleAction`, which contains a `Data` element with a list of values.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-150">Getting the actual image URLs requires a cast that reads an `ActionType` as `ImageModuleAction`, which contains a `Data` element with a list of values.</span></span>  <span data-ttu-id="8fbc8-151">Each value is the URL of an image.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-151">Each value is the URL of an image.</span></span>  <span data-ttu-id="8fbc8-152">The following casts the `PagesIncluding` action type to `ImageModuleAction` and reads the values.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-152">The following casts the `PagesIncluding` action type to `ImageModuleAction` and reads the values.</span></span>
```
    if (i.ActionType == "PagesIncluding")
    {
        foreach(ImageObject o in (i as ImageModuleAction).Data.Value)
        {
            Console.WriteLine("ContentURL: " + o.ContentUrl);
        }
    }
```

## <a name="complete-code"></a><span data-ttu-id="8fbc8-153">Complete code</span><span class="sxs-lookup"><span data-stu-id="8fbc8-153">Complete code</span></span>

<span data-ttu-id="8fbc8-154">The following code runs previous examples.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-154">The following code runs previous examples.</span></span> <span data-ttu-id="8fbc8-155">It sends an image binary in the body of the post request, along with a cropArea object, and prints out the Bing search URLs for each ActionType.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-155">It sends an image binary in the body of the post request, along with a cropArea object, and prints out the Bing search URLs for each ActionType.</span></span> <span data-ttu-id="8fbc8-156">If the ActionType is PagesIncluding, the code gets the ImageObject items in ImageObject Data.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-156">If the ActionType is PagesIncluding, the code gets the ImageObject items in ImageObject Data.</span></span>  <span data-ttu-id="8fbc8-157">The Data contains a list of values, which are the URLs of images on Web pages.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-157">The Data contains a list of values, which are the URLs of images on Web pages.</span></span>  <span data-ttu-id="8fbc8-158">Copy and paste resulting Visual Search URLs to browser to show results.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-158">Copy and paste resulting Visual Search URLs to browser to show results.</span></span> <span data-ttu-id="8fbc8-159">Copy and paste ContentUrl items to browser to show images.</span><span class="sxs-lookup"><span data-stu-id="8fbc8-159">Copy and paste ContentUrl items to browser to show images.</span></span>

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

            VisualSearchImageBinaryWithCropArea(subscriptionKey);

            Console.WriteLine("Any key to quit...");
            Console.ReadKey();

        }

        public static void VisualSearchImageBinaryWithCropArea(string subscriptionKey)
        {
            var client = new VisualSearchAPI(new Microsoft.Azure.CognitiveServices.Search.VisualSearch.ApiKeyServiceClientCredentials(subscriptionKey));

            try
            {
                CropArea CropArea = new CropArea(top: (float)0.01, bottom: (float)0.30, left: (float)0.01, right: (float)0.20);
                
                // The ImageInfo struct specifies the crop area in the image and the URL of the larger image. 
                string imageURL = "https://docs.microsoft.com/en-us/azure/cognitive-services/bing-visual-search/media/ms_srleaders.jpg";
                ImageInfo imageInfo = new ImageInfo(cropArea: CropArea, url: imageURL);
                
                VisualSearchRequest visualSearchRequest = new VisualSearchRequest(imageInfo: imageInfo);

                var visualSearchResults = client.Images.VisualSearchMethodAsync(knowledgeRequest: visualSearchRequest).Result; 

                Console.WriteLine("\r\nVisual search request with image from URL and crop area combined in knowledgeRequest");

                if (visualSearchResults == null)
                {
                    Console.WriteLine("No visual search result data.");
                }
                else
                {
                    // List of tags
                    if (visualSearchResults.Tags.Count > 0)
                    {

                        foreach(ImageTag t in visualSearchResults.Tags)
                        {
                            foreach (ImageAction i in t.Actions)
                            { 
                                Console.WriteLine("\r\n" + "ActionType: " + i.ActionType + " -> WebSearchUrl: " + i.WebSearchUrl);

                                if (i.ActionType == "PagesIncluding")
                                {
                                    foreach(ImageObject o in (i as ImageModuleAction).Data.Value)
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
## <a name="next-steps"></a><span data-ttu-id="8fbc8-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fbc8-160">Next steps</span></span>
[<span data-ttu-id="8fbc8-161">Visual Search response</span><span class="sxs-lookup"><span data-stu-id="8fbc8-161">Visual Search response</span></span>](https://docs.microsoft.com/en-us/azure/cognitive-services/bing-visual-search/overview#the-response)