---
title: Emotion API FAQs | Microsoft Docs
description: Get answers to frequently asked questions about the Emotion API in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 01/26/2017
ms.author: anroth
ms.openlocfilehash: ceb16690d29606ea272ec8f64154b7fa51418f75
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551211"
---
# <a name="emotion-api-frequently-asked-questions"></a><span data-ttu-id="e4a24-103">Emotion API Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="e4a24-103">Emotion API Frequently Asked Questions</span></span>
### <a name="if-you-cant-find-answers-to-your-questions-in-this-faq-try-asking-the-emotion-api-community-on-stackoverflowhttpsstackoverflowcomquestionstaggedproject-oxfordormicrosoft-cognitive-or-contact-help-and-support-on-uservoicehttpscognitiveuservoicecom"></a><span data-ttu-id="e4a24-104">If you can't find answers to your questions in this FAQ, try asking the Emotion API community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) or contact Help and Support on [UserVoice](https://cognitive.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="e4a24-104">If you can't find answers to your questions in this FAQ, try asking the Emotion API community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) or contact Help and Support on [UserVoice](https://cognitive.uservoice.com/).</span></span>  

-----

<span data-ttu-id="e4a24-105">**Question**: *What types of images get the best results from Emotion API?*</span><span class="sxs-lookup"><span data-stu-id="e4a24-105">**Question**: *What types of images get the best results from Emotion API?*</span></span>

<span data-ttu-id="e4a24-106">**Answer**: Use unobstructed, full frontal facial images for best results.</span><span class="sxs-lookup"><span data-stu-id="e4a24-106">**Answer**: Use unobstructed, full frontal facial images for best results.</span></span> <span data-ttu-id="e4a24-107">Reliability decreases with partial frontal faces and Emotion API may not recognize emotions in images where the face is rotated 45 degrees or more.</span><span class="sxs-lookup"><span data-stu-id="e4a24-107">Reliability decreases with partial frontal faces and Emotion API may not recognize emotions in images where the face is rotated 45 degrees or more.</span></span>

-----

<span data-ttu-id="e4a24-108">**Question**: *How many emotions can Emotion API identify?*</span><span class="sxs-lookup"><span data-stu-id="e4a24-108">**Question**: *How many emotions can Emotion API identify?*</span></span>

<span data-ttu-id="e4a24-109">**Answer**: Emotion API recognizes eight different universally-accepted emotions:</span><span class="sxs-lookup"><span data-stu-id="e4a24-109">**Answer**: Emotion API recognizes eight different universally-accepted emotions:</span></span> 
* <span data-ttu-id="e4a24-110">Happiness</span><span class="sxs-lookup"><span data-stu-id="e4a24-110">Happiness</span></span>
* <span data-ttu-id="e4a24-111">Sadness</span><span class="sxs-lookup"><span data-stu-id="e4a24-111">Sadness</span></span>
* <span data-ttu-id="e4a24-112">Surprise</span><span class="sxs-lookup"><span data-stu-id="e4a24-112">Surprise</span></span>
* <span data-ttu-id="e4a24-113">Anger</span><span class="sxs-lookup"><span data-stu-id="e4a24-113">Anger</span></span>
* <span data-ttu-id="e4a24-114">Fear</span><span class="sxs-lookup"><span data-stu-id="e4a24-114">Fear</span></span>
* <span data-ttu-id="e4a24-115">Contempt</span><span class="sxs-lookup"><span data-stu-id="e4a24-115">Contempt</span></span>
* <span data-ttu-id="e4a24-116">Disgust</span><span class="sxs-lookup"><span data-stu-id="e4a24-116">Disgust</span></span> 
* <span data-ttu-id="e4a24-117">Neutral</span><span class="sxs-lookup"><span data-stu-id="e4a24-117">Neutral</span></span> 

-----

<span data-ttu-id="e4a24-118">**Question**: *Is there any way to pass a live video stream to the API and get the result simultaneously?*</span><span class="sxs-lookup"><span data-stu-id="e4a24-118">**Question**: *Is there any way to pass a live video stream to the API and get the result simultaneously?*</span></span>

<span data-ttu-id="e4a24-119">**Answer**: Use the image based emotion API and call it on each frame or skip frames for performance.</span><span class="sxs-lookup"><span data-stu-id="e4a24-119">**Answer**: Use the image based emotion API and call it on each frame or skip frames for performance.</span></span>  <span data-ttu-id="e4a24-120">Video Frame-by-Frame Analysis samples are available.</span><span class="sxs-lookup"><span data-stu-id="e4a24-120">Video Frame-by-Frame Analysis samples are available.</span></span>

-----

<span data-ttu-id="e4a24-121">**Question**: *I am passing the binary image data in but it gives me: "Invalid face image.*\*</span><span class="sxs-lookup"><span data-stu-id="e4a24-121">**Question**: *I am passing the binary image data in but it gives me: "Invalid face image.*\*</span></span>

<span data-ttu-id="e4a24-122">**Answer**: This implies that the algorithm had an issue parsing the image.</span><span class="sxs-lookup"><span data-stu-id="e4a24-122">**Answer**: This implies that the algorithm had an issue parsing the image.</span></span>  
* <span data-ttu-id="e4a24-123">The supported input image formats includes JPEG, PNG, GIF(the first frame), BMP.</span><span class="sxs-lookup"><span data-stu-id="e4a24-123">The supported input image formats includes JPEG, PNG, GIF(the first frame), BMP.</span></span> 
* <span data-ttu-id="e4a24-124">Image file size should be no larger than 4MB</span><span class="sxs-lookup"><span data-stu-id="e4a24-124">Image file size should be no larger than 4MB</span></span>
* <span data-ttu-id="e4a24-125">The detectable face size range is 36x36 to 4096x4096 pixels.</span><span class="sxs-lookup"><span data-stu-id="e4a24-125">The detectable face size range is 36x36 to 4096x4096 pixels.</span></span> <span data-ttu-id="e4a24-126">Faces out of this range will not be detected</span><span class="sxs-lookup"><span data-stu-id="e4a24-126">Faces out of this range will not be detected</span></span>
* <span data-ttu-id="e4a24-127">Some faces may not be detected due to technical challenges, e.g. very large face angles (head-pose), large occlusion.</span><span class="sxs-lookup"><span data-stu-id="e4a24-127">Some faces may not be detected due to technical challenges, e.g. very large face angles (head-pose), large occlusion.</span></span> <span data-ttu-id="e4a24-128">Frontal and near-frontal faces have the best results</span><span class="sxs-lookup"><span data-stu-id="e4a24-128">Frontal and near-frontal faces have the best results</span></span>

-----
