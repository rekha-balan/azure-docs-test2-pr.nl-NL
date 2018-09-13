---
title: Review API for Content Moderator | Microsoft Docs
description: The Review API integrates content with the review tool to handle automated moderation and human reviews.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 11/21/2016
ms.author: sajagtap
ms.openlocfilehash: 112914e8ab0d14f8c2b43387aefa8cdec2d95e5d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552875"
---
# <a name="the-review-api"></a><span data-ttu-id="e375f-103">The Review API</span><span class="sxs-lookup"><span data-stu-id="e375f-103">The Review API</span></span>

<span data-ttu-id="e375f-104">Use Content Moderators's review API [(See API reference)](api-reference.md "Content Moderator API Reference") to integrate your content with the review tool to get both automated moderation and human reviews.</span><span class="sxs-lookup"><span data-stu-id="e375f-104">Use Content Moderators's review API [(See API reference)](api-reference.md "Content Moderator API Reference") to integrate your content with the review tool to get both automated moderation and human reviews.</span></span>

<span data-ttu-id="e375f-105">The Review API has a small set of operations that use the underlying moderation APIs to moderate your content and make the tagged images available within the review tool for human review.</span><span class="sxs-lookup"><span data-stu-id="e375f-105">The Review API has a small set of operations that use the underlying moderation APIs to moderate your content and make the tagged images available within the review tool for human review.</span></span>

<span data-ttu-id="e375f-106">Here is a sample sequence of steps you might follow:</span><span class="sxs-lookup"><span data-stu-id="e375f-106">Here is a sample sequence of steps you might follow:</span></span>

1. <span data-ttu-id="e375f-107">Submit an image to start a moderation job.</span><span class="sxs-lookup"><span data-stu-id="e375f-107">Submit an image to start a moderation job.</span></span>
1. <span data-ttu-id="e375f-108">Get details for a moderation job that is either in-progress or completed.</span><span class="sxs-lookup"><span data-stu-id="e375f-108">Get details for a moderation job that is either in-progress or completed.</span></span>
1. <span data-ttu-id="e375f-109">Once the human reviews are completed, get the detailed results.</span><span class="sxs-lookup"><span data-stu-id="e375f-109">Once the human reviews are completed, get the detailed results.</span></span>

## <a name="submitting-an-image-to-start-a-moderation-job"></a><span data-ttu-id="e375f-110">Submitting an image to start a moderation job</span><span class="sxs-lookup"><span data-stu-id="e375f-110">Submitting an image to start a moderation job</span></span> ##
<span data-ttu-id="e375f-111">Use the **Job-Create** operation to start a moderation job for an image.</span><span class="sxs-lookup"><span data-stu-id="e375f-111">Use the **Job-Create** operation to start a moderation job for an image.</span></span> <span data-ttu-id="e375f-112">The Moderator will scan the image and generate reviews by evaluating the default or custom workflow configured within the review tool.</span><span class="sxs-lookup"><span data-stu-id="e375f-112">The Moderator will scan the image and generate reviews by evaluating the default or custom workflow configured within the review tool.</span></span>

<span data-ttu-id="e375f-113">Your inputs will include:</span><span class="sxs-lookup"><span data-stu-id="e375f-113">Your inputs will include:</span></span>

- <span data-ttu-id="e375f-114">The image to be moderated (file or URL)</span><span class="sxs-lookup"><span data-stu-id="e375f-114">The image to be moderated (file or URL)</span></span>
- <span data-ttu-id="e375f-115">The default workflow identifier (“default”)</span><span class="sxs-lookup"><span data-stu-id="e375f-115">The default workflow identifier (“default”)</span></span>
- <span data-ttu-id="e375f-116">Your API callback point for notification</span><span class="sxs-lookup"><span data-stu-id="e375f-116">Your API callback point for notification</span></span>

<span data-ttu-id="e375f-117">The response will return the identifier of the job that was started.</span><span class="sxs-lookup"><span data-stu-id="e375f-117">The response will return the identifier of the job that was started.</span></span>

<span data-ttu-id="e375f-118">Once the job is completed, the operation will use your API callback information to notify you.</span><span class="sxs-lookup"><span data-stu-id="e375f-118">Once the job is completed, the operation will use your API callback information to notify you.</span></span> <span data-ttu-id="e375f-119">You can then use the job identifier to get the detailed information back and take further action.</span><span class="sxs-lookup"><span data-stu-id="e375f-119">You can then use the job identifier to get the detailed information back and take further action.</span></span>

## <a name="getting-details-for-an-in-progress-or-completed-job"></a><span data-ttu-id="e375f-120">Getting details for an in-progress or completed job</span><span class="sxs-lookup"><span data-stu-id="e375f-120">Getting details for an in-progress or completed job</span></span>

<span data-ttu-id="e375f-121">Use the **Job-Get** operation to get the details of a moderation job for the identifier returned by the previous operation.</span><span class="sxs-lookup"><span data-stu-id="e375f-121">Use the **Job-Get** operation to get the details of a moderation job for the identifier returned by the previous operation.</span></span> <span data-ttu-id="e375f-122">Note that while the method returns immediately with the job settings information, the moderation job itself is run asynchronously.</span><span class="sxs-lookup"><span data-stu-id="e375f-122">Note that while the method returns immediately with the job settings information, the moderation job itself is run asynchronously.</span></span> <span data-ttu-id="e375f-123">The results are returned through the callback point, and can also be queried by using the operation that we discuss in the next section.</span><span class="sxs-lookup"><span data-stu-id="e375f-123">The results are returned through the callback point, and can also be queried by using the operation that we discuss in the next section.</span></span>

<span data-ttu-id="e375f-124">Your inputs will include at a minimum:</span><span class="sxs-lookup"><span data-stu-id="e375f-124">Your inputs will include at a minimum:</span></span>

- <span data-ttu-id="e375f-125">The human review team name</span><span class="sxs-lookup"><span data-stu-id="e375f-125">The human review team name</span></span>
- <span data-ttu-id="e375f-126">The job identifier returned by the previous operation</span><span class="sxs-lookup"><span data-stu-id="e375f-126">The job identifier returned by the previous operation</span></span>

<span data-ttu-id="e375f-127">The response will include the following information:</span><span class="sxs-lookup"><span data-stu-id="e375f-127">The response will include the following information:</span></span>

- <span data-ttu-id="e375f-128">The identifier of the review created (use this to get the final review results)</span><span class="sxs-lookup"><span data-stu-id="e375f-128">The identifier of the review created (use this to get the final review results)</span></span>
- <span data-ttu-id="e375f-129">The status of the review (completed or in-progress)</span><span class="sxs-lookup"><span data-stu-id="e375f-129">The status of the review (completed or in-progress)</span></span>
- <span data-ttu-id="e375f-130">The assigned moderation tags (key-value pairs)</span><span class="sxs-lookup"><span data-stu-id="e375f-130">The assigned moderation tags (key-value pairs)</span></span>

## <a name="getting-results-after-a-human-review"></a><span data-ttu-id="e375f-131">Getting results after a human review</span><span class="sxs-lookup"><span data-stu-id="e375f-131">Getting results after a human review</span></span>

<span data-ttu-id="e375f-132">Use the **Review-Get** operation to get the results after a human review of the moderated image is completed.</span><span class="sxs-lookup"><span data-stu-id="e375f-132">Use the **Review-Get** operation to get the results after a human review of the moderated image is completed.</span></span> <span data-ttu-id="e375f-133">You will get notified when your defined callback point is called by the review API.</span><span class="sxs-lookup"><span data-stu-id="e375f-133">You will get notified when your defined callback point is called by the review API.</span></span> <span data-ttu-id="e375f-134">The operation will return two sets of tag data - the tags assigned by the moderation service, and the tags after the human review was completed.</span><span class="sxs-lookup"><span data-stu-id="e375f-134">The operation will return two sets of tag data - the tags assigned by the moderation service, and the tags after the human review was completed.</span></span>

<span data-ttu-id="e375f-135">Your inputs will include at a minimum:</span><span class="sxs-lookup"><span data-stu-id="e375f-135">Your inputs will include at a minimum:</span></span>

- <span data-ttu-id="e375f-136">The human review team name</span><span class="sxs-lookup"><span data-stu-id="e375f-136">The human review team name</span></span>
- <span data-ttu-id="e375f-137">The review identifier returned by the previous operation</span><span class="sxs-lookup"><span data-stu-id="e375f-137">The review identifier returned by the previous operation</span></span>

<span data-ttu-id="e375f-138">The response will include the following information:</span><span class="sxs-lookup"><span data-stu-id="e375f-138">The response will include the following information:</span></span>

- <span data-ttu-id="e375f-139">The tags (key-value pairs) confirmed by the human reviewer</span><span class="sxs-lookup"><span data-stu-id="e375f-139">The tags (key-value pairs) confirmed by the human reviewer</span></span>
- <span data-ttu-id="e375f-140">The tags (key-value pairs) assigned by the moderation service</span><span class="sxs-lookup"><span data-stu-id="e375f-140">The tags (key-value pairs) assigned by the moderation service</span></span>

## <a name="directly-creating-reviews-within-the-review-tool"></a><span data-ttu-id="e375f-141">Directly creating reviews within the review tool</span><span class="sxs-lookup"><span data-stu-id="e375f-141">Directly creating reviews within the review tool</span></span>

<span data-ttu-id="e375f-142">If you want to use the review tool just for the human review capability because you are either already using the moderation APIs, or you want to separate them for other reasons, you can do that using the **Review-Create** operation.</span><span class="sxs-lookup"><span data-stu-id="e375f-142">If you want to use the review tool just for the human review capability because you are either already using the moderation APIs, or you want to separate them for other reasons, you can do that using the **Review-Create** operation.</span></span>

<span data-ttu-id="e375f-143">Your inputs to this operation will include:</span><span class="sxs-lookup"><span data-stu-id="e375f-143">Your inputs to this operation will include:</span></span>

- <span data-ttu-id="e375f-144">The content (image) to be reviewed</span><span class="sxs-lookup"><span data-stu-id="e375f-144">The content (image) to be reviewed</span></span>
- <span data-ttu-id="e375f-145">The tags (key value pairs)</span><span class="sxs-lookup"><span data-stu-id="e375f-145">The tags (key value pairs)</span></span>

## <a name="creating-or-updating-custom-workflow"></a><span data-ttu-id="e375f-146">Creating or updating custom workflow</span><span class="sxs-lookup"><span data-stu-id="e375f-146">Creating or updating custom workflow</span></span>

<span data-ttu-id="e375f-147">While the review tool uses a default workflow, you can also define your custom workflow based on your business rules and content policies.</span><span class="sxs-lookup"><span data-stu-id="e375f-147">While the review tool uses a default workflow, you can also define your custom workflow based on your business rules and content policies.</span></span>

<span data-ttu-id="e375f-148">You would do that using the **Workflow-Create or Update** operation.</span><span class="sxs-lookup"><span data-stu-id="e375f-148">You would do that using the **Workflow-Create or Update** operation.</span></span>

<span data-ttu-id="e375f-149">Your inputs to this operation will include:</span><span class="sxs-lookup"><span data-stu-id="e375f-149">Your inputs to this operation will include:</span></span>

- <span data-ttu-id="e375f-150">The review team name</span><span class="sxs-lookup"><span data-stu-id="e375f-150">The review team name</span></span>
- <span data-ttu-id="e375f-151">The name of your workflow</span><span class="sxs-lookup"><span data-stu-id="e375f-151">The name of your workflow</span></span>

<span data-ttu-id="e375f-152">Your request will contain the expression for describing the workflow.</span><span class="sxs-lookup"><span data-stu-id="e375f-152">Your request will contain the expression for describing the workflow.</span></span> <span data-ttu-id="e375f-153">When creating Jobs, the Expression in the specified workflow is evaluated against the moderator API results.</span><span class="sxs-lookup"><span data-stu-id="e375f-153">When creating Jobs, the Expression in the specified workflow is evaluated against the moderator API results.</span></span>

<span data-ttu-id="e375f-154">For example:</span><span class="sxs-lookup"><span data-stu-id="e375f-154">For example:</span></span>

<span data-ttu-id="e375f-155">Expression with one condition as in: Create review if **adult score > 0.4**.</span><span class="sxs-lookup"><span data-stu-id="e375f-155">Expression with one condition as in: Create review if **adult score > 0.4**.</span></span>

    {
        "ConnectorName": "imagemoderator",
        "OutputName": "adultscore",
        "Operator": "ge",  //- where ge = greater than or equal to
        "Value": "0.4",
        "Type": "Condition"
    }

<span data-ttu-id="e375f-156">Expression with two conditions combined as in: Create review if **(adult score > 0.5 AND racy score > 0.5)**.</span><span class="sxs-lookup"><span data-stu-id="e375f-156">Expression with two conditions combined as in: Create review if **(adult score > 0.5 AND racy score > 0.5)**.</span></span>

    {
        "Left": {
            "ConnectorName": "imagemoderator",
            "OutputName": "adultscore",
            "Operator": "ge",
            "Value": "0.4",
            "Type": "Condition"
        },
        "Right": {
            "ConnectorName": "imagemoderator",
            "OutputName": "racyscore",
            "Operator": "ge",
            "Value": "0.5",
            "Type": "Condition"
        },
        "Combine": "AND",
        "Type": "Combine"
    }

<span data-ttu-id="e375f-157">Please refer to the API Reference for more information and examples.</span><span class="sxs-lookup"><span data-stu-id="e375f-157">Please refer to the API Reference for more information and examples.</span></span>
