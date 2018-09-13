---
title: Get image insights | Microsoft Docs
titleSuffix: Bing Web Search APIs - Cognitive Services
description: Shows how to use the Bing Image Search API to get more information about an image.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 0BCD936E-D4C0-472D-AE40-F4B2AB6912D5
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: f651d9f773f475e633aed698e134aa6a7c07393b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870618"
---
# <a name="get-insights-about-an-image"></a><span data-ttu-id="e53f4-103">Get insights about an image</span><span class="sxs-lookup"><span data-stu-id="e53f4-103">Get insights about an image</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e53f4-104">Instead of using the /images/details endpoint to get image insights, you should use [Visual Search](../bing-visual-search/overview.md) since it provides more comprehensive insights.</span><span class="sxs-lookup"><span data-stu-id="e53f4-104">Instead of using the /images/details endpoint to get image insights, you should use [Visual Search](../bing-visual-search/overview.md) since it provides more comprehensive insights.</span></span>


<span data-ttu-id="e53f4-105">Each image includes an insights token that you can use to get information about the image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-105">Each image includes an insights token that you can use to get information about the image.</span></span> <span data-ttu-id="e53f4-106">For example, you can get a collection of related images, web pages that include the image, or a list of merchants where you can buy the product shown in the image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-106">For example, you can get a collection of related images, web pages that include the image, or a list of merchants where you can buy the product shown in the image.</span></span>  
  
<span data-ttu-id="e53f4-107">To get insights about an image, capture the image's [imageInsightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image-imageinsightstoken) token in the response.</span><span class="sxs-lookup"><span data-stu-id="e53f4-107">To get insights about an image, capture the image's [imageInsightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image-imageinsightstoken) token in the response.</span></span> 

```json
"value" : [{
        . . .
        "name":"sailing dinghy.jpg",
        "imageInsightsToken" : "mid_D6426898706EC7..."
        "insightsSourcesSummary" : {
            "shoppingSourcesCount" : 9,
            "recipeSourcesCount" : 0
        },
        . . .
}],
```

<span data-ttu-id="e53f4-108">Next, call the Image Details endpoint and set the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) query parameter to the token in `imageInsightsToken`.</span><span class="sxs-lookup"><span data-stu-id="e53f4-108">Next, call the Image Details endpoint and set the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) query parameter to the token in `imageInsightsToken`.</span></span>  

<span data-ttu-id="e53f4-109">To specify the insights that you want to get, set the `modules` query parameter.</span><span class="sxs-lookup"><span data-stu-id="e53f4-109">To specify the insights that you want to get, set the `modules` query parameter.</span></span> <span data-ttu-id="e53f4-110">To get all insights, set `modules` to `All`.</span><span class="sxs-lookup"><span data-stu-id="e53f4-110">To get all insights, set `modules` to `All`.</span></span> <span data-ttu-id="e53f4-111">To get only the caption and collection insights, set `modules` to `Caption%2CCollection`.</span><span class="sxs-lookup"><span data-stu-id="e53f4-111">To get only the caption and collection insights, set `modules` to `Caption%2CCollection`.</span></span> <span data-ttu-id="e53f4-112">For a complete list of possible insights, see [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested).</span><span class="sxs-lookup"><span data-stu-id="e53f4-112">For a complete list of possible insights, see [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested).</span></span> <span data-ttu-id="e53f4-113">Not all insights are available for all images.</span><span class="sxs-lookup"><span data-stu-id="e53f4-113">Not all insights are available for all images.</span></span> <span data-ttu-id="e53f4-114">The response includes all insights that you requested, if available.</span><span class="sxs-lookup"><span data-stu-id="e53f4-114">The response includes all insights that you requested, if available.</span></span>

<span data-ttu-id="e53f4-115">The following example requests all available insights for the preceding image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-115">The following example requests all available insights for the preceding image.</span></span>

```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?q=sailing+dinghy&insightsToken=mid_D6426898706EC7...&modules=All&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
``` 

## <a name="getting-insights-of-a-known-image"></a><span data-ttu-id="e53f4-116">Getting insights of a known image</span><span class="sxs-lookup"><span data-stu-id="e53f4-116">Getting insights of a known image</span></span>

<span data-ttu-id="e53f4-117">If you have the URL to an image that you want to get insights of, use the [imgUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imgurl) query parameter instead of the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) parameter to specify the image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-117">If you have the URL to an image that you want to get insights of, use the [imgUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imgurl) query parameter instead of the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) parameter to specify the image.</span></span> <span data-ttu-id="e53f4-118">Or, if you have the image file, you may send the binary of the image in the body of a POST request.</span><span class="sxs-lookup"><span data-stu-id="e53f4-118">Or, if you have the image file, you may send the binary of the image in the body of a POST request.</span></span> <span data-ttu-id="e53f4-119">If you use a POST request, the `Content-Type` header must be set to `multipart/data-form`.</span><span class="sxs-lookup"><span data-stu-id="e53f4-119">If you use a POST request, the `Content-Type` header must be set to `multipart/data-form`.</span></span> <span data-ttu-id="e53f4-120">With either option, the size of the image may not exceed 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e53f4-120">With either option, the size of the image may not exceed 1 MB.</span></span>  
  
<span data-ttu-id="e53f4-121">If you have a URL to the image, the following example shows how to request insights of an image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-121">If you have a URL to the image, the following example shows how to request insights of an image.</span></span>

```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?q=sailing+dinghy&imgUrl=https%3A%2F%2Fwww.mydomain.com%2Fimages%2Fsunflower.png&modules=All&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
``` 
  
## <a name="getting-all-image-insights"></a><span data-ttu-id="e53f4-122">Getting all image insights</span><span class="sxs-lookup"><span data-stu-id="e53f4-122">Getting all image insights</span></span>  

<span data-ttu-id="e53f4-123">To request all insights of an image, set the [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) query parameter to `All`.</span><span class="sxs-lookup"><span data-stu-id="e53f4-123">To request all insights of an image, set the [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) query parameter to `All`.</span></span> <span data-ttu-id="e53f4-124">To get related searches, the request must include the user's query string.</span><span class="sxs-lookup"><span data-stu-id="e53f4-124">To get related searches, the request must include the user's query string.</span></span> <span data-ttu-id="e53f4-125">This example shows using the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) to specify the image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-125">This example shows using the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) to specify the image.</span></span>  
  
```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?q=sailing+dinghy&insightsToken=mid_68364D764J...&modules=All&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="e53f4-126">The top-level object is an [ImageInsightsResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imageinsightsresponse) object instead of an [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) object.</span><span class="sxs-lookup"><span data-stu-id="e53f4-126">The top-level object is an [ImageInsightsResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imageinsightsresponse) object instead of an [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) object.</span></span>  
  
```json
{
    "_type" : "ImageInsights",
    "imageInsightsToken" : "bcid_3297E6A54E4787A5F51C49D9BA342B9A*ccid_Fe2Hx...",
    "bestRepresentativeQuery" : {
        "text" : "Sailing Dinghy",
        "displayText" : "Sailing Dinghy",
        "webSearchUrl" : "https:\/\/www.bing.com\/images\/search?q=Sailing+Dinghy...",
    },
    "pagesIncluding" : {
        "value" : [
            {
                "webSearchUrl" : "https:\/\/www.bing.com\/images\/search?view=...",
                "name" : "Powerboating Dublin, Dinghy Sailing Courses...",
                "thumbnailUrl" : "https:\/\/tse1.mm.bing.net\/th?id=OIP....",
                "datePublished" : "2017-01-20T00:41:00.0000000Z",
                "contentUrl" : "http:\/\/www.contoso.ie\/content...",
                "hostPageUrl" : "http:\/\/www.contoso.ie\/powerboating...",
                "contentSize" : "59063 B",
                "encodingFormat" : "jpeg",
                "hostPageDisplayUrl" : "www.contoso.ie\/powerboating...",
                "width" : 800,
                "height" : 600,
                "thumbnail" : {
                    "width" : 300,
                    "height" : 225
                },
                "imageInsightsToken" : "ccid_pHjQIA0x*mid_17F61B1316A39C92214...",
                "imageId" : "17F61B1316A39C922143FFDE9DFB5B0FB41171",
                "accentColor" : "0997C2"
            },
            . . .
        ]
    },
    "relatedSearches" : {
        "value" : [
            {
                "text" : "Sailing Fun",
                "displayText" : "Sailing Fun",
                "webSearchUrl" : "https:\/\/www.bing.com\/images\/search?q=Sailing...",
                "thumbnail" : {
                    "url" : "https:\/\/tse1.mm.bing.net\/th?q=Sailing+Fun..."
                }
            },
            . . .
        ]
    },
    "visuallySimilarImages" : {
        "value" : [
            {
                "webSearchUrl" : "https:\/\/www.bing.com\/images\/search?view=...",
                "name" : "Weekend On the Water",
                "thumbnailUrl" : "https:\/\/tse2.mm.bing.net\/th?id=OIP...",
                "datePublished" : "2010-09-05T12:00:00.0000000Z",
                "contentUrl" : "http:\/\/1.bp.contoso.com\/_dc_6...",
                "hostPageUrl" : "http:\/\/contoso.com\/2010...",
                "contentSize" : "203806 B",
                "encodingFormat" : "jpeg",
                "hostPageDisplayUrl" : "contoso.com\/2010...",
                "width" : 1600,
                "height" : 1249,
                "thumbnail" : {
                    "width" : 300,
                    "height" : 234
                },
                "imageInsightsToken" : "ccid_Jg1Kwuc4*mid_5B7DA43976D3A422...",
                "imageId" : "5B7DA43976D3A422BA679A3AB019BB52C08DBC",
                "accentColor" : "0B2543"
            },
            . . .
        ]
    },
    "imageTags" : {
        "value" : [
            {
                "name" : "sail boat"
            },
            . . .
        ]
    }
}
```

## <a name="recognizing-entities-in-an-image"></a><span data-ttu-id="e53f4-127">Recognizing entities in an image</span><span class="sxs-lookup"><span data-stu-id="e53f4-127">Recognizing entities in an image</span></span>  

<span data-ttu-id="e53f4-128">The entity recognition feature identifies entities in an image, currently only people.</span><span class="sxs-lookup"><span data-stu-id="e53f4-128">The entity recognition feature identifies entities in an image, currently only people.</span></span> <span data-ttu-id="e53f4-129">To identify entities in an image, set the [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) query parameter to `RecognizedEntities`.</span><span class="sxs-lookup"><span data-stu-id="e53f4-129">To identify entities in an image, set the [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) query parameter to `RecognizedEntities`.</span></span>  

> [!NOTE]
> <span data-ttu-id="e53f4-130">You may not specify this module with any other module.</span><span class="sxs-lookup"><span data-stu-id="e53f4-130">You may not specify this module with any other module.</span></span> <span data-ttu-id="e53f4-131">If you specify this module with other modules, the response does not include recognized entities.</span><span class="sxs-lookup"><span data-stu-id="e53f4-131">If you specify this module with other modules, the response does not include recognized entities.</span></span>  
  
<span data-ttu-id="e53f4-132">The following shows how to specify the image by using the [imgUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imgurl) parameter.</span><span class="sxs-lookup"><span data-stu-id="e53f4-132">The following shows how to specify the image by using the [imgUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imgurl) parameter.</span></span> <span data-ttu-id="e53f4-133">Remember to URL encode the query parameters.</span><span class="sxs-lookup"><span data-stu-id="e53f4-133">Remember to URL encode the query parameters.</span></span>  
  
```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?q=faith+hill&insightsToken=mid_68364D764J...&modules=RecognizedEntities&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
```  
  
<span data-ttu-id="e53f4-134">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="e53f4-134">The following shows the response to the previous request.</span></span> <span data-ttu-id="e53f4-135">Because the image contains two people, the response identifies a region for each person.</span><span class="sxs-lookup"><span data-stu-id="e53f4-135">Because the image contains two people, the response identifies a region for each person.</span></span> <span data-ttu-id="e53f4-136">In this case, the people were recognized in the CelebrityAnnotations and CelebRecognitionAnnotations groups.</span><span class="sxs-lookup"><span data-stu-id="e53f4-136">In this case, the people were recognized in the CelebrityAnnotations and CelebRecognitionAnnotations groups.</span></span> <span data-ttu-id="e53f4-137">Bing lists the people in each group based on the likelihood that they match the person in the original image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-137">Bing lists the people in each group based on the likelihood that they match the person in the original image.</span></span> <span data-ttu-id="e53f4-138">The list is in descending order of confidence.</span><span class="sxs-lookup"><span data-stu-id="e53f4-138">The list is in descending order of confidence.</span></span> <span data-ttu-id="e53f4-139">The CelebRecognitionAnnotations group provides the highest level of confidence that the match is correct.</span><span class="sxs-lookup"><span data-stu-id="e53f4-139">The CelebRecognitionAnnotations group provides the highest level of confidence that the match is correct.</span></span>  
  
```json
{
    "_type" : "ImageInsights",
    "imageInsightsToken" : "ccid_ldi5nX38*mid_29470780DE0E6F969...",
    "recognizedEntityGroups" : {
        "value" : [
            {
                "recognizedEntityRegions" : [...],
                "name" : "CelebRecognitionAnnotations"
            },
            {
                "recognizedEntityRegions" : [...],
                "name" : "CelebrityAnnotations"
            }
        ]
    }
}
```
  
<span data-ttu-id="e53f4-140">The `region` field identifies the area of the image where Bing recognized the entity.</span><span class="sxs-lookup"><span data-stu-id="e53f4-140">The `region` field identifies the area of the image where Bing recognized the entity.</span></span> <span data-ttu-id="e53f4-141">For people, the region represents the person's face.</span><span class="sxs-lookup"><span data-stu-id="e53f4-141">For people, the region represents the person's face.</span></span>  
  
<span data-ttu-id="e53f4-142">The values of the rectangle are relative to the width and height of the original image and are in the range 0.0 through 1.0.</span><span class="sxs-lookup"><span data-stu-id="e53f4-142">The values of the rectangle are relative to the width and height of the original image and are in the range 0.0 through 1.0.</span></span> <span data-ttu-id="e53f4-143">For example, if the image is 300x200, and the region's top, left corner is at point (10, 20) and the bottom, right corner is at point (290, 150), then the normalized rectangle is:</span><span class="sxs-lookup"><span data-stu-id="e53f4-143">For example, if the image is 300x200, and the region's top, left corner is at point (10, 20) and the bottom, right corner is at point (290, 150), then the normalized rectangle is:</span></span>  
  
-   <span data-ttu-id="e53f4-144">Left: 10 / 300 = 0.03333...</span><span class="sxs-lookup"><span data-stu-id="e53f4-144">Left: 10 / 300 = 0.03333...</span></span>  
-   <span data-ttu-id="e53f4-145">Top:  20 / 200 = 0.1</span><span class="sxs-lookup"><span data-stu-id="e53f4-145">Top:  20 / 200 = 0.1</span></span>  
-   <span data-ttu-id="e53f4-146">Right: 290 / 300 = 0.9667...</span><span class="sxs-lookup"><span data-stu-id="e53f4-146">Right: 290 / 300 = 0.9667...</span></span>  
-   <span data-ttu-id="e53f4-147">Bottom: 150 / 200 = 0.75</span><span class="sxs-lookup"><span data-stu-id="e53f4-147">Bottom: 150 / 200 = 0.75</span></span>  
  
<span data-ttu-id="e53f4-148">You can use the region that Bing returns in subsequent insights calls.</span><span class="sxs-lookup"><span data-stu-id="e53f4-148">You can use the region that Bing returns in subsequent insights calls.</span></span> <span data-ttu-id="e53f4-149">For example, to get visually similar images of the recognized entity.</span><span class="sxs-lookup"><span data-stu-id="e53f4-149">For example, to get visually similar images of the recognized entity.</span></span> <span data-ttu-id="e53f4-150">For more information, see [Cropping Images to use with Visually Similar and Entity Recognition Modules](#croppingimages).</span><span class="sxs-lookup"><span data-stu-id="e53f4-150">For more information, see [Cropping Images to use with Visually Similar and Entity Recognition Modules](#croppingimages).</span></span> <span data-ttu-id="e53f4-151">The following shows the mapping between the region fields and the query parameters that you'd use to crop images.</span><span class="sxs-lookup"><span data-stu-id="e53f4-151">The following shows the mapping between the region fields and the query parameters that you'd use to crop images.</span></span>  
  
-   <span data-ttu-id="e53f4-152">Left maps to [cal](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cal)</span><span class="sxs-lookup"><span data-stu-id="e53f4-152">Left maps to [cal](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cal)</span></span>  
-   <span data-ttu-id="e53f4-153">Top maps to [cat](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cat)</span><span class="sxs-lookup"><span data-stu-id="e53f4-153">Top maps to [cat](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cat)</span></span>  
-   <span data-ttu-id="e53f4-154">Right maps to [car](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#car)</span><span class="sxs-lookup"><span data-stu-id="e53f4-154">Right maps to [car](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#car)</span></span>  
-   <span data-ttu-id="e53f4-155">Bottom maps to [cab](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cab)</span><span class="sxs-lookup"><span data-stu-id="e53f4-155">Bottom maps to [cab](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cab)</span></span>  

## <a name="finding-visually-similar-images"></a><span data-ttu-id="e53f4-156">Finding visually similar images</span><span class="sxs-lookup"><span data-stu-id="e53f4-156">Finding visually similar images</span></span>  

<span data-ttu-id="e53f4-157">To find images that are visually similar to the original image, set the [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) query parameter to SimilarImages.</span><span class="sxs-lookup"><span data-stu-id="e53f4-157">To find images that are visually similar to the original image, set the [modules](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) query parameter to SimilarImages.</span></span>  
  
<span data-ttu-id="e53f4-158">The following request shows how to get visually similar images.</span><span class="sxs-lookup"><span data-stu-id="e53f4-158">The following request shows how to get visually similar images.</span></span> <span data-ttu-id="e53f4-159">The request uses the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) query parameter to identify the original image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-159">The request uses the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) query parameter to identify the original image.</span></span> <span data-ttu-id="e53f4-160">To improve relevance, you should include the user's query string.</span><span class="sxs-lookup"><span data-stu-id="e53f4-160">To improve relevance, you should include the user's query string.</span></span>  
  
```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?insightsToken=mid_68364D764J...&modules=SimilarImages&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
```

  
<span data-ttu-id="e53f4-161">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="e53f4-161">The following shows the response to the previous request.</span></span>  
  
```json
{
    "_type" : "ImageInsights",
    "imageInsightsToken" : "ccid_ldi5nX38*mid_29470780DE0E6F969...",
    "visuallySimilarImages" : {
        "value" : [
            {
                "name" : "typical Hawaiian Sunset! :) | Scenes of Hawaii",
                "webSearchUrl" : "https:\/\/www.bing.com\/images\/search?view=detailv2...",
                "thumbnailUrl" : "https:\/\/tse1.mm.bing.net\/th?id=OIP.Mda2a86...",
                 . . .
            }
        ]
    }
```
  
## <a name="cropping-images-to-use-with-visually-similar-and-entity-recognition-modules"></a><span data-ttu-id="e53f4-162">Cropping images to use with visually similar and entity recognition modules</span><span class="sxs-lookup"><span data-stu-id="e53f4-162">Cropping images to use with visually similar and entity recognition modules</span></span>  

<span data-ttu-id="e53f4-163">To specify the region of the image that Bing uses to determine whether images are visually similar or to perform entity recognition, use the [cal](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cal), [cat](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cat), [cab](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cab), and [car](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#car) query parameters.</span><span class="sxs-lookup"><span data-stu-id="e53f4-163">To specify the region of the image that Bing uses to determine whether images are visually similar or to perform entity recognition, use the [cal](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cal), [cat](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cat), [cab](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#cab), and [car](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#car) query parameters.</span></span> <span data-ttu-id="e53f4-164">By default, Bing uses the entire image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-164">By default, Bing uses the entire image.</span></span>  
  
<span data-ttu-id="e53f4-165">The parameters specify the top, left corner and bottom, right corner of the region that Bing uses for comparison.</span><span class="sxs-lookup"><span data-stu-id="e53f4-165">The parameters specify the top, left corner and bottom, right corner of the region that Bing uses for comparison.</span></span> <span data-ttu-id="e53f4-166">Specify the values as fractions of the original image's width and height.</span><span class="sxs-lookup"><span data-stu-id="e53f4-166">Specify the values as fractions of the original image's width and height.</span></span> <span data-ttu-id="e53f4-167">The fractional values start with (0.0, 0.0) at the top, left corner and end with (1.0, 1.0) at the bottom right corner.</span><span class="sxs-lookup"><span data-stu-id="e53f4-167">The fractional values start with (0.0, 0.0) at the top, left corner and end with (1.0, 1.0) at the bottom right corner.</span></span> <span data-ttu-id="e53f4-168">For example, to specify that the top, left corner starts a quarter of the way down from the top and a quarter of the way in from the left side, set `cal` to 0.25 and `cat` 0.25.</span><span class="sxs-lookup"><span data-stu-id="e53f4-168">For example, to specify that the top, left corner starts a quarter of the way down from the top and a quarter of the way in from the left side, set `cal` to 0.25 and `cat` 0.25.</span></span>  
  
<span data-ttu-id="e53f4-169">The following sequence of calls shows the effect of specifying the cropping region.</span><span class="sxs-lookup"><span data-stu-id="e53f4-169">The following sequence of calls shows the effect of specifying the cropping region.</span></span> <span data-ttu-id="e53f4-170">The first call does not include cropping and Bing recognizes two people standing side by side in the middle of the image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-170">The first call does not include cropping and Bing recognizes two people standing side by side in the middle of the image.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?modules=RecognizedEntities&imgurl=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOIP.M0cbee6fadb43f35b2344e53da7a23ec1o0%26pid%3DApi&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
```  

<span data-ttu-id="e53f4-171">The response shows two recognized entities.</span><span class="sxs-lookup"><span data-stu-id="e53f4-171">The response shows two recognized entities.</span></span>  
  
```json 
{  
    "_type" : "ImageInsights",  
    "recognizedEntityGroups" : {
        "value": [  
            . . .  
            {  
                "recognizedEntityRegions" : [{  
                    "region" : {  
                        "left" : 0.5066667,  
                        "top" : 0.1955556,  
                        "right" : 0.75,  
                        "bottom" : 0.52  
                    },  
                    "matchingEntities" : [{  
                        "entity" : {  
                            "_type" : "Person",  
                            "name" : "Charlene Whitney",  
                            . . .  
                        },  
                        "matchConfidence" : 0.9961388  
                    }]  
                },  
                {  
                    "region" : {  
                        "left" : 0.25,  
                        "top" : 0.2488889,  
                        "right" : 0.4466667,  
                        "bottom" : 0.5111111  
                    },  
                    "matchingEntities" : [{  
                        "entity" : {  
                            "_type" : "Person",  
                            "name" : "Marcus Appel",  
                            . . .  
                        },  
                        "matchConfidence" : 0.9961388  
                    }]  
                }],  
            "name" : "CelebRecognitionAnnotations"
        }]
    }  
}  
```  
  
<span data-ttu-id="e53f4-172">The second call crops the image vertically down the middle and Bing recognized a single person on the right side of the image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-172">The second call crops the image vertically down the middle and Bing recognized a single person on the right side of the image.</span></span>  
  
```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?cal=0.5&cat=0.0&car=1.0&cab=1.0&modules=RecognizedEntities&imgurl=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOIP.M0cbee6fadb43f35b2344e53da7a23ec1o0%26pid%3DApi&mkt=en-us HTTP/1.1    
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="e53f4-173">The response shows one recognized entity.</span><span class="sxs-lookup"><span data-stu-id="e53f4-173">The response shows one recognized entity.</span></span>  
  
```json  
{  
    "_type" : "ImageInsights",  
    "recognizedEntityGroups" : {
        "value" : [  
            . . .  
            {  
                "recognizedEntityRegions" : [{  
                    "region" : {  
                        "left" : 0.5066667,  
                        "top" : 0.1955556,  
                        "right" : 0.75,  
                        "bottom" : 0.52  
                    },  
                    "matchingEntities" : [{  
                        "entity" : {  
                            "_type" : "Person",  
                            "name" : "Charlene Whitney",  
                            . . .  
                        },  
                        "matchConfidence" : 0.9961388  
                    }]  
                }],  
                "name" : "CelebRecognitionAnnotations"  
            }
        ]
    }
}  
```  
  
## <a name="finding-visually-similar-products"></a><span data-ttu-id="e53f4-174">Finding visually similar products</span><span class="sxs-lookup"><span data-stu-id="e53f4-174">Finding visually similar products</span></span>  

<span data-ttu-id="e53f4-175">To find images that contain products that are visually similar to the products found in the original image, set the [modueles](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) query parameter to SimilarProducts.</span><span class="sxs-lookup"><span data-stu-id="e53f4-175">To find images that contain products that are visually similar to the products found in the original image, set the [modueles](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#modulesrequested) query parameter to SimilarProducts.</span></span>  
  
<span data-ttu-id="e53f4-176">The following request shows how to get images of visually similar products.</span><span class="sxs-lookup"><span data-stu-id="e53f4-176">The following request shows how to get images of visually similar products.</span></span> <span data-ttu-id="e53f4-177">The request uses the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) query parameter to identify the original image that was returned in a previous request.</span><span class="sxs-lookup"><span data-stu-id="e53f4-177">The request uses the [insightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#insightstoken) query parameter to identify the original image that was returned in a previous request.</span></span> <span data-ttu-id="e53f4-178">To improve relevance, you should include the user's query string.</span><span class="sxs-lookup"><span data-stu-id="e53f4-178">To improve relevance, you should include the user's query string.</span></span>  
  
```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?q=anne+klein+dresses&modules=SimilarProducts&insightsToken=ccid_WOeyfoSp*mid_4B0A357&mkt=en-us HTTP/1.1    
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
```
  
<span data-ttu-id="e53f4-179">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="e53f4-179">The following shows the response to the previous request.</span></span> <span data-ttu-id="e53f4-180">The response contains an image of a similar product and indicates how many merchants offer the product online, whether there are product ratings, and the lowest price found (see the `aggregateOffer` field).</span><span class="sxs-lookup"><span data-stu-id="e53f4-180">The response contains an image of a similar product and indicates how many merchants offer the product online, whether there are product ratings, and the lowest price found (see the `aggregateOffer` field).</span></span>  
  
```json
{
    "_type" : "ImageInsights",
    "imageInsightsToken" : "ccid_ldi5nX38*mid_29470780DE0E6F969...",
    "visuallySimilarProducts" : {
        "value" : [
            {
                "name" : "Sequin One-Shoulder Twist-Drape Dress",  
                "webSearchUrl" : "https:\/\/www.bing.com\/images\/search?view=de...",  
                "thumbnailUrl" : "https:\/\/tse2.mm.bing.net\/th?id=OIP.M85bdee...",  
                . . .
            },
            . . .
        ]
    }
}
```
  
<span data-ttu-id="e53f4-181">To get a list of the merchants that offer the product online (see the [offerCount](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#offer-offercount) field), call the API again and set `modules` to ShoppingSources.</span><span class="sxs-lookup"><span data-stu-id="e53f4-181">To get a list of the merchants that offer the product online (see the [offerCount](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#offer-offercount) field), call the API again and set `modules` to ShoppingSources.</span></span> <span data-ttu-id="e53f4-182">Then, set the `insightsToken` query parameter to the token found in the product summary image.</span><span class="sxs-lookup"><span data-stu-id="e53f4-182">Then, set the `insightsToken` query parameter to the token found in the product summary image.</span></span>  
  
```
GET https://api.cognitive.microsoft.com/bing/v7.0/images/details?modules=ShoppingSources&insightsToken=ccid_hb3uRvUk*mid_BF5C252A47F2C765...&mkt=en-us HTTP/1.1    
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="e53f4-183">The following is the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="e53f4-183">The following is the response to the previous request.</span></span>  
  
```json  
{  
    "_type" : "ImageInsights",  
    "shoppingSources" : {  
        "offers" : [{  
            "url" : "http:\/\/www.contoso.com\/dp\/B00O...",  
            "seller" : {  
                "name" : "Contoso",  
                "image" : {  
                    "url" : "https:\/\/tse3.mm.bing.net\/th?id=A10d50fe..."  
                }  
            },  
            "price" : 126.87,  
            "priceCurrency" : "USD",  
            "availability" : "InStock"  
        },  
        {  
            "url" : "http:\/\/www.adatum.com\/product\/heritage...\/",  
            "seller" : {  
                "name" : "fabrikam.com"  
            },  
            "price" : 495,  
            "priceCurrency" : "USD",  
            "availability" : "InStock"  
        }]  
    }  
}  
```
