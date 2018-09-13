---
title: API reference for Content Moderator  | Microsoft Docs
description: Learn about the Review API, Image and Text Moderation APIs, and List Management API for the Content Moderator.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 02/19/2017
ms.author: sajagtap
ms.openlocfilehash: e07c91b5e08b2693a8401296daa13307395c7868
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551220"
---
# <a name="api-reference"></a><span data-ttu-id="1fe3e-103">API Reference</span><span class="sxs-lookup"><span data-stu-id="1fe3e-103">API Reference</span></span> #
<span data-ttu-id="1fe3e-104">You get started with the Content Moderator APIs in the following ways:</span><span class="sxs-lookup"><span data-stu-id="1fe3e-104">You get started with the Content Moderator APIs in the following ways:</span></span>

  1. <span data-ttu-id="1fe3e-105">[Subscribe to the Content Moderator API](https://portal.azure.com/#create/Microsoft.CognitiveServices/apitype/ContentModerator) on the Microsoft Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-105">[Subscribe to the Content Moderator API](https://portal.azure.com/#create/Microsoft.CognitiveServices/apitype/ContentModerator) on the Microsoft Azure portal.</span></span>
  1. <span data-ttu-id="1fe3e-106">Sign up for the [content moderator review tool](http://contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="1fe3e-106">Sign up for the [content moderator review tool](http://contentmoderator.cognitive.microsoft.com/).</span></span>

<span data-ttu-id="1fe3e-107">If you sign up for the review tool, you will find your free tier key in the **Credentials** TAB under **Settings** as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="1fe3e-107">If you sign up for the review tool, you will find your free tier key in the **Credentials** TAB under **Settings** as shown in the following screenshot:</span></span>

![Your Content Moderator API Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/images/7-Settings-Credentials.png)

## <a name="image-moderation-api"></a><span data-ttu-id="1fe3e-109">Image Moderation API</span><span class="sxs-lookup"><span data-stu-id="1fe3e-109">Image Moderation API</span></span> ##

<span data-ttu-id="1fe3e-110">Use the image moderation API to scan your images and get back predicted tags, their confidence scores, and other extracted information.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-110">Use the image moderation API to scan your images and get back predicted tags, their confidence scores, and other extracted information.</span></span> <span data-ttu-id="1fe3e-111">Use this information to implement your post-moderation workflow such as publish, reject, or review the content within your systems.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-111">Use this information to implement your post-moderation workflow such as publish, reject, or review the content within your systems.</span></span>

[<span data-ttu-id="1fe3e-112">**Image Moderation API Reference**</span><span class="sxs-lookup"><span data-stu-id="1fe3e-112">**Image Moderation API Reference**</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c "Image Moderation API")

## <a name="text-moderation-api"></a><span data-ttu-id="1fe3e-113">Text Moderation API</span><span class="sxs-lookup"><span data-stu-id="1fe3e-113">Text Moderation API</span></span> ##

<span data-ttu-id="1fe3e-114">Use the text moderation API to scan your text content and get back identified profanity terms, predicted tags and confidence scores.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-114">Use the text moderation API to scan your text content and get back identified profanity terms, predicted tags and confidence scores.</span></span> <span data-ttu-id="1fe3e-115">Use this information to implement your post-moderation workflow such as publish, reject, or review the content within your systems.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-115">Use this information to implement your post-moderation workflow such as publish, reject, or review the content within your systems.</span></span>

[<span data-ttu-id="1fe3e-116">**Text Moderation API Reference**</span><span class="sxs-lookup"><span data-stu-id="1fe3e-116">**Text Moderation API Reference**</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f "Text Moderation API")

## <a name="review-api"></a><span data-ttu-id="1fe3e-117">Review API</span><span class="sxs-lookup"><span data-stu-id="1fe3e-117">Review API</span></span> ##

<span data-ttu-id="1fe3e-118">Use the review API to initiate scan-and-review moderation workflows with both image and text content.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-118">Use the review API to initiate scan-and-review moderation workflows with both image and text content.</span></span> <span data-ttu-id="1fe3e-119">The moderation job scans your content by using the image and text moderation APIs.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-119">The moderation job scans your content by using the image and text moderation APIs.</span></span> <span data-ttu-id="1fe3e-120">It then uses the default and custom workflows defined within the review tool to generate reviews within the review tool.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-120">It then uses the default and custom workflows defined within the review tool to generate reviews within the review tool.</span></span> <span data-ttu-id="1fe3e-121">Once your human moderators have reviewed the auto-assigned tags and prediction data and submitted their final decision, the review API submits all information to your API endpoint.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-121">Once your human moderators have reviewed the auto-assigned tags and prediction data and submitted their final decision, the review API submits all information to your API endpoint.</span></span>

[<span data-ttu-id="1fe3e-122">**Review API Reference**</span><span class="sxs-lookup"><span data-stu-id="1fe3e-122">**Review API Reference**</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5 "Content Moderator Review API")

## <a name="workflow-api"></a><span data-ttu-id="1fe3e-123">Workflow API</span><span class="sxs-lookup"><span data-stu-id="1fe3e-123">Workflow API</span></span> ##

<span data-ttu-id="1fe3e-124">Use this API to create, update, and get details of your custom workflows created by your team.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-124">Use this API to create, update, and get details of your custom workflows created by your team.</span></span> <span data-ttu-id="1fe3e-125">You or your team colleagues define these workflows in the review tool.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-125">You or your team colleagues define these workflows in the review tool.</span></span> <span data-ttu-id="1fe3e-126">These workflows use Content Moderator or even other APIs available as connectors within the review tool.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-126">These workflows use Content Moderator or even other APIs available as connectors within the review tool.</span></span>

[<span data-ttu-id="1fe3e-127">**Workflow API Reference**</span><span class="sxs-lookup"><span data-stu-id="1fe3e-127">**Workflow API Reference**</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59 "Content Moderator Workflow API")

## <a name="list-management-api"></a><span data-ttu-id="1fe3e-128">List Management API</span><span class="sxs-lookup"><span data-stu-id="1fe3e-128">List Management API</span></span> ##

<span data-ttu-id="1fe3e-129">Use this API to create and manage your custom exclusion or inclusion lists of images and text.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-129">Use this API to create and manage your custom exclusion or inclusion lists of images and text.</span></span> <span data-ttu-id="1fe3e-130">If enabled, the **Image/Match** and **Text/Screen** operations do fuzzy matching of the submitted content against your custom lists and skip the ML-based moderation step for efficiency.</span><span class="sxs-lookup"><span data-stu-id="1fe3e-130">If enabled, the **Image/Match** and **Text/Screen** operations do fuzzy matching of the submitted content against your custom lists and skip the ML-based moderation step for efficiency.</span></span>

[<span data-ttu-id="1fe3e-131">**List Management API Reference**</span><span class="sxs-lookup"><span data-stu-id="1fe3e-131">**List Management API Reference**</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f675 "Content Moderator List Management API")

