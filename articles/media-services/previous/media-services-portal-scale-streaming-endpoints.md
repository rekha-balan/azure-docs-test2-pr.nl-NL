---
title: Scale streaming endpoints with the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of scaling streaming endpoints with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2017
ms.author: juliako
ms.openlocfilehash: f2a14f2622d78a4222a8518172eb1ce8ed9e6637
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871667"
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="e245c-103">Scale streaming endpoints with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e245c-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="e245c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e245c-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="e245c-105">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="e245c-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="e245c-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e245c-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="e245c-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span><span class="sxs-lookup"><span data-stu-id="e245c-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="e245c-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span><span class="sxs-lookup"><span data-stu-id="e245c-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="e245c-109">The streaming endpoint can be scaled by adding SUs.</span><span class="sxs-lookup"><span data-stu-id="e245c-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="e245c-110">Each SU provides additional bandwidth capacity to the application.</span><span class="sxs-lookup"><span data-stu-id="e245c-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="e245c-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-streaming-endpoints-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="e245c-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-streaming-endpoints-overview.md) topic.</span></span>
 
<span data-ttu-id="e245c-112">This topic shows how to scale a streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="e245c-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="e245c-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="e245c-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="e245c-114">Scale streaming endpoints</span><span class="sxs-lookup"><span data-stu-id="e245c-114">Scale streaming endpoints</span></span>

<span data-ttu-id="e245c-115">To change the number of streaming units, do the following:</span><span class="sxs-lookup"><span data-stu-id="e245c-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="e245c-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="e245c-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="e245c-117">In the **Settings** window, select **Streaming endpoints**.</span><span class="sxs-lookup"><span data-stu-id="e245c-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="e245c-118">Click on the streaming endpoint that you want to scale.</span><span class="sxs-lookup"><span data-stu-id="e245c-118">Click on the streaming endpoint that you want to scale.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="e245c-119">You can only scale **Premium** streaming endpoints.</span><span class="sxs-lookup"><span data-stu-id="e245c-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="e245c-120">Move the slider to specify the number of streaming units.</span><span class="sxs-lookup"><span data-stu-id="e245c-120">Move the slider to specify the number of streaming units.</span></span>

    ![Streaming endpoint](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="e245c-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="e245c-122">Next steps</span></span>
<span data-ttu-id="e245c-123">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="e245c-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e245c-124">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="e245c-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

