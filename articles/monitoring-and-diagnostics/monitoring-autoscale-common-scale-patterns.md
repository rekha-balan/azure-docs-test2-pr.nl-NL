---
title: Overview of common autoscale patterns
description: Learn some of the common patterns to auto scale your resource in Azure.
author: anirudhcavale
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 05/07/2017
ms.author: ancav
ms.component: autoscale
ms.openlocfilehash: 84727ec3694f64d40ad002a248a255df9074d7f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966444"
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="10a31-103">Overview of common autoscale patterns</span><span class="sxs-lookup"><span data-stu-id="10a31-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="10a31-104">This article describes some of the common patterns to scale your resource in Azure.</span><span class="sxs-lookup"><span data-stu-id="10a31-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="10a31-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span><span class="sxs-lookup"><span data-stu-id="10a31-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="10a31-106">Lets get started</span><span class="sxs-lookup"><span data-stu-id="10a31-106">Lets get started</span></span>

<span data-ttu-id="10a31-107">This article assumes that you are familiar with auto scale.</span><span class="sxs-lookup"><span data-stu-id="10a31-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="10a31-108">You can [get started here to scale your resource][1].</span><span class="sxs-lookup"><span data-stu-id="10a31-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="10a31-109">The following are some of the common scale patterns.</span><span class="sxs-lookup"><span data-stu-id="10a31-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="10a31-110">Scale based on CPU</span><span class="sxs-lookup"><span data-stu-id="10a31-110">Scale based on CPU</span></span>

<span data-ttu-id="10a31-111">You have a web app (/VMSS/cloud service role) and</span><span class="sxs-lookup"><span data-stu-id="10a31-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="10a31-112">You want to scale out/scale in based on CPU.</span><span class="sxs-lookup"><span data-stu-id="10a31-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="10a31-113">Additionally, you want to ensure there is a minimum number of instances.</span><span class="sxs-lookup"><span data-stu-id="10a31-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="10a31-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span><span class="sxs-lookup"><span data-stu-id="10a31-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![Scale based on CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="10a31-116">Scale differently on weekdays vs weekends</span><span class="sxs-lookup"><span data-stu-id="10a31-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="10a31-117">You have a web app (/VMSS/cloud service role) and</span><span class="sxs-lookup"><span data-stu-id="10a31-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="10a31-118">You want 3 instances by default (on weekdays)</span><span class="sxs-lookup"><span data-stu-id="10a31-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="10a31-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span><span class="sxs-lookup"><span data-stu-id="10a31-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![Scale differently on weekdays vs weekends][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="10a31-121">Scale differently during holidays</span><span class="sxs-lookup"><span data-stu-id="10a31-121">Scale differently during holidays</span></span>

<span data-ttu-id="10a31-122">You have a web app (/VMSS/cloud service role) and</span><span class="sxs-lookup"><span data-stu-id="10a31-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="10a31-123">You want to scale up/down based on CPU usage by default</span><span class="sxs-lookup"><span data-stu-id="10a31-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="10a31-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span><span class="sxs-lookup"><span data-stu-id="10a31-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![Scale differently on holidays][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="10a31-126">Scale based on custom metric</span><span class="sxs-lookup"><span data-stu-id="10a31-126">Scale based on custom metric</span></span>

<span data-ttu-id="10a31-127">You have a web front end and a API tier that communicates with the backend.</span><span class="sxs-lookup"><span data-stu-id="10a31-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="10a31-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span><span class="sxs-lookup"><span data-stu-id="10a31-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![Scale based on custom metric][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png