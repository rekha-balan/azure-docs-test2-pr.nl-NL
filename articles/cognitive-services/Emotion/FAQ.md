---
title: Emotion API FAQs | Microsoft Docs
description: Get answers to frequently asked questions about the Emotion API in Cognitive Services.
services: cognitive-services
author: anrothMSFT
manager: corncar
ms.service: cognitive-services
ms.component: emotion-api
ms.topic: article
ms.date: 01/26/2017
ms.author: anroth
ms.openlocfilehash: 8532d7c00fd8d7b01d84b5e55cb9bbc60241789c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809813"
---
# <a name="emotion-api-frequently-asked-questions"></a><span data-ttu-id="64d67-103">Emotion API Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="64d67-103">Emotion API Frequently Asked Questions</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="64d67-104">Video API Preview will end on October 30th, 2017.</span><span class="sxs-lookup"><span data-stu-id="64d67-104">Video API Preview will end on October 30th, 2017.</span></span> <span data-ttu-id="64d67-105">Try the new [Video Indexer API Preview](https://azure.microsoft.com/services/cognitive-services/video-indexer/) to easily extract insights from videos and to enhance content discovery experiences, such as search results, by detecting spoken words, faces, characters, and emotions.</span><span class="sxs-lookup"><span data-stu-id="64d67-105">Try the new [Video Indexer API Preview](https://azure.microsoft.com/services/cognitive-services/video-indexer/) to easily extract insights from videos and to enhance content discovery experiences, such as search results, by detecting spoken words, faces, characters, and emotions.</span></span> <span data-ttu-id="64d67-106">[Learn more](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview).</span><span class="sxs-lookup"><span data-stu-id="64d67-106">[Learn more](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview).</span></span>

### <a name="if-you-cant-find-answers-to-your-questions-in-this-faq-try-asking-the-emotion-api-community-on-stackoverflowhttpsstackoverflowcomquestionstaggedproject-oxfordormicrosoft-cognitive-or-contact-help-and-support-on-uservoicehttpscognitiveuservoicecom"></a><span data-ttu-id="64d67-107">If you can't find answers to your questions in this FAQ, try asking the Emotion API community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) or contact Help and Support on [UserVoice](https://cognitive.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="64d67-107">If you can't find answers to your questions in this FAQ, try asking the Emotion API community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) or contact Help and Support on [UserVoice](https://cognitive.uservoice.com/).</span></span>  

-----

<span data-ttu-id="64d67-108">**Question**: *What types of images get the best results from Emotion API?*</span><span class="sxs-lookup"><span data-stu-id="64d67-108">**Question**: *What types of images get the best results from Emotion API?*</span></span>

<span data-ttu-id="64d67-109">**Answer**: Use unobstructed, full frontal facial images for best results.</span><span class="sxs-lookup"><span data-stu-id="64d67-109">**Answer**: Use unobstructed, full frontal facial images for best results.</span></span> <span data-ttu-id="64d67-110">Reliability decreases with partial frontal faces and Emotion API may not recognize emotions in images where the face is rotated 45 degrees or more.</span><span class="sxs-lookup"><span data-stu-id="64d67-110">Reliability decreases with partial frontal faces and Emotion API may not recognize emotions in images where the face is rotated 45 degrees or more.</span></span>

-----

<span data-ttu-id="64d67-111">**Question**: *How many emotions can Emotion API identify?*</span><span class="sxs-lookup"><span data-stu-id="64d67-111">**Question**: *How many emotions can Emotion API identify?*</span></span>

<span data-ttu-id="64d67-112">**Answer**: Emotion API recognizes eight different universally-accepted emotions:</span><span class="sxs-lookup"><span data-stu-id="64d67-112">**Answer**: Emotion API recognizes eight different universally-accepted emotions:</span></span> 
* <span data-ttu-id="64d67-113">Happiness</span><span class="sxs-lookup"><span data-stu-id="64d67-113">Happiness</span></span>
* <span data-ttu-id="64d67-114">Sadness</span><span class="sxs-lookup"><span data-stu-id="64d67-114">Sadness</span></span>
* <span data-ttu-id="64d67-115">Surprise</span><span class="sxs-lookup"><span data-stu-id="64d67-115">Surprise</span></span>
* <span data-ttu-id="64d67-116">Anger</span><span class="sxs-lookup"><span data-stu-id="64d67-116">Anger</span></span>
* <span data-ttu-id="64d67-117">Fear</span><span class="sxs-lookup"><span data-stu-id="64d67-117">Fear</span></span>
* <span data-ttu-id="64d67-118">Contempt</span><span class="sxs-lookup"><span data-stu-id="64d67-118">Contempt</span></span>
* <span data-ttu-id="64d67-119">Disgust</span><span class="sxs-lookup"><span data-stu-id="64d67-119">Disgust</span></span> 
* <span data-ttu-id="64d67-120">Neutral</span><span class="sxs-lookup"><span data-stu-id="64d67-120">Neutral</span></span> 

-----

<span data-ttu-id="64d67-121">**Question**: *Is there any way to pass a live video stream to the API and get the result simultaneously?*</span><span class="sxs-lookup"><span data-stu-id="64d67-121">**Question**: *Is there any way to pass a live video stream to the API and get the result simultaneously?*</span></span>

<span data-ttu-id="64d67-122">**Answer**: Use the image based emotion API and call it on each frame or skip frames for performance.</span><span class="sxs-lookup"><span data-stu-id="64d67-122">**Answer**: Use the image based emotion API and call it on each frame or skip frames for performance.</span></span>  <span data-ttu-id="64d67-123">Video Frame-by-Frame Analysis samples are available.</span><span class="sxs-lookup"><span data-stu-id="64d67-123">Video Frame-by-Frame Analysis samples are available.</span></span>

-----

<span data-ttu-id="64d67-124">**Question**: *I am passing the binary image data in but it gives me: "Invalid face image.*\*</span><span class="sxs-lookup"><span data-stu-id="64d67-124">**Question**: *I am passing the binary image data in but it gives me: "Invalid face image.*\*</span></span>

<span data-ttu-id="64d67-125">**Answer**: This implies that the algorithm had an issue parsing the image.</span><span class="sxs-lookup"><span data-stu-id="64d67-125">**Answer**: This implies that the algorithm had an issue parsing the image.</span></span>  
* <span data-ttu-id="64d67-126">The supported input image formats includes JPEG, PNG, GIF(the first frame), BMP.</span><span class="sxs-lookup"><span data-stu-id="64d67-126">The supported input image formats includes JPEG, PNG, GIF(the first frame), BMP.</span></span> 
* <span data-ttu-id="64d67-127">Image file size should be no larger than 4MB</span><span class="sxs-lookup"><span data-stu-id="64d67-127">Image file size should be no larger than 4MB</span></span>
* <span data-ttu-id="64d67-128">The detectable face size range is 36x36 to 4096x4096 pixels.</span><span class="sxs-lookup"><span data-stu-id="64d67-128">The detectable face size range is 36x36 to 4096x4096 pixels.</span></span> <span data-ttu-id="64d67-129">Faces out of this range will not be detected</span><span class="sxs-lookup"><span data-stu-id="64d67-129">Faces out of this range will not be detected</span></span>
* <span data-ttu-id="64d67-130">Some faces may not be detected due to technical challenges, e.g. very large face angles (head-pose), large occlusion.</span><span class="sxs-lookup"><span data-stu-id="64d67-130">Some faces may not be detected due to technical challenges, e.g. very large face angles (head-pose), large occlusion.</span></span> <span data-ttu-id="64d67-131">Frontal and near-frontal faces have the best results</span><span class="sxs-lookup"><span data-stu-id="64d67-131">Frontal and near-frontal faces have the best results</span></span>

-----
