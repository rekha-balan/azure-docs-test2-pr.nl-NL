---
title: Manage a Video Indexer account connected to Azure | Microsoft Docs
description: This article shows how to manage a Video Indexer account connected to Azure.
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 08/23/2018
ms.author: juliako
ms.openlocfilehash: 1b794f488da4470aefabb10dbad0a9202f5984e9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870229"
---
# <a name="manage-a-video-indexer-account-connected-to-azure"></a><span data-ttu-id="aa03e-103">Manage a Video Indexer account connected to Azure</span><span class="sxs-lookup"><span data-stu-id="aa03e-103">Manage a Video Indexer account connected to Azure</span></span>

<span data-ttu-id="aa03e-104">This article demonstrates how to manage a Video Indexer account that is connected to your Azure subscription and an Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="aa03e-104">This article demonstrates how to manage a Video Indexer account that is connected to your Azure subscription and an Azure Media Services account.</span></span>

> [!NOTE]
> <span data-ttu-id="aa03e-105">You have to be the Video Indexer account owner to do account configuration adjustments discussed in this topic.</span><span class="sxs-lookup"><span data-stu-id="aa03e-105">You have to be the Video Indexer account owner to do account configuration adjustments discussed in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa03e-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aa03e-106">Prerequisites</span></span>

<span data-ttu-id="aa03e-107">Connect your Video Indexer account to Azure, as described in [Connected to Azure](connect-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="aa03e-107">Connect your Video Indexer account to Azure, as described in [Connected to Azure](connect-to-azure.md).</span></span> 

<span data-ttu-id="aa03e-108">Make sure to follow [Prerequisites](connect-to-azure.md#prerequisites) and review [Considerations](connect-to-azure.md#considerations) in the article.</span><span class="sxs-lookup"><span data-stu-id="aa03e-108">Make sure to follow [Prerequisites](connect-to-azure.md#prerequisites) and review [Considerations](connect-to-azure.md#considerations) in the article.</span></span>

## <a name="examine-account-settings"></a><span data-ttu-id="aa03e-109">Examine account settings</span><span class="sxs-lookup"><span data-stu-id="aa03e-109">Examine account settings</span></span>

<span data-ttu-id="aa03e-110">This section examines settings of your Video Indexer account.</span><span class="sxs-lookup"><span data-stu-id="aa03e-110">This section examines settings of your Video Indexer account.</span></span>

<span data-ttu-id="aa03e-111">To view settings:</span><span class="sxs-lookup"><span data-stu-id="aa03e-111">To view settings:</span></span>

1. <span data-ttu-id="aa03e-112">Click on the user icon in the top right corner and select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="aa03e-112">Click on the user icon in the top right corner and select **Settings**.</span></span>

    ![Settings](./media/manage-account-connected-to-azure/select-settings.png)

2. <span data-ttu-id="aa03e-114">On the **Settings** page, select the **Account** tab.</span><span class="sxs-lookup"><span data-stu-id="aa03e-114">On the **Settings** page, select the **Account** tab.</span></span>

<span data-ttu-id="aa03e-115">If your Videos Indexer account is connected to Azure, you see the following:</span><span class="sxs-lookup"><span data-stu-id="aa03e-115">If your Videos Indexer account is connected to Azure, you see the following:</span></span>

* <span data-ttu-id="aa03e-116">The name of the underlying Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="aa03e-116">The name of the underlying Azure Media Services account.</span></span>
* <span data-ttu-id="aa03e-117">The number of indexing jobs running and queued.</span><span class="sxs-lookup"><span data-stu-id="aa03e-117">The number of indexing jobs running and queued.</span></span>
* <span data-ttu-id="aa03e-118">The number and type of allocated Reserved Units.</span><span class="sxs-lookup"><span data-stu-id="aa03e-118">The number and type of allocated Reserved Units.</span></span>

<span data-ttu-id="aa03e-119">If your account needs some adjustments, you will see relevant errors and warnings about your account configuration on the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="aa03e-119">If your account needs some adjustments, you will see relevant errors and warnings about your account configuration on the **Settings** page.</span></span> <span data-ttu-id="aa03e-120">The messages contain links to exact places in Azure portal where you need to make changes.</span><span class="sxs-lookup"><span data-stu-id="aa03e-120">The messages contain links to exact places in Azure portal where you need to make changes.</span></span> <span data-ttu-id="aa03e-121">For more information, see the [errors and warnings](#errors-and-warnings) section that follows.</span><span class="sxs-lookup"><span data-stu-id="aa03e-121">For more information, see the [errors and warnings](#errors-and-warnings) section that follows.</span></span>

## <a name="auto-scale-reserved-units"></a><span data-ttu-id="aa03e-122">Auto-scale reserved units</span><span class="sxs-lookup"><span data-stu-id="aa03e-122">Auto-scale reserved units</span></span>

<span data-ttu-id="aa03e-123">The **Settings** page enables you to set the autoscaling of Media Reserved Units (RU).</span><span class="sxs-lookup"><span data-stu-id="aa03e-123">The **Settings** page enables you to set the autoscaling of Media Reserved Units (RU).</span></span> <span data-ttu-id="aa03e-124">If the option is **On**, you can allocate the maximum number of RUs and be sure that Video Indexer stops/starts RUs automatically.</span><span class="sxs-lookup"><span data-stu-id="aa03e-124">If the option is **On**, you can allocate the maximum number of RUs and be sure that Video Indexer stops/starts RUs automatically.</span></span> <span data-ttu-id="aa03e-125">With this option, you don't pay extra money for idle time but also do not wait for indexing jobs to complete a long time when the indexing load is high.</span><span class="sxs-lookup"><span data-stu-id="aa03e-125">With this option, you don't pay extra money for idle time but also do not wait for indexing jobs to complete a long time when the indexing load is high.</span></span>

<span data-ttu-id="aa03e-126">Auto-scale does not scale below 1 RU or above the default limit of the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="aa03e-126">Auto-scale does not scale below 1 RU or above the default limit of the Media Services account.</span></span> <span data-ttu-id="aa03e-127">In order to increase the limit, create a service request.</span><span class="sxs-lookup"><span data-stu-id="aa03e-127">In order to increase the limit, create a service request.</span></span> <span data-ttu-id="aa03e-128">For information about quotas and limitations and how to open a support ticket, see [Quotas and limitations](../../media-services/previous/media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="aa03e-128">For information about quotas and limitations and how to open a support ticket, see [Quotas and limitations](../../media-services/previous/media-services-quotas-and-limitations.md).</span></span>

![Sign up](./media/manage-account-connected-to-azure/autoscale-reserved-units.png)

## <a name="errors-and-warnings"></a><span data-ttu-id="aa03e-130">Errors and warnings</span><span class="sxs-lookup"><span data-stu-id="aa03e-130">Errors and warnings</span></span>

<span data-ttu-id="aa03e-131">If your account needs some adjustments, you see relevant errors and warnings about your account configuration on the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="aa03e-131">If your account needs some adjustments, you see relevant errors and warnings about your account configuration on the **Settings** page.</span></span> <span data-ttu-id="aa03e-132">The messages contain links to exact places in Azure portal where you need to make changes.</span><span class="sxs-lookup"><span data-stu-id="aa03e-132">The messages contain links to exact places in Azure portal where you need to make changes.</span></span> <span data-ttu-id="aa03e-133">This section gives more details about the error and warning messages.</span><span class="sxs-lookup"><span data-stu-id="aa03e-133">This section gives more details about the error and warning messages.</span></span>

* <span data-ttu-id="aa03e-134">Event Grid</span><span class="sxs-lookup"><span data-stu-id="aa03e-134">Event Grid</span></span>

    <span data-ttu-id="aa03e-135">You have to register the EventGrid resource provider using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="aa03e-135">You have to register the EventGrid resource provider using the Azure portal.</span></span> <span data-ttu-id="aa03e-136">In the [Azure portal](https://portal.azure.com/), go to **Subscriptions** > [subscription] > **ResourceProviders** > **Microsoft.EventGrid**.</span><span class="sxs-lookup"><span data-stu-id="aa03e-136">In the [Azure portal](https://portal.azure.com/), go to **Subscriptions** > [subscription] > **ResourceProviders** > **Microsoft.EventGrid**.</span></span> <span data-ttu-id="aa03e-137">If not in the **Registered** state, click **Register**.</span><span class="sxs-lookup"><span data-stu-id="aa03e-137">If not in the **Registered** state, click **Register**.</span></span> <span data-ttu-id="aa03e-138">It takes a couple of minutes to register.</span><span class="sxs-lookup"><span data-stu-id="aa03e-138">It takes a couple of minutes to register.</span></span> 

* <span data-ttu-id="aa03e-139">Streaming Endpoint</span><span class="sxs-lookup"><span data-stu-id="aa03e-139">Streaming Endpoint</span></span>

    <span data-ttu-id="aa03e-140">Make sure the underlying Media Services account has the default **Streaming Endpoint** in a started state.</span><span class="sxs-lookup"><span data-stu-id="aa03e-140">Make sure the underlying Media Services account has the default **Streaming Endpoint** in a started state.</span></span> <span data-ttu-id="aa03e-141">Otherwise, you will not be able to watch videos from this Media Services account or in Video Indexer.</span><span class="sxs-lookup"><span data-stu-id="aa03e-141">Otherwise, you will not be able to watch videos from this Media Services account or in Video Indexer.</span></span>

* <span data-ttu-id="aa03e-142">Media Reserved Units</span><span class="sxs-lookup"><span data-stu-id="aa03e-142">Media Reserved Units</span></span> 

    <span data-ttu-id="aa03e-143">You must allocate Media Reserved Units on your Media Service resource in order to index videos.</span><span class="sxs-lookup"><span data-stu-id="aa03e-143">You must allocate Media Reserved Units on your Media Service resource in order to index videos.</span></span> <span data-ttu-id="aa03e-144">For optimal indexing performance, it's recommended to allocate at least 10 S3 Reserved Units.</span><span class="sxs-lookup"><span data-stu-id="aa03e-144">For optimal indexing performance, it's recommended to allocate at least 10 S3 Reserved Units.</span></span> <span data-ttu-id="aa03e-145">For pricing information, see the FAQ section of the [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/) page.</span><span class="sxs-lookup"><span data-stu-id="aa03e-145">For pricing information, see the FAQ section of the [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/) page.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="aa03e-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa03e-146">Next steps</span></span>

<span data-ttu-id="aa03e-147">You can programmatically interact with your trial account and/or with your Video Indexer accounts that are connected to azure by following the instructions in: [Use APIs](video-indexer-use-apis.md).</span><span class="sxs-lookup"><span data-stu-id="aa03e-147">You can programmatically interact with your trial account and/or with your Video Indexer accounts that are connected to azure by following the instructions in: [Use APIs](video-indexer-use-apis.md).</span></span>

<span data-ttu-id="aa03e-148">You should use the same Azure AD user you used when connecting to Azure.</span><span class="sxs-lookup"><span data-stu-id="aa03e-148">You should use the same Azure AD user you used when connecting to Azure.</span></span>
