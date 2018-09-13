---
title: Azure Content Moderator - Moderation jobs and human-in-the-loop reviews | Microsoft Docs
description: Apply human oversight to machine-assisted moderation for best results.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 1/21/2018
ms.author: sajagtap
ms.openlocfilehash: 35b3cdaa410712c3fd08d3df4ebe4c83e3955d50
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44785361"
---
# <a name="moderation-jobs-and-reviews"></a><span data-ttu-id="5bb0c-103">Moderation jobs and reviews</span><span class="sxs-lookup"><span data-stu-id="5bb0c-103">Moderation jobs and reviews</span></span>

<span data-ttu-id="5bb0c-104">Combine machine-assisted moderation with human-in-the-loop capabilities by using the Azure Content Moderator [Review API](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5) to get the best results for your business.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-104">Combine machine-assisted moderation with human-in-the-loop capabilities by using the Azure Content Moderator [Review API](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5) to get the best results for your business.</span></span>

<span data-ttu-id="5bb0c-105">The Review API offers the following ways to include human oversight in your content moderation process:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-105">The Review API offers the following ways to include human oversight in your content moderation process:</span></span>

* <span data-ttu-id="5bb0c-106">`Job` operations are used to start machine-assisted moderation and human review creation as one step.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-106">`Job` operations are used to start machine-assisted moderation and human review creation as one step.</span></span>
* <span data-ttu-id="5bb0c-107">`Review` operations are used for human review creation, outside of the moderation step.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-107">`Review` operations are used for human review creation, outside of the moderation step.</span></span>
* <span data-ttu-id="5bb0c-108">`Workflow` operations are used to manage workflows that automate scanning with thresholds for review creation.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-108">`Workflow` operations are used to manage workflows that automate scanning with thresholds for review creation.</span></span>

<span data-ttu-id="5bb0c-109">The `Job` and `Review` operations accept your callback endpoints for receiving status and results.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-109">The `Job` and `Review` operations accept your callback endpoints for receiving status and results.</span></span>

<span data-ttu-id="5bb0c-110">This article covers the `Job` and `Review` operations.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-110">This article covers the `Job` and `Review` operations.</span></span> <span data-ttu-id="5bb0c-111">Read the [Workflows overview](workflow-api.md) for information on how to create, edit, and get workflow definitions.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-111">Read the [Workflows overview](workflow-api.md) for information on how to create, edit, and get workflow definitions.</span></span>

## <a name="job-operations"></a><span data-ttu-id="5bb0c-112">Job operations</span><span class="sxs-lookup"><span data-stu-id="5bb0c-112">Job operations</span></span>

### <a name="start-a-job"></a><span data-ttu-id="5bb0c-113">Start a job</span><span class="sxs-lookup"><span data-stu-id="5bb0c-113">Start a job</span></span>
<span data-ttu-id="5bb0c-114">Use the `Job.Create` operation to start a moderation and human review creation job.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-114">Use the `Job.Create` operation to start a moderation and human review creation job.</span></span> <span data-ttu-id="5bb0c-115">Content Moderator scans the content and evaluates the designated workflow.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-115">Content Moderator scans the content and evaluates the designated workflow.</span></span> <span data-ttu-id="5bb0c-116">Based on the workflow results, it either creates reviews or skips the step.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-116">Based on the workflow results, it either creates reviews or skips the step.</span></span> <span data-ttu-id="5bb0c-117">It also submits the post-moderation and post-review tags to your callback endpoint.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-117">It also submits the post-moderation and post-review tags to your callback endpoint.</span></span>

<span data-ttu-id="5bb0c-118">The inputs include the following information:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-118">The inputs include the following information:</span></span>

- <span data-ttu-id="5bb0c-119">The review team ID.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-119">The review team ID.</span></span>
- <span data-ttu-id="5bb0c-120">The content to be moderated.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-120">The content to be moderated.</span></span>
- <span data-ttu-id="5bb0c-121">The workflow name.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-121">The workflow name.</span></span> <span data-ttu-id="5bb0c-122">(The default is the "default" workflow.)</span><span class="sxs-lookup"><span data-stu-id="5bb0c-122">(The default is the "default" workflow.)</span></span>
- <span data-ttu-id="5bb0c-123">Your API callback point for notifications.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-123">Your API callback point for notifications.</span></span>
 
<span data-ttu-id="5bb0c-124">The following response shows the identifier of the job that was started.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-124">The following response shows the identifier of the job that was started.</span></span> <span data-ttu-id="5bb0c-125">You use the job identifier to get the job status and receive detailed information.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-125">You use the job identifier to get the job status and receive detailed information.</span></span>

    {
        "JobId": "2018014caceddebfe9446fab29056fd8d31ffe"
    }

### <a name="get-job-status"></a><span data-ttu-id="5bb0c-126">Get job status</span><span class="sxs-lookup"><span data-stu-id="5bb0c-126">Get job status</span></span>

<span data-ttu-id="5bb0c-127">Use the `Job.Get` operation and the job identifier to get the details of a running or completed job.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-127">Use the `Job.Get` operation and the job identifier to get the details of a running or completed job.</span></span> <span data-ttu-id="5bb0c-128">The operation returns immediately while the moderation job runs asynchronously.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-128">The operation returns immediately while the moderation job runs asynchronously.</span></span> <span data-ttu-id="5bb0c-129">The results are returned through the callback endpoint.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-129">The results are returned through the callback endpoint.</span></span>

<span data-ttu-id="5bb0c-130">Your inputs include the following information:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-130">Your inputs include the following information:</span></span>

- <span data-ttu-id="5bb0c-131">The review team ID: The job identifier returned by the previous operation</span><span class="sxs-lookup"><span data-stu-id="5bb0c-131">The review team ID: The job identifier returned by the previous operation</span></span>

<span data-ttu-id="5bb0c-132">The response includes the following information:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-132">The response includes the following information:</span></span>

- <span data-ttu-id="5bb0c-133">The identifier of the review created.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-133">The identifier of the review created.</span></span> <span data-ttu-id="5bb0c-134">(Use this ID to get the final review results.)</span><span class="sxs-lookup"><span data-stu-id="5bb0c-134">(Use this ID to get the final review results.)</span></span>
- <span data-ttu-id="5bb0c-135">The status of the job (completed or in-progress): The assigned moderation tags (key-value pairs).</span><span class="sxs-lookup"><span data-stu-id="5bb0c-135">The status of the job (completed or in-progress): The assigned moderation tags (key-value pairs).</span></span>
- <span data-ttu-id="5bb0c-136">The job execution report.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-136">The job execution report.</span></span>
 
 
        {
            "Id": "2018014caceddebfe9446fab29056fd8d31ffe",
            "TeamName": "some team name",
            "Status": "Complete",
            "WorkflowId": "OCR",
            "Type": "Image",
            "CallBackEndpoint": "",
            "ReviewId": "201801i28fc0f7cbf424447846e509af853ea54",
            "ResultMetaData":[
            {
            "Key": "hasText",
            "Value": "True"
            },
            {
            "Key": "ocrText",
            "Value": "IF WE DID \r\nALL \r\nTHE THINGS \r\nWE ARE \r\nCAPABLE \r\nOF DOING, \r\nWE WOULD \r\nLITERALLY \r\nASTOUND \r\nOURSELVE \r\n"
            }
            ],
            "JobExecutionReport": [
            {
                "Ts": "2018-01-07T00:38:29.3238715",
                "Msg": "Posted results to the Callbackendpoint: https://requestb.in/vxke1mvx"
                },
                {
                "Ts": "2018-01-07T00:38:29.2928416",
                "Msg": "Job marked completed and job content has been removed"
                },
                {
                "Ts": "2018-01-07T00:38:29.0856472",
                "Msg": "Execution Complete"
                },
            {
                "Ts": "2018-01-07T00:38:26.7714671",
                "Msg": "Successfully got hasText response from Moderator"
                },
                {
                "Ts": "2018-01-07T00:38:26.4181346",
                "Msg": "Getting hasText from Moderator"
                },
                {
                "Ts": "2018-01-07T00:38:25.5122828",
                "Msg": "Starting Execution - Try 1"
                }
            ]
        }
 
![Image review for human moderators](images/ocr-sample-image.PNG)

## <a name="review-operations"></a><span data-ttu-id="5bb0c-138">Review operations</span><span class="sxs-lookup"><span data-stu-id="5bb0c-138">Review operations</span></span>

### <a name="create-reviews"></a><span data-ttu-id="5bb0c-139">Create reviews</span><span class="sxs-lookup"><span data-stu-id="5bb0c-139">Create reviews</span></span>

<span data-ttu-id="5bb0c-140">Use the `Review.Create` operation to create the human reviews.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-140">Use the `Review.Create` operation to create the human reviews.</span></span> <span data-ttu-id="5bb0c-141">You either moderate them elsewhere or use custom logic to assign the moderation tags.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-141">You either moderate them elsewhere or use custom logic to assign the moderation tags.</span></span>

<span data-ttu-id="5bb0c-142">Your inputs to this operation include:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-142">Your inputs to this operation include:</span></span>

- <span data-ttu-id="5bb0c-143">The content to be reviewed.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-143">The content to be reviewed.</span></span>
- <span data-ttu-id="5bb0c-144">The assigned tags (key value pairs) for review by human moderators.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-144">The assigned tags (key value pairs) for review by human moderators.</span></span>

<span data-ttu-id="5bb0c-145">The following response shows the review identifier:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-145">The following response shows the review identifier:</span></span>

    [
        "201712i46950138c61a4740b118a43cac33f434",
    ]


### <a name="get-review-status"></a><span data-ttu-id="5bb0c-146">Get review status</span><span class="sxs-lookup"><span data-stu-id="5bb0c-146">Get review status</span></span>
<span data-ttu-id="5bb0c-147">Use the `Review.Get` operation to get the results after a human review of the moderated image is completed.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-147">Use the `Review.Get` operation to get the results after a human review of the moderated image is completed.</span></span> <span data-ttu-id="5bb0c-148">You get notified via your provided callback endpoint.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-148">You get notified via your provided callback endpoint.</span></span> 

<span data-ttu-id="5bb0c-149">The operation returns two sets of tags:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-149">The operation returns two sets of tags:</span></span> 

* <span data-ttu-id="5bb0c-150">The tags assigned by the moderation service</span><span class="sxs-lookup"><span data-stu-id="5bb0c-150">The tags assigned by the moderation service</span></span>
* <span data-ttu-id="5bb0c-151">The tags after the human review was completed</span><span class="sxs-lookup"><span data-stu-id="5bb0c-151">The tags after the human review was completed</span></span>

<span data-ttu-id="5bb0c-152">Your inputs include at a minimum:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-152">Your inputs include at a minimum:</span></span>

- <span data-ttu-id="5bb0c-153">The review team name</span><span class="sxs-lookup"><span data-stu-id="5bb0c-153">The review team name</span></span>
- <span data-ttu-id="5bb0c-154">The review identifier returned by the previous operation</span><span class="sxs-lookup"><span data-stu-id="5bb0c-154">The review identifier returned by the previous operation</span></span>

<span data-ttu-id="5bb0c-155">The response includes the following information:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-155">The response includes the following information:</span></span>

- <span data-ttu-id="5bb0c-156">The review status</span><span class="sxs-lookup"><span data-stu-id="5bb0c-156">The review status</span></span>
- <span data-ttu-id="5bb0c-157">The tags (key-value pairs) confirmed by the human reviewer</span><span class="sxs-lookup"><span data-stu-id="5bb0c-157">The tags (key-value pairs) confirmed by the human reviewer</span></span>
- <span data-ttu-id="5bb0c-158">The tags (key-value pairs) assigned by the moderation service</span><span class="sxs-lookup"><span data-stu-id="5bb0c-158">The tags (key-value pairs) assigned by the moderation service</span></span>

<span data-ttu-id="5bb0c-159">You see both the reviewer-assigned tags (**reviewerResultTags**) and the initial tags (**metadata**) in the following sample response:</span><span class="sxs-lookup"><span data-stu-id="5bb0c-159">You see both the reviewer-assigned tags (**reviewerResultTags**) and the initial tags (**metadata**) in the following sample response:</span></span>

    {
        "reviewId": "201712i46950138c61a4740b118a43cac33f434",
        "subTeam": "public",
        "status": "Complete",
        "reviewerResultTags": [
        {
            "key": "a",
            "value": "False"
        },
        {
            "key": "r",
            "value": "True"
        },
        {
            "key": "sc",
            "value": "True"
        }
        ],
        "createdBy": "{teamname}",
        "metadata": [
        {
            "key": "sc",
            "value": "true"
        }
        ],
        "type": "Image",
        "content": "https://reviewcontentprod.blob.core.windows.net/{teamname}/IMG_201712i46950138c61a4740b118a43cac33f434",
        "contentId": "0",
        "callbackEndpoint": "{callbackUrl}"
    }

## <a name="next-steps"></a><span data-ttu-id="5bb0c-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="5bb0c-160">Next steps</span></span>

* <span data-ttu-id="5bb0c-161">Test drive the [Job API console](try-review-api-job.md), and use the REST API code samples.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-161">Test drive the [Job API console](try-review-api-job.md), and use the REST API code samples.</span></span> <span data-ttu-id="5bb0c-162">If you're familiar with Visual Studio and C#, also check out the [Jobs .NET quickstart](moderation-jobs-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5bb0c-162">If you're familiar with Visual Studio and C#, also check out the [Jobs .NET quickstart](moderation-jobs-quickstart-dotnet.md).</span></span> 
* <span data-ttu-id="5bb0c-163">For reviews, get started with the [Review API console](try-review-api-review.md), and use the REST API code samples.</span><span class="sxs-lookup"><span data-stu-id="5bb0c-163">For reviews, get started with the [Review API console](try-review-api-review.md), and use the REST API code samples.</span></span> <span data-ttu-id="5bb0c-164">Then see the [Reviews .NET quickstart](moderation-reviews-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5bb0c-164">Then see the [Reviews .NET quickstart](moderation-reviews-quickstart-dotnet.md).</span></span>
* <span data-ttu-id="5bb0c-165">For video reviews, use the [Video review quickstart](video-reviews-quickstart-dotnet.md), and learn how to [add transcripts to the video review](video-transcript-reviews-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5bb0c-165">For video reviews, use the [Video review quickstart](video-reviews-quickstart-dotnet.md), and learn how to [add transcripts to the video review](video-transcript-reviews-quickstart-dotnet.md).</span></span>
