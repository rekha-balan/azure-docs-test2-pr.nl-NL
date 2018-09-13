---
title: Azure Container Instances quotas and region availability
description: The default quotas and region availability of the Azure Container Instances service.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: overview
ms.date: 02/27/2018
ms.author: marsma
ms.openlocfilehash: 1bc890abc8b406ae75f292f37775e4cb62cf0473
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868464"
---
# <a name="quotas-and-region-availability-for-azure-container-instances"></a><span data-ttu-id="04200-103">Quotas and region availability for Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="04200-103">Quotas and region availability for Azure Container Instances</span></span>

<span data-ttu-id="04200-104">All Azure services include certain default limits and quotas for resources and features.</span><span class="sxs-lookup"><span data-stu-id="04200-104">All Azure services include certain default limits and quotas for resources and features.</span></span> <span data-ttu-id="04200-105">The following sections detail the default resource limits for several Azure Container Instances (ACI) resources, as well as the availability of the ACI service in Azure regions.</span><span class="sxs-lookup"><span data-stu-id="04200-105">The following sections detail the default resource limits for several Azure Container Instances (ACI) resources, as well as the availability of the ACI service in Azure regions.</span></span>

## <a name="service-quotas-and-limits"></a><span data-ttu-id="04200-106">Service quotas and limits</span><span class="sxs-lookup"><span data-stu-id="04200-106">Service quotas and limits</span></span>

[!INCLUDE [container-instances-limits](../../includes/container-instances-limits.md)]

## <a name="region-availability"></a><span data-ttu-id="04200-107">Region availability</span><span class="sxs-lookup"><span data-stu-id="04200-107">Region availability</span></span>

<span data-ttu-id="04200-108">Azure Container Instances is available in the following regions with the specified CPU and memory limits.</span><span class="sxs-lookup"><span data-stu-id="04200-108">Azure Container Instances is available in the following regions with the specified CPU and memory limits.</span></span>

| <span data-ttu-id="04200-109">Location</span><span class="sxs-lookup"><span data-stu-id="04200-109">Location</span></span> | <span data-ttu-id="04200-110">OS</span><span class="sxs-lookup"><span data-stu-id="04200-110">OS</span></span> | <span data-ttu-id="04200-111">CPU</span><span class="sxs-lookup"><span data-stu-id="04200-111">CPU</span></span> | <span data-ttu-id="04200-112">Memory (GB)</span><span class="sxs-lookup"><span data-stu-id="04200-112">Memory (GB)</span></span> |
| -------- | -- | :---: | :-----------: |
| <span data-ttu-id="04200-113">West US, East US, West Europe, North Europe</span><span class="sxs-lookup"><span data-stu-id="04200-113">West US, East US, West Europe, North Europe</span></span> | <span data-ttu-id="04200-114">Linux</span><span class="sxs-lookup"><span data-stu-id="04200-114">Linux</span></span> | <span data-ttu-id="04200-115">4</span><span class="sxs-lookup"><span data-stu-id="04200-115">4</span></span> | <span data-ttu-id="04200-116">14</span><span class="sxs-lookup"><span data-stu-id="04200-116">14</span></span> |
| <span data-ttu-id="04200-117">West US 2, Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="04200-117">West US 2, Southeast Asia</span></span> | <span data-ttu-id="04200-118">Linux</span><span class="sxs-lookup"><span data-stu-id="04200-118">Linux</span></span> | <span data-ttu-id="04200-119">2</span><span class="sxs-lookup"><span data-stu-id="04200-119">2</span></span> | <span data-ttu-id="04200-120">7</span><span class="sxs-lookup"><span data-stu-id="04200-120">7</span></span> |
| <span data-ttu-id="04200-121">Australia East, East US 2, Central US</span><span class="sxs-lookup"><span data-stu-id="04200-121">Australia East, East US 2, Central US</span></span> | <span data-ttu-id="04200-122">Linux</span><span class="sxs-lookup"><span data-stu-id="04200-122">Linux</span></span> | <span data-ttu-id="04200-123">1</span><span class="sxs-lookup"><span data-stu-id="04200-123">1</span></span> | <span data-ttu-id="04200-124">1.5</span><span class="sxs-lookup"><span data-stu-id="04200-124">1.5</span></span> |
| <span data-ttu-id="04200-125">West US, East US, West Europe, North Europe</span><span class="sxs-lookup"><span data-stu-id="04200-125">West US, East US, West Europe, North Europe</span></span> | <span data-ttu-id="04200-126">Windows</span><span class="sxs-lookup"><span data-stu-id="04200-126">Windows</span></span> | <span data-ttu-id="04200-127">4</span><span class="sxs-lookup"><span data-stu-id="04200-127">4</span></span> | <span data-ttu-id="04200-128">14</span><span class="sxs-lookup"><span data-stu-id="04200-128">14</span></span> |
| <span data-ttu-id="04200-129">West US 2, Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="04200-129">West US 2, Southeast Asia</span></span> | <span data-ttu-id="04200-130">Windows</span><span class="sxs-lookup"><span data-stu-id="04200-130">Windows</span></span> | <span data-ttu-id="04200-131">2</span><span class="sxs-lookup"><span data-stu-id="04200-131">2</span></span> | <span data-ttu-id="04200-132">3.5</span><span class="sxs-lookup"><span data-stu-id="04200-132">3.5</span></span> |

<span data-ttu-id="04200-133">Container instances created within these resource limits are subject to availability within the deployment region.</span><span class="sxs-lookup"><span data-stu-id="04200-133">Container instances created within these resource limits are subject to availability within the deployment region.</span></span> <span data-ttu-id="04200-134">When a region is under heavy load, you may experience a failure when deploying instances.</span><span class="sxs-lookup"><span data-stu-id="04200-134">When a region is under heavy load, you may experience a failure when deploying instances.</span></span> <span data-ttu-id="04200-135">To mitigate such a deployment failure, try deploying instances with lower CPU and memory settings, or try your deployment at a later time.</span><span class="sxs-lookup"><span data-stu-id="04200-135">To mitigate such a deployment failure, try deploying instances with lower CPU and memory settings, or try your deployment at a later time.</span></span>

<span data-ttu-id="04200-136">Let the team know of additional regions required or increased CPU/Memory limits at [aka.ms/aci/feedback](https://aka.ms/aci/feedback).</span><span class="sxs-lookup"><span data-stu-id="04200-136">Let the team know of additional regions required or increased CPU/Memory limits at [aka.ms/aci/feedback](https://aka.ms/aci/feedback).</span></span>

<span data-ttu-id="04200-137">For more information on troubleshooting container instance deployment, see [Troubleshoot deployment issues with Azure Container Instances](container-instances-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="04200-137">For more information on troubleshooting container instance deployment, see [Troubleshoot deployment issues with Azure Container Instances](container-instances-troubleshooting.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04200-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="04200-138">Next steps</span></span>

<span data-ttu-id="04200-139">Certain default limits and quotas can be increased.</span><span class="sxs-lookup"><span data-stu-id="04200-139">Certain default limits and quotas can be increased.</span></span> <span data-ttu-id="04200-140">To request an increase of one or more resources that support such an increase, please submit an [Azure support request][azure-support] (select "Quota" for **Issue type**).</span><span class="sxs-lookup"><span data-stu-id="04200-140">To request an increase of one or more resources that support such an increase, please submit an [Azure support request][azure-support] (select "Quota" for **Issue type**).</span></span>

<!-- LINKS - External -->
[azure-support]: https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest
