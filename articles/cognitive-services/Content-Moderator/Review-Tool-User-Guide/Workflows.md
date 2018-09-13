---
title: Define and use workflows in Content Moderator | Microsoft Docs
description: Content Moderator includes default workflows, and you can create your own based on content policies that are specific to your business.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 02/03/2017
ms.author: sajagtap
ms.openlocfilehash: 7609622a3b4ad1b03f3757916aae649618ba5472
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556775"
---
# <a name="defining-and-using-workflows"></a><span data-ttu-id="4ca9c-103">Defining and using workflows</span><span class="sxs-lookup"><span data-stu-id="4ca9c-103">Defining and using workflows</span></span>  #

<span data-ttu-id="4ca9c-104">In addition to default workflow used for generating reviews, you can define custom workflows and thresholds based on content policies that are specific to your business.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-104">In addition to default workflow used for generating reviews, you can define custom workflows and thresholds based on content policies that are specific to your business.</span></span> <span data-ttu-id="4ca9c-105">Content Moderator allows you to use other APIs in addition to its own API as long as a connector for that API is available.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-105">Content Moderator allows you to use other APIs in addition to its own API as long as a connector for that API is available.</span></span>

## <a name="make-sure-you-have-valid-credentials"></a><span data-ttu-id="4ca9c-106">Make sure you have valid credentials</span><span class="sxs-lookup"><span data-stu-id="4ca9c-106">Make sure you have valid credentials</span></span> ##

<span data-ttu-id="4ca9c-107">To get started on defining a workflow, make sure you have valid credentials for the API you intend to use in your workflow.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-107">To get started on defining a workflow, make sure you have valid credentials for the API you intend to use in your workflow.</span></span> <span data-ttu-id="4ca9c-108">Content Moderator includes a small set of Connectors by default.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-108">Content Moderator includes a small set of Connectors by default.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows.PNG)

## <a name="navigate-to-the-workflows-section"></a><span data-ttu-id="4ca9c-110">Navigate to the Workflows section</span><span class="sxs-lookup"><span data-stu-id="4ca9c-110">Navigate to the Workflows section</span></span> ##

<span data-ttu-id="4ca9c-111">Select the **Workflows** option under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-111">Select the **Workflows** option under **Settings**.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-0.PNG)

## <a name="start-a-new-workflow"></a><span data-ttu-id="4ca9c-113">Start a new workflow</span><span class="sxs-lookup"><span data-stu-id="4ca9c-113">Start a new workflow</span></span> ##

<span data-ttu-id="4ca9c-114">Use the **Add Workflows** option to get started.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-114">Use the **Add Workflows** option to get started.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-1.PNG)

## <a name="name-your-workflow"></a><span data-ttu-id="4ca9c-116">Name your workflow</span><span class="sxs-lookup"><span data-stu-id="4ca9c-116">Name your workflow</span></span> ##

<span data-ttu-id="4ca9c-117">Name your workflow, provide a description, and select whether you want to process images or text.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-117">Name your workflow, provide a description, and select whether you want to process images or text.</span></span>
<span data-ttu-id="4ca9c-118">In the screenshot below, you can see the fields and view the If-Then-Else selections that you need to make to define your custom workflows.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-118">In the screenshot below, you can see the fields and view the If-Then-Else selections that you need to make to define your custom workflows.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-2.PNG)

## <a name="define-the-evaluation-criteria-condition"></a><span data-ttu-id="4ca9c-120">Define the evaluation criteria (condition)</span><span class="sxs-lookup"><span data-stu-id="4ca9c-120">Define the evaluation criteria (condition)</span></span> ##

<span data-ttu-id="4ca9c-121">As a first step, enter all the information needed to define your criteria for executing the workflow.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-121">As a first step, enter all the information needed to define your criteria for executing the workflow.</span></span> <span data-ttu-id="4ca9c-122">As shown in the screen below, this includes selecting the API you want to get results from.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-122">As shown in the screen below, this includes selecting the API you want to get results from.</span></span> <span data-ttu-id="4ca9c-123">When you select one of the available APIs (that you have entered your credentials for in the very first step), the next drop-down will show the available outputs from the API.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-123">When you select one of the available APIs (that you have entered your credentials for in the very first step), the next drop-down will show the available outputs from the API.</span></span> <span data-ttu-id="4ca9c-124">The next two fields allow you to specify the check to be performed.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-124">The next two fields allow you to specify the check to be performed.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-3.PNG)

## <a name="define-the-action"></a><span data-ttu-id="4ca9c-126">Define the action</span><span class="sxs-lookup"><span data-stu-id="4ca9c-126">Define the action</span></span> ##

<span data-ttu-id="4ca9c-127">Once you have defined the condition, you will tell Content Moderator what action to perform if the condition is met.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-127">Once you have defined the condition, you will tell Content Moderator what action to perform if the condition is met.</span></span> <span data-ttu-id="4ca9c-128">The example shown below creates an image review and assigns it to a subteam.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-128">The example shown below creates an image review and assigns it to a subteam.</span></span> <span data-ttu-id="4ca9c-129">It also specifies an aditional criteria that must be fulfilled for the assigned 'a' tag to be selected.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-129">It also specifies an aditional criteria that must be fulfilled for the assigned 'a' tag to be selected.</span></span> <span data-ttu-id="4ca9c-130">In this way, you can combine multiple conditions to get the results you want.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-130">In this way, you can combine multiple conditions to get the results you want.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-5.PNG)

## <a name="optionally-define-the-else-section"></a><span data-ttu-id="4ca9c-132">Optionally, define the Else section</span><span class="sxs-lookup"><span data-stu-id="4ca9c-132">Optionally, define the Else section</span></span> ##

<span data-ttu-id="4ca9c-133">Optionally, expand the **Else** section to provide similar information like you did for the **If** section.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-133">Optionally, expand the **Else** section to provide similar information like you did for the **If** section.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-6.PNG)

## <a name="save-the-workflow"></a><span data-ttu-id="4ca9c-135">Save the workflow</span><span class="sxs-lookup"><span data-stu-id="4ca9c-135">Save the workflow</span></span> ##

<span data-ttu-id="4ca9c-136">Finally, save your workflow and note the workflow name.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-136">Finally, save your workflow and note the workflow name.</span></span> <span data-ttu-id="4ca9c-137">You will need it to invoke the workflow with the Review API.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-137">You will need it to invoke the workflow with the Review API.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-7.PNG)

## <a name="use-the-review-api"></a><span data-ttu-id="4ca9c-139">Use the Review API</span><span class="sxs-lookup"><span data-stu-id="4ca9c-139">Use the Review API</span></span> ##

<span data-ttu-id="4ca9c-140">Now that you have a custom workflow defined, use the [**Review API**](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5) to start a moderation job with the workflow name as one of the parameters.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-140">Now that you have a custom workflow defined, use the [**Review API**](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5) to start a moderation job with the workflow name as one of the parameters.</span></span> <span data-ttu-id="4ca9c-141">This should be the workflow name that you noted in the previous step.</span><span class="sxs-lookup"><span data-stu-id="4ca9c-141">This should be the workflow name that you noted in the previous step.</span></span>








