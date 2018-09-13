---
title: Create a custom speech endpoint with Custom Speech Service on Azure | Microsoft Docs
description: Learn how to create a custom speech-to-text endpoint with the Custom Speech Service in Cognitive Services.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 07/08/2017
ms.author: panosper
ms.openlocfilehash: 99bc275db1f0c1b45b3db440d2e03d0db9ab5cf6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868238"
---
# <a name="create-a-custom-speech-to-text-endpoint"></a><span data-ttu-id="9f816-103">Create a custom speech-to-text endpoint</span><span class="sxs-lookup"><span data-stu-id="9f816-103">Create a custom speech-to-text endpoint</span></span>
<span data-ttu-id="9f816-104">After you have created custom acoustic models or language models, you can deploy them in a custom speech-to-text endpoint.</span><span class="sxs-lookup"><span data-stu-id="9f816-104">After you have created custom acoustic models or language models, you can deploy them in a custom speech-to-text endpoint.</span></span> 

## <a name="create-an-endpoint"></a><span data-ttu-id="9f816-105">Create an endpoint</span><span class="sxs-lookup"><span data-stu-id="9f816-105">Create an endpoint</span></span>
<span data-ttu-id="9f816-106">To create a new custom endpoint, select **Deployments** on the **Custom Speech** menu at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="9f816-106">To create a new custom endpoint, select **Deployments** on the **Custom Speech** menu at the top of the page.</span></span> <span data-ttu-id="9f816-107">This action takes you to the **Deployments** page, which contains a table of current custom endpoints.</span><span class="sxs-lookup"><span data-stu-id="9f816-107">This action takes you to the **Deployments** page, which contains a table of current custom endpoints.</span></span> <span data-ttu-id="9f816-108">If you have not yet created any endpoints, the table is empty.</span><span class="sxs-lookup"><span data-stu-id="9f816-108">If you have not yet created any endpoints, the table is empty.</span></span> <span data-ttu-id="9f816-109">The current locale is reflected in the table title.</span><span class="sxs-lookup"><span data-stu-id="9f816-109">The current locale is reflected in the table title.</span></span> 

<span data-ttu-id="9f816-110">To create a deployment for a different language, select **Change Locale**.</span><span class="sxs-lookup"><span data-stu-id="9f816-110">To create a deployment for a different language, select **Change Locale**.</span></span> <span data-ttu-id="9f816-111">For more information about supported languages, see [Supported locales in Custom Speech Service](cognitive-services-custom-speech-change-locale.md).</span><span class="sxs-lookup"><span data-stu-id="9f816-111">For more information about supported languages, see [Supported locales in Custom Speech Service](cognitive-services-custom-speech-change-locale.md).</span></span>

<span data-ttu-id="9f816-112">To create a new endpoint, select **Create New**.</span><span class="sxs-lookup"><span data-stu-id="9f816-112">To create a new endpoint, select **Create New**.</span></span> <span data-ttu-id="9f816-113">In the **Create Deployment** pane, enter information in the **Name** and **Description** boxes of your custom deployment.</span><span class="sxs-lookup"><span data-stu-id="9f816-113">In the **Create Deployment** pane, enter information in the **Name** and **Description** boxes of your custom deployment.</span></span>

<span data-ttu-id="9f816-114">In the **Subscription** combo box, select the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="9f816-114">In the **Subscription** combo box, select the subscription that you want to use.</span></span> <span data-ttu-id="9f816-115">If it is an S2 subscription, you can select scale units and content logging.</span><span class="sxs-lookup"><span data-stu-id="9f816-115">If it is an S2 subscription, you can select scale units and content logging.</span></span> <span data-ttu-id="9f816-116">For more information about scale units and logging, see [Custom Speech Service meters and quotas](../cognitive-services-custom-speech-meters.md).</span><span class="sxs-lookup"><span data-stu-id="9f816-116">For more information about scale units and logging, see [Custom Speech Service meters and quotas](../cognitive-services-custom-speech-meters.md).</span></span>

<span data-ttu-id="9f816-117">The following table shows how scale units map to available concurrent requests:</span><span class="sxs-lookup"><span data-stu-id="9f816-117">The following table shows how scale units map to available concurrent requests:</span></span>

| <span data-ttu-id="9f816-118">Scale unit</span><span class="sxs-lookup"><span data-stu-id="9f816-118">Scale unit</span></span> | <span data-ttu-id="9f816-119">Number of concurrent requests</span><span class="sxs-lookup"><span data-stu-id="9f816-119">Number of concurrent requests</span></span> |
| ------ | ----- |
| <span data-ttu-id="9f816-120">0</span><span class="sxs-lookup"><span data-stu-id="9f816-120">0</span></span> | <span data-ttu-id="9f816-121">1</span><span class="sxs-lookup"><span data-stu-id="9f816-121">1</span></span> |
| <span data-ttu-id="9f816-122">1</span><span class="sxs-lookup"><span data-stu-id="9f816-122">1</span></span> | <span data-ttu-id="9f816-123">5</span><span class="sxs-lookup"><span data-stu-id="9f816-123">5</span></span> |
| <span data-ttu-id="9f816-124">2</span><span class="sxs-lookup"><span data-stu-id="9f816-124">2</span></span> | <span data-ttu-id="9f816-125">10</span><span class="sxs-lookup"><span data-stu-id="9f816-125">10</span></span> |
| <span data-ttu-id="9f816-126">3</span><span class="sxs-lookup"><span data-stu-id="9f816-126">3</span></span> | <span data-ttu-id="9f816-127">15</span><span class="sxs-lookup"><span data-stu-id="9f816-127">15</span></span> |
| <span data-ttu-id="9f816-128">n</span><span class="sxs-lookup"><span data-stu-id="9f816-128">n</span></span> | <span data-ttu-id="9f816-129">5 \* n</span><span class="sxs-lookup"><span data-stu-id="9f816-129">5 \* n</span></span> |

<span data-ttu-id="9f816-130">You can also select whether content logging is switched on or off.</span><span class="sxs-lookup"><span data-stu-id="9f816-130">You can also select whether content logging is switched on or off.</span></span> <span data-ttu-id="9f816-131">That is, you're selecting whether the endpoint traffic is stored for Microsoft internal use.</span><span class="sxs-lookup"><span data-stu-id="9f816-131">That is, you're selecting whether the endpoint traffic is stored for Microsoft internal use.</span></span> <span data-ttu-id="9f816-132">If it is not selected, storing the traffic will be suppressed.</span><span class="sxs-lookup"><span data-stu-id="9f816-132">If it is not selected, storing the traffic will be suppressed.</span></span> <span data-ttu-id="9f816-133">Suppressing content logging results in additional cost.</span><span class="sxs-lookup"><span data-stu-id="9f816-133">Suppressing content logging results in additional cost.</span></span> <span data-ttu-id="9f816-134">Consult the [pricing information page](https://azure.microsoft.com/pricing/details/cognitive-services/custom-speech-service/) for details.</span><span class="sxs-lookup"><span data-stu-id="9f816-134">Consult the [pricing information page](https://azure.microsoft.com/pricing/details/cognitive-services/custom-speech-service/) for details.</span></span>

> [!NOTE]
> <span data-ttu-id="9f816-135">Content Logging is called "No Trace" on pricing page.</span><span class="sxs-lookup"><span data-stu-id="9f816-135">Content Logging is called "No Trace" on pricing page.</span></span>
>


<span data-ttu-id="9f816-136">In addition, Microsoft provides a rough estimate of costs so that you are aware of the impact on the costs of scale units and content logging.</span><span class="sxs-lookup"><span data-stu-id="9f816-136">In addition, Microsoft provides a rough estimate of costs so that you are aware of the impact on the costs of scale units and content logging.</span></span> <span data-ttu-id="9f816-137">This estimate is a rough estimate and might differ from your actual costs.</span><span class="sxs-lookup"><span data-stu-id="9f816-137">This estimate is a rough estimate and might differ from your actual costs.</span></span>

> [!NOTE]
> <span data-ttu-id="9f816-138">These settings are not available with F0 (free tier) subscriptions.</span><span class="sxs-lookup"><span data-stu-id="9f816-138">These settings are not available with F0 (free tier) subscriptions.</span></span>
>

<span data-ttu-id="9f816-139">In the **Acoustic Model** list, select the acoustic model that you want, and in the **Language Model** list, select the language model that you want.</span><span class="sxs-lookup"><span data-stu-id="9f816-139">In the **Acoustic Model** list, select the acoustic model that you want, and in the **Language Model** list, select the language model that you want.</span></span> <span data-ttu-id="9f816-140">The choices for acoustic and language models always include the base Microsoft models.</span><span class="sxs-lookup"><span data-stu-id="9f816-140">The choices for acoustic and language models always include the base Microsoft models.</span></span> <span data-ttu-id="9f816-141">The selection of the base model limits the combinations.</span><span class="sxs-lookup"><span data-stu-id="9f816-141">The selection of the base model limits the combinations.</span></span> <span data-ttu-id="9f816-142">You cannot mix conversational base models with search and dictate base models.</span><span class="sxs-lookup"><span data-stu-id="9f816-142">You cannot mix conversational base models with search and dictate base models.</span></span>

![The Create Deployment page](../../../media/cognitive-services/custom-speech-service/custom-speech-deployment-create2.png)

> [!NOTE]
> <span data-ttu-id="9f816-144">Be sure to accept the terms of use and pricing information by selecting the check box.</span><span class="sxs-lookup"><span data-stu-id="9f816-144">Be sure to accept the terms of use and pricing information by selecting the check box.</span></span>
>

<span data-ttu-id="9f816-145">After you have selected your acoustic and language models, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9f816-145">After you have selected your acoustic and language models, select **Create**.</span></span> <span data-ttu-id="9f816-146">This action returns you to the **Deployments** page.</span><span class="sxs-lookup"><span data-stu-id="9f816-146">This action returns you to the **Deployments** page.</span></span> <span data-ttu-id="9f816-147">The table now includes an entry that corresponds to your new endpoint.</span><span class="sxs-lookup"><span data-stu-id="9f816-147">The table now includes an entry that corresponds to your new endpoint.</span></span> <span data-ttu-id="9f816-148">The endpoint’s status reflects its current state while it is being created.</span><span class="sxs-lookup"><span data-stu-id="9f816-148">The endpoint’s status reflects its current state while it is being created.</span></span> <span data-ttu-id="9f816-149">It can take up to 30 minutes to instantiate a new endpoint with your custom models.</span><span class="sxs-lookup"><span data-stu-id="9f816-149">It can take up to 30 minutes to instantiate a new endpoint with your custom models.</span></span> <span data-ttu-id="9f816-150">When the status of the deployment is *Complete*, the endpoint is ready for use.</span><span class="sxs-lookup"><span data-stu-id="9f816-150">When the status of the deployment is *Complete*, the endpoint is ready for use.</span></span>

![The Deployments page](../../../media/cognitive-services/custom-speech-service/custom-speech-deployment-ready.png)

<span data-ttu-id="9f816-152">When the deployment is ready, the deployment name becomes a link.</span><span class="sxs-lookup"><span data-stu-id="9f816-152">When the deployment is ready, the deployment name becomes a link.</span></span> <span data-ttu-id="9f816-153">Selecting the link displays the **Deployment Information** page, which displays the URLs of your custom endpoint to use with either an HTTP request or the Microsoft Cognitive Services Speech Client Library, which uses web sockets.</span><span class="sxs-lookup"><span data-stu-id="9f816-153">Selecting the link displays the **Deployment Information** page, which displays the URLs of your custom endpoint to use with either an HTTP request or the Microsoft Cognitive Services Speech Client Library, which uses web sockets.</span></span>

![The Deployment Information page](../../../media/cognitive-services/custom-speech-service/custom-speech-deployment-info2.png)

## <a name="next-steps"></a><span data-ttu-id="9f816-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f816-155">Next steps</span></span>

<span data-ttu-id="9f816-156">For more tutorials, see:</span><span class="sxs-lookup"><span data-stu-id="9f816-156">For more tutorials, see:</span></span>
* [<span data-ttu-id="9f816-157">Use a custom speech-to-text endpoint</span><span class="sxs-lookup"><span data-stu-id="9f816-157">Use a custom speech-to-text endpoint</span></span>](cognitive-services-custom-speech-use-endpoint.md)
* [<span data-ttu-id="9f816-158">Create a custom acoustic model</span><span class="sxs-lookup"><span data-stu-id="9f816-158">Create a custom acoustic model</span></span>](cognitive-services-custom-speech-create-acoustic-model.md)
* [<span data-ttu-id="9f816-159">Create a custom language model</span><span class="sxs-lookup"><span data-stu-id="9f816-159">Create a custom language model</span></span>](cognitive-services-custom-speech-create-language-model.md)
