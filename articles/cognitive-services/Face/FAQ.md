---
title: Frequently asked questions for the Face API Service | Microsoft Docs
description: Here are answers to the most popular questions about the Face API Service.
services: cognitive-services
author: SteveMSFT
manager: corncar
ms.service: cognitive-services
ms.component: face-api
ms.topic: article
ms.date: 01/26/2017
ms.author: sbowles
ms.openlocfilehash: da2f75deef8a8beea3ba23b6a39eb6d2fe104b54
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800155"
---
# <a name="face-api-frequently-asked-questions"></a><span data-ttu-id="eaa2a-103">Face API Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="eaa2a-103">Face API Frequently Asked Questions</span></span>
### <a name="if-you-cant-find-answers-to-your-questions-in-this-faq-try-asking-the-face-api-community-on-stackoverflowhttpsstackoverflowcomquestionstaggedproject-oxfordormicrosoft-cognitive-or-contact-help-and-support-on-uservoicehttpscognitiveuservoicecom"></a><span data-ttu-id="eaa2a-104">If you can't find answers to your questions in this FAQ, try asking the Face API community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) or contact Help and Support on [UserVoice](https://cognitive.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="eaa2a-104">If you can't find answers to your questions in this FAQ, try asking the Face API community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) or contact Help and Support on [UserVoice](https://cognitive.uservoice.com/).</span></span>

-----
<span data-ttu-id="eaa2a-105">**Question**: What factors can reduce Face API’s accuracy for Recognition, Verification, or Find Similar?</span><span class="sxs-lookup"><span data-stu-id="eaa2a-105">**Question**: What factors can reduce Face API’s accuracy for Recognition, Verification, or Find Similar?</span></span>

<span data-ttu-id="eaa2a-106">**Answer**: Generally it is the same cases where humans have difficulty identifying someone including;</span><span class="sxs-lookup"><span data-stu-id="eaa2a-106">**Answer**: Generally it is the same cases where humans have difficulty identifying someone including;</span></span>
* <span data-ttu-id="eaa2a-107">Obstructions blocking one or both eyes</span><span class="sxs-lookup"><span data-stu-id="eaa2a-107">Obstructions blocking one or both eyes</span></span>
* <span data-ttu-id="eaa2a-108">Harsh lighting, e.g. severe backlighting</span><span class="sxs-lookup"><span data-stu-id="eaa2a-108">Harsh lighting, e.g. severe backlighting</span></span>
* <span data-ttu-id="eaa2a-109">Changes to hair style or facial hair</span><span class="sxs-lookup"><span data-stu-id="eaa2a-109">Changes to hair style or facial hair</span></span>
* <span data-ttu-id="eaa2a-110">Changes due to age</span><span class="sxs-lookup"><span data-stu-id="eaa2a-110">Changes due to age</span></span>
* <span data-ttu-id="eaa2a-111">Extreme facial expressions (e.g. screaming)</span><span class="sxs-lookup"><span data-stu-id="eaa2a-111">Extreme facial expressions (e.g. screaming)</span></span>

<span data-ttu-id="eaa2a-112">Face API is often successful in challenging cases like these, but accuracy can be reduced.</span><span class="sxs-lookup"><span data-stu-id="eaa2a-112">Face API is often successful in challenging cases like these, but accuracy can be reduced.</span></span> <span data-ttu-id="eaa2a-113">To make recognition more robust and address these challenges, train your Persons with photos that include a diversity of angles and lighting.</span><span class="sxs-lookup"><span data-stu-id="eaa2a-113">To make recognition more robust and address these challenges, train your Persons with photos that include a diversity of angles and lighting.</span></span>

-----
<span data-ttu-id="eaa2a-114">**Question**:  I am passing the binary image data in but I get an "Invalid face image" error.</span><span class="sxs-lookup"><span data-stu-id="eaa2a-114">**Question**:  I am passing the binary image data in but I get an "Invalid face image" error.</span></span>

<span data-ttu-id="eaa2a-115">**Answer**:  This implies that the algorithm had an issue parsing the image.</span><span class="sxs-lookup"><span data-stu-id="eaa2a-115">**Answer**:  This implies that the algorithm had an issue parsing the image.</span></span> <span data-ttu-id="eaa2a-116">Causes include:</span><span class="sxs-lookup"><span data-stu-id="eaa2a-116">Causes include:</span></span>
* <span data-ttu-id="eaa2a-117">The supported input image formats includes JPEG, PNG, GIF(the first frame), BMP.</span><span class="sxs-lookup"><span data-stu-id="eaa2a-117">The supported input image formats includes JPEG, PNG, GIF(the first frame), BMP.</span></span>
* <span data-ttu-id="eaa2a-118">Image file size should be no larger than 4MB</span><span class="sxs-lookup"><span data-stu-id="eaa2a-118">Image file size should be no larger than 4MB</span></span>
* <span data-ttu-id="eaa2a-119">The detectable face size range is 36x36 to 4096x4096 pixels.</span><span class="sxs-lookup"><span data-stu-id="eaa2a-119">The detectable face size range is 36x36 to 4096x4096 pixels.</span></span> <span data-ttu-id="eaa2a-120">Faces out of this range will not be detected</span><span class="sxs-lookup"><span data-stu-id="eaa2a-120">Faces out of this range will not be detected</span></span>
* <span data-ttu-id="eaa2a-121">Some faces may not be detected due to technical challenges, e.g. very large face angles (head-pose), large occlusion.</span><span class="sxs-lookup"><span data-stu-id="eaa2a-121">Some faces may not be detected due to technical challenges, e.g. very large face angles (head-pose), large occlusion.</span></span> <span data-ttu-id="eaa2a-122">Frontal and near-frontal faces have the best results</span><span class="sxs-lookup"><span data-stu-id="eaa2a-122">Frontal and near-frontal faces have the best results</span></span>

-----
