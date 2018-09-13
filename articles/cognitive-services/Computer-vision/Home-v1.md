---
title: Computer Vision API for Microsoft Cognitive Services | Microsoft Docs
description: Use advanced algorithms in the Computer Vision API to help you process images and return information in Microsoft Cognitive Services.
services: cognitive-services
author: KellyDF
manager: corncar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: article
ms.date: 08/10/2017
ms.author: kefre
ms.openlocfilehash: 86e0441c600162e479c678d3cb1dbeaad423ddb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965680"
---
# <a name="what-is-computer-vision-api-version-10"></a><span data-ttu-id="f6dda-103">What is Computer Vision API Version 1.0?</span><span class="sxs-lookup"><span data-stu-id="f6dda-103">What is Computer Vision API Version 1.0?</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6dda-104">A new version of Computer Vision API is now available, see:</span><span class="sxs-lookup"><span data-stu-id="f6dda-104">A new version of Computer Vision API is now available, see:</span></span>
>- [<span data-ttu-id="f6dda-105">Overview</span><span class="sxs-lookup"><span data-stu-id="f6dda-105">Overview</span></span>](https://docs.microsoft.com/azure/cognitive-services/computer-vision/home)
>- [<span data-ttu-id="f6dda-106">Computer Vision API Version 2.0</span><span class="sxs-lookup"><span data-stu-id="f6dda-106">Computer Vision API Version 2.0</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)

<span data-ttu-id="f6dda-107">The cloud-based Computer Vision API provides developers with access to advanced algorithms for processing images and returning information.</span><span class="sxs-lookup"><span data-stu-id="f6dda-107">The cloud-based Computer Vision API provides developers with access to advanced algorithms for processing images and returning information.</span></span> <span data-ttu-id="f6dda-108">By uploading an image or specifying an image URL, Microsoft Computer Vision algorithms can analyze visual content in different ways based on inputs and user choices.</span><span class="sxs-lookup"><span data-stu-id="f6dda-108">By uploading an image or specifying an image URL, Microsoft Computer Vision algorithms can analyze visual content in different ways based on inputs and user choices.</span></span> <span data-ttu-id="f6dda-109">With the Computer Vision API users can analyze images to:</span><span class="sxs-lookup"><span data-stu-id="f6dda-109">With the Computer Vision API users can analyze images to:</span></span>
* [<span data-ttu-id="f6dda-110">Tag images based on content.</span><span class="sxs-lookup"><span data-stu-id="f6dda-110">Tag images based on content.</span></span>](#Tagging)
* [<span data-ttu-id="f6dda-111">Categorize images.</span><span class="sxs-lookup"><span data-stu-id="f6dda-111">Categorize images.</span></span>](#Categorizing)
* [<span data-ttu-id="f6dda-112">Identify the type and quality of images.</span><span class="sxs-lookup"><span data-stu-id="f6dda-112">Identify the type and quality of images.</span></span>](#Identifying)
* [<span data-ttu-id="f6dda-113">Detect human faces and return their coordinates. </span><span class="sxs-lookup"><span data-stu-id="f6dda-113">Detect human faces and return their coordinates. </span></span>](#Faces)
* [<span data-ttu-id="f6dda-114">Recognize domain-specific content.</span><span class="sxs-lookup"><span data-stu-id="f6dda-114">Recognize domain-specific content.</span></span>](#Domain-Specific)
* [<span data-ttu-id="f6dda-115">Generate descriptions of the content.</span><span class="sxs-lookup"><span data-stu-id="f6dda-115">Generate descriptions of the content.</span></span>](#Descriptions)
* [<span data-ttu-id="f6dda-116">Use optical character recognition to identify printed text found in images.</span><span class="sxs-lookup"><span data-stu-id="f6dda-116">Use optical character recognition to identify printed text found in images.</span></span>](#OCR)
* [<span data-ttu-id="f6dda-117">Recognize handwritten text.</span><span class="sxs-lookup"><span data-stu-id="f6dda-117">Recognize handwritten text.</span></span>](#RecognizeText)
* [<span data-ttu-id="f6dda-118">Distinguish color schemes.</span><span class="sxs-lookup"><span data-stu-id="f6dda-118">Distinguish color schemes.</span></span>](#Color)
* [<span data-ttu-id="f6dda-119">Flag adult content.</span><span class="sxs-lookup"><span data-stu-id="f6dda-119">Flag adult content.</span></span>](#Adult)
* [<span data-ttu-id="f6dda-120">Crop photos to be used as thumbnails.</span><span class="sxs-lookup"><span data-stu-id="f6dda-120">Crop photos to be used as thumbnails.</span></span>](#Thumbnails)

## <a name="requirements"></a><span data-ttu-id="f6dda-121">Requirements</span><span class="sxs-lookup"><span data-stu-id="f6dda-121">Requirements</span></span>
* <span data-ttu-id="f6dda-122">Supported input methods: Raw image binary in the form of an application/octet stream or image URL.</span><span class="sxs-lookup"><span data-stu-id="f6dda-122">Supported input methods: Raw image binary in the form of an application/octet stream or image URL.</span></span>
* <span data-ttu-id="f6dda-123">Supported image formats: JPEG, PNG, GIF, BMP.</span><span class="sxs-lookup"><span data-stu-id="f6dda-123">Supported image formats: JPEG, PNG, GIF, BMP.</span></span>
* <span data-ttu-id="f6dda-124">Image file size: Less than 4 MB.</span><span class="sxs-lookup"><span data-stu-id="f6dda-124">Image file size: Less than 4 MB.</span></span>
* <span data-ttu-id="f6dda-125">Image dimension: Greater than 50 x 50 pixels.</span><span class="sxs-lookup"><span data-stu-id="f6dda-125">Image dimension: Greater than 50 x 50 pixels.</span></span>

## <a name="tagging-images"></a><span data-ttu-id="f6dda-126">Tagging Images</span><span class="sxs-lookup"><span data-stu-id="f6dda-126">Tagging Images</span></span>
<span data-ttu-id="f6dda-127">Computer Vision API returns tags based on more than 2000 recognizable objects, living beings, scenery, and actions.</span><span class="sxs-lookup"><span data-stu-id="f6dda-127">Computer Vision API returns tags based on more than 2000 recognizable objects, living beings, scenery, and actions.</span></span> <span data-ttu-id="f6dda-128">When tags are ambiguous or not common knowledge, the API response provides 'hints' to clarify the meaning of the tag in context of a known setting.</span><span class="sxs-lookup"><span data-stu-id="f6dda-128">When tags are ambiguous or not common knowledge, the API response provides 'hints' to clarify the meaning of the tag in context of a known setting.</span></span> <span data-ttu-id="f6dda-129">Tags are not organized as a taxonomy and no inheritance hierarchies exist.</span><span class="sxs-lookup"><span data-stu-id="f6dda-129">Tags are not organized as a taxonomy and no inheritance hierarchies exist.</span></span> <span data-ttu-id="f6dda-130">A collection of content tags forms the foundation for an image 'description' displayed as human readable language formatted in complete sentences.</span><span class="sxs-lookup"><span data-stu-id="f6dda-130">A collection of content tags forms the foundation for an image 'description' displayed as human readable language formatted in complete sentences.</span></span> <span data-ttu-id="f6dda-131">Note, that at this point English is the only supported language for image description.</span><span class="sxs-lookup"><span data-stu-id="f6dda-131">Note, that at this point English is the only supported language for image description.</span></span>

<span data-ttu-id="f6dda-132">After uploading an image or specifying an image URL, Computer Vision API's algorithms output tags based on the objects, living beings, and actions identified in the image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-132">After uploading an image or specifying an image URL, Computer Vision API's algorithms output tags based on the objects, living beings, and actions identified in the image.</span></span> <span data-ttu-id="f6dda-133">Tagging is not limited to the main subject, such as a person in the foreground, but also includes the setting (indoor or outdoor), furniture, tools, plants, animals, accessories, gadgets etc.</span><span class="sxs-lookup"><span data-stu-id="f6dda-133">Tagging is not limited to the main subject, such as a person in the foreground, but also includes the setting (indoor or outdoor), furniture, tools, plants, animals, accessories, gadgets etc.</span></span>

### <a name="example"></a><span data-ttu-id="f6dda-134">Example</span><span class="sxs-lookup"><span data-stu-id="f6dda-134">Example</span></span>
![House_Yard](./Images/house_yard.jpg) <span data-ttu-id="f6dda-136">'</span><span class="sxs-lookup"><span data-stu-id="f6dda-136">'</span></span>

```json
Returned Json
{
   'tags':[
      {
         "name":"grass",
         "confidence":0.999999761581421
      },
      {
         "name":"outdoor",
         "confidence":0.999970674514771
      },
      {
         "name":"sky",
         "confidence":999289751052856
      },
      {
         "name":"building",
         "confidence":0.996463239192963
      },
      {
         "name":"house",
         "confidence":0.992798030376434
      },
      {
         "name":"lawn",
         "confidence":0.822680294513702
      },
      {
         "name":"green",
         "confidence":0.641222536563873
      },
      {
         "name":"residential",
         "confidence":0.314032256603241
      },
   ],
}
```
## <a name="categorizing-images"></a><span data-ttu-id="f6dda-137">Categorizing Images</span><span class="sxs-lookup"><span data-stu-id="f6dda-137">Categorizing Images</span></span>
<span data-ttu-id="f6dda-138">In addition to tagging and descriptions, Computer Vision API returns the taxonomy-based categories defined in previous versions.</span><span class="sxs-lookup"><span data-stu-id="f6dda-138">In addition to tagging and descriptions, Computer Vision API returns the taxonomy-based categories defined in previous versions.</span></span> <span data-ttu-id="f6dda-139">These categories are organized as a taxonomy with parent/child hereditary hierarchies.</span><span class="sxs-lookup"><span data-stu-id="f6dda-139">These categories are organized as a taxonomy with parent/child hereditary hierarchies.</span></span> <span data-ttu-id="f6dda-140">All categories are in English.</span><span class="sxs-lookup"><span data-stu-id="f6dda-140">All categories are in English.</span></span> <span data-ttu-id="f6dda-141">They can be used alone or with our new models.</span><span class="sxs-lookup"><span data-stu-id="f6dda-141">They can be used alone or with our new models.</span></span>

### <a name="the-86-category-concept"></a><span data-ttu-id="f6dda-142">The 86-category concept</span><span class="sxs-lookup"><span data-stu-id="f6dda-142">The 86-category concept</span></span>
<span data-ttu-id="f6dda-143">Based on a list of 86 concepts seen in the following diagram, visual features found in an image can be categorized ranging from broad to specific.</span><span class="sxs-lookup"><span data-stu-id="f6dda-143">Based on a list of 86 concepts seen in the following diagram, visual features found in an image can be categorized ranging from broad to specific.</span></span> <span data-ttu-id="f6dda-144">For the full taxonomy in text format, see [Category Taxonomy](https://docs.microsoft.com/azure/cognitive-services/computer-vision/category-taxonomy).</span><span class="sxs-lookup"><span data-stu-id="f6dda-144">For the full taxonomy in text format, see [Category Taxonomy](https://docs.microsoft.com/azure/cognitive-services/computer-vision/category-taxonomy).</span></span>

![Analyze Categories](./Images/analyze_categories.jpg)

<span data-ttu-id="f6dda-146">Image</span><span class="sxs-lookup"><span data-stu-id="f6dda-146">Image</span></span>                                                  | <span data-ttu-id="f6dda-147">Response</span><span class="sxs-lookup"><span data-stu-id="f6dda-147">Response</span></span>
------------------------------------------------------ | ----------------
![Woman Roof](./Images/woman_roof.jpg)                 | <span data-ttu-id="f6dda-149">people</span><span class="sxs-lookup"><span data-stu-id="f6dda-149">people</span></span>
![Family Photo](./Images/family_photo.jpg)             | <span data-ttu-id="f6dda-151">people_crowd</span><span class="sxs-lookup"><span data-stu-id="f6dda-151">people_crowd</span></span>
![Cute Dog](./Images/cute_dog.jpg)                     | <span data-ttu-id="f6dda-153">animal_dog</span><span class="sxs-lookup"><span data-stu-id="f6dda-153">animal_dog</span></span>
![Outdoor Mountain](./Images/mountain_vista.jpg)       | <span data-ttu-id="f6dda-155">outdoor_mountain</span><span class="sxs-lookup"><span data-stu-id="f6dda-155">outdoor_mountain</span></span>
![Vision Analyze Food Bread](./Images/bread.jpg)       | <span data-ttu-id="f6dda-157">food_bread</span><span class="sxs-lookup"><span data-stu-id="f6dda-157">food_bread</span></span>

## <a name="identifying-image-types"></a><span data-ttu-id="f6dda-158">Identifying Image Types</span><span class="sxs-lookup"><span data-stu-id="f6dda-158">Identifying Image Types</span></span>
<span data-ttu-id="f6dda-159">There are several ways to categorize images.</span><span class="sxs-lookup"><span data-stu-id="f6dda-159">There are several ways to categorize images.</span></span> <span data-ttu-id="f6dda-160">Computer Vision API can set a boolean flag to indicate whether an image is black and white or color.</span><span class="sxs-lookup"><span data-stu-id="f6dda-160">Computer Vision API can set a boolean flag to indicate whether an image is black and white or color.</span></span> <span data-ttu-id="f6dda-161">It can also set a flag to indicate whether an image is a line drawing or not.</span><span class="sxs-lookup"><span data-stu-id="f6dda-161">It can also set a flag to indicate whether an image is a line drawing or not.</span></span> <span data-ttu-id="f6dda-162">It can also indicate whether an image is clip art or not and indicate its quality as such on a scale of 0-3.</span><span class="sxs-lookup"><span data-stu-id="f6dda-162">It can also indicate whether an image is clip art or not and indicate its quality as such on a scale of 0-3.</span></span>

### <a name="clip-art-type"></a><span data-ttu-id="f6dda-163">Clip-art type</span><span class="sxs-lookup"><span data-stu-id="f6dda-163">Clip-art type</span></span>
<span data-ttu-id="f6dda-164">Detects whether an image is clip art or not.</span><span class="sxs-lookup"><span data-stu-id="f6dda-164">Detects whether an image is clip art or not.</span></span>  

<span data-ttu-id="f6dda-165">Value</span><span class="sxs-lookup"><span data-stu-id="f6dda-165">Value</span></span> | <span data-ttu-id="f6dda-166">Meaning</span><span class="sxs-lookup"><span data-stu-id="f6dda-166">Meaning</span></span>
----- | --------------
<span data-ttu-id="f6dda-167">0</span><span class="sxs-lookup"><span data-stu-id="f6dda-167">0</span></span>     | <span data-ttu-id="f6dda-168">Non-clip-art</span><span class="sxs-lookup"><span data-stu-id="f6dda-168">Non-clip-art</span></span>
<span data-ttu-id="f6dda-169">1</span><span class="sxs-lookup"><span data-stu-id="f6dda-169">1</span></span>     | <span data-ttu-id="f6dda-170">ambiguous</span><span class="sxs-lookup"><span data-stu-id="f6dda-170">ambiguous</span></span>
<span data-ttu-id="f6dda-171">2</span><span class="sxs-lookup"><span data-stu-id="f6dda-171">2</span></span>     | <span data-ttu-id="f6dda-172">normal-clip-art</span><span class="sxs-lookup"><span data-stu-id="f6dda-172">normal-clip-art</span></span>
<span data-ttu-id="f6dda-173">3</span><span class="sxs-lookup"><span data-stu-id="f6dda-173">3</span></span>     | <span data-ttu-id="f6dda-174">good-clip-art</span><span class="sxs-lookup"><span data-stu-id="f6dda-174">good-clip-art</span></span>

<span data-ttu-id="f6dda-175">Image</span><span class="sxs-lookup"><span data-stu-id="f6dda-175">Image</span></span>|<span data-ttu-id="f6dda-176">Response</span><span class="sxs-lookup"><span data-stu-id="f6dda-176">Response</span></span>
----|----
![Vision Analyze Cheese Clip Art](./Images/cheese_clipart.jpg)|<span data-ttu-id="f6dda-178">3 good-clip-art</span><span class="sxs-lookup"><span data-stu-id="f6dda-178">3 good-clip-art</span></span>
![Vision Analyze House Yard](./Images/house_yard.jpg)|<span data-ttu-id="f6dda-180">0 Non-clip-art</span><span class="sxs-lookup"><span data-stu-id="f6dda-180">0 Non-clip-art</span></span>

### <a name="line-drawing-type"></a><span data-ttu-id="f6dda-181">Line drawing type</span><span class="sxs-lookup"><span data-stu-id="f6dda-181">Line drawing type</span></span>
<span data-ttu-id="f6dda-182">Detects whether an image is a line drawing or not.</span><span class="sxs-lookup"><span data-stu-id="f6dda-182">Detects whether an image is a line drawing or not.</span></span>

<span data-ttu-id="f6dda-183">Image</span><span class="sxs-lookup"><span data-stu-id="f6dda-183">Image</span></span>|<span data-ttu-id="f6dda-184">Response</span><span class="sxs-lookup"><span data-stu-id="f6dda-184">Response</span></span>
----|----
![Vision Analyze Lion Drawing](./Images/lion_drawing.jpg)|<span data-ttu-id="f6dda-186">True</span><span class="sxs-lookup"><span data-stu-id="f6dda-186">True</span></span>
![Vision Analyze Flower](./Images/flower.jpg)|<span data-ttu-id="f6dda-188">False</span><span class="sxs-lookup"><span data-stu-id="f6dda-188">False</span></span>

### <a name="faces"></a><span data-ttu-id="f6dda-189">Faces</span><span class="sxs-lookup"><span data-stu-id="f6dda-189">Faces</span></span>
<span data-ttu-id="f6dda-190">Detects human faces within a picture and generates the face coordinates, the rectangle for the face, gender, and age.</span><span class="sxs-lookup"><span data-stu-id="f6dda-190">Detects human faces within a picture and generates the face coordinates, the rectangle for the face, gender, and age.</span></span> <span data-ttu-id="f6dda-191">These visual features are a subset of metadata generated for face.</span><span class="sxs-lookup"><span data-stu-id="f6dda-191">These visual features are a subset of metadata generated for face.</span></span> <span data-ttu-id="f6dda-192">For more extensive metadata generated for faces (facial identification, pose detection, and more), use the Face API.</span><span class="sxs-lookup"><span data-stu-id="f6dda-192">For more extensive metadata generated for faces (facial identification, pose detection, and more), use the Face API.</span></span>  

<span data-ttu-id="f6dda-193">Image</span><span class="sxs-lookup"><span data-stu-id="f6dda-193">Image</span></span>|<span data-ttu-id="f6dda-194">Response</span><span class="sxs-lookup"><span data-stu-id="f6dda-194">Response</span></span>
----|----
![Vision Analyze Woman Roof Face](./Images/woman_roof_face.png) | <span data-ttu-id="f6dda-196">[ { "age": 23, "gender": "Female", "faceRectangle": { "left": 1379, "top": 320, "width": 310, "height": 310 } } ]</span><span class="sxs-lookup"><span data-stu-id="f6dda-196">[ { "age": 23, "gender": "Female", "faceRectangle": { "left": 1379, "top": 320, "width": 310, "height": 310 } } ]</span></span>
![Vision Analyze Mom Daughter Face](./Images/mom_daughter_face.png) | <span data-ttu-id="f6dda-198">[ { "age": 28, "gender": "Female", "faceRectangle": { "left": 447, "top": 195, "width": 162, "height": 162 } }, { "age": 10, "gender": "Male", "faceRectangle": { "left": 355, "top": 87, "width": 143, "height": 143 } } ]</span><span class="sxs-lookup"><span data-stu-id="f6dda-198">[ { "age": 28, "gender": "Female", "faceRectangle": { "left": 447, "top": 195, "width": 162, "height": 162 } }, { "age": 10, "gender": "Male", "faceRectangle": { "left": 355, "top": 87, "width": 143, "height": 143 } } ]</span></span>
![Vision Analyze Family Phot Face](./Images/family_photo_face.png) | <span data-ttu-id="f6dda-200">[ { "age": 11, "gender": "Male", "faceRectangle": { "left": 113, "top": 314, "width": 222, "height": 222 } }, { "age": 11, "gender": "Female", "faceRectangle": { "left": 1200, "top": 632, "width": 215, "height": 215 } }, { "age": 41, "gender": "Male", "faceRectangle": { "left": 514, "top": 223, "width": 205, "height": 205 } }, { "age": 37, "gender": "Female", "faceRectangle": { "left": 1008, "top": 277, "width": 201, "height": 201 } } ]</span><span class="sxs-lookup"><span data-stu-id="f6dda-200">[ { "age": 11, "gender": "Male", "faceRectangle": { "left": 113, "top": 314, "width": 222, "height": 222 } }, { "age": 11, "gender": "Female", "faceRectangle": { "left": 1200, "top": 632, "width": 215, "height": 215 } }, { "age": 41, "gender": "Male", "faceRectangle": { "left": 514, "top": 223, "width": 205, "height": 205 } }, { "age": 37, "gender": "Female", "faceRectangle": { "left": 1008, "top": 277, "width": 201, "height": 201 } } ]</span></span>


## <a name="domain-specific-content"></a><span data-ttu-id="f6dda-201">Domain-Specific Content</span><span class="sxs-lookup"><span data-stu-id="f6dda-201">Domain-Specific Content</span></span>

<span data-ttu-id="f6dda-202">In addition to tagging and top-level categorization, Computer Vision API also supports specialized (or domain-specific) information.</span><span class="sxs-lookup"><span data-stu-id="f6dda-202">In addition to tagging and top-level categorization, Computer Vision API also supports specialized (or domain-specific) information.</span></span> <span data-ttu-id="f6dda-203">Specialized information can be implemented as a standalone method or with the high-level categorization.</span><span class="sxs-lookup"><span data-stu-id="f6dda-203">Specialized information can be implemented as a standalone method or with the high-level categorization.</span></span> <span data-ttu-id="f6dda-204">It functions as a means to further refine the 86-category taxonomy through the addition of domain-specific models.</span><span class="sxs-lookup"><span data-stu-id="f6dda-204">It functions as a means to further refine the 86-category taxonomy through the addition of domain-specific models.</span></span>

<span data-ttu-id="f6dda-205">Currently, the only specialized information supported are celebrity recognition and landmark recognition.</span><span class="sxs-lookup"><span data-stu-id="f6dda-205">Currently, the only specialized information supported are celebrity recognition and landmark recognition.</span></span> <span data-ttu-id="f6dda-206">They are domain-specific refinements for the people and people group categories, and landmarks around the world.</span><span class="sxs-lookup"><span data-stu-id="f6dda-206">They are domain-specific refinements for the people and people group categories, and landmarks around the world.</span></span>

<span data-ttu-id="f6dda-207">There are two options for using the domain-specific models:</span><span class="sxs-lookup"><span data-stu-id="f6dda-207">There are two options for using the domain-specific models:</span></span>

### <a name="option-one---scoped-analysis"></a><span data-ttu-id="f6dda-208">Option One - Scoped Analysis</span><span class="sxs-lookup"><span data-stu-id="f6dda-208">Option One - Scoped Analysis</span></span>
<span data-ttu-id="f6dda-209">Analyze only a chosen model, by invoking an HTTP POST call.</span><span class="sxs-lookup"><span data-stu-id="f6dda-209">Analyze only a chosen model, by invoking an HTTP POST call.</span></span> <span data-ttu-id="f6dda-210">For this option, if you know which model you want to use, you specify the model's name, and you only get information relevant to that model.</span><span class="sxs-lookup"><span data-stu-id="f6dda-210">For this option, if you know which model you want to use, you specify the model's name, and you only get information relevant to that model.</span></span> <span data-ttu-id="f6dda-211">For example, you can use this option to only look for celebrity-recognition.</span><span class="sxs-lookup"><span data-stu-id="f6dda-211">For example, you can use this option to only look for celebrity-recognition.</span></span> <span data-ttu-id="f6dda-212">The response contains a list of potential matching celebrities, accompanied by their confidence scores.</span><span class="sxs-lookup"><span data-stu-id="f6dda-212">The response contains a list of potential matching celebrities, accompanied by their confidence scores.</span></span>

### <a name="option-two---enhanced-analysis"></a><span data-ttu-id="f6dda-213">Option Two - Enhanced Analysis</span><span class="sxs-lookup"><span data-stu-id="f6dda-213">Option Two - Enhanced Analysis</span></span>
<span data-ttu-id="f6dda-214">Analyze to provide additional details related to categories from the 86-category taxonomy.</span><span class="sxs-lookup"><span data-stu-id="f6dda-214">Analyze to provide additional details related to categories from the 86-category taxonomy.</span></span> <span data-ttu-id="f6dda-215">This option is available for use in applications where users want to get generic image analysis in addition to details from one or more domain-specific models.</span><span class="sxs-lookup"><span data-stu-id="f6dda-215">This option is available for use in applications where users want to get generic image analysis in addition to details from one or more domain-specific models.</span></span> <span data-ttu-id="f6dda-216">When this method is invoked, the 86-category taxonomy classifier is called first.</span><span class="sxs-lookup"><span data-stu-id="f6dda-216">When this method is invoked, the 86-category taxonomy classifier is called first.</span></span> <span data-ttu-id="f6dda-217">If any of the categories match that of known/matching models, a second pass of classifier invocations follows.</span><span class="sxs-lookup"><span data-stu-id="f6dda-217">If any of the categories match that of known/matching models, a second pass of classifier invocations follows.</span></span> <span data-ttu-id="f6dda-218">For example, if 'details=all' or "details" include 'celebrities', the method calls the celebrity classifier after the 86-category classifier is called.</span><span class="sxs-lookup"><span data-stu-id="f6dda-218">For example, if 'details=all' or "details" include 'celebrities', the method calls the celebrity classifier after the 86-category classifier is called.</span></span> <span data-ttu-id="f6dda-219">The result includes tags starting with 'people_'.</span><span class="sxs-lookup"><span data-stu-id="f6dda-219">The result includes tags starting with 'people_'.</span></span>

## <a name="generating-descriptions"></a><span data-ttu-id="f6dda-220">Generating Descriptions</span><span class="sxs-lookup"><span data-stu-id="f6dda-220">Generating Descriptions</span></span> 
<span data-ttu-id="f6dda-221">Computer Vision API's algorithms analyze the content in an image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-221">Computer Vision API's algorithms analyze the content in an image.</span></span> <span data-ttu-id="f6dda-222">This analysis forms the foundation for a 'description' displayed as human-readable language in complete sentences.</span><span class="sxs-lookup"><span data-stu-id="f6dda-222">This analysis forms the foundation for a 'description' displayed as human-readable language in complete sentences.</span></span> <span data-ttu-id="f6dda-223">The description summarizes what is found in the image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-223">The description summarizes what is found in the image.</span></span> <span data-ttu-id="f6dda-224">Computer Vision API's algorithms generate various descriptions based on the objects identified in the image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-224">Computer Vision API's algorithms generate various descriptions based on the objects identified in the image.</span></span> <span data-ttu-id="f6dda-225">The descriptions are each evaluated and a confidence score generated.</span><span class="sxs-lookup"><span data-stu-id="f6dda-225">The descriptions are each evaluated and a confidence score generated.</span></span> <span data-ttu-id="f6dda-226">A list is then returned ordered from highest confidence score to lowest.</span><span class="sxs-lookup"><span data-stu-id="f6dda-226">A list is then returned ordered from highest confidence score to lowest.</span></span> <span data-ttu-id="f6dda-227">An example of a bot that uses this technology to generate image captions can be found [here](https://github.com/Microsoft/BotBuilder-Samples/tree/master/CSharp/intelligence-ImageCaption).</span><span class="sxs-lookup"><span data-stu-id="f6dda-227">An example of a bot that uses this technology to generate image captions can be found [here](https://github.com/Microsoft/BotBuilder-Samples/tree/master/CSharp/intelligence-ImageCaption).</span></span>  

### <a name="example-description-generation"></a><span data-ttu-id="f6dda-228">Example Description Generation</span><span class="sxs-lookup"><span data-stu-id="f6dda-228">Example Description Generation</span></span>
![B&W Buildings](./Images/bw_buildings.jpg) <span data-ttu-id="f6dda-230">'</span><span class="sxs-lookup"><span data-stu-id="f6dda-230">'</span></span>
```json
 Returned Json

'description':{
   "captions":[
      {
         "type":"phrase",
         'text':'a black and white photo of a large city',
         'confidence':0.607638706850331
      }
   ]   
   "captions":[
      {
         "type":"phrase",
         'text':'a photo of a large city',
         'confidence':0.577256764264197
      }
   ]   
   "captions":[
      {
         "type":"phrase",
         'text':'a black and white photo of a city',
         'confidence':0.538493271791207
      }
   ]   
   'description':[
      "tags":{
         "outdoor",
         "city",
         "building",
         "photo",
         "large",
      }
   ]
}
```

## <a name="perceiving-color-schemes"></a><span data-ttu-id="f6dda-231">Perceiving Color Schemes</span><span class="sxs-lookup"><span data-stu-id="f6dda-231">Perceiving Color Schemes</span></span>
<span data-ttu-id="f6dda-232">The Computer Vision algorithm extracts colors from an image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-232">The Computer Vision algorithm extracts colors from an image.</span></span> <span data-ttu-id="f6dda-233">The colors are analyzed in three different contexts: foreground, background, and whole.</span><span class="sxs-lookup"><span data-stu-id="f6dda-233">The colors are analyzed in three different contexts: foreground, background, and whole.</span></span> <span data-ttu-id="f6dda-234">They are grouped into twelve 12 dominant accent colors.</span><span class="sxs-lookup"><span data-stu-id="f6dda-234">They are grouped into twelve 12 dominant accent colors.</span></span> <span data-ttu-id="f6dda-235">Those accent colors are black, blue, brown, gray, green, orange, pink, purple, red, teal, white, and yellow.</span><span class="sxs-lookup"><span data-stu-id="f6dda-235">Those accent colors are black, blue, brown, gray, green, orange, pink, purple, red, teal, white, and yellow.</span></span> <span data-ttu-id="f6dda-236">Depending on the colors in an image, simple black and white or accent colors may be returned in hexadecimal color codes.</span><span class="sxs-lookup"><span data-stu-id="f6dda-236">Depending on the colors in an image, simple black and white or accent colors may be returned in hexadecimal color codes.</span></span>

<span data-ttu-id="f6dda-237">Image</span><span class="sxs-lookup"><span data-stu-id="f6dda-237">Image</span></span>                                                       | <span data-ttu-id="f6dda-238">Foreground</span><span class="sxs-lookup"><span data-stu-id="f6dda-238">Foreground</span></span> |<span data-ttu-id="f6dda-239">Background</span><span class="sxs-lookup"><span data-stu-id="f6dda-239">Background</span></span>| <span data-ttu-id="f6dda-240">Colors</span><span class="sxs-lookup"><span data-stu-id="f6dda-240">Colors</span></span>
----------------------------------------------------------- | --------- | ------- | ------
![Outdoor Mountain](./Images/mountain_vista.jpg)            | <span data-ttu-id="f6dda-242">Black</span><span class="sxs-lookup"><span data-stu-id="f6dda-242">Black</span></span>     | <span data-ttu-id="f6dda-243">Black</span><span class="sxs-lookup"><span data-stu-id="f6dda-243">Black</span></span>   | <span data-ttu-id="f6dda-244">White</span><span class="sxs-lookup"><span data-stu-id="f6dda-244">White</span></span>
![Vision Analyze Flower](./Images/flower.jpg)               | <span data-ttu-id="f6dda-246">Black</span><span class="sxs-lookup"><span data-stu-id="f6dda-246">Black</span></span>     | <span data-ttu-id="f6dda-247">White</span><span class="sxs-lookup"><span data-stu-id="f6dda-247">White</span></span>   | <span data-ttu-id="f6dda-248">White, Black, Green</span><span class="sxs-lookup"><span data-stu-id="f6dda-248">White, Black, Green</span></span>
![Vision Analyze Train Station](./Images/train_station.jpg) | <span data-ttu-id="f6dda-250">Black</span><span class="sxs-lookup"><span data-stu-id="f6dda-250">Black</span></span>     | <span data-ttu-id="f6dda-251">Black</span><span class="sxs-lookup"><span data-stu-id="f6dda-251">Black</span></span>   | <span data-ttu-id="f6dda-252">Black</span><span class="sxs-lookup"><span data-stu-id="f6dda-252">Black</span></span>

### <a name="accent-color"></a><span data-ttu-id="f6dda-253">Accent color</span><span class="sxs-lookup"><span data-stu-id="f6dda-253">Accent color</span></span>
<span data-ttu-id="f6dda-254">Color extracted from an image designed to represent the most eye-popping color to users via a mix of dominant colors and saturation.</span><span class="sxs-lookup"><span data-stu-id="f6dda-254">Color extracted from an image designed to represent the most eye-popping color to users via a mix of dominant colors and saturation.</span></span>

<span data-ttu-id="f6dda-255">Image</span><span class="sxs-lookup"><span data-stu-id="f6dda-255">Image</span></span>                                                       | <span data-ttu-id="f6dda-256">Response</span><span class="sxs-lookup"><span data-stu-id="f6dda-256">Response</span></span>
----------------------------------------------------------- | ----
![Outdoor Mountain](./Images/mountain_vista.jpg)            | <span data-ttu-id="f6dda-258">#BC6F0F</span><span class="sxs-lookup"><span data-stu-id="f6dda-258">#BC6F0F</span></span>
![Vision Analyze Flower](./Images/flower.jpg)               | <span data-ttu-id="f6dda-260">#CAA501</span><span class="sxs-lookup"><span data-stu-id="f6dda-260">#CAA501</span></span>
![Vision Analyze Train Station](./Images/train_station.jpg) | <span data-ttu-id="f6dda-262">#484B83</span><span class="sxs-lookup"><span data-stu-id="f6dda-262">#484B83</span></span>


### <a name="black--white"></a><span data-ttu-id="f6dda-263">Black & White</span><span class="sxs-lookup"><span data-stu-id="f6dda-263">Black & White</span></span>
<span data-ttu-id="f6dda-264">Boolean flag that indicates whether an image is black&white or not.</span><span class="sxs-lookup"><span data-stu-id="f6dda-264">Boolean flag that indicates whether an image is black&white or not.</span></span>

<span data-ttu-id="f6dda-265">Image</span><span class="sxs-lookup"><span data-stu-id="f6dda-265">Image</span></span>                                                      | <span data-ttu-id="f6dda-266">Response</span><span class="sxs-lookup"><span data-stu-id="f6dda-266">Response</span></span>
---------------------------------------------------------- | ----
![Vision Analyze Building](./Images/bw_buildings.jpg)      | <span data-ttu-id="f6dda-268">True</span><span class="sxs-lookup"><span data-stu-id="f6dda-268">True</span></span>
![Vision Analyze House Yard](./Images/house_yard.jpg)      | <span data-ttu-id="f6dda-270">False</span><span class="sxs-lookup"><span data-stu-id="f6dda-270">False</span></span>

## <a name="flagging-adult-content"></a><span data-ttu-id="f6dda-271">Flagging Adult Content</span><span class="sxs-lookup"><span data-stu-id="f6dda-271">Flagging Adult Content</span></span>
<span data-ttu-id="f6dda-272">Among the various visual categories is the adult and racy group, which enables detection of adult materials and restricts the display of images containing sexual content.</span><span class="sxs-lookup"><span data-stu-id="f6dda-272">Among the various visual categories is the adult and racy group, which enables detection of adult materials and restricts the display of images containing sexual content.</span></span> <span data-ttu-id="f6dda-273">The filter for adult and racy content detection can be set on a sliding scale to accommodate the user's preference.</span><span class="sxs-lookup"><span data-stu-id="f6dda-273">The filter for adult and racy content detection can be set on a sliding scale to accommodate the user's preference.</span></span>

## <a name="optical-character-recognition-ocr"></a><span data-ttu-id="f6dda-274">Optical Character Recognition (OCR)</span><span class="sxs-lookup"><span data-stu-id="f6dda-274">Optical Character Recognition (OCR)</span></span>
<span data-ttu-id="f6dda-275">OCR technology detects text content in an image and extracts the identified text into a machine-readable character stream.</span><span class="sxs-lookup"><span data-stu-id="f6dda-275">OCR technology detects text content in an image and extracts the identified text into a machine-readable character stream.</span></span> <span data-ttu-id="f6dda-276">You can use the result for search and numerous other purposes like medical records, security, and banking.</span><span class="sxs-lookup"><span data-stu-id="f6dda-276">You can use the result for search and numerous other purposes like medical records, security, and banking.</span></span> <span data-ttu-id="f6dda-277">It automatically detects the language.</span><span class="sxs-lookup"><span data-stu-id="f6dda-277">It automatically detects the language.</span></span> <span data-ttu-id="f6dda-278">OCR saves time and provides convenience for users by allowing them to take photos of text instead of transcribing the text.</span><span class="sxs-lookup"><span data-stu-id="f6dda-278">OCR saves time and provides convenience for users by allowing them to take photos of text instead of transcribing the text.</span></span>

<span data-ttu-id="f6dda-279">OCR supports 25 languages.</span><span class="sxs-lookup"><span data-stu-id="f6dda-279">OCR supports 25 languages.</span></span> <span data-ttu-id="f6dda-280">These languages are: Arabic, Chinese Simplified, Chinese Traditional, Czech, Danish, Dutch, English, Finnish, French, German, Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, Serbian (Cyrillic and Latin), Slovak, Spanish, Swedish, and Turkish.</span><span class="sxs-lookup"><span data-stu-id="f6dda-280">These languages are: Arabic, Chinese Simplified, Chinese Traditional, Czech, Danish, Dutch, English, Finnish, French, German, Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, Serbian (Cyrillic and Latin), Slovak, Spanish, Swedish, and Turkish.</span></span>

<span data-ttu-id="f6dda-281">If needed, OCR corrects the rotation of the recognized text, in degrees, around the horizontal image axis.</span><span class="sxs-lookup"><span data-stu-id="f6dda-281">If needed, OCR corrects the rotation of the recognized text, in degrees, around the horizontal image axis.</span></span> <span data-ttu-id="f6dda-282">OCR provides the frame coordinates of each word as seen in below illustration.</span><span class="sxs-lookup"><span data-stu-id="f6dda-282">OCR provides the frame coordinates of each word as seen in below illustration.</span></span>

<span data-ttu-id="f6dda-283">![OCR Overview](./Images/vision-overview-ocr.png) Requirements for OCR:</span><span class="sxs-lookup"><span data-stu-id="f6dda-283">![OCR Overview](./Images/vision-overview-ocr.png) Requirements for OCR:</span></span>
- <span data-ttu-id="f6dda-284">The size of the input image must be between 40 x 40 and 3200 x 3200 pixels.</span><span class="sxs-lookup"><span data-stu-id="f6dda-284">The size of the input image must be between 40 x 40 and 3200 x 3200 pixels.</span></span>
- <span data-ttu-id="f6dda-285">The image cannot be bigger than 10 megapixels.</span><span class="sxs-lookup"><span data-stu-id="f6dda-285">The image cannot be bigger than 10 megapixels.</span></span>

<span data-ttu-id="f6dda-286">Input image can be rotated by any multiple of 90 degrees plus a small angle of up to '40 degrees.</span><span class="sxs-lookup"><span data-stu-id="f6dda-286">Input image can be rotated by any multiple of 90 degrees plus a small angle of up to '40 degrees.</span></span>

<span data-ttu-id="f6dda-287">The accuracy of text recognition depends on the quality of the image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-287">The accuracy of text recognition depends on the quality of the image.</span></span> <span data-ttu-id="f6dda-288">An inaccurate reading may be caused by the following situations:</span><span class="sxs-lookup"><span data-stu-id="f6dda-288">An inaccurate reading may be caused by the following situations:</span></span>
- <span data-ttu-id="f6dda-289">Blurry images.</span><span class="sxs-lookup"><span data-stu-id="f6dda-289">Blurry images.</span></span>
- <span data-ttu-id="f6dda-290">Handwritten or cursive text.</span><span class="sxs-lookup"><span data-stu-id="f6dda-290">Handwritten or cursive text.</span></span>
- <span data-ttu-id="f6dda-291">Artistic font styles.</span><span class="sxs-lookup"><span data-stu-id="f6dda-291">Artistic font styles.</span></span>
- <span data-ttu-id="f6dda-292">Small text size.</span><span class="sxs-lookup"><span data-stu-id="f6dda-292">Small text size.</span></span>
- <span data-ttu-id="f6dda-293">Complex backgrounds, shadows, or glare over text or perspective distortion.</span><span class="sxs-lookup"><span data-stu-id="f6dda-293">Complex backgrounds, shadows, or glare over text or perspective distortion.</span></span>
- <span data-ttu-id="f6dda-294">Oversized or missing capital letters at the beginnings of words</span><span class="sxs-lookup"><span data-stu-id="f6dda-294">Oversized or missing capital letters at the beginnings of words</span></span>
- <span data-ttu-id="f6dda-295">Subscript, superscript, or strikethrough text.</span><span class="sxs-lookup"><span data-stu-id="f6dda-295">Subscript, superscript, or strikethrough text.</span></span>

<span data-ttu-id="f6dda-296">Limitations: On photos where text is dominant, false positives may come from partially recognized words.</span><span class="sxs-lookup"><span data-stu-id="f6dda-296">Limitations: On photos where text is dominant, false positives may come from partially recognized words.</span></span> <span data-ttu-id="f6dda-297">On some photos, especially photos without any text, precision can vary a lot depending on the type of image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-297">On some photos, especially photos without any text, precision can vary a lot depending on the type of image.</span></span>

## <a name="recognize-handwritten-text"></a><span data-ttu-id="f6dda-298">Recognize Handwritten Text</span><span class="sxs-lookup"><span data-stu-id="f6dda-298">Recognize Handwritten Text</span></span>
<span data-ttu-id="f6dda-299">This technology allows you to detect and extract handwritten text from notes, letters, essays, whiteboards, forms, etc. It works with different surfaces and backgrounds, such as white paper, yellow sticky notes, and whiteboards.</span><span class="sxs-lookup"><span data-stu-id="f6dda-299">This technology allows you to detect and extract handwritten text from notes, letters, essays, whiteboards, forms, etc. It works with different surfaces and backgrounds, such as white paper, yellow sticky notes, and whiteboards.</span></span>

<span data-ttu-id="f6dda-300">Handwritten text recognition saves time and effort and can make you more productive by allowing you to take images of text, rather than having to transcribe it.</span><span class="sxs-lookup"><span data-stu-id="f6dda-300">Handwritten text recognition saves time and effort and can make you more productive by allowing you to take images of text, rather than having to transcribe it.</span></span> <span data-ttu-id="f6dda-301">It makes it possible to digitize notes.</span><span class="sxs-lookup"><span data-stu-id="f6dda-301">It makes it possible to digitize notes.</span></span> <span data-ttu-id="f6dda-302">This digitization allows you to implement quick and easy search.</span><span class="sxs-lookup"><span data-stu-id="f6dda-302">This digitization allows you to implement quick and easy search.</span></span> <span data-ttu-id="f6dda-303">It also reduces paper clutter.</span><span class="sxs-lookup"><span data-stu-id="f6dda-303">It also reduces paper clutter.</span></span>

<span data-ttu-id="f6dda-304">Input requirements:</span><span class="sxs-lookup"><span data-stu-id="f6dda-304">Input requirements:</span></span>
- <span data-ttu-id="f6dda-305">Supported image formats: JPEG, PNG, and BMP.</span><span class="sxs-lookup"><span data-stu-id="f6dda-305">Supported image formats: JPEG, PNG, and BMP.</span></span>
- <span data-ttu-id="f6dda-306">Image file size must be less than 4 MB.</span><span class="sxs-lookup"><span data-stu-id="f6dda-306">Image file size must be less than 4 MB.</span></span>
- <span data-ttu-id="f6dda-307">Image dimensions must be at least 40 x 40, at most 3200 x 3200.</span><span class="sxs-lookup"><span data-stu-id="f6dda-307">Image dimensions must be at least 40 x 40, at most 3200 x 3200.</span></span>

<span data-ttu-id="f6dda-308">Note: this technology is currently in preview and is only available for English text.</span><span class="sxs-lookup"><span data-stu-id="f6dda-308">Note: this technology is currently in preview and is only available for English text.</span></span>

## <a name="generating-thumbnails"></a><span data-ttu-id="f6dda-309">Generating Thumbnails</span><span class="sxs-lookup"><span data-stu-id="f6dda-309">Generating Thumbnails</span></span>
<span data-ttu-id="f6dda-310">A thumbnail is a small representation of a full-size image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-310">A thumbnail is a small representation of a full-size image.</span></span> <span data-ttu-id="f6dda-311">Varied devices such as phones, tablets, and PCs create a need for different user experience (UX) layouts and thumbnail sizes.</span><span class="sxs-lookup"><span data-stu-id="f6dda-311">Varied devices such as phones, tablets, and PCs create a need for different user experience (UX) layouts and thumbnail sizes.</span></span> <span data-ttu-id="f6dda-312">Using smart cropping, this Computer Vision API feature helps solve the problem.</span><span class="sxs-lookup"><span data-stu-id="f6dda-312">Using smart cropping, this Computer Vision API feature helps solve the problem.</span></span>

<span data-ttu-id="f6dda-313">After uploading an image, a high-quality thumbnail gets generated and the Computer Vision API algorithm analyzes the objects within the image.</span><span class="sxs-lookup"><span data-stu-id="f6dda-313">After uploading an image, a high-quality thumbnail gets generated and the Computer Vision API algorithm analyzes the objects within the image.</span></span> <span data-ttu-id="f6dda-314">It then crops the image to fit the requirements of the 'region of interest' (ROI).</span><span class="sxs-lookup"><span data-stu-id="f6dda-314">It then crops the image to fit the requirements of the 'region of interest' (ROI).</span></span> <span data-ttu-id="f6dda-315">The output gets displayed within a special framework as seen in below illustration.</span><span class="sxs-lookup"><span data-stu-id="f6dda-315">The output gets displayed within a special framework as seen in below illustration.</span></span> <span data-ttu-id="f6dda-316">The generated thumbnail can be presented using an aspect ration that is different from the aspect ratio of the original image to accommodate a user's needs.</span><span class="sxs-lookup"><span data-stu-id="f6dda-316">The generated thumbnail can be presented using an aspect ration that is different from the aspect ratio of the original image to accommodate a user's needs.</span></span>

<span data-ttu-id="f6dda-317">The thumbnail algorithm works as follows:</span><span class="sxs-lookup"><span data-stu-id="f6dda-317">The thumbnail algorithm works as follows:</span></span>

1. <span data-ttu-id="f6dda-318">Removes distracting elements from the image and recognizes the main object, the 'region of interest' (ROI).</span><span class="sxs-lookup"><span data-stu-id="f6dda-318">Removes distracting elements from the image and recognizes the main object, the 'region of interest' (ROI).</span></span>
2. <span data-ttu-id="f6dda-319">Crops the image based on the identified region of interest.</span><span class="sxs-lookup"><span data-stu-id="f6dda-319">Crops the image based on the identified region of interest.</span></span>
3. <span data-ttu-id="f6dda-320">Changes the aspect ratio to fit the target thumbnail dimensions.</span><span class="sxs-lookup"><span data-stu-id="f6dda-320">Changes the aspect ratio to fit the target thumbnail dimensions.</span></span>

![Thumbnails](./Images/thumbnail-demo.png)
