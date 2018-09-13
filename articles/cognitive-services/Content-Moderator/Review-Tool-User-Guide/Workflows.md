---
title: Define and use workflows in Azure Content Moderator | Microsoft Docs
description: Learn how to create custom workflows based on your content policies.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/07/2018
ms.author: sajagtap
ms.openlocfilehash: dfe3ba8a2ef1bcbc69ef585b504a9367d9420bf0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803716"
---
# <a name="define-test-and-use-workflows"></a><span data-ttu-id="afcb1-103">Define, test, and use workflows</span><span class="sxs-lookup"><span data-stu-id="afcb1-103">Define, test, and use workflows</span></span>

<span data-ttu-id="afcb1-104">You can use the Azure Content Moderator workflow designer and APIs to define custom workflows and thresholds based on your content policies.</span><span class="sxs-lookup"><span data-stu-id="afcb1-104">You can use the Azure Content Moderator workflow designer and APIs to define custom workflows and thresholds based on your content policies.</span></span>

<span data-ttu-id="afcb1-105">Workflows "connect" to the Content Moderator API by using connectors.</span><span class="sxs-lookup"><span data-stu-id="afcb1-105">Workflows "connect" to the Content Moderator API by using connectors.</span></span> <span data-ttu-id="afcb1-106">You can use other APIs if a connector for that API is available.</span><span class="sxs-lookup"><span data-stu-id="afcb1-106">You can use other APIs if a connector for that API is available.</span></span> <span data-ttu-id="afcb1-107">The example here uses the Content Moderator connector that is included by default.</span><span class="sxs-lookup"><span data-stu-id="afcb1-107">The example here uses the Content Moderator connector that is included by default.</span></span>

## <a name="browse-to-the-workflows-section"></a><span data-ttu-id="afcb1-108">Browse to the Workflows section</span><span class="sxs-lookup"><span data-stu-id="afcb1-108">Browse to the Workflows section</span></span>

<span data-ttu-id="afcb1-109">On the **Settings** tab, select **Workflows**.</span><span class="sxs-lookup"><span data-stu-id="afcb1-109">On the **Settings** tab, select **Workflows**.</span></span>

  ![Workflows setting](images/2-workflows-0.png)

## <a name="start-a-new-workflow"></a><span data-ttu-id="afcb1-111">Start a new workflow</span><span class="sxs-lookup"><span data-stu-id="afcb1-111">Start a new workflow</span></span>

<span data-ttu-id="afcb1-112">Select **Add Workflow**.</span><span class="sxs-lookup"><span data-stu-id="afcb1-112">Select **Add Workflow**.</span></span>

  ![Add a workflow](images/2-workflows-1.png)

## <a name="assign-a-name-and-description"></a><span data-ttu-id="afcb1-114">Assign a name and description</span><span class="sxs-lookup"><span data-stu-id="afcb1-114">Assign a name and description</span></span>

<span data-ttu-id="afcb1-115">Name your workflow, enter a description, and choose whether the workflow handles images or text.</span><span class="sxs-lookup"><span data-stu-id="afcb1-115">Name your workflow, enter a description, and choose whether the workflow handles images or text.</span></span>

  ![Workflow name and description](images/ocr-workflow-step-1.PNG)

## <a name="define-the-evaluation-criteria-condition"></a><span data-ttu-id="afcb1-117">Define the evaluation criteria ("condition")</span><span class="sxs-lookup"><span data-stu-id="afcb1-117">Define the evaluation criteria ("condition")</span></span>

<span data-ttu-id="afcb1-118">In the following screenshot, you see the fields and the If-Then-Else selections that you need to define for your workflows.</span><span class="sxs-lookup"><span data-stu-id="afcb1-118">In the following screenshot, you see the fields and the If-Then-Else selections that you need to define for your workflows.</span></span> <span data-ttu-id="afcb1-119">Choose a connector.</span><span class="sxs-lookup"><span data-stu-id="afcb1-119">Choose a connector.</span></span> <span data-ttu-id="afcb1-120">This example uses **Content Moderator**.</span><span class="sxs-lookup"><span data-stu-id="afcb1-120">This example uses **Content Moderator**.</span></span> <span data-ttu-id="afcb1-121">Depending on the connector you choose, the available options for output change.</span><span class="sxs-lookup"><span data-stu-id="afcb1-121">Depending on the connector you choose, the available options for output change.</span></span>

  ![Define workflow condition](images/ocr-workflow-step-2-condition.PNG)

<span data-ttu-id="afcb1-123">After you choose the connector and its output that you want, select an operator and the value for the condition.</span><span class="sxs-lookup"><span data-stu-id="afcb1-123">After you choose the connector and its output that you want, select an operator and the value for the condition.</span></span>

## <a name="define-the-action-to-take"></a><span data-ttu-id="afcb1-124">Define the action to take</span><span class="sxs-lookup"><span data-stu-id="afcb1-124">Define the action to take</span></span>

<span data-ttu-id="afcb1-125">Select the action to take and the condition to meet.</span><span class="sxs-lookup"><span data-stu-id="afcb1-125">Select the action to take and the condition to meet.</span></span> <span data-ttu-id="afcb1-126">The following example creates an image review, assigns a tag `a`, and highlights it for the condition shown.</span><span class="sxs-lookup"><span data-stu-id="afcb1-126">The following example creates an image review, assigns a tag `a`, and highlights it for the condition shown.</span></span> <span data-ttu-id="afcb1-127">You also can combine multiple conditions to get the results you want.</span><span class="sxs-lookup"><span data-stu-id="afcb1-127">You also can combine multiple conditions to get the results you want.</span></span> <span data-ttu-id="afcb1-128">Optionally, add an alternative (Else) path.</span><span class="sxs-lookup"><span data-stu-id="afcb1-128">Optionally, add an alternative (Else) path.</span></span>

  ![Define workflow action](images/ocr-workflow-step-3-action.PNG)

## <a name="save-your-workflow"></a><span data-ttu-id="afcb1-130">Save your workflow</span><span class="sxs-lookup"><span data-stu-id="afcb1-130">Save your workflow</span></span>

<span data-ttu-id="afcb1-131">Finally, save the workflow, and note the workflow name.</span><span class="sxs-lookup"><span data-stu-id="afcb1-131">Finally, save the workflow, and note the workflow name.</span></span> <span data-ttu-id="afcb1-132">You need the name to start a moderation job by using the Review API.</span><span class="sxs-lookup"><span data-stu-id="afcb1-132">You need the name to start a moderation job by using the Review API.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="afcb1-133">Test the workflow</span><span class="sxs-lookup"><span data-stu-id="afcb1-133">Test the workflow</span></span>

<span data-ttu-id="afcb1-134">Now that you defined a custom workflow, test it with sample content.</span><span class="sxs-lookup"><span data-stu-id="afcb1-134">Now that you defined a custom workflow, test it with sample content.</span></span>

<span data-ttu-id="afcb1-135">Select the corresponding **Execute Workflow** button.</span><span class="sxs-lookup"><span data-stu-id="afcb1-135">Select the corresponding **Execute Workflow** button.</span></span>

  ![Workflow test](images/ocr-workflow-step-6-list.PNG)

### <a name="upload-a-file"></a><span data-ttu-id="afcb1-137">Upload a file</span><span class="sxs-lookup"><span data-stu-id="afcb1-137">Upload a file</span></span>

<span data-ttu-id="afcb1-138">Save the [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png) to your local drive.</span><span class="sxs-lookup"><span data-stu-id="afcb1-138">Save the [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png) to your local drive.</span></span> <span data-ttu-id="afcb1-139">To test the workflow, select **Choose File(s)** and upload the image.</span><span class="sxs-lookup"><span data-stu-id="afcb1-139">To test the workflow, select **Choose File(s)** and upload the image.</span></span>

  ![Upload image file](images/ocr-workflow-step-7-upload.PNG)

### <a name="track-the-workflow"></a><span data-ttu-id="afcb1-141">Track the workflow</span><span class="sxs-lookup"><span data-stu-id="afcb1-141">Track the workflow</span></span>

<span data-ttu-id="afcb1-142">Track the workflow as it executes.</span><span class="sxs-lookup"><span data-stu-id="afcb1-142">Track the workflow as it executes.</span></span>

  ![Track workflow execution](images/ocr-workflow-step-4-test.PNG)

### <a name="review-any-images-flagged-for-human-moderation"></a><span data-ttu-id="afcb1-144">Review any images flagged for human moderation</span><span class="sxs-lookup"><span data-stu-id="afcb1-144">Review any images flagged for human moderation</span></span>

<span data-ttu-id="afcb1-145">To see the image review, go to the **Image** tab under **Review**.</span><span class="sxs-lookup"><span data-stu-id="afcb1-145">To see the image review, go to the **Image** tab under **Review**.</span></span>

  ![Review images](images/ocr-sample-image-workflow1.PNG)

## <a name="next-steps"></a><span data-ttu-id="afcb1-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="afcb1-147">Next steps</span></span> 

<span data-ttu-id="afcb1-148">To invoke the workflow from code, use custom workflows with the [`Job` API console quickstart](../try-review-api-job.md) and the [.NET SDK quickstart](../moderation-jobs-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="afcb1-148">To invoke the workflow from code, use custom workflows with the [`Job` API console quickstart](../try-review-api-job.md) and the [.NET SDK quickstart](../moderation-jobs-quickstart-dotnet.md).</span></span>
