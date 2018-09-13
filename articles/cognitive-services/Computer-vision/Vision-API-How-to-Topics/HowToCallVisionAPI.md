---
title: Call the Computer Vision API | Microsoft Docs
description: Learn how to call the Computer Vision API by using REST in Cognitive Services.
services: cognitive-services
author: JuliaNik
manager: ytkuo
ms.service: cognitive-services
ms.technology: computer-vision
ms.topic: article
ms.date: 01/20/2017
ms.author: juliakuz
ms.openlocfilehash: 95ac8106bd374c586d4a288bbc406d0de2eb59ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549163"
---
# <a name="how-to-call-computer-vision-api"></a><span data-ttu-id="8c187-103">How to Call Computer Vision API</span><span class="sxs-lookup"><span data-stu-id="8c187-103">How to Call Computer Vision API</span></span>

<span data-ttu-id="8c187-104">This guide demonstrates how to call Computer Vision API using REST.</span><span class="sxs-lookup"><span data-stu-id="8c187-104">This guide demonstrates how to call Computer Vision API using REST.</span></span> <span data-ttu-id="8c187-105">The samples are written both in C# using the Computer Vision API client library, and as HTTP POST/GET calls.</span><span class="sxs-lookup"><span data-stu-id="8c187-105">The samples are written both in C# using the Computer Vision API client library, and as HTTP POST/GET calls.</span></span> <span data-ttu-id="8c187-106">We will focus on:</span><span class="sxs-lookup"><span data-stu-id="8c187-106">We will focus on:</span></span>

-   <span data-ttu-id="8c187-107">How to get "Tags", "Description" and "Categories".</span><span class="sxs-lookup"><span data-stu-id="8c187-107">How to get "Tags", "Description" and "Categories".</span></span>
-   <span data-ttu-id="8c187-108">How to get "Domain-specific" information (celebrities).</span><span class="sxs-lookup"><span data-stu-id="8c187-108">How to get "Domain-specific" information (celebrities).</span></span>

### <span data-ttu-id="8c187-109"><a name="Prerequisites">Prerequisites</a></span><span class="sxs-lookup"><span data-stu-id="8c187-109"><a name="Prerequisites">Prerequisites</a></span></span> 
<span data-ttu-id="8c187-110">Image URL or path to locally stored image.</span><span class="sxs-lookup"><span data-stu-id="8c187-110">Image URL or path to locally stored image.</span></span>
  * <span data-ttu-id="8c187-111">Supported input methods: Raw image binary in the form of an application/octet stream or image URL</span><span class="sxs-lookup"><span data-stu-id="8c187-111">Supported input methods: Raw image binary in the form of an application/octet stream or image URL</span></span>
  * <span data-ttu-id="8c187-112">Supported image formats: JPEG, PNG, GIF, BMP</span><span class="sxs-lookup"><span data-stu-id="8c187-112">Supported image formats: JPEG, PNG, GIF, BMP</span></span>
  * <span data-ttu-id="8c187-113">Image file size: Less than 4MB</span><span class="sxs-lookup"><span data-stu-id="8c187-113">Image file size: Less than 4MB</span></span>
  * <span data-ttu-id="8c187-114">Image dimension: Greater than 50 x 50 pixels</span><span class="sxs-lookup"><span data-stu-id="8c187-114">Image dimension: Greater than 50 x 50 pixels</span></span>
  
<span data-ttu-id="8c187-115">In the examples below, the following features are demonstrated:</span><span class="sxs-lookup"><span data-stu-id="8c187-115">In the examples below, the following features are demonstrated:</span></span>

1. <span data-ttu-id="8c187-116">Analyzing an image and getting an array of tags and a description returned.</span><span class="sxs-lookup"><span data-stu-id="8c187-116">Analyzing an image and getting an array of tags and a description returned.</span></span>
2. <span data-ttu-id="8c187-117">Analyzing an image with a domain-specific model (specifically, "celebrities"  model) and getting the corresponding result in JSON retune.</span><span class="sxs-lookup"><span data-stu-id="8c187-117">Analyzing an image with a domain-specific model (specifically, "celebrities"  model) and getting the corresponding result in JSON retune.</span></span>

<span data-ttu-id="8c187-118">Features are broken down on:</span><span class="sxs-lookup"><span data-stu-id="8c187-118">Features are broken down on:</span></span>

  * <span data-ttu-id="8c187-119">**Option One:** Scoped Analysis - Analyze only a given model</span><span class="sxs-lookup"><span data-stu-id="8c187-119">**Option One:** Scoped Analysis - Analyze only a given model</span></span>
  * <span data-ttu-id="8c187-120">**Option Two:** Enhanced Analysis - Analyze to provide additional details with [86-categories taxonomy](../Category-Taxonomy.md)</span><span class="sxs-lookup"><span data-stu-id="8c187-120">**Option Two:** Enhanced Analysis - Analyze to provide additional details with [86-categories taxonomy](../Category-Taxonomy.md)</span></span>
  
### <span data-ttu-id="8c187-121"><a name="Step1">Step 1: Authorize the API call</a></span><span class="sxs-lookup"><span data-stu-id="8c187-121"><a name="Step1">Step 1: Authorize the API call</a></span></span> 
<span data-ttu-id="8c187-122">Every call to the Computer Vision API requires a subscription key.</span><span class="sxs-lookup"><span data-stu-id="8c187-122">Every call to the Computer Vision API requires a subscription key.</span></span> <span data-ttu-id="8c187-123">This key needs to be either passed through a query string parameter or specified in the request header.</span><span class="sxs-lookup"><span data-stu-id="8c187-123">This key needs to be either passed through a query string parameter or specified in the request header.</span></span> 

<span data-ttu-id="8c187-124">To obtain a subscription key, see [How to Obtain Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md
).</span><span class="sxs-lookup"><span data-stu-id="8c187-124">To obtain a subscription key, see [How to Obtain Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md
).</span></span>

<span data-ttu-id="8c187-125">**1.** Passing the subscription key through a query string, see below as a Computer Vision API example:</span><span class="sxs-lookup"><span data-stu-id="8c187-125">**1.** Passing the subscription key through a query string, see below as a Computer Vision API example:</span></span>

```https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Description,Tags&subscription-key=<Your subscription key>```

<span data-ttu-id="8c187-126">**2.** Passing the subscription key can also be specified in the HTTP request header:</span><span class="sxs-lookup"><span data-stu-id="8c187-126">**2.** Passing the subscription key can also be specified in the HTTP request header:</span></span>

```ocp-apim-subscription-key: <Your subscription key>```

<span data-ttu-id="8c187-127">**3.** When using the client library, the subscription key is passed in through the constructor of VisionServiceClient:</span><span class="sxs-lookup"><span data-stu-id="8c187-127">**3.** When using the client library, the subscription key is passed in through the constructor of VisionServiceClient:</span></span>

```var visionClient = new VisionServiceClient(“Your subscriptionKey”);```

### <span data-ttu-id="8c187-128"><a name="Step2">Step 2: Upload an image to the Computer Vision API service and get back tags, descriptions and celebrities</a></span><span class="sxs-lookup"><span data-stu-id="8c187-128"><a name="Step2">Step 2: Upload an image to the Computer Vision API service and get back tags, descriptions and celebrities</a></span></span>
<span data-ttu-id="8c187-129">The basic way to perform the Computer Vision API call is by uploading an image directly.</span><span class="sxs-lookup"><span data-stu-id="8c187-129">The basic way to perform the Computer Vision API call is by uploading an image directly.</span></span> <span data-ttu-id="8c187-130">This is done by sending a "POST" request with application/octet-stream content type together with the data read from the image.</span><span class="sxs-lookup"><span data-stu-id="8c187-130">This is done by sending a "POST" request with application/octet-stream content type together with the data read from the image.</span></span> <span data-ttu-id="8c187-131">For "Tags" and "Description", this upload method will be the same for all the Computer Vision API calls.</span><span class="sxs-lookup"><span data-stu-id="8c187-131">For "Tags" and "Description", this upload method will be the same for all the Computer Vision API calls.</span></span> <span data-ttu-id="8c187-132">The only difference will be the query parameters the user specifies.</span><span class="sxs-lookup"><span data-stu-id="8c187-132">The only difference will be the query parameters the user specifies.</span></span> 

<span data-ttu-id="8c187-133">Here’s how to get "Tags" and "Description" for a given image:</span><span class="sxs-lookup"><span data-stu-id="8c187-133">Here’s how to get "Tags" and "Description" for a given image:</span></span>

<span data-ttu-id="8c187-134">**Option One:** Get list of "Tags" and one "Description"</span><span class="sxs-lookup"><span data-stu-id="8c187-134">**Option One:** Get list of "Tags" and one "Description"</span></span>
```
POST https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Description,Tags&subscription-key=<Your subscription key>
```
```
using Microsoft.ProjectOxford.Vision;
using Microsoft.ProjectOxford.Vision.Contract;
using System.IO;

AnalysisResult analysisResult;
var features = new VisualFeature[] { VisualFeature.Tags, VisualFeature.Description };

using (var fs = new FileStream(@"C:\Vision\Sample.jpg", FileMode.Open))
{
  analysisResult = await visionClient.AnalyzeImageAsync(fs, features);
}
```
<span data-ttu-id="8c187-135">**Option Two** Get list of "Tags" only, or list of "Description" only:</span><span class="sxs-lookup"><span data-stu-id="8c187-135">**Option Two** Get list of "Tags" only, or list of "Description" only:</span></span>

###### <a name="tags-only"></a><span data-ttu-id="8c187-136">Tags-only:</span><span class="sxs-lookup"><span data-stu-id="8c187-136">Tags-only:</span></span>
```
POST https://westus.api.cognitive.microsoft.com/vision/v1.0/tag&subscription-key=<Your subscription key>
var analysisResult = await visionClient.GetTagsAsync("http://contoso.com/example.jpg");
```

###### <a name="description-only"></a><span data-ttu-id="8c187-137">Description-only:</span><span class="sxs-lookup"><span data-stu-id="8c187-137">Description-only:</span></span>
```
POST https://westus.api.cognitive.microsoft.com/vision/v1.0/describe&subscription-key=<Your subscription key>
using (var fs = new FileStream(@"C:\Vision\Sample.jpg", FileMode.Open))
{
  analysisResult = await visionClient.DescribeAsync(fs);
}
```
### <a name="here-is-how-to-get-domain-specific-analysis-in-our-case-for-celebrities"></a><span data-ttu-id="8c187-138">Here is how to get domain-specific analysis (in our case, for celebrities).</span><span class="sxs-lookup"><span data-stu-id="8c187-138">Here is how to get domain-specific analysis (in our case, for celebrities).</span></span>

<span data-ttu-id="8c187-139">**Option One:** Scoped Analysis - Analyze only a given model</span><span class="sxs-lookup"><span data-stu-id="8c187-139">**Option One:** Scoped Analysis - Analyze only a given model</span></span>
```
POST https://westus.api.cognitive.microsoft.com/vision/v1.0/models/celebrities/analyze
var celebritiesResult = await visionClient.AnalyzeImageInDomainAsync(url, "celebrities");
```
<span data-ttu-id="8c187-140">For this option, all other query parameters {visualFeatures, details} are not valid.</span><span class="sxs-lookup"><span data-stu-id="8c187-140">For this option, all other query parameters {visualFeatures, details} are not valid.</span></span> <span data-ttu-id="8c187-141">If you want to see all supported models, use:</span><span class="sxs-lookup"><span data-stu-id="8c187-141">If you want to see all supported models, use:</span></span> 
```
GET https://westus.api.cognitive.microsoft.com/vision/v1.0/models 
var models = await visionClient.ListModelsAsync();
```
<span data-ttu-id="8c187-142">**Option Two:** Enhanced Analysis - Analyze to provide additional details with [86-categories taxonomy](../Category-Taxonomy.md)</span><span class="sxs-lookup"><span data-stu-id="8c187-142">**Option Two:** Enhanced Analysis - Analyze to provide additional details with [86-categories taxonomy](../Category-Taxonomy.md)</span></span>

<span data-ttu-id="8c187-143">For applications where you want to get generic image analysis in addition to details from one or more domain-specific models, we extend the v1 API with the models query parameter.</span><span class="sxs-lookup"><span data-stu-id="8c187-143">For applications where you want to get generic image analysis in addition to details from one or more domain-specific models, we extend the v1 API with the models query parameter.</span></span>
```
POST https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?details=celebrities
```
<span data-ttu-id="8c187-144">When this method is invoked, we will call the 86-category classifier first.</span><span class="sxs-lookup"><span data-stu-id="8c187-144">When this method is invoked, we will call the 86-category classifier first.</span></span> <span data-ttu-id="8c187-145">If any of the categories match that of a known/matching model, a second pass of classifier invocations will occur.</span><span class="sxs-lookup"><span data-stu-id="8c187-145">If any of the categories match that of a known/matching model, a second pass of classifier invocations will occur.</span></span> <span data-ttu-id="8c187-146">For example, if "details=all", or "details" include ‘celebrities’, we will call the celebrities model after the 86-category classifier is called and the result includes the category person.</span><span class="sxs-lookup"><span data-stu-id="8c187-146">For example, if "details=all", or "details" include ‘celebrities’, we will call the celebrities model after the 86-category classifier is called and the result includes the category person.</span></span> <span data-ttu-id="8c187-147">This will increase latency for users interested in celebrities, compared to Option One.</span><span class="sxs-lookup"><span data-stu-id="8c187-147">This will increase latency for users interested in celebrities, compared to Option One.</span></span>

<span data-ttu-id="8c187-148">All v1 query parameters will behave the same in this case.</span><span class="sxs-lookup"><span data-stu-id="8c187-148">All v1 query parameters will behave the same in this case.</span></span>  <span data-ttu-id="8c187-149">If visualFeatures=categories is not specified, it will be implicitly enabled.</span><span class="sxs-lookup"><span data-stu-id="8c187-149">If visualFeatures=categories is not specified, it will be implicitly enabled.</span></span>

### <span data-ttu-id="8c187-150"><a name="Step3">Step 3: Retrieving and understanding the JSON output for analyze&visualFeatures=Tags, Description</a></span><span class="sxs-lookup"><span data-stu-id="8c187-150"><a name="Step3">Step 3: Retrieving and understanding the JSON output for analyze&visualFeatures=Tags, Description</a></span></span>

<span data-ttu-id="8c187-151">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="8c187-151">Here's an example:</span></span>
```
  {
    “tags”: [
    {
    "name": "outdoor",
        "score": 0.976
    },
    {
    "name": "bird",
        "score": 0.95
    }
            ],
    “description”: 
    {
    "tags": [
    "outdoor",
    "bird"
            ],
    "captions": [
    {
    "text”: “partridge in a pear tree”,
            “confidence”: 0.96
    }
                ]
    }
  }
```
<span data-ttu-id="8c187-152">Field</span><span class="sxs-lookup"><span data-stu-id="8c187-152">Field</span></span>   | <span data-ttu-id="8c187-153">Type</span><span class="sxs-lookup"><span data-stu-id="8c187-153">Type</span></span>  | <span data-ttu-id="8c187-154">Content</span><span class="sxs-lookup"><span data-stu-id="8c187-154">Content</span></span>
------|------|------|
<span data-ttu-id="8c187-155">Tags</span><span class="sxs-lookup"><span data-stu-id="8c187-155">Tags</span></span>    | <span data-ttu-id="8c187-156">object</span><span class="sxs-lookup"><span data-stu-id="8c187-156">object</span></span>    | <span data-ttu-id="8c187-157">Top-level object for array of tags</span><span class="sxs-lookup"><span data-stu-id="8c187-157">Top-level object for array of tags</span></span>
<span data-ttu-id="8c187-158">tags[].Name</span><span class="sxs-lookup"><span data-stu-id="8c187-158">tags[].Name</span></span> | <span data-ttu-id="8c187-159">string</span><span class="sxs-lookup"><span data-stu-id="8c187-159">string</span></span>    | <span data-ttu-id="8c187-160">Keyword from tags classifier</span><span class="sxs-lookup"><span data-stu-id="8c187-160">Keyword from tags classifier</span></span>
<span data-ttu-id="8c187-161">tags[].Score</span><span class="sxs-lookup"><span data-stu-id="8c187-161">tags[].Score</span></span>    | <span data-ttu-id="8c187-162">number</span><span class="sxs-lookup"><span data-stu-id="8c187-162">number</span></span>    | <span data-ttu-id="8c187-163">Confidence score, between 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="8c187-163">Confidence score, between 0 and 1.</span></span>
<span data-ttu-id="8c187-164">description</span><span class="sxs-lookup"><span data-stu-id="8c187-164">description</span></span>  | <span data-ttu-id="8c187-165">object</span><span class="sxs-lookup"><span data-stu-id="8c187-165">object</span></span>   | <span data-ttu-id="8c187-166">Top-level object for a description.</span><span class="sxs-lookup"><span data-stu-id="8c187-166">Top-level object for a description.</span></span>
<span data-ttu-id="8c187-167">description.tags[]</span><span class="sxs-lookup"><span data-stu-id="8c187-167">description.tags[]</span></span> |    <span data-ttu-id="8c187-168">string</span><span class="sxs-lookup"><span data-stu-id="8c187-168">string</span></span>  | <span data-ttu-id="8c187-169">List of tags.</span><span class="sxs-lookup"><span data-stu-id="8c187-169">List of tags.</span></span>  <span data-ttu-id="8c187-170">If there insufficient confidence in the ability to produce a caption, the tags maybe the only information available to the caller.</span><span class="sxs-lookup"><span data-stu-id="8c187-170">If there insufficient confidence in the ability to produce a caption, the tags maybe the only information available to the caller.</span></span>
<span data-ttu-id="8c187-171">description.captions[].text</span><span class="sxs-lookup"><span data-stu-id="8c187-171">description.captions[].text</span></span> | <span data-ttu-id="8c187-172">string</span><span class="sxs-lookup"><span data-stu-id="8c187-172">string</span></span>    | <span data-ttu-id="8c187-173">A phrase describing the image.</span><span class="sxs-lookup"><span data-stu-id="8c187-173">A phrase describing the image.</span></span>
<span data-ttu-id="8c187-174">description.captions[].confidence</span><span class="sxs-lookup"><span data-stu-id="8c187-174">description.captions[].confidence</span></span>   | <span data-ttu-id="8c187-175">number</span><span class="sxs-lookup"><span data-stu-id="8c187-175">number</span></span>    | <span data-ttu-id="8c187-176">Confidence for the phrase.</span><span class="sxs-lookup"><span data-stu-id="8c187-176">Confidence for the phrase.</span></span>

### <span data-ttu-id="8c187-177"><a name="Step4">Step 4: Retrieving and understanding the JSON output of domain-specific models</a></span><span class="sxs-lookup"><span data-stu-id="8c187-177"><a name="Step4">Step 4: Retrieving and understanding the JSON output of domain-specific models</a></span></span>

<span data-ttu-id="8c187-178">**Option One:** Scoped Analysis - Analyze only a given model</span><span class="sxs-lookup"><span data-stu-id="8c187-178">**Option One:** Scoped Analysis - Analyze only a given model</span></span>

<span data-ttu-id="8c187-179">The output will be an array of tags, an example will be like this example:</span><span class="sxs-lookup"><span data-stu-id="8c187-179">The output will be an array of tags, an example will be like this example:</span></span>
```
  { 
    "result": [ 
      { 
    "name": "golden retriever", 
    "score": 0.98
    },
    { 
    "name": "Labrador retriever", 
    "score": 0.78
    }
              ]
  }
```

<span data-ttu-id="8c187-180">**Option Two:** Enhanced Analysis - Analyze to provide additional details with 86-categories taxonomy</span><span class="sxs-lookup"><span data-stu-id="8c187-180">**Option Two:** Enhanced Analysis - Analyze to provide additional details with 86-categories taxonomy</span></span>

<span data-ttu-id="8c187-181">For domain-specific models using Option Two (Enhanced Analysis), the categories return type is extended.</span><span class="sxs-lookup"><span data-stu-id="8c187-181">For domain-specific models using Option Two (Enhanced Analysis), the categories return type is extended.</span></span> <span data-ttu-id="8c187-182">An example follows:</span><span class="sxs-lookup"><span data-stu-id="8c187-182">An example follows:</span></span>
```
  {
    "requestId": "87e44580-925a-49c8-b661-d1c54d1b83b5",
    "metadata":     {
      "width": 640,
      "height": 430,
      "format": "Jpeg"
                    },
    "result": {
      "celebrities": 
      [
        {
        "name": "Richard Nixon",
        "faceRectangle": {
          "left": 107,
          "top": 98,
          "width": 165,
          "height": 165
                         },
        "confidence": 0.9999827
        }
      ]
  }
```

<span data-ttu-id="8c187-183">The categories field is a list of one or more of the [86-categories](../Category-Taxonomy.md) in the original taxonomy.</span><span class="sxs-lookup"><span data-stu-id="8c187-183">The categories field is a list of one or more of the [86-categories](../Category-Taxonomy.md) in the original taxonomy.</span></span> <span data-ttu-id="8c187-184">Note also that categories ending in an underscore will match that category and its children (for example, people_ as well as people_group, for celebrities model).</span><span class="sxs-lookup"><span data-stu-id="8c187-184">Note also that categories ending in an underscore will match that category and its children (for example, people_ as well as people_group, for celebrities model).</span></span>

<span data-ttu-id="8c187-185">Field</span><span class="sxs-lookup"><span data-stu-id="8c187-185">Field</span></span>   | <span data-ttu-id="8c187-186">Type</span><span class="sxs-lookup"><span data-stu-id="8c187-186">Type</span></span>  | <span data-ttu-id="8c187-187">Content</span><span class="sxs-lookup"><span data-stu-id="8c187-187">Content</span></span>
------|------|------|
<span data-ttu-id="8c187-188">categories</span><span class="sxs-lookup"><span data-stu-id="8c187-188">categories</span></span> | <span data-ttu-id="8c187-189">object</span><span class="sxs-lookup"><span data-stu-id="8c187-189">object</span></span> | <span data-ttu-id="8c187-190">Top-level object</span><span class="sxs-lookup"><span data-stu-id="8c187-190">Top-level object</span></span>
<span data-ttu-id="8c187-191">categories[].name</span><span class="sxs-lookup"><span data-stu-id="8c187-191">categories[].name</span></span>    | <span data-ttu-id="8c187-192">string</span><span class="sxs-lookup"><span data-stu-id="8c187-192">string</span></span>   | <span data-ttu-id="8c187-193">Name from 86-category taxonomy</span><span class="sxs-lookup"><span data-stu-id="8c187-193">Name from 86-category taxonomy</span></span>
<span data-ttu-id="8c187-194">categories[].score</span><span class="sxs-lookup"><span data-stu-id="8c187-194">categories[].score</span></span>  | <span data-ttu-id="8c187-195">number</span><span class="sxs-lookup"><span data-stu-id="8c187-195">number</span></span>    | <span data-ttu-id="8c187-196">Confidence score, between 0 and 1</span><span class="sxs-lookup"><span data-stu-id="8c187-196">Confidence score, between 0 and 1</span></span>
<span data-ttu-id="8c187-197">categories[].detail</span><span class="sxs-lookup"><span data-stu-id="8c187-197">categories[].detail</span></span>  | <span data-ttu-id="8c187-198">object?</span><span class="sxs-lookup"><span data-stu-id="8c187-198">object?</span></span>      | <span data-ttu-id="8c187-199">Optional detail object</span><span class="sxs-lookup"><span data-stu-id="8c187-199">Optional detail object</span></span>

<span data-ttu-id="8c187-200">Note that if multiple categories match (for example, 86-category classifier returns a score for both people_ and people_young when model=celebrities), the details are attached to the most general level match (people_ in that example.)</span><span class="sxs-lookup"><span data-stu-id="8c187-200">Note that if multiple categories match (for example, 86-category classifier returns a score for both people_ and people_young when model=celebrities), the details are attached to the most general level match (people_ in that example.)</span></span>

### <span data-ttu-id="8c187-201"><a name="Errors">Errors Responses</a></span><span class="sxs-lookup"><span data-stu-id="8c187-201"><a name="Errors">Errors Responses</a></span></span>
<span data-ttu-id="8c187-202">These are identical to vision.analyze, with the additional error of NotSupportedModel error (HTTP 400), which may be returned in both Option One and Option Two scenarios.</span><span class="sxs-lookup"><span data-stu-id="8c187-202">These are identical to vision.analyze, with the additional error of NotSupportedModel error (HTTP 400), which may be returned in both Option One and Option Two scenarios.</span></span> <span data-ttu-id="8c187-203">For Option Two (Enhanced Analysis), if any of the models specified in details are not recognized, the API will return a NotSupportedModel, even if one or more of them are valid.</span><span class="sxs-lookup"><span data-stu-id="8c187-203">For Option Two (Enhanced Analysis), if any of the models specified in details are not recognized, the API will return a NotSupportedModel, even if one or more of them are valid.</span></span>  <span data-ttu-id="8c187-204">Users can call listModels to find out what models are supported.</span><span class="sxs-lookup"><span data-stu-id="8c187-204">Users can call listModels to find out what models are supported.</span></span>

### <span data-ttu-id="8c187-205"><a name="Summary">Summary</a></span><span class="sxs-lookup"><span data-stu-id="8c187-205"><a name="Summary">Summary</a></span></span>

<span data-ttu-id="8c187-206">These are the basic functionalities of the Computer Vision API: how you can upload images and retrieve valuable metadata in return.</span><span class="sxs-lookup"><span data-stu-id="8c187-206">These are the basic functionalities of the Computer Vision API: how you can upload images and retrieve valuable metadata in return.</span></span>

<span data-ttu-id="8c187-207">To use the REST API, go to [Computer Vision API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739).</span><span class="sxs-lookup"><span data-stu-id="8c187-207">To use the REST API, go to [Computer Vision API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739).</span></span>
 
