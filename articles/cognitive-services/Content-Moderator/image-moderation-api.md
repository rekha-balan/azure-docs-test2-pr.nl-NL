---
title: Image Moderator API for Content Moderator | Microsoft Docs
description: Use the Image Moderator API to moderate inappropriate images and implement optical character recognition and face detection.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 11/21/2016
ms.author: sajagtap
ms.openlocfilehash: 093414ae32c9114b799d9fd3b0e221c2bddb87c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552457"
---
# <a name="image-moderation-api"></a><span data-ttu-id="1b4e1-103">Image Moderation API</span><span class="sxs-lookup"><span data-stu-id="1b4e1-103">Image Moderation API</span></span> #

<span data-ttu-id="1b4e1-104">Use Content Moderator’s image moderation API [(see API reference)](api-reference.md "Content Moderator API Reference") to moderate images for adult and racy content.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-104">Use Content Moderator’s image moderation API [(see API reference)](api-reference.md "Content Moderator API Reference") to moderate images for adult and racy content.</span></span> <span data-ttu-id="1b4e1-105">Match against custom and shared lists and implement optical character recognition (OCR) and face detection.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-105">Match against custom and shared lists and implement optical character recognition (OCR) and face detection.</span></span>

## <a name="evaluating-for-adult-and-racy-content"></a><span data-ttu-id="1b4e1-106">Evaluating for adult and racy content</span><span class="sxs-lookup"><span data-stu-id="1b4e1-106">Evaluating for adult and racy content</span></span> ##

<span data-ttu-id="1b4e1-107">The Content Moderator API’s **Evaluate** operation returns a classification scores (between 0 and 1) and Boolean data (true or false) to indicate whether the image contains adult or racy content.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-107">The Content Moderator API’s **Evaluate** operation returns a classification scores (between 0 and 1) and Boolean data (true or false) to indicate whether the image contains adult or racy content.</span></span> <span data-ttu-id="1b4e1-108">For example, when you call the API with your image (file or URL), you get back information that includes:</span><span class="sxs-lookup"><span data-stu-id="1b4e1-108">For example, when you call the API with your image (file or URL), you get back information that includes:</span></span>

- <span data-ttu-id="1b4e1-109">The match score (between 0 and 1)</span><span class="sxs-lookup"><span data-stu-id="1b4e1-109">The match score (between 0 and 1)</span></span>
- <span data-ttu-id="1b4e1-110">A Boolean value (true or false) based on default thresholds and actual score</span><span class="sxs-lookup"><span data-stu-id="1b4e1-110">A Boolean value (true or false) based on default thresholds and actual score</span></span>

## <a name="detecting-text-with-optical-character-recognition-ocr"></a><span data-ttu-id="1b4e1-111">Detecting text with Optical Character Recognition (OCR)</span><span class="sxs-lookup"><span data-stu-id="1b4e1-111">Detecting text with Optical Character Recognition (OCR)</span></span> ##

<span data-ttu-id="1b4e1-112">The Optical Character Recognition (**OCR**) capability detects text content in an image and extracts it for search and numerous other purposes.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-112">The Optical Character Recognition (**OCR**) capability detects text content in an image and extracts it for search and numerous other purposes.</span></span> <span data-ttu-id="1b4e1-113">If you do not specify a language, the detection defaults to English.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-113">If you do not specify a language, the detection defaults to English.</span></span>

<span data-ttu-id="1b4e1-114">A response includes:</span><span class="sxs-lookup"><span data-stu-id="1b4e1-114">A response includes:</span></span>

- <span data-ttu-id="1b4e1-115">The original text</span><span class="sxs-lookup"><span data-stu-id="1b4e1-115">The original text</span></span>
- <span data-ttu-id="1b4e1-116">The detected text elements with their confidence scores</span><span class="sxs-lookup"><span data-stu-id="1b4e1-116">The detected text elements with their confidence scores</span></span>

## <a name="detecting-faces"></a><span data-ttu-id="1b4e1-117">Detecting faces</span><span class="sxs-lookup"><span data-stu-id="1b4e1-117">Detecting faces</span></span> ##

<span data-ttu-id="1b4e1-118">Detecting faces is important in the context of content moderation because you may not want your users to upload any personally identifiable information (PII) and risk their privacy and your brand.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-118">Detecting faces is important in the context of content moderation because you may not want your users to upload any personally identifiable information (PII) and risk their privacy and your brand.</span></span> <span data-ttu-id="1b4e1-119">Using the Detect faces operation, you can detect the probability of finding faces and their count in each image.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-119">Using the Detect faces operation, you can detect the probability of finding faces and their count in each image.</span></span>

<span data-ttu-id="1b4e1-120">A response includes:</span><span class="sxs-lookup"><span data-stu-id="1b4e1-120">A response includes:</span></span>

- <span data-ttu-id="1b4e1-121">Faces count</span><span class="sxs-lookup"><span data-stu-id="1b4e1-121">Faces count</span></span>
- <span data-ttu-id="1b4e1-122">List of locations of faces detected</span><span class="sxs-lookup"><span data-stu-id="1b4e1-122">List of locations of faces detected</span></span>

## <a name="matching-against-your-custom-list"></a><span data-ttu-id="1b4e1-123">Matching against your custom list</span><span class="sxs-lookup"><span data-stu-id="1b4e1-123">Matching against your custom list</span></span> ##

<span data-ttu-id="1b4e1-124">In many online communities, after users upload images or other type of content, the offensive may get shared multiple times over the following days, weeks, and months.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-124">In many online communities, after users upload images or other type of content, the offensive may get shared multiple times over the following days, weeks, and months.</span></span> <span data-ttu-id="1b4e1-125">The costs of repeatedly scanning and filtering out the same image or even slightly modified versions of the image from multiple places can be expensive and error-prone.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-125">The costs of repeatedly scanning and filtering out the same image or even slightly modified versions of the image from multiple places can be expensive and error-prone.</span></span>

<span data-ttu-id="1b4e1-126">Instead of moderating the same image multiple times, you may want to add the offensive images to your custom list of blocked content.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-126">Instead of moderating the same image multiple times, you may want to add the offensive images to your custom list of blocked content.</span></span> <span data-ttu-id="1b4e1-127">That way, your content moderation system can compare incoming images against your custom list of images and stop any further processing right away.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-127">That way, your content moderation system can compare incoming images against your custom list of images and stop any further processing right away.</span></span>

<span data-ttu-id="1b4e1-128">The **Match** operation allows fuzzy matching of incoming images against any of your custom lists, created and managed using the List operations.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-128">The **Match** operation allows fuzzy matching of incoming images against any of your custom lists, created and managed using the List operations.</span></span>

<span data-ttu-id="1b4e1-129">If found, the operation returns the identifier and the moderation tags of the matched image.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-129">If found, the operation returns the identifier and the moderation tags of the matched image.</span></span> <span data-ttu-id="1b4e1-130">The information includes:</span><span class="sxs-lookup"><span data-stu-id="1b4e1-130">The information includes:</span></span>

- <span data-ttu-id="1b4e1-131">Match score (between 0 & 1)</span><span class="sxs-lookup"><span data-stu-id="1b4e1-131">Match score (between 0 & 1)</span></span>
- <span data-ttu-id="1b4e1-132">Matched image</span><span class="sxs-lookup"><span data-stu-id="1b4e1-132">Matched image</span></span>
- <span data-ttu-id="1b4e1-133">Image tags (assigned during a previous moderation)</span><span class="sxs-lookup"><span data-stu-id="1b4e1-133">Image tags (assigned during a previous moderation)</span></span>
- <span data-ttu-id="1b4e1-134">Image labels</span><span class="sxs-lookup"><span data-stu-id="1b4e1-134">Image labels</span></span>

## <a name="creating-and-managing-your-custom-lists"></a><span data-ttu-id="1b4e1-135">Creating and managing your custom lists</span><span class="sxs-lookup"><span data-stu-id="1b4e1-135">Creating and managing your custom lists</span></span> ##

<span data-ttu-id="1b4e1-136">As mentioned previously, if the images are already tagged, you would match repeated content against pre-approved or pre-rejected images, without having to go through the moderation-and-review workflow.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-136">As mentioned previously, if the images are already tagged, you would match repeated content against pre-approved or pre-rejected images, without having to go through the moderation-and-review workflow.</span></span>

<span data-ttu-id="1b4e1-137">The Content Moderator provides a complete list management API with operations for creating and deleting lists, and for adding and removing images from those lists.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-137">The Content Moderator provides a complete list management API with operations for creating and deleting lists, and for adding and removing images from those lists.</span></span>

<span data-ttu-id="1b4e1-138">A typical sequence of operations would be to:</span><span class="sxs-lookup"><span data-stu-id="1b4e1-138">A typical sequence of operations would be to:</span></span>

1. <span data-ttu-id="1b4e1-139">Create a list.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-139">Create a list.</span></span>
1. <span data-ttu-id="1b4e1-140">Add images to your list.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-140">Add images to your list.</span></span>
1. <span data-ttu-id="1b4e1-141">Match images against the ones in the list.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-141">Match images against the ones in the list.</span></span>
1. <span data-ttu-id="1b4e1-142">Delete image from the list.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-142">Delete image from the list.</span></span>
1. <span data-ttu-id="1b4e1-143">Delete the list.</span><span class="sxs-lookup"><span data-stu-id="1b4e1-143">Delete the list.</span></span>
