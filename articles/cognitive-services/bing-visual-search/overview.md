---
title: Bing Visual Search API overview | Microsoft Docs
titleSuffix: Bing Web Search APIs - Cognitive Services
description: Shows how to get details or insights about an image such as similar images or shopping sources.
services: cognitive-services
author: swhite-msft
manager: rosh
ms.service: cognitive-services
ms.technology: bing-visual-search
ms.topic: article
ms.date: 04/10/2018
ms.author: scottwhi
ms.openlocfilehash: aa563d89b1834f5be952f13c31a2451d809709b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967431"
---
# <a name="what-is-bing-visual-search-api"></a><span data-ttu-id="1b338-103">What is Bing Visual Search API?</span><span class="sxs-lookup"><span data-stu-id="1b338-103">What is Bing Visual Search API?</span></span>

<span data-ttu-id="1b338-104">Bing Visual Search API provides an experience similar to the image details shown on Bing.com/images.</span><span class="sxs-lookup"><span data-stu-id="1b338-104">Bing Visual Search API provides an experience similar to the image details shown on Bing.com/images.</span></span> <span data-ttu-id="1b338-105">With Visual Search, you can upload a picture and get back insights about the image such as visually similar images, shopping sources, webpages that include the image, and more.</span><span class="sxs-lookup"><span data-stu-id="1b338-105">With Visual Search, you can upload a picture and get back insights about the image such as visually similar images, shopping sources, webpages that include the image, and more.</span></span> <span data-ttu-id="1b338-106">Instead of uploading an image, you can also provide an insights token that you get from an image in the images search results (see [Bing Images API](../bing-image-search/overview.md)).</span><span class="sxs-lookup"><span data-stu-id="1b338-106">Instead of uploading an image, you can also provide an insights token that you get from an image in the images search results (see [Bing Images API](../bing-image-search/overview.md)).</span></span>

<span data-ttu-id="1b338-107">Visual Search can identify celebrities, monuments and landmarks, artwork, home furnishings, fashion, products, character recognition (OCR), and more.</span><span class="sxs-lookup"><span data-stu-id="1b338-107">Visual Search can identify celebrities, monuments and landmarks, artwork, home furnishings, fashion, products, character recognition (OCR), and more.</span></span>

<span data-ttu-id="1b338-108">The following are the insights that Visual Search lets you discover.</span><span class="sxs-lookup"><span data-stu-id="1b338-108">The following are the insights that Visual Search lets you discover.</span></span>

- <span data-ttu-id="1b338-109">Visually similar images&mdash;A list of images that are visually similar to the input image</span><span class="sxs-lookup"><span data-stu-id="1b338-109">Visually similar images&mdash;A list of images that are visually similar to the input image</span></span>
- <span data-ttu-id="1b338-110">Visually similar products&mdash;A list of images that contain products that are visually similar to the product shown in the input image</span><span class="sxs-lookup"><span data-stu-id="1b338-110">Visually similar products&mdash;A list of images that contain products that are visually similar to the product shown in the input image</span></span>
- <span data-ttu-id="1b338-111">Shopping sources&mdash;A list of places where you can buy the item shown in the input image</span><span class="sxs-lookup"><span data-stu-id="1b338-111">Shopping sources&mdash;A list of places where you can buy the item shown in the input image</span></span>
- <span data-ttu-id="1b338-112">Related searches&mdash;A list of related searches made by others or that are based on the contents of the image</span><span class="sxs-lookup"><span data-stu-id="1b338-112">Related searches&mdash;A list of related searches made by others or that are based on the contents of the image</span></span>
- <span data-ttu-id="1b338-113">Web pages that include the image&mdash;A list of webpages that include the input image</span><span class="sxs-lookup"><span data-stu-id="1b338-113">Web pages that include the image&mdash;A list of webpages that include the input image</span></span>
- <span data-ttu-id="1b338-114">Recipes&mdash;A list of webpages that include recipes for making the dish shown in the input image</span><span class="sxs-lookup"><span data-stu-id="1b338-114">Recipes&mdash;A list of webpages that include recipes for making the dish shown in the input image</span></span>

<span data-ttu-id="1b338-115">In addition to these insights, Visual Search also returns a diverse set of terms (tags) derived from the input image.</span><span class="sxs-lookup"><span data-stu-id="1b338-115">In addition to these insights, Visual Search also returns a diverse set of terms (tags) derived from the input image.</span></span> <span data-ttu-id="1b338-116">These tags allow users to explore concepts found in the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-116">These tags allow users to explore concepts found in the image.</span></span> <span data-ttu-id="1b338-117">For example, if the input image is of a famous athlete, one of the tags could be the name of the athlete, another tag could be Sports.</span><span class="sxs-lookup"><span data-stu-id="1b338-117">For example, if the input image is of a famous athlete, one of the tags could be the name of the athlete, another tag could be Sports.</span></span> <span data-ttu-id="1b338-118">Or, if the input image is of an apple pie, the tags could be Apple Pie, Pies, Desserts, so users can explore related concepts.</span><span class="sxs-lookup"><span data-stu-id="1b338-118">Or, if the input image is of an apple pie, the tags could be Apple Pie, Pies, Desserts, so users can explore related concepts.</span></span>

<span data-ttu-id="1b338-119">The Visual Search results also include bounding boxes for regions of interest in the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-119">The Visual Search results also include bounding boxes for regions of interest in the image.</span></span> <span data-ttu-id="1b338-120">For example, if the image contains several celebrities, the results may include bounding boxes for each of the recognized celebrities in the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-120">For example, if the image contains several celebrities, the results may include bounding boxes for each of the recognized celebrities in the image.</span></span> <span data-ttu-id="1b338-121">Or, if Bing recognizes a product or clothing in the image, the result may include a bounding box for the recognized product or clothing item.</span><span class="sxs-lookup"><span data-stu-id="1b338-121">Or, if Bing recognizes a product or clothing in the image, the result may include a bounding box for the recognized product or clothing item.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b338-122">If you use the /images/details endpoint to [get image insights](../bing-image-search/image-insights.md), you should update your code to use Visual Search instead since it provides more comprehensive insights.</span><span class="sxs-lookup"><span data-stu-id="1b338-122">If you use the /images/details endpoint to [get image insights](../bing-image-search/image-insights.md), you should update your code to use Visual Search instead since it provides more comprehensive insights.</span></span>


## <a name="the-request"></a><span data-ttu-id="1b338-123">The request</span><span class="sxs-lookup"><span data-stu-id="1b338-123">The request</span></span>

<span data-ttu-id="1b338-124">The following are the options for getting insights about an image.</span><span class="sxs-lookup"><span data-stu-id="1b338-124">The following are the options for getting insights about an image.</span></span> 

- <span data-ttu-id="1b338-125">Send an insights token that you get from an image in a previous call to one of the [Bing Images API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference) endpoints</span><span class="sxs-lookup"><span data-stu-id="1b338-125">Send an insights token that you get from an image in a previous call to one of the [Bing Images API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference) endpoints</span></span>
- <span data-ttu-id="1b338-126">Send the URL of an image</span><span class="sxs-lookup"><span data-stu-id="1b338-126">Send the URL of an image</span></span>
- <span data-ttu-id="1b338-127">Upload an image (binary)</span><span class="sxs-lookup"><span data-stu-id="1b338-127">Upload an image (binary)</span></span>


<span data-ttu-id="1b338-128">If you send Visual Search an image token or URL, the following shows the JSON object that you must include in the body of the POST.</span><span class="sxs-lookup"><span data-stu-id="1b338-128">If you send Visual Search an image token or URL, the following shows the JSON object that you must include in the body of the POST.</span></span> 

```json
{
    "imageInfo" : {
        "url" : "",
        "imageInsightsToken" : "",
        "cropArea" : {
            "top" : 0.1,
            "left" : 0.5,
            "right" : 0.9,
            "bottom" : 0.9
        }
    },
    "knowledgeRequest" : {
      "filters" : {
        "site" : ""
      }
    }
}
```

<span data-ttu-id="1b338-129">The `imageInfo` object must include either the `url` or `imageInsightsToken` field but not both.</span><span class="sxs-lookup"><span data-stu-id="1b338-129">The `imageInfo` object must include either the `url` or `imageInsightsToken` field but not both.</span></span> <span data-ttu-id="1b338-130">Set the `url` field to the URL of an Internet accessible image.</span><span class="sxs-lookup"><span data-stu-id="1b338-130">Set the `url` field to the URL of an Internet accessible image.</span></span> <span data-ttu-id="1b338-131">The maximum supported image size is 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1b338-131">The maximum supported image size is 1 MB.</span></span>

<span data-ttu-id="1b338-132">The `imageInsightsToken` must be set to an insights token.</span><span class="sxs-lookup"><span data-stu-id="1b338-132">The `imageInsightsToken` must be set to an insights token.</span></span> <span data-ttu-id="1b338-133">To get an insights token, call the Bing Image API.</span><span class="sxs-lookup"><span data-stu-id="1b338-133">To get an insights token, call the Bing Image API.</span></span> <span data-ttu-id="1b338-134">The response contains a list of `Image` objects.</span><span class="sxs-lookup"><span data-stu-id="1b338-134">The response contains a list of `Image` objects.</span></span> <span data-ttu-id="1b338-135">Each `Image` object contains an `imageInsightsToken` field, which contains the token.</span><span class="sxs-lookup"><span data-stu-id="1b338-135">Each `Image` object contains an `imageInsightsToken` field, which contains the token.</span></span>

<span data-ttu-id="1b338-136">The `cropArea` field is optional.</span><span class="sxs-lookup"><span data-stu-id="1b338-136">The `cropArea` field is optional.</span></span> <span data-ttu-id="1b338-137">The crop area specifies the top, left corner and bottom, right corner of a region of interest.</span><span class="sxs-lookup"><span data-stu-id="1b338-137">The crop area specifies the top, left corner and bottom, right corner of a region of interest.</span></span> <span data-ttu-id="1b338-138">Specify the values in the range 0.0 through 1.0.</span><span class="sxs-lookup"><span data-stu-id="1b338-138">Specify the values in the range 0.0 through 1.0.</span></span> <span data-ttu-id="1b338-139">The values are a percentage of the overall width or height.</span><span class="sxs-lookup"><span data-stu-id="1b338-139">The values are a percentage of the overall width or height.</span></span> <span data-ttu-id="1b338-140">For example, the above example marks the right half of the image as the region of interest.</span><span class="sxs-lookup"><span data-stu-id="1b338-140">For example, the above example marks the right half of the image as the region of interest.</span></span> <span data-ttu-id="1b338-141">Include it if you want to limit the insights request to the region of interest.</span><span class="sxs-lookup"><span data-stu-id="1b338-141">Include it if you want to limit the insights request to the region of interest.</span></span>

<span data-ttu-id="1b338-142">The `filters` object contains a site filter (see the `site` field) that you can use to restrict the similar images and similar products results to a specific domain.</span><span class="sxs-lookup"><span data-stu-id="1b338-142">The `filters` object contains a site filter (see the `site` field) that you can use to restrict the similar images and similar products results to a specific domain.</span></span> <span data-ttu-id="1b338-143">For example, if the image is of a Surface Book, you can set `site` to www.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="1b338-143">For example, if the image is of a Surface Book, you can set `site` to www.microsoft.com.</span></span> 

<span data-ttu-id="1b338-144">If you want to get insights about a local copy of an image, upload the image as binary data.</span><span class="sxs-lookup"><span data-stu-id="1b338-144">If you want to get insights about a local copy of an image, upload the image as binary data.</span></span>

<span data-ttu-id="1b338-145">For details about including these options in the body of the POST, see [Content form types](#content-form-types).</span><span class="sxs-lookup"><span data-stu-id="1b338-145">For details about including these options in the body of the POST, see [Content form types](#content-form-types).</span></span>


### <a name="endpoint"></a><span data-ttu-id="1b338-146">Endpoint</span><span class="sxs-lookup"><span data-stu-id="1b338-146">Endpoint</span></span>

<span data-ttu-id="1b338-147">The Visual Search endpoint is: https:\/\/api.cognitive.microsoft.com/bing/v7.0/images/visualsearch.</span><span class="sxs-lookup"><span data-stu-id="1b338-147">The Visual Search endpoint is: https:\/\/api.cognitive.microsoft.com/bing/v7.0/images/visualsearch.</span></span>

<span data-ttu-id="1b338-148">Requests must be sent as HTTP POST requests only.</span><span class="sxs-lookup"><span data-stu-id="1b338-148">Requests must be sent as HTTP POST requests only.</span></span> 


### <a name="query-parameters"></a><span data-ttu-id="1b338-149">Query parameters</span><span class="sxs-lookup"><span data-stu-id="1b338-149">Query parameters</span></span>

<span data-ttu-id="1b338-150">The following are the query parameters your request should specify.</span><span class="sxs-lookup"><span data-stu-id="1b338-150">The following are the query parameters your request should specify.</span></span> <span data-ttu-id="1b338-151">At a minimum, you should include the `mkt` query parameter.</span><span class="sxs-lookup"><span data-stu-id="1b338-151">At a minimum, you should include the `mkt` query parameter.</span></span>

|<span data-ttu-id="1b338-152">Name</span><span class="sxs-lookup"><span data-stu-id="1b338-152">Name</span></span>|<span data-ttu-id="1b338-153">Value</span><span class="sxs-lookup"><span data-stu-id="1b338-153">Value</span></span>|<span data-ttu-id="1b338-154">Type</span><span class="sxs-lookup"><span data-stu-id="1b338-154">Type</span></span>|<span data-ttu-id="1b338-155">Required</span><span class="sxs-lookup"><span data-stu-id="1b338-155">Required</span></span>|  
|----------|-----------|----------|--------------|  
|<span data-ttu-id="1b338-156"><a name="cc" />cc</span><span class="sxs-lookup"><span data-stu-id="1b338-156"><a name="cc" />cc</span></span>|<span data-ttu-id="1b338-157">A 2-character country code of the country where the results come from.</span><span class="sxs-lookup"><span data-stu-id="1b338-157">A 2-character country code of the country where the results come from.</span></span><br /><br /> <span data-ttu-id="1b338-158">If you set this parameter, you must also specify the [Accept-Language](#acceptlanguage) header.</span><span class="sxs-lookup"><span data-stu-id="1b338-158">If you set this parameter, you must also specify the [Accept-Language](#acceptlanguage) header.</span></span> <span data-ttu-id="1b338-159">Bing uses the first supported language it finds from the list of languages, and combines the language with the country code that you specify to determine the market to return results from.</span><span class="sxs-lookup"><span data-stu-id="1b338-159">Bing uses the first supported language it finds from the list of languages, and combines the language with the country code that you specify to determine the market to return results from.</span></span> <span data-ttu-id="1b338-160">If the languages list does not include a supported language, Bing finds the closest language and market that supports the request.</span><span class="sxs-lookup"><span data-stu-id="1b338-160">If the languages list does not include a supported language, Bing finds the closest language and market that supports the request.</span></span> <span data-ttu-id="1b338-161">Or it may use an aggregated or default market for the results instead of the specified one.</span><span class="sxs-lookup"><span data-stu-id="1b338-161">Or it may use an aggregated or default market for the results instead of the specified one.</span></span><br /><br /> <span data-ttu-id="1b338-162">You should use this query parameter and the `Accept-Language` query parameter only if you specify multiple languages; otherwise, you should use the `mkt` and `setLang` query parameters.</span><span class="sxs-lookup"><span data-stu-id="1b338-162">You should use this query parameter and the `Accept-Language` query parameter only if you specify multiple languages; otherwise, you should use the `mkt` and `setLang` query parameters.</span></span><br /><br /> <span data-ttu-id="1b338-163">This parameter and the [mkt](#mkt) query parameter are mutually exclusive&mdash;do not specify both.</span><span class="sxs-lookup"><span data-stu-id="1b338-163">This parameter and the [mkt](#mkt) query parameter are mutually exclusive&mdash;do not specify both.</span></span>|<span data-ttu-id="1b338-164">String</span><span class="sxs-lookup"><span data-stu-id="1b338-164">String</span></span>|<span data-ttu-id="1b338-165">No</span><span class="sxs-lookup"><span data-stu-id="1b338-165">No</span></span>|  
|<span data-ttu-id="1b338-166"><a name="mkt" />mkt</span><span class="sxs-lookup"><span data-stu-id="1b338-166"><a name="mkt" />mkt</span></span>|<span data-ttu-id="1b338-167">The market where the results come from.</span><span class="sxs-lookup"><span data-stu-id="1b338-167">The market where the results come from.</span></span> <br /><br /> <span data-ttu-id="1b338-168">**NOTE:** You are encouraged to always specify the market, if known.</span><span class="sxs-lookup"><span data-stu-id="1b338-168">**NOTE:** You are encouraged to always specify the market, if known.</span></span> <span data-ttu-id="1b338-169">Specifying the market helps Bing route the request and return an appropriate and optimal response.</span><span class="sxs-lookup"><span data-stu-id="1b338-169">Specifying the market helps Bing route the request and return an appropriate and optimal response.</span></span><br /><br /> <span data-ttu-id="1b338-170">This parameter and the [cc](#cc) query parameter are mutually exclusive&mdash;do not specify both.</span><span class="sxs-lookup"><span data-stu-id="1b338-170">This parameter and the [cc](#cc) query parameter are mutually exclusive&mdash;do not specify both.</span></span>|<span data-ttu-id="1b338-171">String</span><span class="sxs-lookup"><span data-stu-id="1b338-171">String</span></span>|<span data-ttu-id="1b338-172">Yes</span><span class="sxs-lookup"><span data-stu-id="1b338-172">Yes</span></span>|  
|<span data-ttu-id="1b338-173"><a name="safesearch" />safeSearch</span><span class="sxs-lookup"><span data-stu-id="1b338-173"><a name="safesearch" />safeSearch</span></span>|<span data-ttu-id="1b338-174">A filter used to filter adult content.</span><span class="sxs-lookup"><span data-stu-id="1b338-174">A filter used to filter adult content.</span></span> <span data-ttu-id="1b338-175">The following are the possible case-insensitive filter values.</span><span class="sxs-lookup"><span data-stu-id="1b338-175">The following are the possible case-insensitive filter values.</span></span><br /><ul><li><span data-ttu-id="1b338-176">Off&mdash;Return webpages with adult text or images.</span><span class="sxs-lookup"><span data-stu-id="1b338-176">Off&mdash;Return webpages with adult text or images.</span></span><br /><br/></li><li><span data-ttu-id="1b338-177">Moderate&mdash;Return webpages with adult text, but not adult images.</span><span class="sxs-lookup"><span data-stu-id="1b338-177">Moderate&mdash;Return webpages with adult text, but not adult images.</span></span><br /><br/></li><li><span data-ttu-id="1b338-178">Strict&mdash;Do not return webpages with adult text or images.</span><span class="sxs-lookup"><span data-stu-id="1b338-178">Strict&mdash;Do not return webpages with adult text or images.</span></span></li></ul><br /> <span data-ttu-id="1b338-179">The default is Moderate.</span><span class="sxs-lookup"><span data-stu-id="1b338-179">The default is Moderate.</span></span><br /><br /> <span data-ttu-id="1b338-180">**NOTE:** If the request comes from a market that Bing's adult policy requires that `safeSearch` be set to Strict, Bing ignores the `safeSearch` value and uses Strict.</span><span class="sxs-lookup"><span data-stu-id="1b338-180">**NOTE:** If the request comes from a market that Bing's adult policy requires that `safeSearch` be set to Strict, Bing ignores the `safeSearch` value and uses Strict.</span></span><br/><br/><span data-ttu-id="1b338-181">**NOTE:** If you use the `site:` query operator, there is the chance that the response may contain adult content regardless of what the `safeSearch` query parameter is set to.</span><span class="sxs-lookup"><span data-stu-id="1b338-181">**NOTE:** If you use the `site:` query operator, there is the chance that the response may contain adult content regardless of what the `safeSearch` query parameter is set to.</span></span> <span data-ttu-id="1b338-182">Use `site:` only if you are aware of the content on the site and your scenario supports the possibility of adult content.</span><span class="sxs-lookup"><span data-stu-id="1b338-182">Use `site:` only if you are aware of the content on the site and your scenario supports the possibility of adult content.</span></span> |<span data-ttu-id="1b338-183">String</span><span class="sxs-lookup"><span data-stu-id="1b338-183">String</span></span>|<span data-ttu-id="1b338-184">No</span><span class="sxs-lookup"><span data-stu-id="1b338-184">No</span></span>|  
|<span data-ttu-id="1b338-185"><a name="setlang" />setLang</span><span class="sxs-lookup"><span data-stu-id="1b338-185"><a name="setlang" />setLang</span></span>|<span data-ttu-id="1b338-186">The language to use for user interface strings.</span><span class="sxs-lookup"><span data-stu-id="1b338-186">The language to use for user interface strings.</span></span> <span data-ttu-id="1b338-187">Specify the language using the ISO 639-1 2-letter language code.</span><span class="sxs-lookup"><span data-stu-id="1b338-187">Specify the language using the ISO 639-1 2-letter language code.</span></span> <span data-ttu-id="1b338-188">For example, the language code for English is EN.</span><span class="sxs-lookup"><span data-stu-id="1b338-188">For example, the language code for English is EN.</span></span> <span data-ttu-id="1b338-189">The default is EN (English).</span><span class="sxs-lookup"><span data-stu-id="1b338-189">The default is EN (English).</span></span><br /><br /> <span data-ttu-id="1b338-190">Although optional, you should always specify the language.</span><span class="sxs-lookup"><span data-stu-id="1b338-190">Although optional, you should always specify the language.</span></span> <span data-ttu-id="1b338-191">Typically, you set `setLang` to the same language specified by `mkt` unless the user wants the user interface strings displayed in a different language.</span><span class="sxs-lookup"><span data-stu-id="1b338-191">Typically, you set `setLang` to the same language specified by `mkt` unless the user wants the user interface strings displayed in a different language.</span></span><br /><br /> <span data-ttu-id="1b338-192">This parameter and the [Accept-Language](#acceptlanguage) header are mutually exclusive&mdash;do not specify both.</span><span class="sxs-lookup"><span data-stu-id="1b338-192">This parameter and the [Accept-Language](#acceptlanguage) header are mutually exclusive&mdash;do not specify both.</span></span><br /><br /> <span data-ttu-id="1b338-193">A user interface string is a string that's used as a label in a user interface.</span><span class="sxs-lookup"><span data-stu-id="1b338-193">A user interface string is a string that's used as a label in a user interface.</span></span> <span data-ttu-id="1b338-194">There are few user interface strings in the JSON response objects.</span><span class="sxs-lookup"><span data-stu-id="1b338-194">There are few user interface strings in the JSON response objects.</span></span> <span data-ttu-id="1b338-195">Also, any links to Bing.com properties in the response objects apply the specified language.</span><span class="sxs-lookup"><span data-stu-id="1b338-195">Also, any links to Bing.com properties in the response objects apply the specified language.</span></span>|<span data-ttu-id="1b338-196">String</span><span class="sxs-lookup"><span data-stu-id="1b338-196">String</span></span>|<span data-ttu-id="1b338-197">No</span><span class="sxs-lookup"><span data-stu-id="1b338-197">No</span></span>| 

### <a name="headers"></a><span data-ttu-id="1b338-198">Headers</span><span class="sxs-lookup"><span data-stu-id="1b338-198">Headers</span></span>

<span data-ttu-id="1b338-199">The following are the headers that your request should specify.</span><span class="sxs-lookup"><span data-stu-id="1b338-199">The following are the headers that your request should specify.</span></span> <span data-ttu-id="1b338-200">The Content-Type and Ocp-Apim-Subscription-Key headers are the only required headers but you should also include User-Agent, X-MSEdge-ClientID, X-MSEdge-ClientIP, and X-Search-Location.</span><span class="sxs-lookup"><span data-stu-id="1b338-200">The Content-Type and Ocp-Apim-Subscription-Key headers are the only required headers but you should also include User-Agent, X-MSEdge-ClientID, X-MSEdge-ClientIP, and X-Search-Location.</span></span>


|<span data-ttu-id="1b338-201">Header</span><span class="sxs-lookup"><span data-stu-id="1b338-201">Header</span></span>|<span data-ttu-id="1b338-202">Description</span><span class="sxs-lookup"><span data-stu-id="1b338-202">Description</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="1b338-203"><a name="acceptlanguage" />Accept-Language</span><span class="sxs-lookup"><span data-stu-id="1b338-203"><a name="acceptlanguage" />Accept-Language</span></span>|<span data-ttu-id="1b338-204">Optional request header.</span><span class="sxs-lookup"><span data-stu-id="1b338-204">Optional request header.</span></span><br /><br /> <span data-ttu-id="1b338-205">A comma-delimited list of languages to use for user interface strings.</span><span class="sxs-lookup"><span data-stu-id="1b338-205">A comma-delimited list of languages to use for user interface strings.</span></span> <span data-ttu-id="1b338-206">The list is in decreasing order of preference.</span><span class="sxs-lookup"><span data-stu-id="1b338-206">The list is in decreasing order of preference.</span></span> <span data-ttu-id="1b338-207">For more information, including expected format, see [RFC2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span><span class="sxs-lookup"><span data-stu-id="1b338-207">For more information, including expected format, see [RFC2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span></span><br /><br /> <span data-ttu-id="1b338-208">This header and the [setLang](#setlang) query parameter are mutually exclusive&mdash;do not specify both.</span><span class="sxs-lookup"><span data-stu-id="1b338-208">This header and the [setLang](#setlang) query parameter are mutually exclusive&mdash;do not specify both.</span></span><br /><br /> <span data-ttu-id="1b338-209">If you set this header, you must also specify the [cc](#cc) query parameter.</span><span class="sxs-lookup"><span data-stu-id="1b338-209">If you set this header, you must also specify the [cc](#cc) query parameter.</span></span> <span data-ttu-id="1b338-210">To determine the market to return results for, Bing uses the first supported language it finds from the list and combines it with the `cc` parameter value.</span><span class="sxs-lookup"><span data-stu-id="1b338-210">To determine the market to return results for, Bing uses the first supported language it finds from the list and combines it with the `cc` parameter value.</span></span> <span data-ttu-id="1b338-211">If the list does not include a supported language, Bing finds the closest language and market that supports the request or it uses an aggregated or default market for the results.</span><span class="sxs-lookup"><span data-stu-id="1b338-211">If the list does not include a supported language, Bing finds the closest language and market that supports the request or it uses an aggregated or default market for the results.</span></span> <span data-ttu-id="1b338-212">To determine the market that Bing used, see the BingAPIs-Market header.</span><span class="sxs-lookup"><span data-stu-id="1b338-212">To determine the market that Bing used, see the BingAPIs-Market header.</span></span><br /><br /> <span data-ttu-id="1b338-213">Use this header and the `cc` query parameter only if you specify multiple languages.</span><span class="sxs-lookup"><span data-stu-id="1b338-213">Use this header and the `cc` query parameter only if you specify multiple languages.</span></span> <span data-ttu-id="1b338-214">Otherwise, use the [mkt](#mkt) and [setLang](#setlang) query parameters.</span><span class="sxs-lookup"><span data-stu-id="1b338-214">Otherwise, use the [mkt](#mkt) and [setLang](#setlang) query parameters.</span></span><br /><br /> <span data-ttu-id="1b338-215">A user interface string is a string that's used as a label in a user interface.</span><span class="sxs-lookup"><span data-stu-id="1b338-215">A user interface string is a string that's used as a label in a user interface.</span></span> <span data-ttu-id="1b338-216">There are few user interface strings in the JSON response objects.</span><span class="sxs-lookup"><span data-stu-id="1b338-216">There are few user interface strings in the JSON response objects.</span></span> <span data-ttu-id="1b338-217">Any links to Bing.com properties in the response objects apply the specified language.</span><span class="sxs-lookup"><span data-stu-id="1b338-217">Any links to Bing.com properties in the response objects apply the specified language.</span></span>|  
|<span data-ttu-id="1b338-218"><a name="contenttype" />Content-Type</span><span class="sxs-lookup"><span data-stu-id="1b338-218"><a name="contenttype" />Content-Type</span></span>|<span data-ttu-id="1b338-219">Required request header.</span><span class="sxs-lookup"><span data-stu-id="1b338-219">Required request header.</span></span><br /><br /><span data-ttu-id="1b338-220">Must be set to multipart/form-data and include a boundary parameter (for example, multipart/form-data; boundary=\<boundary string\>).</span><span class="sxs-lookup"><span data-stu-id="1b338-220">Must be set to multipart/form-data and include a boundary parameter (for example, multipart/form-data; boundary=\<boundary string\>).</span></span> <span data-ttu-id="1b338-221">For more information, see [Content form types](#content-form-types).</span><span class="sxs-lookup"><span data-stu-id="1b338-221">For more information, see [Content form types](#content-form-types).</span></span>
|<span data-ttu-id="1b338-222"><a name="market" />BingAPIs-Market</span><span class="sxs-lookup"><span data-stu-id="1b338-222"><a name="market" />BingAPIs-Market</span></span>|<span data-ttu-id="1b338-223">Response header.</span><span class="sxs-lookup"><span data-stu-id="1b338-223">Response header.</span></span><br /><br /> <span data-ttu-id="1b338-224">The market used by the request.</span><span class="sxs-lookup"><span data-stu-id="1b338-224">The market used by the request.</span></span> <span data-ttu-id="1b338-225">The form is \<languageCode\>-\<countryCode\>.</span><span class="sxs-lookup"><span data-stu-id="1b338-225">The form is \<languageCode\>-\<countryCode\>.</span></span> <span data-ttu-id="1b338-226">For example, en-US.</span><span class="sxs-lookup"><span data-stu-id="1b338-226">For example, en-US.</span></span>|  
|<span data-ttu-id="1b338-227"><a name="traceid" />BingAPIs-TraceId</span><span class="sxs-lookup"><span data-stu-id="1b338-227"><a name="traceid" />BingAPIs-TraceId</span></span>|<span data-ttu-id="1b338-228">Response header.</span><span class="sxs-lookup"><span data-stu-id="1b338-228">Response header.</span></span><br /><br /> <span data-ttu-id="1b338-229">The ID of the log entry that contains the details of the request.</span><span class="sxs-lookup"><span data-stu-id="1b338-229">The ID of the log entry that contains the details of the request.</span></span> <span data-ttu-id="1b338-230">When an error occurs, capture this ID.</span><span class="sxs-lookup"><span data-stu-id="1b338-230">When an error occurs, capture this ID.</span></span> <span data-ttu-id="1b338-231">If you are not able to determine and resolve the issue, include this ID along with the other information that you provide the Support team.</span><span class="sxs-lookup"><span data-stu-id="1b338-231">If you are not able to determine and resolve the issue, include this ID along with the other information that you provide the Support team.</span></span>|  
|<span data-ttu-id="1b338-232"><a name="subscriptionkey" />Ocp-Apim-Subscription-Key</span><span class="sxs-lookup"><span data-stu-id="1b338-232"><a name="subscriptionkey" />Ocp-Apim-Subscription-Key</span></span>|<span data-ttu-id="1b338-233">Required request header.</span><span class="sxs-lookup"><span data-stu-id="1b338-233">Required request header.</span></span><br /><br /> <span data-ttu-id="1b338-234">The subscription key that you received when you signed up for this service in [Cognitive Services](https://www.microsoft.com/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="1b338-234">The subscription key that you received when you signed up for this service in [Cognitive Services](https://www.microsoft.com/cognitive-services/).</span></span>|  
|<span data-ttu-id="1b338-235"><a name="pragma" />Pragma</span><span class="sxs-lookup"><span data-stu-id="1b338-235"><a name="pragma" />Pragma</span></span>|<span data-ttu-id="1b338-236">Optional request header</span><span class="sxs-lookup"><span data-stu-id="1b338-236">Optional request header</span></span><br /><br /> <span data-ttu-id="1b338-237">By default, Bing returns cached content, if available.</span><span class="sxs-lookup"><span data-stu-id="1b338-237">By default, Bing returns cached content, if available.</span></span> <span data-ttu-id="1b338-238">To prevent Bing from returning cached content, set the Pragma header to no-cache (for example, Pragma: no-cache).</span><span class="sxs-lookup"><span data-stu-id="1b338-238">To prevent Bing from returning cached content, set the Pragma header to no-cache (for example, Pragma: no-cache).</span></span>
|<span data-ttu-id="1b338-239"><a name="useragent" />User-Agent</span><span class="sxs-lookup"><span data-stu-id="1b338-239"><a name="useragent" />User-Agent</span></span>|<span data-ttu-id="1b338-240">Optional request header.</span><span class="sxs-lookup"><span data-stu-id="1b338-240">Optional request header.</span></span><br /><br /> <span data-ttu-id="1b338-241">The user agent originating the request.</span><span class="sxs-lookup"><span data-stu-id="1b338-241">The user agent originating the request.</span></span> <span data-ttu-id="1b338-242">Bing uses the user agent to provide mobile users with an optimized experience.</span><span class="sxs-lookup"><span data-stu-id="1b338-242">Bing uses the user agent to provide mobile users with an optimized experience.</span></span> <span data-ttu-id="1b338-243">Although optional, you are encouraged to always specify this header.</span><span class="sxs-lookup"><span data-stu-id="1b338-243">Although optional, you are encouraged to always specify this header.</span></span><br /><br /> <span data-ttu-id="1b338-244">The user-agent should be the same string that any commonly used browser sends.</span><span class="sxs-lookup"><span data-stu-id="1b338-244">The user-agent should be the same string that any commonly used browser sends.</span></span> <span data-ttu-id="1b338-245">For information about user agents, see [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span><span class="sxs-lookup"><span data-stu-id="1b338-245">For information about user agents, see [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span></span><br /><br /> <span data-ttu-id="1b338-246">The following are examples of user-agent strings.</span><span class="sxs-lookup"><span data-stu-id="1b338-246">The following are examples of user-agent strings.</span></span><br /><ul><li><span data-ttu-id="1b338-247">Windows Phone&mdash;Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)</span><span class="sxs-lookup"><span data-stu-id="1b338-247">Windows Phone&mdash;Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)</span></span><br /><br /></li><li><span data-ttu-id="1b338-248">Android&mdash;Mozilla/5.0 (Linux; U; Android 2.3.5; en-us; SCH-I500 Build/GINGERBREAD) AppleWebKit/533.1 (KHTML; like Gecko) Version/4.0 Mobile Safari/533.1</span><span class="sxs-lookup"><span data-stu-id="1b338-248">Android&mdash;Mozilla/5.0 (Linux; U; Android 2.3.5; en-us; SCH-I500 Build/GINGERBREAD) AppleWebKit/533.1 (KHTML; like Gecko) Version/4.0 Mobile Safari/533.1</span></span><br /><br /></li><li><span data-ttu-id="1b338-249">iPhone&mdash;Mozilla/5.0 (iPhone; CPU iPhone OS 6_1 like Mac OS X) AppleWebKit/536.26 (KHTML; like Gecko) Mobile/10B142 iPhone4;1 BingWeb/3.03.1428.20120423</span><span class="sxs-lookup"><span data-stu-id="1b338-249">iPhone&mdash;Mozilla/5.0 (iPhone; CPU iPhone OS 6_1 like Mac OS X) AppleWebKit/536.26 (KHTML; like Gecko) Mobile/10B142 iPhone4;1 BingWeb/3.03.1428.20120423</span></span><br /><br /></li><li><span data-ttu-id="1b338-250">PC&mdash;Mozilla/5.0 (Windows NT 6.3; WOW64; Trident/7.0; Touch; rv:11.0) like Gecko</span><span class="sxs-lookup"><span data-stu-id="1b338-250">PC&mdash;Mozilla/5.0 (Windows NT 6.3; WOW64; Trident/7.0; Touch; rv:11.0) like Gecko</span></span><br /><br /></li><li><span data-ttu-id="1b338-251">iPad&mdash;Mozilla/5.0 (iPad; CPU OS 7_0 like Mac OS X) AppleWebKit/537.51.1 (KHTML, like Gecko) Version/7.0 Mobile/11A465 Safari/9537.53</span><span class="sxs-lookup"><span data-stu-id="1b338-251">iPad&mdash;Mozilla/5.0 (iPad; CPU OS 7_0 like Mac OS X) AppleWebKit/537.51.1 (KHTML, like Gecko) Version/7.0 Mobile/11A465 Safari/9537.53</span></span></li></ul>|
|<span data-ttu-id="1b338-252"><a name="clientid" />X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="1b338-252"><a name="clientid" />X-MSEdge-ClientID</span></span>|<span data-ttu-id="1b338-253">Optional request and response header.</span><span class="sxs-lookup"><span data-stu-id="1b338-253">Optional request and response header.</span></span><br /><br /> <span data-ttu-id="1b338-254">Bing uses this header to provide users with consistent behavior across Bing API calls.</span><span class="sxs-lookup"><span data-stu-id="1b338-254">Bing uses this header to provide users with consistent behavior across Bing API calls.</span></span> <span data-ttu-id="1b338-255">Bing often flights new features and improvements, and it uses the client ID as a key for assigning traffic on different flights.</span><span class="sxs-lookup"><span data-stu-id="1b338-255">Bing often flights new features and improvements, and it uses the client ID as a key for assigning traffic on different flights.</span></span> <span data-ttu-id="1b338-256">If you do not use the same client ID for a user across multiple requests, then Bing may assign the user to multiple conflicting flights.</span><span class="sxs-lookup"><span data-stu-id="1b338-256">If you do not use the same client ID for a user across multiple requests, then Bing may assign the user to multiple conflicting flights.</span></span> <span data-ttu-id="1b338-257">Being assigned to multiple conflicting flights can lead to an inconsistent user experience.</span><span class="sxs-lookup"><span data-stu-id="1b338-257">Being assigned to multiple conflicting flights can lead to an inconsistent user experience.</span></span> <span data-ttu-id="1b338-258">For example, if the second request has a different flight assignment than the first, the experience may be unexpected.</span><span class="sxs-lookup"><span data-stu-id="1b338-258">For example, if the second request has a different flight assignment than the first, the experience may be unexpected.</span></span> <span data-ttu-id="1b338-259">Also, Bing can use the client ID to tailor web results to that client ID’s search history, providing a richer experience for the user.</span><span class="sxs-lookup"><span data-stu-id="1b338-259">Also, Bing can use the client ID to tailor web results to that client ID’s search history, providing a richer experience for the user.</span></span><br /><br /> <span data-ttu-id="1b338-260">Bing also uses this header to help improve result rankings by analyzing the activity generated by a client ID.</span><span class="sxs-lookup"><span data-stu-id="1b338-260">Bing also uses this header to help improve result rankings by analyzing the activity generated by a client ID.</span></span> <span data-ttu-id="1b338-261">The relevance improvements help with better quality of results delivered by Bing APIs and in turn enables higher click-through rates for the API consumer.</span><span class="sxs-lookup"><span data-stu-id="1b338-261">The relevance improvements help with better quality of results delivered by Bing APIs and in turn enables higher click-through rates for the API consumer.</span></span><br /><br /> <span data-ttu-id="1b338-262">**IMPORTANT:** Although optional, you should consider this header required.</span><span class="sxs-lookup"><span data-stu-id="1b338-262">**IMPORTANT:** Although optional, you should consider this header required.</span></span> <span data-ttu-id="1b338-263">Persisting the client ID across multiple requests for the same end user and device combination enables 1) the API consumer to receive a consistent user experience, and 2) higher click-through rates via better quality of results from the Bing APIs.</span><span class="sxs-lookup"><span data-stu-id="1b338-263">Persisting the client ID across multiple requests for the same end user and device combination enables 1) the API consumer to receive a consistent user experience, and 2) higher click-through rates via better quality of results from the Bing APIs.</span></span><br /><br /> <span data-ttu-id="1b338-264">The following are the basic usage rules that apply to this header.</span><span class="sxs-lookup"><span data-stu-id="1b338-264">The following are the basic usage rules that apply to this header.</span></span><br /><ul><li><span data-ttu-id="1b338-265">Each user that uses your application on the device must have a unique, Bing generated client ID.</span><span class="sxs-lookup"><span data-stu-id="1b338-265">Each user that uses your application on the device must have a unique, Bing generated client ID.</span></span><br /><br/><span data-ttu-id="1b338-266">If you do not include this header in the request, Bing generates an ID and returns it in the X-MSEdge-ClientID response header.</span><span class="sxs-lookup"><span data-stu-id="1b338-266">If you do not include this header in the request, Bing generates an ID and returns it in the X-MSEdge-ClientID response header.</span></span> <span data-ttu-id="1b338-267">The only time that you should NOT include this header in a request is the first time the user uses your app on that device.</span><span class="sxs-lookup"><span data-stu-id="1b338-267">The only time that you should NOT include this header in a request is the first time the user uses your app on that device.</span></span><br /><br/></li><li><span data-ttu-id="1b338-268">**ATTENTION:** You must ensure that this Client ID is not linkable to any authenticated user account information.</span><span class="sxs-lookup"><span data-stu-id="1b338-268">**ATTENTION:** You must ensure that this Client ID is not linkable to any authenticated user account information.</span></span></li><li><span data-ttu-id="1b338-269">Use the client ID for each Bing API request that your app makes for this user on the device.</span><span class="sxs-lookup"><span data-stu-id="1b338-269">Use the client ID for each Bing API request that your app makes for this user on the device.</span></span><br /><br/></li><li><span data-ttu-id="1b338-270">Persist the client ID.</span><span class="sxs-lookup"><span data-stu-id="1b338-270">Persist the client ID.</span></span> <span data-ttu-id="1b338-271">To persist the ID in a browser app, use a persistent HTTP cookie to ensure the ID is used across all sessions.</span><span class="sxs-lookup"><span data-stu-id="1b338-271">To persist the ID in a browser app, use a persistent HTTP cookie to ensure the ID is used across all sessions.</span></span> <span data-ttu-id="1b338-272">Do not use a session cookie.</span><span class="sxs-lookup"><span data-stu-id="1b338-272">Do not use a session cookie.</span></span> <span data-ttu-id="1b338-273">For other apps such as mobile apps, use the device's persistent storage to persist the ID.</span><span class="sxs-lookup"><span data-stu-id="1b338-273">For other apps such as mobile apps, use the device's persistent storage to persist the ID.</span></span><br /><br/><span data-ttu-id="1b338-274">The next time the user uses your app on that device, get the client ID that you persisted.</span><span class="sxs-lookup"><span data-stu-id="1b338-274">The next time the user uses your app on that device, get the client ID that you persisted.</span></span></li></ul><br /> <span data-ttu-id="1b338-275">**NOTE:** Bing responses may or may not include this header.</span><span class="sxs-lookup"><span data-stu-id="1b338-275">**NOTE:** Bing responses may or may not include this header.</span></span> <span data-ttu-id="1b338-276">If the response includes this header, capture the client ID and use it for all subsequent Bing requests for the user on that device.</span><span class="sxs-lookup"><span data-stu-id="1b338-276">If the response includes this header, capture the client ID and use it for all subsequent Bing requests for the user on that device.</span></span><br /><br /> <span data-ttu-id="1b338-277">**NOTE:** If you include the X-MSEdge-ClientID, you must not include cookies in the request.</span><span class="sxs-lookup"><span data-stu-id="1b338-277">**NOTE:** If you include the X-MSEdge-ClientID, you must not include cookies in the request.</span></span>|  
|<span data-ttu-id="1b338-278"><a name="clientip" />X-MSEdge-ClientIP</span><span class="sxs-lookup"><span data-stu-id="1b338-278"><a name="clientip" />X-MSEdge-ClientIP</span></span>|<span data-ttu-id="1b338-279">Optional request header.</span><span class="sxs-lookup"><span data-stu-id="1b338-279">Optional request header.</span></span><br /><br /> <span data-ttu-id="1b338-280">The IPv4 or IPv6 address of the client device.</span><span class="sxs-lookup"><span data-stu-id="1b338-280">The IPv4 or IPv6 address of the client device.</span></span> <span data-ttu-id="1b338-281">The IP address is used to discover the user's location.</span><span class="sxs-lookup"><span data-stu-id="1b338-281">The IP address is used to discover the user's location.</span></span> <span data-ttu-id="1b338-282">Bing uses the location information to determine safe search behavior.</span><span class="sxs-lookup"><span data-stu-id="1b338-282">Bing uses the location information to determine safe search behavior.</span></span><br /><br /> <span data-ttu-id="1b338-283">**NOTE:** Although optional, you are encouraged to always specify this header and the X-Search-Location header.</span><span class="sxs-lookup"><span data-stu-id="1b338-283">**NOTE:** Although optional, you are encouraged to always specify this header and the X-Search-Location header.</span></span><br /><br /> <span data-ttu-id="1b338-284">Do not obfuscate the address (for example, by changing the last octet to 0).</span><span class="sxs-lookup"><span data-stu-id="1b338-284">Do not obfuscate the address (for example, by changing the last octet to 0).</span></span> <span data-ttu-id="1b338-285">Obfuscating the address results in the location not being anywhere near the device's actual location, which may result in Bing serving erroneous results.</span><span class="sxs-lookup"><span data-stu-id="1b338-285">Obfuscating the address results in the location not being anywhere near the device's actual location, which may result in Bing serving erroneous results.</span></span>|  
|<span data-ttu-id="1b338-286"><a name="location" />X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="1b338-286"><a name="location" />X-Search-Location</span></span>|<span data-ttu-id="1b338-287">Optional request header.</span><span class="sxs-lookup"><span data-stu-id="1b338-287">Optional request header.</span></span><br /><br /> <span data-ttu-id="1b338-288">A semicolon-delimited list of key/value pairs that describe the client's geographical location.</span><span class="sxs-lookup"><span data-stu-id="1b338-288">A semicolon-delimited list of key/value pairs that describe the client's geographical location.</span></span> <span data-ttu-id="1b338-289">Bing uses the location information to determine safe search behavior and to return relevant local content.</span><span class="sxs-lookup"><span data-stu-id="1b338-289">Bing uses the location information to determine safe search behavior and to return relevant local content.</span></span> <span data-ttu-id="1b338-290">Specify the key/value pair as \<key\>:\<value\>.</span><span class="sxs-lookup"><span data-stu-id="1b338-290">Specify the key/value pair as \<key\>:\<value\>.</span></span> <span data-ttu-id="1b338-291">The following are the keys that you use to specify the user's location.</span><span class="sxs-lookup"><span data-stu-id="1b338-291">The following are the keys that you use to specify the user's location.</span></span><br /><br /><ul><li><span data-ttu-id="1b338-292">lat&mdash;Required.</span><span class="sxs-lookup"><span data-stu-id="1b338-292">lat&mdash;Required.</span></span> <span data-ttu-id="1b338-293">The latitude of the client's location, in degrees.</span><span class="sxs-lookup"><span data-stu-id="1b338-293">The latitude of the client's location, in degrees.</span></span> <span data-ttu-id="1b338-294">The latitude must be greater than or equal to -90.0 and less than or equal to +90.0.</span><span class="sxs-lookup"><span data-stu-id="1b338-294">The latitude must be greater than or equal to -90.0 and less than or equal to +90.0.</span></span> <span data-ttu-id="1b338-295">Negative values indicate southern latitudes and positive values indicate northern latitudes.</span><span class="sxs-lookup"><span data-stu-id="1b338-295">Negative values indicate southern latitudes and positive values indicate northern latitudes.</span></span><br /><br /></li><li><span data-ttu-id="1b338-296">long&mdash;Required.</span><span class="sxs-lookup"><span data-stu-id="1b338-296">long&mdash;Required.</span></span> <span data-ttu-id="1b338-297">The longitude of the client's location, in degrees.</span><span class="sxs-lookup"><span data-stu-id="1b338-297">The longitude of the client's location, in degrees.</span></span> <span data-ttu-id="1b338-298">The longitude must be greater than or equal to -180.0 and less than or equal to +180.0.</span><span class="sxs-lookup"><span data-stu-id="1b338-298">The longitude must be greater than or equal to -180.0 and less than or equal to +180.0.</span></span> <span data-ttu-id="1b338-299">Negative values indicate western longitudes and positive values indicate eastern longitudes.</span><span class="sxs-lookup"><span data-stu-id="1b338-299">Negative values indicate western longitudes and positive values indicate eastern longitudes.</span></span><br /><br /></li><li><span data-ttu-id="1b338-300">re&mdash;Required.</span><span class="sxs-lookup"><span data-stu-id="1b338-300">re&mdash;Required.</span></span> <span data-ttu-id="1b338-301">The radius, in meters, which specifies the horizontal accuracy of the coordinates.</span><span class="sxs-lookup"><span data-stu-id="1b338-301">The radius, in meters, which specifies the horizontal accuracy of the coordinates.</span></span> <span data-ttu-id="1b338-302">Pass the value returned by the device's location service.</span><span class="sxs-lookup"><span data-stu-id="1b338-302">Pass the value returned by the device's location service.</span></span> <span data-ttu-id="1b338-303">Typical values might be 22m for GPS/Wi-Fi, 380m for cell tower triangulation, and 18,000m for reverse IP lookup.</span><span class="sxs-lookup"><span data-stu-id="1b338-303">Typical values might be 22m for GPS/Wi-Fi, 380m for cell tower triangulation, and 18,000m for reverse IP lookup.</span></span><br /><br /></li><li><span data-ttu-id="1b338-304">ts&mdash;Optional.</span><span class="sxs-lookup"><span data-stu-id="1b338-304">ts&mdash;Optional.</span></span> <span data-ttu-id="1b338-305">The UTC UNIX timestamp of when the client was at the location.</span><span class="sxs-lookup"><span data-stu-id="1b338-305">The UTC UNIX timestamp of when the client was at the location.</span></span> <span data-ttu-id="1b338-306">(The UNIX timestamp is the number of seconds since January 1, 1970.)</span><span class="sxs-lookup"><span data-stu-id="1b338-306">(The UNIX timestamp is the number of seconds since January 1, 1970.)</span></span><br /><br /></li><li><span data-ttu-id="1b338-307">head&mdash;Optional.</span><span class="sxs-lookup"><span data-stu-id="1b338-307">head&mdash;Optional.</span></span> <span data-ttu-id="1b338-308">The client's relative heading or direction of travel.</span><span class="sxs-lookup"><span data-stu-id="1b338-308">The client's relative heading or direction of travel.</span></span> <span data-ttu-id="1b338-309">Specify the direction of travel as degrees from 0 through 360, counting clockwise relative to true north.</span><span class="sxs-lookup"><span data-stu-id="1b338-309">Specify the direction of travel as degrees from 0 through 360, counting clockwise relative to true north.</span></span> <span data-ttu-id="1b338-310">Specify this key only if the `sp` key is nonzero.</span><span class="sxs-lookup"><span data-stu-id="1b338-310">Specify this key only if the `sp` key is nonzero.</span></span><br /><br /></li><li><span data-ttu-id="1b338-311">sp&mdash;Optional.</span><span class="sxs-lookup"><span data-stu-id="1b338-311">sp&mdash;Optional.</span></span> <span data-ttu-id="1b338-312">The horizontal velocity (speed), in meters per second, that the client device is traveling.</span><span class="sxs-lookup"><span data-stu-id="1b338-312">The horizontal velocity (speed), in meters per second, that the client device is traveling.</span></span><br /><br /></li><li><span data-ttu-id="1b338-313">alt&mdash;Optional.</span><span class="sxs-lookup"><span data-stu-id="1b338-313">alt&mdash;Optional.</span></span> <span data-ttu-id="1b338-314">The altitude of the client device, in meters.</span><span class="sxs-lookup"><span data-stu-id="1b338-314">The altitude of the client device, in meters.</span></span><br /><br /></li><li><span data-ttu-id="1b338-315">are&mdash;Optional.</span><span class="sxs-lookup"><span data-stu-id="1b338-315">are&mdash;Optional.</span></span> <span data-ttu-id="1b338-316">The radius, in meters, that specifies the vertical accuracy of the coordinates.</span><span class="sxs-lookup"><span data-stu-id="1b338-316">The radius, in meters, that specifies the vertical accuracy of the coordinates.</span></span> <span data-ttu-id="1b338-317">Specify this key only if you specify the `alt` key.</span><span class="sxs-lookup"><span data-stu-id="1b338-317">Specify this key only if you specify the `alt` key.</span></span><br /><br /></li></ul> <span data-ttu-id="1b338-318">**NOTE:** Although many of the keys are optional, the more information that you provide, the more accurate the location results are.</span><span class="sxs-lookup"><span data-stu-id="1b338-318">**NOTE:** Although many of the keys are optional, the more information that you provide, the more accurate the location results are.</span></span><br /><br /> <span data-ttu-id="1b338-319">**NOTE:** Although optional, you are encouraged to always specify the user's geographical location.</span><span class="sxs-lookup"><span data-stu-id="1b338-319">**NOTE:** Although optional, you are encouraged to always specify the user's geographical location.</span></span> <span data-ttu-id="1b338-320">Providing the location is especially important if the client's IP address does not accurately reflect the user's physical location (for example, if the client uses VPN).</span><span class="sxs-lookup"><span data-stu-id="1b338-320">Providing the location is especially important if the client's IP address does not accurately reflect the user's physical location (for example, if the client uses VPN).</span></span> <span data-ttu-id="1b338-321">For optimal results, you should include this header and the X-MSEdge-ClientIP header, but at a minimum, you should include this header.</span><span class="sxs-lookup"><span data-stu-id="1b338-321">For optimal results, you should include this header and the X-MSEdge-ClientIP header, but at a minimum, you should include this header.</span></span>|

> [!NOTE] 
> <span data-ttu-id="1b338-322">Remember that the Terms of Use require compliance with all applicable laws, including regarding use of these headers.</span><span class="sxs-lookup"><span data-stu-id="1b338-322">Remember that the Terms of Use require compliance with all applicable laws, including regarding use of these headers.</span></span> <span data-ttu-id="1b338-323">For example, in certain jurisdictions, such as Europe, there are requirements to obtain user consent before placing certain tracking devices on user devices.</span><span class="sxs-lookup"><span data-stu-id="1b338-323">For example, in certain jurisdictions, such as Europe, there are requirements to obtain user consent before placing certain tracking devices on user devices.</span></span>


<a name="content-form-types" />

### <a name="content-form-types"></a><span data-ttu-id="1b338-324">Content form types</span><span class="sxs-lookup"><span data-stu-id="1b338-324">Content form types</span></span>

<span data-ttu-id="1b338-325">Each request must include the Content-Type header.</span><span class="sxs-lookup"><span data-stu-id="1b338-325">Each request must include the Content-Type header.</span></span> <span data-ttu-id="1b338-326">The header must be set to: multipart/form-data; boundary=\<boundary string\>, where \<boundary string\> is a unique, opaque string that identifies the boundary of the form data.</span><span class="sxs-lookup"><span data-stu-id="1b338-326">The header must be set to: multipart/form-data; boundary=\<boundary string\>, where \<boundary string\> is a unique, opaque string that identifies the boundary of the form data.</span></span> <span data-ttu-id="1b338-327">For example, boundary=boundary_1234-abcd.</span><span class="sxs-lookup"><span data-stu-id="1b338-327">For example, boundary=boundary_1234-abcd.</span></span>


<span data-ttu-id="1b338-328">If you send Visual Search an image token or URL, the following shows the form data you must include in the body of the POST.</span><span class="sxs-lookup"><span data-stu-id="1b338-328">If you send Visual Search an image token or URL, the following shows the form data you must include in the body of the POST.</span></span> <span data-ttu-id="1b338-329">The form data must include the Content-Disposition header and its `name` parameter must be set to "knowledgeRequest."</span><span class="sxs-lookup"><span data-stu-id="1b338-329">The form data must include the Content-Disposition header and its `name` parameter must be set to "knowledgeRequest."</span></span> <span data-ttu-id="1b338-330">For details about the `imageInfo` object, see [The request](#the-request).</span><span class="sxs-lookup"><span data-stu-id="1b338-330">For details about the `imageInfo` object, see [The request](#the-request).</span></span>


```
--boundary_1234-abcd
Content-Disposition: form-data; name="knowledgeRequest"

{
    "imageInfo" : {
        "url" : "https://contoso.com/2018/05/fashion/red.jpg"
    }
}

--boundary_1234-abcd--
```

<span data-ttu-id="1b338-331">If you upload a local image, the following shows the form data you must include in the body of the POST.</span><span class="sxs-lookup"><span data-stu-id="1b338-331">If you upload a local image, the following shows the form data you must include in the body of the POST.</span></span> <span data-ttu-id="1b338-332">The form data must include the Content-Disposition header.</span><span class="sxs-lookup"><span data-stu-id="1b338-332">The form data must include the Content-Disposition header.</span></span> <span data-ttu-id="1b338-333">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span><span class="sxs-lookup"><span data-stu-id="1b338-333">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span></span> <span data-ttu-id="1b338-334">The Content-Type header may be set to any commonly used image mime type.</span><span class="sxs-lookup"><span data-stu-id="1b338-334">The Content-Type header may be set to any commonly used image mime type.</span></span> <span data-ttu-id="1b338-335">The contents of the form is the binary of the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-335">The contents of the form is the binary of the image.</span></span> <span data-ttu-id="1b338-336">The maximum image size you may upload is 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1b338-336">The maximum image size you may upload is 1 MB.</span></span> <span data-ttu-id="1b338-337">The largest of the width or height should be 1,500 pixels or less.</span><span class="sxs-lookup"><span data-stu-id="1b338-337">The largest of the width or height should be 1,500 pixels or less.</span></span>


```
--boundary_1234-abcd
Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"
Content-Type: image/jpeg

ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...

--boundary_1234-abcd--
```

<span data-ttu-id="1b338-338">The following shows how to specify the region of interest of an uploaded image.</span><span class="sxs-lookup"><span data-stu-id="1b338-338">The following shows how to specify the region of interest of an uploaded image.</span></span>

```
--boundary_1234-abcd
Content-Disposition: form-data; name="knowledgeRequest"

{
    "imageInfo" : {
        "cropArea" : {
            "top" : 0.2,
            "left" : 0.3,
            "bottom" : 0.7,
            "right" : 0.6
        }
    }
}

--boundary_1234-abcd
Content-Disposition: form-data; name="image"; filename="image"
Content-Type: image/jpeg


ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...

--boundary_1234-abcd--
```



### <a name="example-request"></a><span data-ttu-id="1b338-339">Example request</span><span class="sxs-lookup"><span data-stu-id="1b338-339">Example request</span></span>

<span data-ttu-id="1b338-340">The following shows a complete image insights request that passes an image token and region of interest.</span><span class="sxs-lookup"><span data-stu-id="1b338-340">The following shows a complete image insights request that passes an image token and region of interest.</span></span> <span data-ttu-id="1b338-341">You get the insights token from a previous call to /images/search.</span><span class="sxs-lookup"><span data-stu-id="1b338-341">You get the insights token from a previous call to /images/search.</span></span>


```  
POST https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch?mkt=en-us HTTP/1.1  
Content-Type: multipart/form-data; boundary=boundary_1234-abcd
Ocp-Apim-Subscription-Key: 123456789ABCDE  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com 

--boundary_1234-abcd
Content-Disposition: form-data; name="knowledgeRequest"

{
    "imageInfo" : {
        "imageInsightsToken" : "mid_D6426898706EC7..."
        "cropArea" : {
            "top" : 0.1,
            "left" : 0.2,
            "bottom" : 0.7,
            "right" : 0.5
        }
    }
}

--boundary_1234-abcd--
```


## <a name="the-response"></a><span data-ttu-id="1b338-342">The response</span><span class="sxs-lookup"><span data-stu-id="1b338-342">The response</span></span>

<span data-ttu-id="1b338-343">If there are insights available for the image, the response contains one or more `tags` that contain the insights.</span><span class="sxs-lookup"><span data-stu-id="1b338-343">If there are insights available for the image, the response contains one or more `tags` that contain the insights.</span></span> <span data-ttu-id="1b338-344">The `image` field contains the insights token for the input image.</span><span class="sxs-lookup"><span data-stu-id="1b338-344">The `image` field contains the insights token for the input image.</span></span>

```json
{
  "_type" : "ImageKnowledge",
  "tags" : [
    {...},
    {...},
    {...},
    {...},
    {...}
  ],
  "image" : {
    "imageInsightsToken" : "bcid_AF8C9CA409421B..."
  }
}
```

<span data-ttu-id="1b338-345">The `tags` field contains a display name and list of actions (insights).</span><span class="sxs-lookup"><span data-stu-id="1b338-345">The `tags` field contains a display name and list of actions (insights).</span></span> <span data-ttu-id="1b338-346">One of the tags contains a `displayName` field that is set to an empty string.</span><span class="sxs-lookup"><span data-stu-id="1b338-346">One of the tags contains a `displayName` field that is set to an empty string.</span></span> <span data-ttu-id="1b338-347">This tag contains the default insights such as webpages that include the image, visually similar images, and shopping sources for items found in the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-347">This tag contains the default insights such as webpages that include the image, visually similar images, and shopping sources for items found in the image.</span></span> <span data-ttu-id="1b338-348">Because the entire image is of interest, the default insights tag doesn't include bounding boxes for the regions of interest.</span><span class="sxs-lookup"><span data-stu-id="1b338-348">Because the entire image is of interest, the default insights tag doesn't include bounding boxes for the regions of interest.</span></span>


```json
{
  "_type" : "ImageKnowledge",
  "tags" : [
    {
      "displayName" : "",
      "actions" : [
        {...},
        {...},
        {...},
        {...}
      ]
    },
    {...},
    {...},
    {...},
    {...}
  ],
  "image" : {
    "imageInsightsToken" : "bcid_AF8C9CA409421B..."
  }
}
```

<span data-ttu-id="1b338-349">For a list of the default insights, see [Default insights](./default-insights-tag.md).</span><span class="sxs-lookup"><span data-stu-id="1b338-349">For a list of the default insights, see [Default insights](./default-insights-tag.md).</span></span>



<span data-ttu-id="1b338-350">The remaining tags contain other insights that may be of interest to the user.</span><span class="sxs-lookup"><span data-stu-id="1b338-350">The remaining tags contain other insights that may be of interest to the user.</span></span> <span data-ttu-id="1b338-351">For example, if the image contains text, one of the tags may include a TextResults insight, which contains the recognized text.</span><span class="sxs-lookup"><span data-stu-id="1b338-351">For example, if the image contains text, one of the tags may include a TextResults insight, which contains the recognized text.</span></span> <span data-ttu-id="1b338-352">Or, if Bing recognizes an entity (person, place, or thing) in the image, one of the tags may identify the entity.</span><span class="sxs-lookup"><span data-stu-id="1b338-352">Or, if Bing recognizes an entity (person, place, or thing) in the image, one of the tags may identify the entity.</span></span> <span data-ttu-id="1b338-353">Visual Search also returns a diverse set of terms (tags) derived from the input image.</span><span class="sxs-lookup"><span data-stu-id="1b338-353">Visual Search also returns a diverse set of terms (tags) derived from the input image.</span></span> <span data-ttu-id="1b338-354">These tags allow users to explore concepts found in the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-354">These tags allow users to explore concepts found in the image.</span></span> <span data-ttu-id="1b338-355">For example, if the input image is of a famous athlete, one of the tags might be Sports, which contains links to images of sports.</span><span class="sxs-lookup"><span data-stu-id="1b338-355">For example, if the input image is of a famous athlete, one of the tags might be Sports, which contains links to images of sports.</span></span>

<span data-ttu-id="1b338-356">Each tag includes a display name that you can use to categorize the insight, bounding box that identifies the region of interest that the insight applies to, the insights themselves, and a thumbnail of the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-356">Each tag includes a display name that you can use to categorize the insight, bounding box that identifies the region of interest that the insight applies to, the insights themselves, and a thumbnail of the image.</span></span> <span data-ttu-id="1b338-357">For example, if the image is of a person wearing a sports jersey, one of the tags might include a bounding box that bounds the jersey and includes VisualSearch and ProductVisualSearch insights.</span><span class="sxs-lookup"><span data-stu-id="1b338-357">For example, if the image is of a person wearing a sports jersey, one of the tags might include a bounding box that bounds the jersey and includes VisualSearch and ProductVisualSearch insights.</span></span> <span data-ttu-id="1b338-358">And another tag might include an ImageResults insight that contains a URL for an /images/search API request to get images that are topically related or a Bing.com search URL that takes the user to the Bing.com image search results.</span><span class="sxs-lookup"><span data-stu-id="1b338-358">And another tag might include an ImageResults insight that contains a URL for an /images/search API request to get images that are topically related or a Bing.com search URL that takes the user to the Bing.com image search results.</span></span>

<span data-ttu-id="1b338-359">All tags other than the default insights tag include bounding boxes that identify regions of interest in the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-359">All tags other than the default insights tag include bounding boxes that identify regions of interest in the image.</span></span> <span data-ttu-id="1b338-360">For example, if the image includes multiple recognized people, tags could include bounding boxes for each of the people, or if the image contains recognized clothing items, tags could include bounding boxes for each recognized clothing item.</span><span class="sxs-lookup"><span data-stu-id="1b338-360">For example, if the image includes multiple recognized people, tags could include bounding boxes for each of the people, or if the image contains recognized clothing items, tags could include bounding boxes for each recognized clothing item.</span></span> <span data-ttu-id="1b338-361">You can use the bounding boxes to create hot spots over the image that when clicked, provide details about the contents in that region of the image.</span><span class="sxs-lookup"><span data-stu-id="1b338-361">You can use the bounding boxes to create hot spots over the image that when clicked, provide details about the contents in that region of the image.</span></span> <span data-ttu-id="1b338-362">You should not include hot spots in an image for bounding boxes that identify the entire image.</span><span class="sxs-lookup"><span data-stu-id="1b338-362">You should not include hot spots in an image for bounding boxes that identify the entire image.</span></span>

### <a name="text-recognition"></a><span data-ttu-id="1b338-363">Text recognition</span><span class="sxs-lookup"><span data-stu-id="1b338-363">Text recognition</span></span>

<span data-ttu-id="1b338-364">If the image contains text that the service recognizes, one of the tags will contain a TextResults insight (action).</span><span class="sxs-lookup"><span data-stu-id="1b338-364">If the image contains text that the service recognizes, one of the tags will contain a TextResults insight (action).</span></span> <span data-ttu-id="1b338-365">The insight's `displayName` contains the recognized text.</span><span class="sxs-lookup"><span data-stu-id="1b338-365">The insight's `displayName` contains the recognized text.</span></span> 

```json
    {
        "image" : {
            "thumbnailUrl" : "https:\/\/tse3.mm.bing.net\/th?q=%23%23Text..."
        },
        "displayName" : "##TextRecognition",
        "boundingBox" : {
            "queryRectangle" : {
                "topLeft" : {"x" : 0, "y" : 0},
                "topRight" : {"x" : 1, "y" : 0},
                "bottomRight" : {"x" : 1, "y" : 1},
                "bottomLeft" : {"x" : 0, "y" : 1}
            },
            "displayRectangle" : {
                "topLeft" : {"x" : 0, "y" : 0},
                "topRight" : {"x" : 1, "y" : 0},
                "bottomRight" : {"x" : 1, "y" : 1},
                "bottomLeft" : {"x" : 0, "y" : 1}
            }
        },
        "actions" : [{
            "displayName" : "WALK BIKE ACROSS BRIDGE",
            "actionType" : "TextResults"
        }],
        "sources" : ["OCR"]
    }
```

<span data-ttu-id="1b338-366">Because the tag's `displayName` field contains ##TextRecognition, do not use it as a category title in the UX.</span><span class="sxs-lookup"><span data-stu-id="1b338-366">Because the tag's `displayName` field contains ##TextRecognition, do not use it as a category title in the UX.</span></span> <span data-ttu-id="1b338-367">That goes for any display name that starts with ##.</span><span class="sxs-lookup"><span data-stu-id="1b338-367">That goes for any display name that starts with ##.</span></span> <span data-ttu-id="1b338-368">Instead use the action's display name.</span><span class="sxs-lookup"><span data-stu-id="1b338-368">Instead use the action's display name.</span></span>


<span data-ttu-id="1b338-369">Text recognition can also recognize the contact information on business cards, such as phone numbers and email addresses.</span><span class="sxs-lookup"><span data-stu-id="1b338-369">Text recognition can also recognize the contact information on business cards, such as phone numbers and email addresses.</span></span> <span data-ttu-id="1b338-370">The bounding box identifies the location of the contact information on the card.</span><span class="sxs-lookup"><span data-stu-id="1b338-370">The bounding box identifies the location of the contact information on the card.</span></span> 

```json
    {
      "image" : {
        "thumbnailUrl" : "https:\/\/tse3.mm.bing.net\/th?q=%23%23TextRecognition..."
      },
      "displayName" : "##TextRecognition",
      "boundingBox" : {
        "queryRectangle" : {
          "topLeft" : {"x" : 0.635, "y" : 0},
          "topRight" : {"x" : 0.77, "y" : 0},
          "bottomRight" : {"x" : 0.77, "y" : 0.4873333},
          "bottomLeft" : {"x" : 0.635, "y" : 0.4873333}
        },
        "displayRectangle" : {
          "topLeft" : {"x" : 0.635, "y" : 0},
          "topRight" : {"x" : 0.77, "y" : 0},
          "bottomRight" : {"x" : 0.77, "y" : 0.4873333},
          "bottomLeft" : {"x" : 0.635, "y" : 0.4873333}
        }
      },
      "actions" : [
        {
          "url" : "tel:888%20555%201212",
          "actionType" : "Uri"
        }
      ],
      "sources" : ["OCR"]
    },
    {
      "image" : {
        "thumbnailUrl" : "https:\/\/tse3.mm.bing.net\/th?q=%23%23TextRecognition..."
      },
      "displayName" : "##TextRecognition",
      "boundingBox" : {
        "queryRectangle" : {
          "topLeft" : {"x" : 0.63, "y" : 0},
          "topRight" : {"x" : 0.866, "y" : 0},
          "bottomRight" : {"x" : 0.866, "y" : 0.5553334},
          "bottomLeft" : {"x" : 0.63, "y" : 0.5553334}
        },
        "displayRectangle" : {
          "topLeft" : {"x" : 0.63, "y" : 0},
          "topRight" : {"x" : 0.866, "y" : 0},
          "bottomRight" : {"x" : 0.866, "y" : 0.5553334},
          "bottomLeft" : {"x" : 0.63, "y" : 0.5553334}
        }
      },
      "actions" : [
        {
          "url" : "mailto:someone@outlook.com",
          "actionType" : "Uri"
        }
      ],
      "sources" : ["OCR"]
    },
    {
      "image" : {
        "thumbnailUrl" : "https:\/\/tse3.mm.bing.net\/th?q=%23%23TextRecognition..."
      },
      "displayName" : "##TextRecognition",
      "boundingBox" : {
        "queryRectangle" : {
          "topLeft" : {"x" : 0, "y" : 0},
          "topRight" : {"x" : 1, "y" : 0},
          "bottomRight" : {"x" : 1, "y" : 1},
          "bottomLeft" : {"x" : 0, "y" : 1}
        },
        "displayRectangle" : {
          "topLeft" : {"x" : 0, "y" : 0},
          "topRight" : {"x" : 1, "y" : 0},
          "bottomRight" : {"x" : 1, "y" : 1},
          "bottomLeft" : {"x" : 0, "y" : 1}
        }
      },
      "actions" : [
        {
          "displayName" : "CHARLENE WHITNEY Graphic Designer 888 555 1212 someone@outlook.com www.contoso.com",
          "actionType" : "TextResults"
        }
      ],
      "sources" : ["OCR"]
    }
```

<span data-ttu-id="1b338-371">If the image contains a recognized entity such as a person, place, or thing, one of the tags may include an Entity insight.</span><span class="sxs-lookup"><span data-stu-id="1b338-371">If the image contains a recognized entity such as a person, place, or thing, one of the tags may include an Entity insight.</span></span> 

```json
    {
      "image" : {
        "thumbnailUrl" : "https:\/\/tse4.mm.bing.net\/th?q=Statue+of+Liberty..."
      },
      "displayName" : "Statue of Liberty",
      "boundingBox" : {
        "queryRectangle" : {
          "topLeft" : {"x" : 0.40625, "y" : 0.1757813},
          "topRight" : {"x" : 0.6171875, "y" : 0.1757813},
          "bottomRight" : {"x" : 0.6171875, "y" : 0.3867188},
          "bottomLeft" : {"x" : 0.40625, "y" : 0.3867188}
        },
        "displayRectangle" : {
          "topLeft" : {"x" : 0.40625, "y" : 0.1757813},
          "topRight" : {"x" : 0.6171875, "y" : 0.1757813},
          "bottomRight" : {"x" : 0.6171875, "y" : 0.3867188},
          "bottomLeft" : {"x" : 0.40625, "y" : 0.3867188}
        }
      },
      "actions" : [
        {
          "_type" : "ImageEntityAction",
          "webSearchUrl" : "https:\/\/www.bing.com\/search?q=Statue+of+Liberty",
          "displayName" : "Statue of Liberty",
          "actionType" : "Entity",
        }
      ]
    }
```



## <a name="next-steps"></a><span data-ttu-id="1b338-372">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b338-372">Next steps</span></span>

<span data-ttu-id="1b338-373">To get started quickly with your first request, see the quickstarts: [C#](quickstarts/csharp.md) | [Java](quickstarts/java.md) | [node.js](quickstarts/nodejs.md) | [Python](quickstarts/python.md).</span><span class="sxs-lookup"><span data-stu-id="1b338-373">To get started quickly with your first request, see the quickstarts: [C#](quickstarts/csharp.md) | [Java](quickstarts/java.md) | [node.js](quickstarts/nodejs.md) | [Python](quickstarts/python.md).</span></span>

<span data-ttu-id="1b338-374">Try out the API.</span><span class="sxs-lookup"><span data-stu-id="1b338-374">Try out the API.</span></span> <span data-ttu-id="1b338-375">Go to [Visual Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/878c38e705b84442845e22c7bff8c9ac).</span><span class="sxs-lookup"><span data-stu-id="1b338-375">Go to [Visual Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/878c38e705b84442845e22c7bff8c9ac).</span></span> 


<span data-ttu-id="1b338-376">Familiarize yourself with the [Visual Search API Reference](https://aka.ms/bingvisualsearchreferencedoc).</span><span class="sxs-lookup"><span data-stu-id="1b338-376">Familiarize yourself with the [Visual Search API Reference](https://aka.ms/bingvisualsearchreferencedoc).</span></span> <span data-ttu-id="1b338-377">The reference contains the list of endpoints, headers, and query parameters that you'd use to request search results.</span><span class="sxs-lookup"><span data-stu-id="1b338-377">The reference contains the list of endpoints, headers, and query parameters that you'd use to request search results.</span></span> <span data-ttu-id="1b338-378">It also includes definitions of the response objects.</span><span class="sxs-lookup"><span data-stu-id="1b338-378">It also includes definitions of the response objects.</span></span> 

<span data-ttu-id="1b338-379">Be sure to read [Bing Use and Display Requirements](./use-and-display-requirements.md) so you don't break any of the rules about using the search results.</span><span class="sxs-lookup"><span data-stu-id="1b338-379">Be sure to read [Bing Use and Display Requirements](./use-and-display-requirements.md) so you don't break any of the rules about using the search results.</span></span>


