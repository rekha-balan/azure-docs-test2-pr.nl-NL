---
title: Differences and considerations for Managed Disks in Azure Stack | Microsoft Docs
description: Learn about differences and considerations when working with Managed Disks in Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.author: brenduns
ms.reviewer: jiahan
ms.openlocfilehash: 26f8880d01da00780317ee2a6f66ee5007576a50
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870235"
---
# <a name="azure-stack-managed-disks-differences-and-considerations"></a><span data-ttu-id="395ad-103">Azure Stack Managed Disks: Differences and considerations</span><span class="sxs-lookup"><span data-stu-id="395ad-103">Azure Stack Managed Disks: Differences and considerations</span></span>
<span data-ttu-id="395ad-104">This article summarizes the known differences between Azure Stack Managed Disks and Managed Disks for Azure.</span><span class="sxs-lookup"><span data-stu-id="395ad-104">This article summarizes the known differences between Azure Stack Managed Disks and Managed Disks for Azure.</span></span> <span data-ttu-id="395ad-105">To learn about high-level differences between Azure Stack and Azure, see the [Key considerations](azure-stack-considerations.md) article.</span><span class="sxs-lookup"><span data-stu-id="395ad-105">To learn about high-level differences between Azure Stack and Azure, see the [Key considerations](azure-stack-considerations.md) article.</span></span>

<span data-ttu-id="395ad-106">Managed Disks simplifies disk management for IaaS VMs by managing the [storage accounts](/azure/azure-stack/azure-stack-manage-storage-accounts) associated with the VM disks.</span><span class="sxs-lookup"><span data-stu-id="395ad-106">Managed Disks simplifies disk management for IaaS VMs by managing the [storage accounts](/azure/azure-stack/azure-stack-manage-storage-accounts) associated with the VM disks.</span></span>
  

## <a name="cheat-sheet-managed-disk-differences"></a><span data-ttu-id="395ad-107">Cheat sheet: Managed disk differences</span><span class="sxs-lookup"><span data-stu-id="395ad-107">Cheat sheet: Managed disk differences</span></span>

| <span data-ttu-id="395ad-108">Feature</span><span class="sxs-lookup"><span data-stu-id="395ad-108">Feature</span></span> | <span data-ttu-id="395ad-109">Azure (global)</span><span class="sxs-lookup"><span data-stu-id="395ad-109">Azure (global)</span></span> | <span data-ttu-id="395ad-110">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="395ad-110">Azure Stack</span></span> |
| --- | --- | --- |
|<span data-ttu-id="395ad-111">Encryption for Data at Rest</span><span class="sxs-lookup"><span data-stu-id="395ad-111">Encryption for Data at Rest</span></span> |<span data-ttu-id="395ad-112">Azure Storage Service Encryption (SSE), Azure Disk Encryption (ADE)</span><span class="sxs-lookup"><span data-stu-id="395ad-112">Azure Storage Service Encryption (SSE), Azure Disk Encryption (ADE)</span></span>     |<span data-ttu-id="395ad-113">BitLocker 128-bit AES encryption</span><span class="sxs-lookup"><span data-stu-id="395ad-113">BitLocker 128-bit AES encryption</span></span>      |
|<span data-ttu-id="395ad-114">Image</span><span class="sxs-lookup"><span data-stu-id="395ad-114">Image</span></span>          | <span data-ttu-id="395ad-115">Support managed custom image</span><span class="sxs-lookup"><span data-stu-id="395ad-115">Support managed custom image</span></span> |<span data-ttu-id="395ad-116">Not yet supported</span><span class="sxs-lookup"><span data-stu-id="395ad-116">Not yet supported</span></span>|
|<span data-ttu-id="395ad-117">Backup options</span><span class="sxs-lookup"><span data-stu-id="395ad-117">Backup options</span></span> |<span data-ttu-id="395ad-118">Support Azure Backup Service</span><span class="sxs-lookup"><span data-stu-id="395ad-118">Support Azure Backup Service</span></span> |<span data-ttu-id="395ad-119">Not yet supported</span><span class="sxs-lookup"><span data-stu-id="395ad-119">Not yet supported</span></span> |
|<span data-ttu-id="395ad-120">Disaster recovery options</span><span class="sxs-lookup"><span data-stu-id="395ad-120">Disaster recovery options</span></span> |<span data-ttu-id="395ad-121">Support Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="395ad-121">Support Azure Site Recovery</span></span> |<span data-ttu-id="395ad-122">Not yet supported</span><span class="sxs-lookup"><span data-stu-id="395ad-122">Not yet supported</span></span>|
|<span data-ttu-id="395ad-123">Disk types</span><span class="sxs-lookup"><span data-stu-id="395ad-123">Disk types</span></span>     |<span data-ttu-id="395ad-124">Premium SSD, Standard SSD (Preview), and Standard HDD</span><span class="sxs-lookup"><span data-stu-id="395ad-124">Premium SSD, Standard SSD (Preview), and Standard HDD</span></span> |<span data-ttu-id="395ad-125">Premium SSD, Standard HDD</span><span class="sxs-lookup"><span data-stu-id="395ad-125">Premium SSD, Standard HDD</span></span> |
|<span data-ttu-id="395ad-126">Premium disks</span><span class="sxs-lookup"><span data-stu-id="395ad-126">Premium disks</span></span>  |<span data-ttu-id="395ad-127">Fully supported</span><span class="sxs-lookup"><span data-stu-id="395ad-127">Fully supported</span></span> |<span data-ttu-id="395ad-128">Can be provisioned, but no performance limit or guarantee</span><span class="sxs-lookup"><span data-stu-id="395ad-128">Can be provisioned, but no performance limit or guarantee</span></span>  |
|<span data-ttu-id="395ad-129">Premium disks IOPs</span><span class="sxs-lookup"><span data-stu-id="395ad-129">Premium disks IOPs</span></span>  |<span data-ttu-id="395ad-130">Depends on disk size</span><span class="sxs-lookup"><span data-stu-id="395ad-130">Depends on disk size</span></span>  |<span data-ttu-id="395ad-131">2300 IOPs per disk</span><span class="sxs-lookup"><span data-stu-id="395ad-131">2300 IOPs per disk</span></span> |
|<span data-ttu-id="395ad-132">Premium disks throughput</span><span class="sxs-lookup"><span data-stu-id="395ad-132">Premium disks throughput</span></span> |<span data-ttu-id="395ad-133">Depends on disk size</span><span class="sxs-lookup"><span data-stu-id="395ad-133">Depends on disk size</span></span> |<span data-ttu-id="395ad-134">145 MB/second per disk</span><span class="sxs-lookup"><span data-stu-id="395ad-134">145 MB/second per disk</span></span> |
|<span data-ttu-id="395ad-135">Disk max size</span><span class="sxs-lookup"><span data-stu-id="395ad-135">Disk max size</span></span>  |<span data-ttu-id="395ad-136">4 TB</span><span class="sxs-lookup"><span data-stu-id="395ad-136">4 TB</span></span>       |<span data-ttu-id="395ad-137">1 TB</span><span class="sxs-lookup"><span data-stu-id="395ad-137">1 TB</span></span>       |
|<span data-ttu-id="395ad-138">Disks performance analytic</span><span class="sxs-lookup"><span data-stu-id="395ad-138">Disks performance analytic</span></span> |<span data-ttu-id="395ad-139">Aggregate metrics and per disk metrics supported</span><span class="sxs-lookup"><span data-stu-id="395ad-139">Aggregate metrics and per disk metrics supported</span></span> |<span data-ttu-id="395ad-140">Not yet supported</span><span class="sxs-lookup"><span data-stu-id="395ad-140">Not yet supported</span></span> |
|<span data-ttu-id="395ad-141">Migration</span><span class="sxs-lookup"><span data-stu-id="395ad-141">Migration</span></span>      |<span data-ttu-id="395ad-142">Provide tool to migrate from existing unmanaged Azure Resource Manager VMs without the need to recreate the VM</span><span class="sxs-lookup"><span data-stu-id="395ad-142">Provide tool to migrate from existing unmanaged Azure Resource Manager VMs without the need to recreate the VM</span></span>  |<span data-ttu-id="395ad-143">Not yet supported</span><span class="sxs-lookup"><span data-stu-id="395ad-143">Not yet supported</span></span> |


## <a name="metrics"></a><span data-ttu-id="395ad-144">Metrics</span><span class="sxs-lookup"><span data-stu-id="395ad-144">Metrics</span></span>
<span data-ttu-id="395ad-145">There are also differences with storage metrics:</span><span class="sxs-lookup"><span data-stu-id="395ad-145">There are also differences with storage metrics:</span></span>
- <span data-ttu-id="395ad-146">With Azure Stack, the transaction data in storage metrics doesn't differentiate internal or external network bandwidth.</span><span class="sxs-lookup"><span data-stu-id="395ad-146">With Azure Stack, the transaction data in storage metrics doesn't differentiate internal or external network bandwidth.</span></span>
- <span data-ttu-id="395ad-147">Azure Stack transaction data in storage metrics doesn't include virtual machine access to the mounted disks.</span><span class="sxs-lookup"><span data-stu-id="395ad-147">Azure Stack transaction data in storage metrics doesn't include virtual machine access to the mounted disks.</span></span>


## <a name="api-versions"></a><span data-ttu-id="395ad-148">API versions</span><span class="sxs-lookup"><span data-stu-id="395ad-148">API versions</span></span>
<span data-ttu-id="395ad-149">Azure Stack Managed Disks supports the following API versions:</span><span class="sxs-lookup"><span data-stu-id="395ad-149">Azure Stack Managed Disks supports the following API versions:</span></span>
- <span data-ttu-id="395ad-150">2017-03-30</span><span class="sxs-lookup"><span data-stu-id="395ad-150">2017-03-30</span></span>


## <a name="next-steps"></a><span data-ttu-id="395ad-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="395ad-151">Next steps</span></span>
[<span data-ttu-id="395ad-152">Learn about Azure Stack virtual machines</span><span class="sxs-lookup"><span data-stu-id="395ad-152">Learn about Azure Stack virtual machines</span></span>](azure-stack-compute-overview.md)
