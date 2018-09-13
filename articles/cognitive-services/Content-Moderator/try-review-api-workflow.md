---
title: Azure Content Moderator - Content moderation workflows from the API console | Microsoft Docs
description: Learn how to use content moderation workflows from the API console.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 02/05/2018
ms.author: sajagtap
ms.openlocfilehash: 700b2bea5e902141659266a94d61ceb810c1b802
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965960"
---
# <a name="workflows-from-the-api-console"></a><span data-ttu-id="9ad1d-103">Workflows from the API console</span><span class="sxs-lookup"><span data-stu-id="9ad1d-103">Workflows from the API console</span></span>

<span data-ttu-id="9ad1d-104">Use the [workflow operations](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59) in Azure Content Moderator to create or update a workflow or get workflow details by using the Review API.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-104">Use the [workflow operations](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59) in Azure Content Moderator to create or update a workflow or get workflow details by using the Review API.</span></span> <span data-ttu-id="9ad1d-105">You can define simple, complex, and even nested expressions for your workflows by using this API.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-105">You can define simple, complex, and even nested expressions for your workflows by using this API.</span></span> <span data-ttu-id="9ad1d-106">The workflows appear in the Review tool for your team to use.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-106">The workflows appear in the Review tool for your team to use.</span></span> <span data-ttu-id="9ad1d-107">The workflows also are used by the Review API's Job operations.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-107">The workflows also are used by the Review API's Job operations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ad1d-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9ad1d-108">Prerequisites</span></span>

1. <span data-ttu-id="9ad1d-109">Go to the [Review tool](https://contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-109">Go to the [Review tool](https://contentmoderator.cognitive.microsoft.com/).</span></span> <span data-ttu-id="9ad1d-110">Sign up if you haven't done so yet.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-110">Sign up if you haven't done so yet.</span></span> 
2. <span data-ttu-id="9ad1d-111">In the Review tool, under **Settings**, select the **Workflows** tab, as shown in the Review tool's [workflow tutorial](Review-Tool-User-Guide/Workflows.md).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-111">In the Review tool, under **Settings**, select the **Workflows** tab, as shown in the Review tool's [workflow tutorial](Review-Tool-User-Guide/Workflows.md).</span></span>

### <a name="browse-to-the-workflows-screen"></a><span data-ttu-id="9ad1d-112">Browse to the workflows screen</span><span class="sxs-lookup"><span data-stu-id="9ad1d-112">Browse to the workflows screen</span></span>

<span data-ttu-id="9ad1d-113">On the Content Moderator dashboard, select **Review** > **Settings** > **Workflows**.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-113">On the Content Moderator dashboard, select **Review** > **Settings** > **Workflows**.</span></span> <span data-ttu-id="9ad1d-114">You see a default workflow.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-114">You see a default workflow.</span></span>

  ![Default workflow](images/default-workflow-listed.PNG)

### <a name="get-the-json-definition-of-the-default-workflow"></a><span data-ttu-id="9ad1d-116">Get the JSON definition of the default workflow</span><span class="sxs-lookup"><span data-stu-id="9ad1d-116">Get the JSON definition of the default workflow</span></span>

<span data-ttu-id="9ad1d-117">Select the **Edit** option for your workflow, and then select the **JSON** tab. You see the following JSON expression:</span><span class="sxs-lookup"><span data-stu-id="9ad1d-117">Select the **Edit** option for your workflow, and then select the **JSON** tab. You see the following JSON expression:</span></span>

    {
        "Type": "Logic",
        "If": {
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

## <a name="get-workflow-details"></a><span data-ttu-id="9ad1d-118">Get workflow details</span><span class="sxs-lookup"><span data-stu-id="9ad1d-118">Get workflow details</span></span>

<span data-ttu-id="9ad1d-119">Use the **Workflow - Get** operation to get details of your existing default workflow.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-119">Use the **Workflow - Get** operation to get details of your existing default workflow.</span></span>

<span data-ttu-id="9ad1d-120">In the Review tool, go to the [Credentials](Review-Tool-User-Guide/credentials.md#the-review-tool) section.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-120">In the Review tool, go to the [Credentials](Review-Tool-User-Guide/credentials.md#the-review-tool) section.</span></span>

### <a name="browse-to-the-api-reference"></a><span data-ttu-id="9ad1d-121">Browse to the API reference</span><span class="sxs-lookup"><span data-stu-id="9ad1d-121">Browse to the API reference</span></span>

1. <span data-ttu-id="9ad1d-122">In the **Credentials** view, select [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-122">In the **Credentials** view, select [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59).</span></span> 
2. <span data-ttu-id="9ad1d-123">When the **Workflow - Create Or Update** page opens, go to the [Workflow - Get](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b44b3f9b0711b43c4c58) reference.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-123">When the **Workflow - Create Or Update** page opens, go to the [Workflow - Get](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b44b3f9b0711b43c4c58) reference.</span></span>

### <a name="select-your-region"></a><span data-ttu-id="9ad1d-124">Select your region</span><span class="sxs-lookup"><span data-stu-id="9ad1d-124">Select your region</span></span>

<span data-ttu-id="9ad1d-125">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-125">For **Open API testing console**, select the region that most closely describes your location.</span></span>

  ![Workflow - Get region selection](images/test-drive-region.png)

  <span data-ttu-id="9ad1d-127">The **Workflow - Get** API console opens.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-127">The **Workflow - Get** API console opens.</span></span>

### <a name="enter-parameters"></a><span data-ttu-id="9ad1d-128">Enter parameters</span><span class="sxs-lookup"><span data-stu-id="9ad1d-128">Enter parameters</span></span>

<span data-ttu-id="9ad1d-129">Enter values for **team**, **workflowname**, and **Ocp-Apim-Subscription-Key** (your subscription key):</span><span class="sxs-lookup"><span data-stu-id="9ad1d-129">Enter values for **team**, **workflowname**, and **Ocp-Apim-Subscription-Key** (your subscription key):</span></span>

- <span data-ttu-id="9ad1d-130">**team**: The team ID that you created when you set up your [Review tool account](https://contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-130">**team**: The team ID that you created when you set up your [Review tool account](https://contentmoderator.cognitive.microsoft.com/).</span></span> 
- <span data-ttu-id="9ad1d-131">**workflowname**: The name of your workflow.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-131">**workflowname**: The name of your workflow.</span></span> <span data-ttu-id="9ad1d-132">Use `default`.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-132">Use `default`.</span></span>
- <span data-ttu-id="9ad1d-133">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-133">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span></span>

  ![Get query parameters and headers](images/workflow-get-default.PNG)

### <a name="submit-your-request"></a><span data-ttu-id="9ad1d-135">Submit your request</span><span class="sxs-lookup"><span data-stu-id="9ad1d-135">Submit your request</span></span>
  
<span data-ttu-id="9ad1d-136">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-136">Select **Send**.</span></span> <span data-ttu-id="9ad1d-137">If the operation succeeds, the **Response status** is `200 OK`, and the **Response content** box displays the following JSON workflow:</span><span class="sxs-lookup"><span data-stu-id="9ad1d-137">If the operation succeeds, the **Response status** is `200 OK`, and the **Response content** box displays the following JSON workflow:</span></span>

    {
        "Name": "default",
        "Description": "Default",
        "Type": "Image",
        "Expression": {
        "If": {
            "ConnectorName": "moderator",
            "OutputName": "isadult",
            "Operator": "eq",
            "Value": "true",
            "AlternateInput": null,
            "Type": "Condition"
            },
        "Then": {
            "Perform": [{
                "Name": "createreview",
                "Subteam": null,
                "CallbackEndpoint": null,
                "Tags": []
            }],
            "Type": "Actions"
            },
            "Else": null,
            "Type": "Logic"
            }
    }


## <a name="create-a-workflow"></a><span data-ttu-id="9ad1d-138">Create a workflow</span><span class="sxs-lookup"><span data-stu-id="9ad1d-138">Create a workflow</span></span>

<span data-ttu-id="9ad1d-139">In the Review tool, go to the [Credentials](Review-Tool-User-Guide/credentials.md#the-review-tool) section.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-139">In the Review tool, go to the [Credentials](Review-Tool-User-Guide/credentials.md#the-review-tool) section.</span></span>

### <a name="browse-to-the-api-reference"></a><span data-ttu-id="9ad1d-140">Browse to the API reference</span><span class="sxs-lookup"><span data-stu-id="9ad1d-140">Browse to the API reference</span></span>

<span data-ttu-id="9ad1d-141">In the **Credentials** view, select [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-141">In the **Credentials** view, select [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/5813b46b3f9b0711b43c4c59).</span></span> <span data-ttu-id="9ad1d-142">The **Workflow - Create Or Update** page opens.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-142">The **Workflow - Create Or Update** page opens.</span></span>

### <a name="select-your-region"></a><span data-ttu-id="9ad1d-143">Select your region</span><span class="sxs-lookup"><span data-stu-id="9ad1d-143">Select your region</span></span>

<span data-ttu-id="9ad1d-144">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-144">For **Open API testing console**, select the region that most closely describes your location.</span></span>

  ![Workflow - Create Or Update page region selection](images/test-drive-region.png)

  <span data-ttu-id="9ad1d-146">The **Workflow - Create Or Update** API console opens.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-146">The **Workflow - Create Or Update** API console opens.</span></span>

### <a name="enter-parameters"></a><span data-ttu-id="9ad1d-147">Enter parameters</span><span class="sxs-lookup"><span data-stu-id="9ad1d-147">Enter parameters</span></span>

<span data-ttu-id="9ad1d-148">Enter values for **team**, **workflowname**, and **Ocp-Apim-Subscription-Key** (your subscription key):</span><span class="sxs-lookup"><span data-stu-id="9ad1d-148">Enter values for **team**, **workflowname**, and **Ocp-Apim-Subscription-Key** (your subscription key):</span></span>

- <span data-ttu-id="9ad1d-149">**team**: The team ID that you created when you set up your [Review tool account](https://contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-149">**team**: The team ID that you created when you set up your [Review tool account](https://contentmoderator.cognitive.microsoft.com/).</span></span> 
- <span data-ttu-id="9ad1d-150">**workflowname**: The name of your new workflow.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-150">**workflowname**: The name of your new workflow.</span></span>
- <span data-ttu-id="9ad1d-151">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-151">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span></span>

  ![Workflow - Create Or Update console query parameters and headers](images/workflow-console-parameters.PNG)

### <a name="enter-the-workflow-definition"></a><span data-ttu-id="9ad1d-153">Enter the workflow definition</span><span class="sxs-lookup"><span data-stu-id="9ad1d-153">Enter the workflow definition</span></span>

1. <span data-ttu-id="9ad1d-154">Edit the **Request body** box to enter the JSON request with details for **Description** and **Type** (Image or Text).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-154">Edit the **Request body** box to enter the JSON request with details for **Description** and **Type** (Image or Text).</span></span> 
2. <span data-ttu-id="9ad1d-155">For **Expression**, copy the default workflow expression from the preceding section, as shown here:</span><span class="sxs-lookup"><span data-stu-id="9ad1d-155">For **Expression**, copy the default workflow expression from the preceding section, as shown here:</span></span>

        {
            "Description": "Default workflow from API console",
            "Type": "Image",
            "Expression": 
                // Copy the default workflow expression from the preceding section
        }

    <span data-ttu-id="9ad1d-156">Your request body looks like the following JSON request:</span><span class="sxs-lookup"><span data-stu-id="9ad1d-156">Your request body looks like the following JSON request:</span></span>

        {
            "Description": "Default workflow from API console",
            "Type": "Image",
            "Expression": {
                "Type": "Logic",
                "If": {
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
                    "Tags": [ ]
                }
                ],
                "Type": "Actions"
                }
            }
        }
 
### <a name="submit-your-request"></a><span data-ttu-id="9ad1d-157">Submit your request</span><span class="sxs-lookup"><span data-stu-id="9ad1d-157">Submit your request</span></span>
  
<span data-ttu-id="9ad1d-158">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-158">Select **Send**.</span></span> <span data-ttu-id="9ad1d-159">If the operation succeeds, the **Response status** is `200 OK`, and the **Response content** box displays `true`.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-159">If the operation succeeds, the **Response status** is `200 OK`, and the **Response content** box displays `true`.</span></span>

### <a name="check-out-the-new-workflow"></a><span data-ttu-id="9ad1d-160">Check out the new workflow</span><span class="sxs-lookup"><span data-stu-id="9ad1d-160">Check out the new workflow</span></span>

<span data-ttu-id="9ad1d-161">In the Review tool, select **Review** > **Settings** > **Workflows**.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-161">In the Review tool, select **Review** > **Settings** > **Workflows**.</span></span> <span data-ttu-id="9ad1d-162">Your new workflow appears and is ready to use.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-162">Your new workflow appears and is ready to use.</span></span>

  ![Review tool list of workflows](images/workflow-console-new-workflow.PNG)
  
### <a name="review-your-new-workflow-details"></a><span data-ttu-id="9ad1d-164">Review your new workflow details</span><span class="sxs-lookup"><span data-stu-id="9ad1d-164">Review your new workflow details</span></span>

1. <span data-ttu-id="9ad1d-165">Select the **Edit** option for your workflow, and then select the **Designer** and **JSON** tabs.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-165">Select the **Edit** option for your workflow, and then select the **Designer** and **JSON** tabs.</span></span>

   ![Designer tab for a selected workflow](images/workflow-console-new-workflow-designer.PNG)

2. <span data-ttu-id="9ad1d-167">To see the JSON view of the workflow, select the **JSON** tab.</span><span class="sxs-lookup"><span data-stu-id="9ad1d-167">To see the JSON view of the workflow, select the **JSON** tab.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ad1d-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ad1d-168">Next steps</span></span>

* <span data-ttu-id="9ad1d-169">For more complex workflow examples, see the [Workflows overview](workflow-api.md).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-169">For more complex workflow examples, see the [Workflows overview](workflow-api.md).</span></span>
* <span data-ttu-id="9ad1d-170">Learn how to use workflows with [content moderation jobs](try-review-api-job.md).</span><span class="sxs-lookup"><span data-stu-id="9ad1d-170">Learn how to use workflows with [content moderation jobs](try-review-api-job.md).</span></span>
