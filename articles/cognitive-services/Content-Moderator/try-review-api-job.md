---
title: Run content moderation jobs in Azure Content Moderator | Microsoft Docs
description: Learn how to run content moderation jobs in the API console.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 08/03/2017
ms.author: sajagtap
ms.openlocfilehash: 6f741be1001ae70d5fdbf6f374204aaad1601abe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965657"
---
# <a name="start-a-moderation-job-from-the-api-console"></a><span data-ttu-id="a3648-103">Start a moderation job from the API console</span><span class="sxs-lookup"><span data-stu-id="a3648-103">Start a moderation job from the API console</span></span>

<span data-ttu-id="a3648-104">Use the Review API's [job operations](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5) to initiate end-to-end content moderation jobs for image or text content in Azure Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="a3648-104">Use the Review API's [job operations](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5) to initiate end-to-end content moderation jobs for image or text content in Azure Content Moderator.</span></span> 

<span data-ttu-id="a3648-105">The moderation job scans your content by using the Content Moderator Image Moderation API or Text Moderation API.</span><span class="sxs-lookup"><span data-stu-id="a3648-105">The moderation job scans your content by using the Content Moderator Image Moderation API or Text Moderation API.</span></span> <span data-ttu-id="a3648-106">Then, the moderation job uses workflows (defined in the review tool) to generate reviews in the Review tool.</span><span class="sxs-lookup"><span data-stu-id="a3648-106">Then, the moderation job uses workflows (defined in the review tool) to generate reviews in the Review tool.</span></span> 

<span data-ttu-id="a3648-107">After a human moderator reviews the auto-assigned tags and prediction data and submits a final moderation decision, the Review API submits all information to your API endpoint.</span><span class="sxs-lookup"><span data-stu-id="a3648-107">After a human moderator reviews the auto-assigned tags and prediction data and submits a final moderation decision, the Review API submits all information to your API endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3648-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3648-108">Prerequisites</span></span>

<span data-ttu-id="a3648-109">Navigate to the [review tool](https://contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a3648-109">Navigate to the [review tool](https://contentmoderator.cognitive.microsoft.com/).</span></span> <span data-ttu-id="a3648-110">Sign up if you have not done so yet.</span><span class="sxs-lookup"><span data-stu-id="a3648-110">Sign up if you have not done so yet.</span></span> <span data-ttu-id="a3648-111">Within the review tool, [define a custom workflow](Review-Tool-User-Guide/Workflows.md) to use in this `Job` operation.</span><span class="sxs-lookup"><span data-stu-id="a3648-111">Within the review tool, [define a custom workflow](Review-Tool-User-Guide/Workflows.md) to use in this `Job` operation.</span></span>

## <a name="use-the-api-console"></a><span data-ttu-id="a3648-112">Use the API console</span><span class="sxs-lookup"><span data-stu-id="a3648-112">Use the API console</span></span>
<span data-ttu-id="a3648-113">To test-drive the API by using the online console, you need a few values to enter into the console:</span><span class="sxs-lookup"><span data-stu-id="a3648-113">To test-drive the API by using the online console, you need a few values to enter into the console:</span></span>
    
- <span data-ttu-id="a3648-114">`teamName`: Use the `Id` field from your review tool's credentials screen.</span><span class="sxs-lookup"><span data-stu-id="a3648-114">`teamName`: Use the `Id` field from your review tool's credentials screen.</span></span> 
- <span data-ttu-id="a3648-115">`ContentId`: This string is passed to the API and returned through the callback.</span><span class="sxs-lookup"><span data-stu-id="a3648-115">`ContentId`: This string is passed to the API and returned through the callback.</span></span> <span data-ttu-id="a3648-116">**ContentId** is useful for associating internal identifiers or metadata with the results of a moderation job.- `Workflowname`: The name of the [workflow that you created](Review-Tool-User-Guide/Workflows.md) in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a3648-116">**ContentId** is useful for associating internal identifiers or metadata with the results of a moderation job.- `Workflowname`: The name of the [workflow that you created](Review-Tool-User-Guide/Workflows.md) in the previous section.</span></span>
- <span data-ttu-id="a3648-117">`Ocp-Apim-Subscription-Key`: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3648-117">`Ocp-Apim-Subscription-Key`: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span></span>

<span data-ttu-id="a3648-118">Access the API console is from the **Credentials** window.</span><span class="sxs-lookup"><span data-stu-id="a3648-118">Access the API console is from the **Credentials** window.</span></span>

### <a name="navigate-to-the-api-reference"></a><span data-ttu-id="a3648-119">Navigate to the API Reference</span><span class="sxs-lookup"><span data-stu-id="a3648-119">Navigate to the API Reference</span></span>
<span data-ttu-id="a3648-120">In the **Credentials** window, select [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5).</span><span class="sxs-lookup"><span data-stu-id="a3648-120">In the **Credentials** window, select [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5).</span></span>

  <span data-ttu-id="a3648-121">The `Job.Create` page opens.</span><span class="sxs-lookup"><span data-stu-id="a3648-121">The `Job.Create` page opens.</span></span>

### <a name="select-your-region"></a><span data-ttu-id="a3648-122">Select your region</span><span class="sxs-lookup"><span data-stu-id="a3648-122">Select your region</span></span>
<span data-ttu-id="a3648-123">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="a3648-123">For **Open API testing console**, select the region that most closely describes your location.</span></span>
  <span data-ttu-id="a3648-124">![Job - Create page region selection](images/test-drive-job-1.png)</span><span class="sxs-lookup"><span data-stu-id="a3648-124">![Job - Create page region selection](images/test-drive-job-1.png)</span></span>

  <span data-ttu-id="a3648-125">The `Job.Create` API console opens.</span><span class="sxs-lookup"><span data-stu-id="a3648-125">The `Job.Create` API console opens.</span></span> 

### <a name="enter-parameters"></a><span data-ttu-id="a3648-126">Enter parameters</span><span class="sxs-lookup"><span data-stu-id="a3648-126">Enter parameters</span></span>

<span data-ttu-id="a3648-127">Enter values for the required query parameters, and your subscription key.</span><span class="sxs-lookup"><span data-stu-id="a3648-127">Enter values for the required query parameters, and your subscription key.</span></span> <span data-ttu-id="a3648-128">In the **Request body** box, specify the location of the information that you want to scan.</span><span class="sxs-lookup"><span data-stu-id="a3648-128">In the **Request body** box, specify the location of the information that you want to scan.</span></span> <span data-ttu-id="a3648-129">For this example, let's use this [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample6.png).</span><span class="sxs-lookup"><span data-stu-id="a3648-129">For this example, let's use this [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample6.png).</span></span>

  ![Job - Create console query parameters, headers, and Request body box](images/job-api-console-inputs.PNG)

### <a name="submit-your-request"></a><span data-ttu-id="a3648-131">Submit your request</span><span class="sxs-lookup"><span data-stu-id="a3648-131">Submit your request</span></span>
<span data-ttu-id="a3648-132">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="a3648-132">Select **Send**.</span></span> <span data-ttu-id="a3648-133">A job ID is created.</span><span class="sxs-lookup"><span data-stu-id="a3648-133">A job ID is created.</span></span> <span data-ttu-id="a3648-134">Copy this to use in the next steps.</span><span class="sxs-lookup"><span data-stu-id="a3648-134">Copy this to use in the next steps.</span></span>

  `"JobId": "2018014caceddebfe9446fab29056fd8d31ffe"`

### <a name="open-the-get-job-details-page"></a><span data-ttu-id="a3648-135">Open the Get Job details page</span><span class="sxs-lookup"><span data-stu-id="a3648-135">Open the Get Job details page</span></span>
<span data-ttu-id="a3648-136">Select **Get**, and then open the API by selecting the button that matches your region.</span><span class="sxs-lookup"><span data-stu-id="a3648-136">Select **Get**, and then open the API by selecting the button that matches your region.</span></span>

  ![Job - Create console Get results](images/test-drive-job-4.png)

### <a name="review-the-response"></a><span data-ttu-id="a3648-138">Review the response</span><span class="sxs-lookup"><span data-stu-id="a3648-138">Review the response</span></span>

<span data-ttu-id="a3648-139">Enter values for **teamName** and **JobID**.</span><span class="sxs-lookup"><span data-stu-id="a3648-139">Enter values for **teamName** and **JobID**.</span></span> <span data-ttu-id="a3648-140">Enter your subscription key, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="a3648-140">Enter your subscription key, and then select **Send**.</span></span> <span data-ttu-id="a3648-141">The following response shows sample Job status and details.</span><span class="sxs-lookup"><span data-stu-id="a3648-141">The following response shows sample Job status and details.</span></span>

```
    {
        "Id": "2018014caceddebfe9446fab29056fd8d31ffe",
        "TeamName": "some team name",
        "Status": "InProgress",
        "WorkflowId": "OCR",
        "Type": "Image",
        "CallBackEndpoint": "",
        "ReviewId": "",
        "ResultMetaData": [],
        "JobExecutionReport": 
        [
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
```

## <a name="navigate-to-the-review-tool"></a><span data-ttu-id="a3648-142">Navigate to the review tool</span><span class="sxs-lookup"><span data-stu-id="a3648-142">Navigate to the review tool</span></span>
<span data-ttu-id="a3648-143">On the Content Moderator Dashboard, select **Review** > **Image**.</span><span class="sxs-lookup"><span data-stu-id="a3648-143">On the Content Moderator Dashboard, select **Review** > **Image**.</span></span> <span data-ttu-id="a3648-144">The image that you scanned appears, ready for human review.</span><span class="sxs-lookup"><span data-stu-id="a3648-144">The image that you scanned appears, ready for human review.</span></span>

  ![Review tool image of three cyclists](images/ocr-sample-image.PNG)

## <a name="next-steps"></a><span data-ttu-id="a3648-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3648-146">Next steps</span></span>

<span data-ttu-id="a3648-147">Use the REST API in your code or start with the [Jobs .NET quickstart](moderation-jobs-quickstart-dotnet.md) to integrate with your application.</span><span class="sxs-lookup"><span data-stu-id="a3648-147">Use the REST API in your code or start with the [Jobs .NET quickstart](moderation-jobs-quickstart-dotnet.md) to integrate with your application.</span></span>
