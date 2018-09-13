---
title: Scaling Media Processing overview | Microsoft Docs
description: This topic is an overview of scaling Media Processing with Azure Media Services.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2018
ms.author: juliako
ms.openlocfilehash: 81fab8903c0101d0e4aae8a392f05129651cd762
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867945"
---
# <a name="scaling-media-processing-overview"></a><span data-ttu-id="97843-103">Scaling Media Processing overview</span><span class="sxs-lookup"><span data-stu-id="97843-103">Scaling Media Processing overview</span></span>
<span data-ttu-id="97843-104">This page gives an overview of how and why to scale media processing.</span><span class="sxs-lookup"><span data-stu-id="97843-104">This page gives an overview of how and why to scale media processing.</span></span> 

## <a name="overview"></a><span data-ttu-id="97843-105">Overview</span><span class="sxs-lookup"><span data-stu-id="97843-105">Overview</span></span>
<span data-ttu-id="97843-106">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span><span class="sxs-lookup"><span data-stu-id="97843-106">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="97843-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span><span class="sxs-lookup"><span data-stu-id="97843-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="97843-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span><span class="sxs-lookup"><span data-stu-id="97843-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="97843-109">For more information, see the [Reserved Unit Types](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).</span><span class="sxs-lookup"><span data-stu-id="97843-109">For more information, see the [Reserved Unit Types](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).</span></span>

<span data-ttu-id="97843-110">In addition to specifying the reserved unit type, you can specify to provision your account with reserved units.</span><span class="sxs-lookup"><span data-stu-id="97843-110">In addition to specifying the reserved unit type, you can specify to provision your account with reserved units.</span></span> <span data-ttu-id="97843-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span><span class="sxs-lookup"><span data-stu-id="97843-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="97843-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span><span class="sxs-lookup"><span data-stu-id="97843-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="97843-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span><span class="sxs-lookup"><span data-stu-id="97843-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="97843-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span><span class="sxs-lookup"><span data-stu-id="97843-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="97843-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span><span class="sxs-lookup"><span data-stu-id="97843-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

## <a name="choosing-between-different-reserved-unit-types"></a><span data-ttu-id="97843-116">Choosing between different reserved unit types</span><span class="sxs-lookup"><span data-stu-id="97843-116">Choosing between different reserved unit types</span></span>
<span data-ttu-id="97843-117">The following table helps you make decision when choosing between different encoding speeds.</span><span class="sxs-lookup"><span data-stu-id="97843-117">The following table helps you make decision when choosing between different encoding speeds.</span></span> <span data-ttu-id="97843-118">It also provides a few benchmark cases and provides SAS URLs that you can use to download videos on which you can perform your own tests:</span><span class="sxs-lookup"><span data-stu-id="97843-118">It also provides a few benchmark cases and provides SAS URLs that you can use to download videos on which you can perform your own tests:</span></span>

| <span data-ttu-id="97843-119">Scenarios</span><span class="sxs-lookup"><span data-stu-id="97843-119">Scenarios</span></span> | <span data-ttu-id="97843-120">**S1**</span><span class="sxs-lookup"><span data-stu-id="97843-120">**S1**</span></span> | <span data-ttu-id="97843-121">**S2**</span><span class="sxs-lookup"><span data-stu-id="97843-121">**S2**</span></span> | <span data-ttu-id="97843-122">**S3**</span><span class="sxs-lookup"><span data-stu-id="97843-122">**S3**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="97843-123">Intended use case</span><span class="sxs-lookup"><span data-stu-id="97843-123">Intended use case</span></span> |<span data-ttu-id="97843-124">Single bitrate encoding.</span><span class="sxs-lookup"><span data-stu-id="97843-124">Single bitrate encoding.</span></span> <br/><span data-ttu-id="97843-125">Files at SD or below resolutions, not time sensitive, low cost.</span><span class="sxs-lookup"><span data-stu-id="97843-125">Files at SD or below resolutions, not time sensitive, low cost.</span></span> |<span data-ttu-id="97843-126">Single bitrate and multiple bitrate encoding.</span><span class="sxs-lookup"><span data-stu-id="97843-126">Single bitrate and multiple bitrate encoding.</span></span><br/><span data-ttu-id="97843-127">Normal usage for both SD and HD encoding.</span><span class="sxs-lookup"><span data-stu-id="97843-127">Normal usage for both SD and HD encoding.</span></span> |<span data-ttu-id="97843-128">Single bitrate and multiple bitrate encoding.</span><span class="sxs-lookup"><span data-stu-id="97843-128">Single bitrate and multiple bitrate encoding.</span></span><br/><span data-ttu-id="97843-129">Full HD and 4K resolution videos.</span><span class="sxs-lookup"><span data-stu-id="97843-129">Full HD and 4K resolution videos.</span></span> <span data-ttu-id="97843-130">Time sensitive, faster turnaround encoding.</span><span class="sxs-lookup"><span data-stu-id="97843-130">Time sensitive, faster turnaround encoding.</span></span> |
| <span data-ttu-id="97843-131">Benchmark</span><span class="sxs-lookup"><span data-stu-id="97843-131">Benchmark</span></span> |<span data-ttu-id="97843-132">Encoding to a single bitrate MP4 file, at the same resolution, takes approximately 11 minutes.</span><span class="sxs-lookup"><span data-stu-id="97843-132">Encoding to a single bitrate MP4 file, at the same resolution, takes approximately 11 minutes.</span></span> |<span data-ttu-id="97843-133">Encoding with "H264 Single Bitrate 720p" preset takes approximately 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="97843-133">Encoding with "H264 Single Bitrate 720p" preset takes approximately 5 minutes.</span></span><br/><br/><span data-ttu-id="97843-134">Encoding with "H264 Multiple Bitrate 720p" preset takes approximately 11.5 minutes.</span><span class="sxs-lookup"><span data-stu-id="97843-134">Encoding with "H264 Multiple Bitrate 720p" preset takes approximately 11.5 minutes.</span></span> |<span data-ttu-id="97843-135">Encoding with "H264 Single Bitrate 1080p" preset takes approximately 2.7 minutes.</span><span class="sxs-lookup"><span data-stu-id="97843-135">Encoding with "H264 Single Bitrate 1080p" preset takes approximately 2.7 minutes.</span></span><br/><br/><span data-ttu-id="97843-136">Encoding with "H264 Multiple Bitrate 1080p" preset takes approximately 5.7 minutes.</span><span class="sxs-lookup"><span data-stu-id="97843-136">Encoding with "H264 Multiple Bitrate 1080p" preset takes approximately 5.7 minutes.</span></span> |


## <a name="considerations"></a><span data-ttu-id="97843-137">Considerations</span><span class="sxs-lookup"><span data-stu-id="97843-137">Considerations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="97843-138">Review considerations described in this section.</span><span class="sxs-lookup"><span data-stu-id="97843-138">Review considerations described in this section.</span></span>  
> 
> 

* <span data-ttu-id="97843-139">For the Audio Analysis and Video Analysis jobs that are triggered by Media Services v3 or Video Indexer, S3 unit type is highly recommended.</span><span class="sxs-lookup"><span data-stu-id="97843-139">For the Audio Analysis and Video Analysis jobs that are triggered by Media Services v3 or Video Indexer, S3 unit type is highly recommended.</span></span>
* <span data-ttu-id="97843-140">If using the shared pool, that is, without any reserved units, then your encode tasks have the same performance as with S1 RUs.</span><span class="sxs-lookup"><span data-stu-id="97843-140">If using the shared pool, that is, without any reserved units, then your encode tasks have the same performance as with S1 RUs.</span></span> <span data-ttu-id="97843-141">However, there is no upper bound to the time your Tasks can spend in queued state, and at any given time, at most only one Task will be running.</span><span class="sxs-lookup"><span data-stu-id="97843-141">However, there is no upper bound to the time your Tasks can spend in queued state, and at any given time, at most only one Task will be running.</span></span>

## <a name="billing"></a><span data-ttu-id="97843-142">Billing</span><span class="sxs-lookup"><span data-stu-id="97843-142">Billing</span></span>

<span data-ttu-id="97843-143">You are charged based on actual minutes of usage of Media Reserved Units.</span><span class="sxs-lookup"><span data-stu-id="97843-143">You are charged based on actual minutes of usage of Media Reserved Units.</span></span> <span data-ttu-id="97843-144">For a detailed explanation, see the FAQ section of the [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/) page.</span><span class="sxs-lookup"><span data-stu-id="97843-144">For a detailed explanation, see the FAQ section of the [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/) page.</span></span>   

## <a name="quotas-and-limitations"></a><span data-ttu-id="97843-145">Quotas and limitations</span><span class="sxs-lookup"><span data-stu-id="97843-145">Quotas and limitations</span></span>
<span data-ttu-id="97843-146">For information about quotas and limitations and how to open a support ticket, see [Quotas and limitations](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="97843-146">For information about quotas and limitations and how to open a support ticket, see [Quotas and limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="97843-147">Next step</span><span class="sxs-lookup"><span data-stu-id="97843-147">Next step</span></span>
<span data-ttu-id="97843-148">Achieve the scaling media processing task with one of these technologies:</span><span class="sxs-lookup"><span data-stu-id="97843-148">Achieve the scaling media processing task with one of these technologies:</span></span> 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 

> [!NOTE]
> To get the latest version of Java SDK and get started developing with Java, see [Get started with the Java client SDK for Media Services](https://docs.microsoft.com/azure/media-services/media-services-java-how-to-use). <br/>
> To download the latest PHP SDK for Media Services, look for version 0.5.7 of the Microsoft/WindowAzure package in the [Packagist repository](https://packagist.org/packages/microsoft/windowsazure#v0.5.7).  

## <a name="media-services-learning-paths"></a><span data-ttu-id="97843-156">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="97843-156">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="97843-157">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="97843-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

