---
title: Get subscription keys for the Custom Speech Service on Azure | Microsoft Docs
description: Learn how to get subscription keys for calls to the Custom Speech Service in Cognitive Services.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 02/08/2017
ms.author: panosper
ms.openlocfilehash: d3969114323f5675c5e14ab36990b124e84ead37
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870831"
---
# <a name="obtain-subscription-keys"></a><span data-ttu-id="94986-103">Obtain subscription keys</span><span class="sxs-lookup"><span data-stu-id="94986-103">Obtain subscription keys</span></span>
<span data-ttu-id="94986-104">To get started using the Azure Custom Speech Service, you first need to link your user account to an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="94986-104">To get started using the Azure Custom Speech Service, you first need to link your user account to an Azure subscription.</span></span> <span data-ttu-id="94986-105">Subscriptions to free and paid tiers are available.</span><span class="sxs-lookup"><span data-stu-id="94986-105">Subscriptions to free and paid tiers are available.</span></span> <span data-ttu-id="94986-106">For information about the tiers, see the [pricing page](https://www.microsoft.com/cognitive-services/en-us/pricing).</span><span class="sxs-lookup"><span data-stu-id="94986-106">For information about the tiers, see the [pricing page](https://www.microsoft.com/cognitive-services/en-us/pricing).</span></span>

## <a name="get-a-subscription-key"></a><span data-ttu-id="94986-107">Get a subscription key</span><span class="sxs-lookup"><span data-stu-id="94986-107">Get a subscription key</span></span>
1. <span data-ttu-id="94986-108">You can get a subscription key from the Azure portal in one of two ways:</span><span class="sxs-lookup"><span data-stu-id="94986-108">You can get a subscription key from the Azure portal in one of two ways:</span></span>

    * <span data-ttu-id="94986-109">Go to the [Azure portal](https://ms.portal.azure.com), and add a new Cognitive Services API by searching for _Cognitive Services_ and then selecting **Cognitive Services APIs**.</span><span class="sxs-lookup"><span data-stu-id="94986-109">Go to the [Azure portal](https://ms.portal.azure.com), and add a new Cognitive Services API by searching for _Cognitive Services_ and then selecting **Cognitive Services APIs**.</span></span>

      ![Cognitive Services search](../../../media/cognitive-services/custom-speech-service/custom-speech-azure-subscription.png)

    * <span data-ttu-id="94986-111">Or go directly to the [Cognitive Services APIs](https://ms.portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="94986-111">Or go directly to the [Cognitive Services APIs](https://ms.portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

        ![Cognitive Services APIs](../../../media/cognitive-services/custom-speech-service/custom-speech-azure-subscription2.png)

    
1. <span data-ttu-id="94986-113">Fill in the following required fields:</span><span class="sxs-lookup"><span data-stu-id="94986-113">Fill in the following required fields:</span></span>

      <span data-ttu-id="94986-114">a.</span><span class="sxs-lookup"><span data-stu-id="94986-114">a.</span></span> <span data-ttu-id="94986-115">**Account name**.</span><span class="sxs-lookup"><span data-stu-id="94986-115">**Account name**.</span></span> <span data-ttu-id="94986-116">Use a name that works for you.</span><span class="sxs-lookup"><span data-stu-id="94986-116">Use a name that works for you.</span></span> <span data-ttu-id="94986-117">Remember this name so that you can find your Cognitive Services subscription in the resources list.</span><span class="sxs-lookup"><span data-stu-id="94986-117">Remember this name so that you can find your Cognitive Services subscription in the resources list.</span></span>

      <span data-ttu-id="94986-118">b.</span><span class="sxs-lookup"><span data-stu-id="94986-118">b.</span></span> <span data-ttu-id="94986-119">**Subscription**.</span><span class="sxs-lookup"><span data-stu-id="94986-119">**Subscription**.</span></span> <span data-ttu-id="94986-120">Select one from your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="94986-120">Select one from your Azure subscriptions.</span></span>

      <span data-ttu-id="94986-121">c.</span><span class="sxs-lookup"><span data-stu-id="94986-121">c.</span></span> <span data-ttu-id="94986-122">**API type**.</span><span class="sxs-lookup"><span data-stu-id="94986-122">**API type**.</span></span> <span data-ttu-id="94986-123">Select **Custom Speech Service (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="94986-123">Select **Custom Speech Service (Preview)**.</span></span>

      <span data-ttu-id="94986-124">d.</span><span class="sxs-lookup"><span data-stu-id="94986-124">d.</span></span> <span data-ttu-id="94986-125">**Location**.</span><span class="sxs-lookup"><span data-stu-id="94986-125">**Location**.</span></span> <span data-ttu-id="94986-126">It's currently **West US**.</span><span class="sxs-lookup"><span data-stu-id="94986-126">It's currently **West US**.</span></span>

      <span data-ttu-id="94986-127">e.</span><span class="sxs-lookup"><span data-stu-id="94986-127">e.</span></span> <span data-ttu-id="94986-128">**Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="94986-128">**Pricing tier**.</span></span> <span data-ttu-id="94986-129">Select the tier that works for you.</span><span class="sxs-lookup"><span data-stu-id="94986-129">Select the tier that works for you.</span></span> <span data-ttu-id="94986-130">**F0** is the free tier.</span><span class="sxs-lookup"><span data-stu-id="94986-130">**F0** is the free tier.</span></span> <span data-ttu-id="94986-131">The quotas that are allowed are explained on the [pricing page](https://www.microsoft.com/cognitive-services/en-us/pricing).</span><span class="sxs-lookup"><span data-stu-id="94986-131">The quotas that are allowed are explained on the [pricing page](https://www.microsoft.com/cognitive-services/en-us/pricing).</span></span>

      ![Cognitive Services account creation](../../../media/cognitive-services/custom-speech-service/custom-speech-azure-cris-blade.png)

1. <span data-ttu-id="94986-133">You should find either a view on your dashboard or a service with the provided account name in your resources list.</span><span class="sxs-lookup"><span data-stu-id="94986-133">You should find either a view on your dashboard or a service with the provided account name in your resources list.</span></span> <span data-ttu-id="94986-134">When you select it, you can see an overview of your service.</span><span class="sxs-lookup"><span data-stu-id="94986-134">When you select it, you can see an overview of your service.</span></span> <span data-ttu-id="94986-135">In the list on the left, under **Resource Management**, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="94986-135">In the list on the left, under **Resource Management**, select **Keys**.</span></span> <span data-ttu-id="94986-136">Copy **KEY 1**.</span><span class="sxs-lookup"><span data-stu-id="94986-136">Copy **KEY 1**.</span></span>

      <span data-ttu-id="94986-137">This subscription key is required in the next steps.</span><span class="sxs-lookup"><span data-stu-id="94986-137">This subscription key is required in the next steps.</span></span>

      ![KEY 1](../../../media/cognitive-services/custom-speech-service/custom-speech-azure-cris-keys2.png)

      > [!NOTE]
      > <span data-ttu-id="94986-139">Do not copy the **Subscription ID** from the overview page.</span><span class="sxs-lookup"><span data-stu-id="94986-139">Do not copy the **Subscription ID** from the overview page.</span></span> <span data-ttu-id="94986-140">You need the subscription key in the next step.</span><span class="sxs-lookup"><span data-stu-id="94986-140">You need the subscription key in the next step.</span></span>
      >

      ![Overview Subscription ID](../../../media/cognitive-services/custom-speech-service/custom-speech-azure-cris-keys.png)

1. <span data-ttu-id="94986-142">To enter your subscription key, on the ribbon at the upper right, select your user account.</span><span class="sxs-lookup"><span data-stu-id="94986-142">To enter your subscription key, on the ribbon at the upper right, select your user account.</span></span> <span data-ttu-id="94986-143">On the drop-down menu, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="94986-143">On the drop-down menu, select **Subscriptions**.</span></span>

      ![Subscriptions menu item](../../../media/cognitive-services/custom-speech-service/custom-speech-subscription-selection.png)

    <span data-ttu-id="94986-145">A table of subscriptions appears, which is empty the first time it opens.</span><span class="sxs-lookup"><span data-stu-id="94986-145">A table of subscriptions appears, which is empty the first time it opens.</span></span>

    ![Subscriptions table](../../../media/cognitive-services/custom-speech-service/custom-speech-subscription-list.png)

1. <span data-ttu-id="94986-147">Select **Add new**.</span><span class="sxs-lookup"><span data-stu-id="94986-147">Select **Add new**.</span></span> <span data-ttu-id="94986-148">Enter a name for the subscription and the subscription key.</span><span class="sxs-lookup"><span data-stu-id="94986-148">Enter a name for the subscription and the subscription key.</span></span> <span data-ttu-id="94986-149">It can be either **KEY 1** (primary key) or **KEY 2** (secondary key) from your subscription.</span><span class="sxs-lookup"><span data-stu-id="94986-149">It can be either **KEY 1** (primary key) or **KEY 2** (secondary key) from your subscription.</span></span>

      ![Subscription key name](../../../media/cognitive-services/custom-speech-service/custom-speech-enter-subsciption.png)

<span data-ttu-id="94986-151">To upload data, train a model, or do a deployment, you need to link your Custom Speech Service activities to an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="94986-151">To upload data, train a model, or do a deployment, you need to link your Custom Speech Service activities to an Azure subscription.</span></span> <span data-ttu-id="94986-152">It can be either a free tier or a paid tier subscription.</span><span class="sxs-lookup"><span data-stu-id="94986-152">It can be either a free tier or a paid tier subscription.</span></span> <span data-ttu-id="94986-153">For more information, see the [pricing page](https://www.microsoft.com/cognitive-services/en-us/pricing).</span><span class="sxs-lookup"><span data-stu-id="94986-153">For more information, see the [pricing page](https://www.microsoft.com/cognitive-services/en-us/pricing).</span></span>

## <a name="get-a-subscription-id"></a><span data-ttu-id="94986-154">Get a subscription ID</span><span class="sxs-lookup"><span data-stu-id="94986-154">Get a subscription ID</span></span>
<span data-ttu-id="94986-155">To get a subscription ID, go to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94986-155">To get a subscription ID, go to the Azure portal.</span></span> <span data-ttu-id="94986-156">Search for *Cognitive Services* and *Custom Speech Service*, and follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="94986-156">Search for *Cognitive Services* and *Custom Speech Service*, and follow the instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="94986-157">The subscription key is required later in this process.</span><span class="sxs-lookup"><span data-stu-id="94986-157">The subscription key is required later in this process.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="94986-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="94986-158">Next steps</span></span>
* <span data-ttu-id="94986-159">Start to create your [custom acoustic model](cognitive-services-custom-speech-create-acoustic-model.md).</span><span class="sxs-lookup"><span data-stu-id="94986-159">Start to create your [custom acoustic model](cognitive-services-custom-speech-create-acoustic-model.md).</span></span>
* <span data-ttu-id="94986-160">Start to create your [custom language model](cognitive-services-custom-speech-create-language-model.md).</span><span class="sxs-lookup"><span data-stu-id="94986-160">Start to create your [custom language model](cognitive-services-custom-speech-create-language-model.md).</span></span>
