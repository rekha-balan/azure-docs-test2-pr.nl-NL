---
title: Migrate a Classic VM to an ARM Managed Disk VM | Microsoft Docs
description: Migrate a single Azure VM from the classic deployment model to Managed Disks in the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 65583f425d08033fc79ece6fdcd2101e3202ee3b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825084"
---
# <a name="manually-migrate-a-classic-vm-to-a-new-arm-managed-disk-vm-from-the-vhd"></a><span data-ttu-id="a8b8a-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span><span class="sxs-lookup"><span data-stu-id="a8b8a-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span></span> 


<span data-ttu-id="a8b8a-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](managed-disks-overview.md) in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](managed-disks-overview.md) in the Resource Manager deployment model.</span></span>


## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="a8b8a-105">Plan for the migration to Managed Disks</span><span class="sxs-lookup"><span data-stu-id="a8b8a-105">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="a8b8a-106">This section helps you to make the best decision on VM and disk types.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-106">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="a8b8a-107">Location</span><span class="sxs-lookup"><span data-stu-id="a8b8a-107">Location</span></span>

<span data-ttu-id="a8b8a-108">Pick a location where Azure Managed Disks are available.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="a8b8a-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="a8b8a-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="a8b8a-111">VM sizes</span><span class="sxs-lookup"><span data-stu-id="a8b8a-111">VM sizes</span></span>

<span data-ttu-id="a8b8a-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="a8b8a-113">Review the VM sizes that are Premium Storage capable.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-113">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="a8b8a-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="a8b8a-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="a8b8a-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="a8b8a-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="a8b8a-117">Disk sizes</span><span class="sxs-lookup"><span data-stu-id="a8b8a-117">Disk sizes</span></span>

<span data-ttu-id="a8b8a-118">**Premium Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="a8b8a-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="a8b8a-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="a8b8a-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="a8b8a-121">Premium Disks Type</span><span class="sxs-lookup"><span data-stu-id="a8b8a-121">Premium Disks Type</span></span>  | <span data-ttu-id="a8b8a-122">P4</span><span class="sxs-lookup"><span data-stu-id="a8b8a-122">P4</span></span>    | <span data-ttu-id="a8b8a-123">P6</span><span class="sxs-lookup"><span data-stu-id="a8b8a-123">P6</span></span>    | <span data-ttu-id="a8b8a-124">P10</span><span class="sxs-lookup"><span data-stu-id="a8b8a-124">P10</span></span>   | <span data-ttu-id="a8b8a-125">P20</span><span class="sxs-lookup"><span data-stu-id="a8b8a-125">P20</span></span>   | <span data-ttu-id="a8b8a-126">P30</span><span class="sxs-lookup"><span data-stu-id="a8b8a-126">P30</span></span>   | <span data-ttu-id="a8b8a-127">P40</span><span class="sxs-lookup"><span data-stu-id="a8b8a-127">P40</span></span>   | <span data-ttu-id="a8b8a-128">P50</span><span class="sxs-lookup"><span data-stu-id="a8b8a-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="a8b8a-129">Disk size</span><span class="sxs-lookup"><span data-stu-id="a8b8a-129">Disk size</span></span>           | <span data-ttu-id="a8b8a-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="a8b8a-130">128 GB</span></span>| <span data-ttu-id="a8b8a-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="a8b8a-131">512 GB</span></span>| <span data-ttu-id="a8b8a-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="a8b8a-132">128 GB</span></span>| <span data-ttu-id="a8b8a-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="a8b8a-133">512 GB</span></span>            | <span data-ttu-id="a8b8a-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="a8b8a-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="a8b8a-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="a8b8a-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="a8b8a-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="a8b8a-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="a8b8a-137">IOPS per disk</span><span class="sxs-lookup"><span data-stu-id="a8b8a-137">IOPS per disk</span></span>       | <span data-ttu-id="a8b8a-138">120</span><span class="sxs-lookup"><span data-stu-id="a8b8a-138">120</span></span>   | <span data-ttu-id="a8b8a-139">240</span><span class="sxs-lookup"><span data-stu-id="a8b8a-139">240</span></span>   | <span data-ttu-id="a8b8a-140">500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-140">500</span></span>   | <span data-ttu-id="a8b8a-141">2300</span><span class="sxs-lookup"><span data-stu-id="a8b8a-141">2300</span></span>              | <span data-ttu-id="a8b8a-142">5000</span><span class="sxs-lookup"><span data-stu-id="a8b8a-142">5000</span></span>              | <span data-ttu-id="a8b8a-143">7500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-143">7500</span></span>              | <span data-ttu-id="a8b8a-144">7500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-144">7500</span></span>              | 
| <span data-ttu-id="a8b8a-145">Throughput per disk</span><span class="sxs-lookup"><span data-stu-id="a8b8a-145">Throughput per disk</span></span> | <span data-ttu-id="a8b8a-146">25 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-146">25 MB per second</span></span>  | <span data-ttu-id="a8b8a-147">50 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-147">50 MB per second</span></span>  | <span data-ttu-id="a8b8a-148">100 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-148">100 MB per second</span></span> | <span data-ttu-id="a8b8a-149">150 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-149">150 MB per second</span></span> | <span data-ttu-id="a8b8a-150">200 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-150">200 MB per second</span></span> | <span data-ttu-id="a8b8a-151">250 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-151">250 MB per second</span></span> | <span data-ttu-id="a8b8a-152">250 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-152">250 MB per second</span></span> | 

<span data-ttu-id="a8b8a-153">**Standard Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="a8b8a-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="a8b8a-154">There are seven types of Standard Managed disks that can be used with your VM.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="a8b8a-155">Each of them have different capacity but have same IOPS and throughput limits.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="a8b8a-156">Choose the type of Standard Managed disks based on the capacity needs of your application.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-156">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="a8b8a-157">Standard Disk Type</span><span class="sxs-lookup"><span data-stu-id="a8b8a-157">Standard Disk Type</span></span>  | <span data-ttu-id="a8b8a-158">S4</span><span class="sxs-lookup"><span data-stu-id="a8b8a-158">S4</span></span>               | <span data-ttu-id="a8b8a-159">S6</span><span class="sxs-lookup"><span data-stu-id="a8b8a-159">S6</span></span>               | <span data-ttu-id="a8b8a-160">S10</span><span class="sxs-lookup"><span data-stu-id="a8b8a-160">S10</span></span>              | <span data-ttu-id="a8b8a-161">S20</span><span class="sxs-lookup"><span data-stu-id="a8b8a-161">S20</span></span>              | <span data-ttu-id="a8b8a-162">S30</span><span class="sxs-lookup"><span data-stu-id="a8b8a-162">S30</span></span>              | <span data-ttu-id="a8b8a-163">S40</span><span class="sxs-lookup"><span data-stu-id="a8b8a-163">S40</span></span>              | <span data-ttu-id="a8b8a-164">S50</span><span class="sxs-lookup"><span data-stu-id="a8b8a-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="a8b8a-165">Disk size</span><span class="sxs-lookup"><span data-stu-id="a8b8a-165">Disk size</span></span>           | <span data-ttu-id="a8b8a-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="a8b8a-166">30 GB</span></span>            | <span data-ttu-id="a8b8a-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="a8b8a-167">64 GB</span></span>            | <span data-ttu-id="a8b8a-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="a8b8a-168">128 GB</span></span>           | <span data-ttu-id="a8b8a-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="a8b8a-169">512 GB</span></span>           | <span data-ttu-id="a8b8a-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="a8b8a-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="a8b8a-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="a8b8a-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="a8b8a-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="a8b8a-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="a8b8a-173">IOPS per disk</span><span class="sxs-lookup"><span data-stu-id="a8b8a-173">IOPS per disk</span></span>       | <span data-ttu-id="a8b8a-174">500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-174">500</span></span>              | <span data-ttu-id="a8b8a-175">500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-175">500</span></span>              | <span data-ttu-id="a8b8a-176">500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-176">500</span></span>              | <span data-ttu-id="a8b8a-177">500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-177">500</span></span>              | <span data-ttu-id="a8b8a-178">500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-178">500</span></span>              | <span data-ttu-id="a8b8a-179">500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-179">500</span></span>             | <span data-ttu-id="a8b8a-180">500</span><span class="sxs-lookup"><span data-stu-id="a8b8a-180">500</span></span>              | 
| <span data-ttu-id="a8b8a-181">Throughput per disk</span><span class="sxs-lookup"><span data-stu-id="a8b8a-181">Throughput per disk</span></span> | <span data-ttu-id="a8b8a-182">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-182">60 MB per second</span></span> | <span data-ttu-id="a8b8a-183">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-183">60 MB per second</span></span> | <span data-ttu-id="a8b8a-184">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-184">60 MB per second</span></span> | <span data-ttu-id="a8b8a-185">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-185">60 MB per second</span></span> | <span data-ttu-id="a8b8a-186">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-186">60 MB per second</span></span> | <span data-ttu-id="a8b8a-187">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-187">60 MB per second</span></span> | <span data-ttu-id="a8b8a-188">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="a8b8a-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="a8b8a-189">Disk caching policy</span><span class="sxs-lookup"><span data-stu-id="a8b8a-189">Disk caching policy</span></span> 

<span data-ttu-id="a8b8a-190">**Premium Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="a8b8a-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="a8b8a-191">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-191">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="a8b8a-192">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-192">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="a8b8a-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="a8b8a-194">Pricing</span><span class="sxs-lookup"><span data-stu-id="a8b8a-194">Pricing</span></span>

<span data-ttu-id="a8b8a-195">Review the [pricing for Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="a8b8a-195">Review the [pricing for Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <span data-ttu-id="a8b8a-196">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-196">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="a8b8a-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="a8b8a-198">Checklist</span><span class="sxs-lookup"><span data-stu-id="a8b8a-198">Checklist</span></span>

1.  <span data-ttu-id="a8b8a-199">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-199">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span></span>

2.  <span data-ttu-id="a8b8a-200">Decide the new VM series you will be using.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-200">Decide the new VM series you will be using.</span></span> <span data-ttu-id="a8b8a-201">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-201">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span></span>

3.  <span data-ttu-id="a8b8a-202">Decide the exact VM size you will use which are available in the region you are migrating to.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-202">Decide the exact VM size you will use which are available in the region you are migrating to.</span></span> <span data-ttu-id="a8b8a-203">VM size needs to be large enough to support the number of data disks you have.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-203">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="a8b8a-204">For example, if you have four data disks, the VM must have two or more cores.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-204">For example, if you have four data disks, the VM must have two or more cores.</span></span> <span data-ttu-id="a8b8a-205">Also, consider processing power, memory and network bandwidth needs.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="a8b8a-206">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-206">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="a8b8a-207">Prepare your application for downtime.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-207">Prepare your application for downtime.</span></span> <span data-ttu-id="a8b8a-208">To do a clean migration, you have to stop all the processing in the current system.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-208">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="a8b8a-209">Only then you can get it to consistent state which you can migrate to the new platform.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-209">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="a8b8a-210">Downtime duration depends on the amount of data in the disks to migrate.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-210">Downtime duration depends on the amount of data in the disks to migrate.</span></span>


## <a name="migrate-the-vm"></a><span data-ttu-id="a8b8a-211">Migrate the VM</span><span class="sxs-lookup"><span data-stu-id="a8b8a-211">Migrate the VM</span></span>

<span data-ttu-id="a8b8a-212">Prepare your application for downtime.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-212">Prepare your application for downtime.</span></span> <span data-ttu-id="a8b8a-213">To do a clean migration, you have to stop all the processing in the current system.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-213">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="a8b8a-214">Only then you can get it to consistent state which you can migrate to the new platform.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-214">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="a8b8a-215">Downtime duration depends the amount of data in the disks to migrate.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-215">Downtime duration depends the amount of data in the disks to migrate.</span></span>

<span data-ttu-id="a8b8a-216">This part requires the Azure PowerShell module version 6.0.0 or later.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-216">This part requires the Azure PowerShell module version 6.0.0 or later.</span></span> <span data-ttu-id="a8b8a-217">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-217">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="a8b8a-218">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a8b8a-218">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="a8b8a-219">You also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-219">You also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>


1.  <span data-ttu-id="a8b8a-220">First, set the common parameters:</span><span class="sxs-lookup"><span data-stu-id="a8b8a-220">First, set the common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="a8b8a-221">Create a managed OS disk using the VHD from the classic VM.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-221">Create a managed OS disk using the VHD from the classic VM.</span></span>

    <span data-ttu-id="a8b8a-222">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-222">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span></span> <span data-ttu-id="a8b8a-223">Also, enter **-AccountType** as **Premium_LRS** or **Standard_LRS** based on type of disks (Premium or Standard) you are migrating to.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-223">Also, enter **-AccountType** as **Premium_LRS** or **Standard_LRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType Premium_LRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="a8b8a-224">Attach the OS disk to the new VM.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-224">Attach the OS disk to the new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType Premium_LRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="a8b8a-225">Create a managed data disk from the data VHD file and add it to the new VM.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-225">Create a managed data disk from the data VHD file and add it to the new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType Premium_LRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="a8b8a-226">Create the new VM by setting public IP, Virtual Network and NIC.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-226">Create the new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="a8b8a-227">There may be additional steps necessary to support your application that is not be covered by this guide.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-227">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a8b8a-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8b8a-228">Next steps</span></span>

- <span data-ttu-id="a8b8a-229">Connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a8b8a-229">Connect to the virtual machine.</span></span> <span data-ttu-id="a8b8a-230">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a8b8a-230">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

