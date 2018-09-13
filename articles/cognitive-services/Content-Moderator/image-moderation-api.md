---
title: Azure Content Moderator - Image Moderation | Microsoft Docs
description: Use image moderation to moderate inappropriate images
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/20/2018
ms.author: sajagtap
ms.openlocfilehash: c7cbc343c6e9113642d0ac79f4a4d60a404e8171
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44815807"
---
# <a name="image-moderation"></a><span data-ttu-id="f6ead-103">Image moderation</span><span class="sxs-lookup"><span data-stu-id="f6ead-103">Image moderation</span></span>

<span data-ttu-id="f6ead-104">Use Content Moderator’s machine-assisted image moderation and [human review tool](Review-Tool-User-Guide/human-in-the-loop.md) to moderate images for adult and racy content.</span><span class="sxs-lookup"><span data-stu-id="f6ead-104">Use Content Moderator’s machine-assisted image moderation and [human review tool](Review-Tool-User-Guide/human-in-the-loop.md) to moderate images for adult and racy content.</span></span> <span data-ttu-id="f6ead-105">Scan images for text content and extract that text, and detect faces.</span><span class="sxs-lookup"><span data-stu-id="f6ead-105">Scan images for text content and extract that text, and detect faces.</span></span> <span data-ttu-id="f6ead-106">You can match images against custom lists, and take further action.</span><span class="sxs-lookup"><span data-stu-id="f6ead-106">You can match images against custom lists, and take further action.</span></span>

## <a name="evaluating-for-adult-and-racy-content"></a><span data-ttu-id="f6ead-107">Evaluating for adult and racy content</span><span class="sxs-lookup"><span data-stu-id="f6ead-107">Evaluating for adult and racy content</span></span>

<span data-ttu-id="f6ead-108">The **Evaluate** operation returns a confidence score between 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="f6ead-108">The **Evaluate** operation returns a confidence score between 0 and 1.</span></span> <span data-ttu-id="f6ead-109">It also returns boolean data equal to true or false.</span><span class="sxs-lookup"><span data-stu-id="f6ead-109">It also returns boolean data equal to true or false.</span></span> <span data-ttu-id="f6ead-110">These values predict whether the image contains potential adult or racy content.</span><span class="sxs-lookup"><span data-stu-id="f6ead-110">These values predict whether the image contains potential adult or racy content.</span></span> <span data-ttu-id="f6ead-111">When you call the API with your image (file or URL), the returned response includes the following information:</span><span class="sxs-lookup"><span data-stu-id="f6ead-111">When you call the API with your image (file or URL), the returned response includes the following information:</span></span>

    "ImageModeration": {
      .............
      "adultClassificationScore": 0.019196987152099609,
      "isImageAdultClassified": false,
      "racyClassificationScore": 0.032390203326940536,
      "isImageRacyClassified": false,
      ............
      ],

> [!NOTE]

> - <span data-ttu-id="f6ead-112">`isImageAdultClassified` represents the potential presence of images that may be considered sexually explicit or adult in certain situations.</span><span class="sxs-lookup"><span data-stu-id="f6ead-112">`isImageAdultClassified` represents the potential presence of images that may be considered sexually explicit or adult in certain situations.</span></span>
> - <span data-ttu-id="f6ead-113">`isImageRacyClassified` represents the potential presence of images that may be considered sexually suggestive or mature in certain situations.</span><span class="sxs-lookup"><span data-stu-id="f6ead-113">`isImageRacyClassified` represents the potential presence of images that may be considered sexually suggestive or mature in certain situations.</span></span>
> - <span data-ttu-id="f6ead-114">The scores are between 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="f6ead-114">The scores are between 0 and 1.</span></span> <span data-ttu-id="f6ead-115">The higher the score, the higher the model is predicting that the category may be applicable.</span><span class="sxs-lookup"><span data-stu-id="f6ead-115">The higher the score, the higher the model is predicting that the category may be applicable.</span></span> <span data-ttu-id="f6ead-116">This preview relies on a statistical model rather than manually coded outcomes.</span><span class="sxs-lookup"><span data-stu-id="f6ead-116">This preview relies on a statistical model rather than manually coded outcomes.</span></span> <span data-ttu-id="f6ead-117">We recommend testing with your own content to determine how each category aligns to your requirements.</span><span class="sxs-lookup"><span data-stu-id="f6ead-117">We recommend testing with your own content to determine how each category aligns to your requirements.</span></span>
> - <span data-ttu-id="f6ead-118">The boolean values are either true or false depending on the internal score thresholds.</span><span class="sxs-lookup"><span data-stu-id="f6ead-118">The boolean values are either true or false depending on the internal score thresholds.</span></span> <span data-ttu-id="f6ead-119">Customers should assess whether to use this value or decide on custom thresholds based on their content policies.</span><span class="sxs-lookup"><span data-stu-id="f6ead-119">Customers should assess whether to use this value or decide on custom thresholds based on their content policies.</span></span>
>

## <a name="detecting-text-with-optical-character-recognition-ocr"></a><span data-ttu-id="f6ead-120">Detecting text with Optical Character Recognition (OCR)</span><span class="sxs-lookup"><span data-stu-id="f6ead-120">Detecting text with Optical Character Recognition (OCR)</span></span>

<span data-ttu-id="f6ead-121">The **Optical Character Recognition (OCR)** operation predicts the presence of text content in an image and extracts it for text moderation, among other uses.</span><span class="sxs-lookup"><span data-stu-id="f6ead-121">The **Optical Character Recognition (OCR)** operation predicts the presence of text content in an image and extracts it for text moderation, among other uses.</span></span> <span data-ttu-id="f6ead-122">You can specify the language.</span><span class="sxs-lookup"><span data-stu-id="f6ead-122">You can specify the language.</span></span> <span data-ttu-id="f6ead-123">If you do not specify a language, the detection defaults to English.</span><span class="sxs-lookup"><span data-stu-id="f6ead-123">If you do not specify a language, the detection defaults to English.</span></span>

<span data-ttu-id="f6ead-124">The response includes the following information:</span><span class="sxs-lookup"><span data-stu-id="f6ead-124">The response includes the following information:</span></span>
- <span data-ttu-id="f6ead-125">The original text.</span><span class="sxs-lookup"><span data-stu-id="f6ead-125">The original text.</span></span>
- <span data-ttu-id="f6ead-126">The detected text elements with their confidence scores.</span><span class="sxs-lookup"><span data-stu-id="f6ead-126">The detected text elements with their confidence scores.</span></span>

<span data-ttu-id="f6ead-127">Example extract:</span><span class="sxs-lookup"><span data-stu-id="f6ead-127">Example extract:</span></span>

    "TextDetection": {
      "status": {
        "code": 3000.0,
        "description": "OK",
        "exception": null
      },
      .........
      "language": "eng",
      "text": "IF WE DID \r\nALL \r\nTHE THINGS \r\nWE ARE \r\nCAPABLE \r\nOF DOING, \r\nWE WOULD \r\nLITERALLY \r\nASTOUND \r\nOURSELVE \r\n",
      "candidates": []
    },


## <a name="detecting-faces"></a><span data-ttu-id="f6ead-128">Detecting faces</span><span class="sxs-lookup"><span data-stu-id="f6ead-128">Detecting faces</span></span>

<span data-ttu-id="f6ead-129">Detecting faces helps to detect personally identifiable information (PII) such as faces in the images.</span><span class="sxs-lookup"><span data-stu-id="f6ead-129">Detecting faces helps to detect personally identifiable information (PII) such as faces in the images.</span></span> <span data-ttu-id="f6ead-130">You detect potential faces and the number of potential faces in each image.</span><span class="sxs-lookup"><span data-stu-id="f6ead-130">You detect potential faces and the number of potential faces in each image.</span></span>

<span data-ttu-id="f6ead-131">A response includes this information:</span><span class="sxs-lookup"><span data-stu-id="f6ead-131">A response includes this information:</span></span>

- <span data-ttu-id="f6ead-132">Faces count</span><span class="sxs-lookup"><span data-stu-id="f6ead-132">Faces count</span></span>
- <span data-ttu-id="f6ead-133">List of locations of faces detected</span><span class="sxs-lookup"><span data-stu-id="f6ead-133">List of locations of faces detected</span></span>

<span data-ttu-id="f6ead-134">Example extract:</span><span class="sxs-lookup"><span data-stu-id="f6ead-134">Example extract:</span></span>


    "FaceDetection": {
       ......
      "result": true,
      "count": 2,
      "advancedInfo": [
      .....
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
        }
      ]
    }

## <a name="creating-and-managing-custom-lists"></a><span data-ttu-id="f6ead-135">Creating and managing custom lists</span><span class="sxs-lookup"><span data-stu-id="f6ead-135">Creating and managing custom lists</span></span>

<span data-ttu-id="f6ead-136">In many online communities, after users upload images or other type of content, offensive items may get shared multiple times over the following days, weeks, and months.</span><span class="sxs-lookup"><span data-stu-id="f6ead-136">In many online communities, after users upload images or other type of content, offensive items may get shared multiple times over the following days, weeks, and months.</span></span> <span data-ttu-id="f6ead-137">The costs of repeatedly scanning and filtering out the same image or even slightly modified versions of the image from multiple places can be expensive and error-prone.</span><span class="sxs-lookup"><span data-stu-id="f6ead-137">The costs of repeatedly scanning and filtering out the same image or even slightly modified versions of the image from multiple places can be expensive and error-prone.</span></span>

<span data-ttu-id="f6ead-138">Instead of moderating the same image multiple times, you add the offensive images to your custom list of blocked content.</span><span class="sxs-lookup"><span data-stu-id="f6ead-138">Instead of moderating the same image multiple times, you add the offensive images to your custom list of blocked content.</span></span> <span data-ttu-id="f6ead-139">That way, your content moderation system compares incoming images against your custom lists and stops any further processing.</span><span class="sxs-lookup"><span data-stu-id="f6ead-139">That way, your content moderation system compares incoming images against your custom lists and stops any further processing.</span></span>

> [!NOTE]
> <span data-ttu-id="f6ead-140">There is a maximum limit of **5 image lists** with each list to **not exceed 10,000 images**.</span><span class="sxs-lookup"><span data-stu-id="f6ead-140">There is a maximum limit of **5 image lists** with each list to **not exceed 10,000 images**.</span></span>
>

<span data-ttu-id="f6ead-141">The Content Moderator provides a complete [Image List Management API](try-image-list-api.md) with operations for managing lists of custom images.</span><span class="sxs-lookup"><span data-stu-id="f6ead-141">The Content Moderator provides a complete [Image List Management API](try-image-list-api.md) with operations for managing lists of custom images.</span></span> <span data-ttu-id="f6ead-142">Start with the [Image Lists API Console](try-image-list-api.md) and use the REST API code samples.</span><span class="sxs-lookup"><span data-stu-id="f6ead-142">Start with the [Image Lists API Console](try-image-list-api.md) and use the REST API code samples.</span></span> <span data-ttu-id="f6ead-143">Also check out the [Image List .NET quickstart](image-lists-quickstart-dotnet.md) if you are familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="f6ead-143">Also check out the [Image List .NET quickstart](image-lists-quickstart-dotnet.md) if you are familiar with Visual Studio and C#.</span></span>

## <a name="matching-against-your-custom-lists"></a><span data-ttu-id="f6ead-144">Matching against your custom lists</span><span class="sxs-lookup"><span data-stu-id="f6ead-144">Matching against your custom lists</span></span>

<span data-ttu-id="f6ead-145">The Match operation allows fuzzy matching of incoming images against any of your custom lists, created and managed using the List operations.</span><span class="sxs-lookup"><span data-stu-id="f6ead-145">The Match operation allows fuzzy matching of incoming images against any of your custom lists, created and managed using the List operations.</span></span>

<span data-ttu-id="f6ead-146">If a match is found, the operation returns the identifier and the moderation tags of the matched image.</span><span class="sxs-lookup"><span data-stu-id="f6ead-146">If a match is found, the operation returns the identifier and the moderation tags of the matched image.</span></span> <span data-ttu-id="f6ead-147">The response includes this information:</span><span class="sxs-lookup"><span data-stu-id="f6ead-147">The response includes this information:</span></span>

- <span data-ttu-id="f6ead-148">Match score (between 0 and 1)</span><span class="sxs-lookup"><span data-stu-id="f6ead-148">Match score (between 0 and 1)</span></span>
- <span data-ttu-id="f6ead-149">Matched image</span><span class="sxs-lookup"><span data-stu-id="f6ead-149">Matched image</span></span>
- <span data-ttu-id="f6ead-150">Image tags (assigned during previous moderation)</span><span class="sxs-lookup"><span data-stu-id="f6ead-150">Image tags (assigned during previous moderation)</span></span>
- <span data-ttu-id="f6ead-151">Image labels</span><span class="sxs-lookup"><span data-stu-id="f6ead-151">Image labels</span></span>

<span data-ttu-id="f6ead-152">Example extract:</span><span class="sxs-lookup"><span data-stu-id="f6ead-152">Example extract:</span></span>

    {
    ..............,
    "IsMatch": true,
    "Matches": [
        {
            "Score": 1.0,
            "MatchId": 169490,
            "Source": "169642",
            "Tags": [],
            "Label": "Sports"
        }
    ],
    ....
    }

## <a name="human-review-tool"></a><span data-ttu-id="f6ead-153">Human review tool</span><span class="sxs-lookup"><span data-stu-id="f6ead-153">Human review tool</span></span>

<span data-ttu-id="f6ead-154">For more nuanced cases, use the Content Moderator [review tool](Review-Tool-User-Guide/human-in-the-loop.md) and its API to surface the moderation results and content in the review for your human moderators.</span><span class="sxs-lookup"><span data-stu-id="f6ead-154">For more nuanced cases, use the Content Moderator [review tool](Review-Tool-User-Guide/human-in-the-loop.md) and its API to surface the moderation results and content in the review for your human moderators.</span></span> <span data-ttu-id="f6ead-155">They review the machine-assigned tags and confirm their final decisions.</span><span class="sxs-lookup"><span data-stu-id="f6ead-155">They review the machine-assigned tags and confirm their final decisions.</span></span>

![Image review for human moderators](images/moderation-reviews-quickstart-dotnet.PNG)

## <a name="next-steps"></a><span data-ttu-id="f6ead-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6ead-157">Next steps</span></span>

<span data-ttu-id="f6ead-158">Test drive the [Image Moderation API console](try-image-api.md) and use the REST API code samples.</span><span class="sxs-lookup"><span data-stu-id="f6ead-158">Test drive the [Image Moderation API console](try-image-api.md) and use the REST API code samples.</span></span> <span data-ttu-id="f6ead-159">Also check out the [Image moderation .NET quickstart](image-moderation-quickstart-dotnet.md) if you are familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="f6ead-159">Also check out the [Image moderation .NET quickstart](image-moderation-quickstart-dotnet.md) if you are familiar with Visual Studio and C#.</span></span>
