---
title: Manage speed and concurrency of your encoding with Azure Media Services | Microsoft Docs
description: This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks with Azure Media Services.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: d7e3d6d0c176d0a903c3027ab4feddb332557566
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865917"
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="d5d2d-103">Manage speed and concurrency of your encoding</span><span class="sxs-lookup"><span data-stu-id="d5d2d-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="d5d2d-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="d5d2d-105">Overview</span><span class="sxs-lookup"><span data-stu-id="d5d2d-105">Overview</span></span>

<span data-ttu-id="d5d2d-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="d5d2d-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="d5d2d-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="d5d2d-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="d5d2d-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="d5d2d-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="d5d2d-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="d5d2d-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="d5d2d-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="d5d2d-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="d5d2d-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="d5d2d-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="d5d2d-117">Next step</span><span class="sxs-lookup"><span data-stu-id="d5d2d-117">Next step</span></span>

[<span data-ttu-id="d5d2d-118">Scale encoding units</span><span class="sxs-lookup"><span data-stu-id="d5d2d-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="d5d2d-119">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d5d2d-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d5d2d-120">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d5d2d-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

