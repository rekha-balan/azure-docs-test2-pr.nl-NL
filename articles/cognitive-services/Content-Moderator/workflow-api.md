---
title: Azure Content Moderator - Moderation workflows | Microsoft Docs
description: Use workflows with content moderation.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 02/04/2018
ms.author: sajagtap
ms.openlocfilehash: 079fcd119f1536f9e76ca57fccc76538b3c3ed78
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966264"
---
# <a name="moderation-workflows"></a><span data-ttu-id="2d753-103">Moderation workflows</span><span class="sxs-lookup"><span data-stu-id="2d753-103">Moderation workflows</span></span>

<span data-ttu-id="2d753-104">Content Moderator includes tools and APIs to manage workflows.</span><span class="sxs-lookup"><span data-stu-id="2d753-104">Content Moderator includes tools and APIs to manage workflows.</span></span> <span data-ttu-id="2d753-105">You use workflows with the [Review API's Job operations](review-api.md) to automate human-in-the-loop review creation based on your content policies and thresholds.</span><span class="sxs-lookup"><span data-stu-id="2d753-105">You use workflows with the [Review API's Job operations](review-api.md) to automate human-in-the-loop review creation based on your content policies and thresholds.</span></span>

<span data-ttu-id="2d753-106">The Review API offers the following ways to include human oversight in your content moderation process:</span><span class="sxs-lookup"><span data-stu-id="2d753-106">The Review API offers the following ways to include human oversight in your content moderation process:</span></span>

1. <span data-ttu-id="2d753-107">The **Job** operations for starting machine-assisted moderation and human review creation as one step.</span><span class="sxs-lookup"><span data-stu-id="2d753-107">The **Job** operations for starting machine-assisted moderation and human review creation as one step.</span></span>
1. <span data-ttu-id="2d753-108">The **Review** operations for human review creation, outside of the moderation step.</span><span class="sxs-lookup"><span data-stu-id="2d753-108">The **Review** operations for human review creation, outside of the moderation step.</span></span>
1. <span data-ttu-id="2d753-109">The **Workflow** operations for managing workflows that automate scanning with thresholds for review creation.</span><span class="sxs-lookup"><span data-stu-id="2d753-109">The **Workflow** operations for managing workflows that automate scanning with thresholds for review creation.</span></span>

<span data-ttu-id="2d753-110">This article covers the **Workflow** operations.</span><span class="sxs-lookup"><span data-stu-id="2d753-110">This article covers the **Workflow** operations.</span></span> <span data-ttu-id="2d753-111">Read the [Jobs and Reviews](review-api.md) overview to learn about content moderation jobs and reviews.</span><span class="sxs-lookup"><span data-stu-id="2d753-111">Read the [Jobs and Reviews](review-api.md) overview to learn about content moderation jobs and reviews.</span></span>

<span data-ttu-id="2d753-112">Checking out the **default** workflow is the best way to get started on understanding workflows in Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="2d753-112">Checking out the **default** workflow is the best way to get started on understanding workflows in Content Moderator.</span></span>

## <a name="your-first-workflow"></a><span data-ttu-id="2d753-113">Your first workflow</span><span class="sxs-lookup"><span data-stu-id="2d753-113">Your first workflow</span></span>

<span data-ttu-id="2d753-114">Your first workflow comes bundled with your [review tool team](https://contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2d753-114">Your first workflow comes bundled with your [review tool team](https://contentmoderator.cognitive.microsoft.com/).</span></span> <span data-ttu-id="2d753-115">Sign up if you have not done so already.</span><span class="sxs-lookup"><span data-stu-id="2d753-115">Sign up if you have not done so already.</span></span>

<span data-ttu-id="2d753-116">Navigate to the [review tool's Workflows](Review-Tool-User-Guide/Workflows.md) screen under the Settings tab. You see a **default** workflow as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="2d753-116">Navigate to the [review tool's Workflows](Review-Tool-User-Guide/Workflows.md) screen under the Settings tab. You see a **default** workflow as shown in the following image:</span></span>

![Content Moderator workflows](Review-Tool-User-Guide/images/2-workflows-1.png)

### <a name="open-the-default-workflow"></a><span data-ttu-id="2d753-118">Open the default workflow</span><span class="sxs-lookup"><span data-stu-id="2d753-118">Open the default workflow</span></span>

<span data-ttu-id="2d753-119">Use the **edit** option to open the workflow editing page as shown in the following image: ![Content Moderator default workflow](images/default-workflow-listed.PNG)</span><span class="sxs-lookup"><span data-stu-id="2d753-119">Use the **edit** option to open the workflow editing page as shown in the following image: ![Content Moderator default workflow](images/default-workflow-listed.PNG)</span></span>

### <a name="the-designer-view"></a><span data-ttu-id="2d753-120">The designer view</span><span class="sxs-lookup"><span data-stu-id="2d753-120">The designer view</span></span>

<span data-ttu-id="2d753-121">You see the **Designer** tab for the workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-121">You see the **Designer** tab for the workflow.</span></span> <span data-ttu-id="2d753-122">The designer view shows the following steps:</span><span class="sxs-lookup"><span data-stu-id="2d753-122">The designer view shows the following steps:</span></span>

1. <span data-ttu-id="2d753-123">The **condition** for the workflow to be evaluated.</span><span class="sxs-lookup"><span data-stu-id="2d753-123">The **condition** for the workflow to be evaluated.</span></span> <span data-ttu-id="2d753-124">In this case, the workflow calls the Content Moderator's image API and checks whether the `isAdult` output equals `true`.</span><span class="sxs-lookup"><span data-stu-id="2d753-124">In this case, the workflow calls the Content Moderator's image API and checks whether the `isAdult` output equals `true`.</span></span>
1. <span data-ttu-id="2d753-125">The **action** to be performed if the condition is met.</span><span class="sxs-lookup"><span data-stu-id="2d753-125">The **action** to be performed if the condition is met.</span></span> <span data-ttu-id="2d753-126">In this case, the workflow creates a review in the review tool if the `isAdult` output is `true`.</span><span class="sxs-lookup"><span data-stu-id="2d753-126">In this case, the workflow creates a review in the review tool if the `isAdult` output is `true`.</span></span>

![Content Moderator default workflow - designer](images/default-workflow-designer.png)

### <a name="the-json-view"></a><span data-ttu-id="2d753-128">The JSON view</span><span class="sxs-lookup"><span data-stu-id="2d753-128">The JSON view</span></span>

<span data-ttu-id="2d753-129">Select the **JSON** tab to see the JSON definition of the workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-129">Select the **JSON** tab to see the JSON definition of the workflow.</span></span>

    {
        "Type": "Logic",
        If": {
            "ConnectorName": "moderator",
            "OutputName": "isAdult",
            "Operator": "eq",
            "Value": "true",
            "Type": "Condition"
        },
        "Then": {
        "Perform": [
        {
            "Name": "createreview",
            "CallbackEndpoint": null,
            "Tags": []
        }
        ],
        "Type": "Actions"
        }
    }

### <a name="key-learning"></a><span data-ttu-id="2d753-130">Key learning</span><span class="sxs-lookup"><span data-stu-id="2d753-130">Key learning</span></span>

<span data-ttu-id="2d753-131">The workflows in Content Moderator are easy to configure and flexible.</span><span class="sxs-lookup"><span data-stu-id="2d753-131">The workflows in Content Moderator are easy to configure and flexible.</span></span> <span data-ttu-id="2d753-132">If the built-in designer does not meet your requirements, write the workflow definition in the **JSON** format.</span><span class="sxs-lookup"><span data-stu-id="2d753-132">If the built-in designer does not meet your requirements, write the workflow definition in the **JSON** format.</span></span> <span data-ttu-id="2d753-133">Then use the JSON definition with the [Workflow API](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59) to create and manage the workflow from your application.</span><span class="sxs-lookup"><span data-stu-id="2d753-133">Then use the JSON definition with the [Workflow API](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59) to create and manage the workflow from your application.</span></span>

## <a name="define-a-custom-workflow"></a><span data-ttu-id="2d753-134">Define a custom workflow</span><span class="sxs-lookup"><span data-stu-id="2d753-134">Define a custom workflow</span></span>

<span data-ttu-id="2d753-135">Content Moderator's workflow capabilities allow defining and using custom workflows.</span><span class="sxs-lookup"><span data-stu-id="2d753-135">Content Moderator's workflow capabilities allow defining and using custom workflows.</span></span> <span data-ttu-id="2d753-136">Use the [review tool workflows how-to](Review-Tool-User-Guide/Workflows.md) article to define a custom workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-136">Use the [review tool workflows how-to](Review-Tool-User-Guide/Workflows.md) article to define a custom workflow.</span></span> <span data-ttu-id="2d753-137">This workflow uses Content Moderator's OCR capability to extract text from a sample image.</span><span class="sxs-lookup"><span data-stu-id="2d753-137">This workflow uses Content Moderator's OCR capability to extract text from a sample image.</span></span> <span data-ttu-id="2d753-138">It then creates a review in the review tool.</span><span class="sxs-lookup"><span data-stu-id="2d753-138">It then creates a review in the review tool.</span></span>

### <a name="the-sample-image"></a><span data-ttu-id="2d753-139">The sample image</span><span class="sxs-lookup"><span data-stu-id="2d753-139">The sample image</span></span>

<span data-ttu-id="2d753-140">Save the [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png) to your local drive.</span><span class="sxs-lookup"><span data-stu-id="2d753-140">Save the [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png) to your local drive.</span></span> <span data-ttu-id="2d753-141">You need this image for your exercise.</span><span class="sxs-lookup"><span data-stu-id="2d753-141">You need this image for your exercise.</span></span>

### <a name="the-designer-view"></a><span data-ttu-id="2d753-142">The designer view</span><span class="sxs-lookup"><span data-stu-id="2d753-142">The designer view</span></span>

<span data-ttu-id="2d753-143">Select the **Designer** tab and the [workflow creation tutorial](Review-Tool-User-Guide/Workflows.md) to define a custom workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-143">Select the **Designer** tab and the [workflow creation tutorial](Review-Tool-User-Guide/Workflows.md) to define a custom workflow.</span></span> <span data-ttu-id="2d753-144">The following image shows the designer's **Condition** view.</span><span class="sxs-lookup"><span data-stu-id="2d753-144">The following image shows the designer's **Condition** view.</span></span> <span data-ttu-id="2d753-145">Refer to the tutorial to see the rest of the steps.</span><span class="sxs-lookup"><span data-stu-id="2d753-145">Refer to the tutorial to see the rest of the steps.</span></span>

![Content Moderator - Workflow condition](Review-Tool-User-Guide/images/ocr-workflow-step-2-condition.PNG)

### <a name="the-json-view"></a><span data-ttu-id="2d753-147">The JSON view</span><span class="sxs-lookup"><span data-stu-id="2d753-147">The JSON view</span></span>

<span data-ttu-id="2d753-148">Select the **JSON** tab to see the following JSON definition of your custom workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-148">Select the **JSON** tab to see the following JSON definition of your custom workflow.</span></span> <span data-ttu-id="2d753-149">Notice how the **If-Then** statements in the JSON definition correspond to the steps you defined using the designer view.</span><span class="sxs-lookup"><span data-stu-id="2d753-149">Notice how the **If-Then** statements in the JSON definition correspond to the steps you defined using the designer view.</span></span>

    {
        "Type": "Logic",
        "If": {
            "ConnectorName": "moderator",
            "OutputName": "hasText",
            "Operator": "eq",
            "Value": "true",
            "Type": "Condition"
        },
        "Then": {
        "Perform": [
        {
            "Name": "createreview",
            "CallbackEndpoint": null,
            "Tags": [
            {
                "Tag": "a",
                "IfCondition": {
                    "ConnectorName": "moderator",
                    "OutputName": "hasText",
                    "Operator": "eq",
                    "Value": "true",
                    "Type": "Condition"
                }
            }
            ]
        }
        ],
        "Type": "Actions"
        }
    }

### <a name="workflow-result"></a><span data-ttu-id="2d753-150">Workflow result</span><span class="sxs-lookup"><span data-stu-id="2d753-150">Workflow result</span></span>

<span data-ttu-id="2d753-151">After you test the workflow from the workflows screen, the following review is created.</span><span class="sxs-lookup"><span data-stu-id="2d753-151">After you test the workflow from the workflows screen, the following review is created.</span></span> <span data-ttu-id="2d753-152">Navigate to the **Image** tab under **Review** to see your review.</span><span class="sxs-lookup"><span data-stu-id="2d753-152">Navigate to the **Image** tab under **Review** to see your review.</span></span>
<span data-ttu-id="2d753-153">The workflow created the review because the primary condition tested positive for the presence of text.</span><span class="sxs-lookup"><span data-stu-id="2d753-153">The workflow created the review because the primary condition tested positive for the presence of text.</span></span> <span data-ttu-id="2d753-154">The review also highlighted the **`a`** tag in the image review.</span><span class="sxs-lookup"><span data-stu-id="2d753-154">The review also highlighted the **`a`** tag in the image review.</span></span>

![Content Moderator - simple workflow output](images/ocr-sample-image-workflow1.PNG)


## <a name="advanced-workflow-with-combination"></a><span data-ttu-id="2d753-156">Advanced workflow with combination</span><span class="sxs-lookup"><span data-stu-id="2d753-156">Advanced workflow with combination</span></span>

### <a name="the-sample-image"></a><span data-ttu-id="2d753-157">The sample image</span><span class="sxs-lookup"><span data-stu-id="2d753-157">The sample image</span></span>

<span data-ttu-id="2d753-158">Use the same [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png) that was used in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="2d753-158">Use the same [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png) that was used in the preceding section.</span></span>

<span data-ttu-id="2d753-159">However, this time around, change your primary condition into a combination of two checks.</span><span class="sxs-lookup"><span data-stu-id="2d753-159">However, this time around, change your primary condition into a combination of two checks.</span></span> <span data-ttu-id="2d753-160">In addition to checking for text, check whether the text has any profanity.</span><span class="sxs-lookup"><span data-stu-id="2d753-160">In addition to checking for text, check whether the text has any profanity.</span></span> <span data-ttu-id="2d753-161">The workflow creates a review if it finds text **and** detects profanity in it.</span><span class="sxs-lookup"><span data-stu-id="2d753-161">The workflow creates a review if it finds text **and** detects profanity in it.</span></span>

### <a name="the-designer-view"></a><span data-ttu-id="2d753-162">The designer view</span><span class="sxs-lookup"><span data-stu-id="2d753-162">The designer view</span></span>

<span data-ttu-id="2d753-163">To change the **Condition** to a **Combination**, modify the workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-163">To change the **Condition** to a **Combination**, modify the workflow.</span></span> <span data-ttu-id="2d753-164">The following image shows the new view you see in the designer.</span><span class="sxs-lookup"><span data-stu-id="2d753-164">The following image shows the new view you see in the designer.</span></span>

![Content Moderator - Modified workflow condition](images/ocr-workflow-2-designer.PNG)

### <a name="the-json-view"></a><span data-ttu-id="2d753-166">The JSON view</span><span class="sxs-lookup"><span data-stu-id="2d753-166">The JSON view</span></span>

<span data-ttu-id="2d753-167">Select the **JSON** tab to see the following JSON definition of your modified custom workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-167">Select the **JSON** tab to see the following JSON definition of your modified custom workflow.</span></span> <span data-ttu-id="2d753-168">Notice how the **If-Then** statements in the JSON definition correspond to the new steps you added to the workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-168">Notice how the **If-Then** statements in the JSON definition correspond to the new steps you added to the workflow.</span></span>

    {
        "Type": "Logic",
        "If": {
        "Left": {
            "ConnectorName": "moderator",
            "OutputName": "hasText",
            "Operator": "eq",
            "Value": "true",
            "Type": "Condition"
            },
        "Right": {
            "ConnectorName": "moderator",
            "OutputName": "text.HasProfanity",
            "Operator": "eq",
            "Value": "true",
            "Type": "Condition",
            "AlternateInput": "moderator.ocrText"
            },
        "Combine": "AND",
        "Type": "Combine"
        },
        "Then": {
        "Perform": [
        {
            "Name": "createreview",
            "CallbackEndpoint": null,
            "Tags": [
            {
                "Tag": "a",
                "IfCondition": {
                    "ConnectorName": "moderator",
                    "OutputName": "hasText",
                    "Operator": "eq",
                    "Value": "true",
                    "Type": "Condition"
                }
            }
            ]
        }
        ],
        "Type": "Actions"
        }
    }

    
### <a name="workflow-result"></a><span data-ttu-id="2d753-169">Workflow result</span><span class="sxs-lookup"><span data-stu-id="2d753-169">Workflow result</span></span>

<span data-ttu-id="2d753-170">After you test the workflow again, you find that no review is created.</span><span class="sxs-lookup"><span data-stu-id="2d753-170">After you test the workflow again, you find that no review is created.</span></span> <span data-ttu-id="2d753-171">To confirm the absence of any review, navigate to the **Image** tab under **Review**.</span><span class="sxs-lookup"><span data-stu-id="2d753-171">To confirm the absence of any review, navigate to the **Image** tab under **Review**.</span></span>
<span data-ttu-id="2d753-172">The workflow did not create the review because it failed to detect profanity in the extracted text.</span><span class="sxs-lookup"><span data-stu-id="2d753-172">The workflow did not create the review because it failed to detect profanity in the extracted text.</span></span>

![Content Moderator - modified workflow output](images/ocr-workflow-2-result.PNG)


## <a name="the-workflow-api"></a><span data-ttu-id="2d753-174">The Workflow API</span><span class="sxs-lookup"><span data-stu-id="2d753-174">The Workflow API</span></span>

<span data-ttu-id="2d753-175">The [Workflow operations](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59) provide the programming interface to the workflow capabilities.</span><span class="sxs-lookup"><span data-stu-id="2d753-175">The [Workflow operations](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59) provide the programming interface to the workflow capabilities.</span></span> <span data-ttu-id="2d753-176">You create workflows, get workflow details, and update workflow definitions using the Workflow API.</span><span class="sxs-lookup"><span data-stu-id="2d753-176">You create workflows, get workflow details, and update workflow definitions using the Workflow API.</span></span>

### <a name="get-all-workflow-details"></a><span data-ttu-id="2d753-177">Get [All] workflow details</span><span class="sxs-lookup"><span data-stu-id="2d753-177">Get [All] workflow details</span></span>

<span data-ttu-id="2d753-178">The **Workflow-Get** operation accepts the following inputs:</span><span class="sxs-lookup"><span data-stu-id="2d753-178">The **Workflow-Get** operation accepts the following inputs:</span></span>

- <span data-ttu-id="2d753-179">**team**: The team ID that you created when you set up your [review tool account](https://contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2d753-179">**team**: The team ID that you created when you set up your [review tool account](https://contentmoderator.cognitive.microsoft.com/).</span></span> 
- <span data-ttu-id="2d753-180">**workflowname**: The name of your workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-180">**workflowname**: The name of your workflow.</span></span> <span data-ttu-id="2d753-181">Use `default` to begin with.</span><span class="sxs-lookup"><span data-stu-id="2d753-181">Use `default` to begin with.</span></span>
- <span data-ttu-id="2d753-182">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d753-182">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span></span>

<span data-ttu-id="2d753-183">If the operation succeeds, the **Response status** is `200 OK` and the **Response content** box displays the workflow definition in the JSON format.</span><span class="sxs-lookup"><span data-stu-id="2d753-183">If the operation succeeds, the **Response status** is `200 OK` and the **Response content** box displays the workflow definition in the JSON format.</span></span>
<span data-ttu-id="2d753-184">To learn more, read the [Workflow API console quickstart](try-review-api-job.md).</span><span class="sxs-lookup"><span data-stu-id="2d753-184">To learn more, read the [Workflow API console quickstart](try-review-api-job.md).</span></span>

### <a name="create-or-update-workflow"></a><span data-ttu-id="2d753-185">Create or update workflow</span><span class="sxs-lookup"><span data-stu-id="2d753-185">Create or update workflow</span></span>

<span data-ttu-id="2d753-186">The creation and update operation allows creating workflow from the API.</span><span class="sxs-lookup"><span data-stu-id="2d753-186">The creation and update operation allows creating workflow from the API.</span></span>

<span data-ttu-id="2d753-187">The **Workflow-Create or Update** operation accepts the following inputs:</span><span class="sxs-lookup"><span data-stu-id="2d753-187">The **Workflow-Create or Update** operation accepts the following inputs:</span></span>

- <span data-ttu-id="2d753-188">**team**: The team ID that you created when you set up your [review tool account](https://contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2d753-188">**team**: The team ID that you created when you set up your [review tool account](https://contentmoderator.cognitive.microsoft.com/).</span></span> 
- <span data-ttu-id="2d753-189">**workflowname**: The name of your workflow.</span><span class="sxs-lookup"><span data-stu-id="2d753-189">**workflowname**: The name of your workflow.</span></span> <span data-ttu-id="2d753-190">Use `default` to begin with.</span><span class="sxs-lookup"><span data-stu-id="2d753-190">Use `default` to begin with.</span></span>
- <span data-ttu-id="2d753-191">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d753-191">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span></span>

<span data-ttu-id="2d753-192">If the operation succeeds, the **Response status** is `200 OK` and the **Response content** box displays `true`.</span><span class="sxs-lookup"><span data-stu-id="2d753-192">If the operation succeeds, the **Response status** is `200 OK` and the **Response content** box displays `true`.</span></span> <span data-ttu-id="2d753-193">To learn more, [test drive the `Create` operation](try-review-api-job.md).</span><span class="sxs-lookup"><span data-stu-id="2d753-193">To learn more, [test drive the `Create` operation](try-review-api-job.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d753-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="2d753-194">Next steps</span></span>

<span data-ttu-id="2d753-195">To learn how to create custom workflows, check out the [review tool's workflow tutorial](Review-Tool-User-Guide/Workflows.md).</span><span class="sxs-lookup"><span data-stu-id="2d753-195">To learn how to create custom workflows, check out the [review tool's workflow tutorial](Review-Tool-User-Guide/Workflows.md).</span></span> 

<span data-ttu-id="2d753-196">Test drive the [Workflow API console](try-review-api-job.md) and use the REST API code samples.</span><span class="sxs-lookup"><span data-stu-id="2d753-196">Test drive the [Workflow API console](try-review-api-job.md) and use the REST API code samples.</span></span> 

<span data-ttu-id="2d753-197">Finally, use your custom workflows with the **Job** operations as shon in [Job API console](try-review-api-job.md) and the [Jobs .NET quickstart](moderation-jobs-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2d753-197">Finally, use your custom workflows with the **Job** operations as shon in [Job API console](try-review-api-job.md) and the [Jobs .NET quickstart](moderation-jobs-quickstart-dotnet.md).</span></span>
