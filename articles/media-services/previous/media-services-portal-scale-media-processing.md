---
title: Scale media processing using the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of scaling media processing using the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 51973916c97282ac93032ab833402d9d1356647e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865839"
---
# <a name="change-the-reserved-unit-type"></a><span data-ttu-id="da1f8-103">Change the reserved unit type</span><span class="sxs-lookup"><span data-stu-id="da1f8-103">Change the reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

> [!NOTE]
> To get the latest version of Java SDK and get started developing with Java, see [Get started with the Java client SDK for Media Services](https://docs.microsoft.com/azure/media-services/media-services-java-how-to-use). <br/>
> To download the latest PHP SDK for Media Services, look for version 0.5.7 of the Microsoft/WindowAzure package in the [Packagist repository](https://packagist.org/packages/microsoft/windowsazure#v0.5.7).  

## <a name="overview"></a><span data-ttu-id="da1f8-111">Overview</span><span class="sxs-lookup"><span data-stu-id="da1f8-111">Overview</span></span>

<span data-ttu-id="da1f8-112">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span><span class="sxs-lookup"><span data-stu-id="da1f8-112">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="da1f8-113">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span><span class="sxs-lookup"><span data-stu-id="da1f8-113">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="da1f8-114">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span><span class="sxs-lookup"><span data-stu-id="da1f8-114">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

<span data-ttu-id="da1f8-115">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span><span class="sxs-lookup"><span data-stu-id="da1f8-115">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="da1f8-116">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span><span class="sxs-lookup"><span data-stu-id="da1f8-116">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
>RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer. However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.

> [!IMPORTANT]
> Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="da1f8-120">Scale media processing</span><span class="sxs-lookup"><span data-stu-id="da1f8-120">Scale media processing</span></span>
<span data-ttu-id="da1f8-121">To change the reserved unit type and the number of reserved units, do the following:</span><span class="sxs-lookup"><span data-stu-id="da1f8-121">To change the reserved unit type and the number of reserved units, do the following:</span></span>

1. <span data-ttu-id="da1f8-122">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="da1f8-122">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="da1f8-123">In the **Settings** window, select **Media reserved units**.</span><span class="sxs-lookup"><span data-stu-id="da1f8-123">In the **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="da1f8-124">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider at the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="da1f8-124">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider at the top of the screen.</span></span>
   
    <span data-ttu-id="da1f8-125">To change the **RESERVED UNIT TYPE**, click on the **Speed of reserved processing units** bar.</span><span class="sxs-lookup"><span data-stu-id="da1f8-125">To change the **RESERVED UNIT TYPE**, click on the **Speed of reserved processing units** bar.</span></span> <span data-ttu-id="da1f8-126">Then, select the pricing tier you need: S1, S2, or S3.</span><span class="sxs-lookup"><span data-stu-id="da1f8-126">Then, select the pricing tier you need: S1, S2, or S3.</span></span>
   
3. <span data-ttu-id="da1f8-127">Press the SAVE button to save your changes.</span><span class="sxs-lookup"><span data-stu-id="da1f8-127">Press the SAVE button to save your changes.</span></span>
   
    <span data-ttu-id="da1f8-128">The new reserved units are allocated when you press SAVE.</span><span class="sxs-lookup"><span data-stu-id="da1f8-128">The new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da1f8-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="da1f8-129">Next steps</span></span>
<span data-ttu-id="da1f8-130">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="da1f8-130">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="da1f8-131">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="da1f8-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

