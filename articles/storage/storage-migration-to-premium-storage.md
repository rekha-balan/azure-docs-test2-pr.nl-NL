---
title: Migrating VMs to Azure Premium Storage | Microsoft Docs
description: Migrate your existing VMs to Azure Premium Storage. Premium Storage offers high-performance, low-latency disk support for I/O-intensive workloads running on Azure Virtual Machines.
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: yuemlu
ms.openlocfilehash: 8a4c785b07c2e9fdce1973b7cbeaac099226025e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553247"
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="e394c-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span><span class="sxs-lookup"><span data-stu-id="e394c-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="e394c-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span><span class="sxs-lookup"><span data-stu-id="e394c-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="e394c-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span><span class="sxs-lookup"><span data-stu-id="e394c-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="e394c-107">Managed Disks handle the underlying storage accounts so you don't have to.</span><span class="sxs-lookup"><span data-stu-id="e394c-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="e394c-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e394c-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="e394c-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span><span class="sxs-lookup"><span data-stu-id="e394c-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="e394c-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="e394c-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="e394c-112">The guide addresses three of the key components in this process:</span><span class="sxs-lookup"><span data-stu-id="e394c-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="e394c-113">Plan for the Migration to Premium Storage</span><span class="sxs-lookup"><span data-stu-id="e394c-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="e394c-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span><span class="sxs-lookup"><span data-stu-id="e394c-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="e394c-115">Create Azure Virtual Machine using Premium Storage</span><span class="sxs-lookup"><span data-stu-id="e394c-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="e394c-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="e394c-117">This guide covers steps for both two scenarios.</span><span class="sxs-lookup"><span data-stu-id="e394c-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="e394c-118">Follow the steps specified in the relevant section depending on your scenario.</span><span class="sxs-lookup"><span data-stu-id="e394c-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="e394c-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e394c-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="e394c-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span><span class="sxs-lookup"><span data-stu-id="e394c-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="e394c-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span><span class="sxs-lookup"><span data-stu-id="e394c-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="e394c-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span><span class="sxs-lookup"><span data-stu-id="e394c-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="e394c-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span><span class="sxs-lookup"><span data-stu-id="e394c-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="e394c-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span><span class="sxs-lookup"><span data-stu-id="e394c-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <a name="plan-the-migration-to-premium-storage"></a><span data-ttu-id="e394c-125">Plan for the migration to Premium Storage</span><span class="sxs-lookup"><span data-stu-id="e394c-125">Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="e394c-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span><span class="sxs-lookup"><span data-stu-id="e394c-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e394c-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e394c-127">Prerequisites</span></span>
* <span data-ttu-id="e394c-128">You will need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e394c-128">You will need an Azure subscription.</span></span> <span data-ttu-id="e394c-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span><span class="sxs-lookup"><span data-stu-id="e394c-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="e394c-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="e394c-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="e394c-131">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span><span class="sxs-lookup"><span data-stu-id="e394c-131">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>
* <span data-ttu-id="e394c-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span><span class="sxs-lookup"><span data-stu-id="e394c-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="e394c-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span><span class="sxs-lookup"><span data-stu-id="e394c-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="e394c-134">Premium storage disks will be available with more VM types in the future.</span><span class="sxs-lookup"><span data-stu-id="e394c-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="e394c-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="e394c-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="e394c-136">Considerations</span><span class="sxs-lookup"><span data-stu-id="e394c-136">Considerations</span></span>
<span data-ttu-id="e394c-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 64 TB of storage per VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 64 TB of storage per VM.</span></span> <span data-ttu-id="e394c-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span><span class="sxs-lookup"><span data-stu-id="e394c-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="e394c-139">You have options in a variety of VMs and Disks.</span><span class="sxs-lookup"><span data-stu-id="e394c-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="e394c-140">This section is to help you to find an option that best suits your workload.</span><span class="sxs-lookup"><span data-stu-id="e394c-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="e394c-141">VM sizes</span><span class="sxs-lookup"><span data-stu-id="e394c-141">VM sizes</span></span>
<span data-ttu-id="e394c-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e394c-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e394c-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span><span class="sxs-lookup"><span data-stu-id="e394c-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="e394c-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span><span class="sxs-lookup"><span data-stu-id="e394c-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="e394c-145">Disk sizes</span><span class="sxs-lookup"><span data-stu-id="e394c-145">Disk sizes</span></span>
<span data-ttu-id="e394c-146">There are three types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span><span class="sxs-lookup"><span data-stu-id="e394c-146">There are three types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="e394c-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span><span class="sxs-lookup"><span data-stu-id="e394c-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="e394c-148">Premium Storage Disk Type</span><span class="sxs-lookup"><span data-stu-id="e394c-148">Premium Storage Disk Type</span></span> | <span data-ttu-id="e394c-149">P10</span><span class="sxs-lookup"><span data-stu-id="e394c-149">P10</span></span> | <span data-ttu-id="e394c-150">P20</span><span class="sxs-lookup"><span data-stu-id="e394c-150">P20</span></span> | <span data-ttu-id="e394c-151">P30</span><span class="sxs-lookup"><span data-stu-id="e394c-151">P30</span></span> |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="e394c-152">Disk size</span><span class="sxs-lookup"><span data-stu-id="e394c-152">Disk size</span></span> |<span data-ttu-id="e394c-153">128 GB</span><span class="sxs-lookup"><span data-stu-id="e394c-153">128 GB</span></span> |<span data-ttu-id="e394c-154">512 GB</span><span class="sxs-lookup"><span data-stu-id="e394c-154">512 GB</span></span> |<span data-ttu-id="e394c-155">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="e394c-155">1024 GB (1 TB)</span></span> |
| <span data-ttu-id="e394c-156">IOPS per disk</span><span class="sxs-lookup"><span data-stu-id="e394c-156">IOPS per disk</span></span> |<span data-ttu-id="e394c-157">500</span><span class="sxs-lookup"><span data-stu-id="e394c-157">500</span></span> |<span data-ttu-id="e394c-158">2300</span><span class="sxs-lookup"><span data-stu-id="e394c-158">2300</span></span> |<span data-ttu-id="e394c-159">5000</span><span class="sxs-lookup"><span data-stu-id="e394c-159">5000</span></span> |
| <span data-ttu-id="e394c-160">Throughput per disk</span><span class="sxs-lookup"><span data-stu-id="e394c-160">Throughput per disk</span></span> |<span data-ttu-id="e394c-161">100 MB per second</span><span class="sxs-lookup"><span data-stu-id="e394c-161">100 MB per second</span></span> |<span data-ttu-id="e394c-162">150 MB per second</span><span class="sxs-lookup"><span data-stu-id="e394c-162">150 MB per second</span></span> |<span data-ttu-id="e394c-163">200 MB per second</span><span class="sxs-lookup"><span data-stu-id="e394c-163">200 MB per second</span></span> |

<span data-ttu-id="e394c-164">Depending on your workload, determine if additional data disks are necessary for your VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-164">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="e394c-165">You can attach several persistent data disks to your VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-165">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="e394c-166">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span><span class="sxs-lookup"><span data-stu-id="e394c-166">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="e394c-167">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span><span class="sxs-lookup"><span data-stu-id="e394c-167">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="e394c-168">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span><span class="sxs-lookup"><span data-stu-id="e394c-168">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="e394c-169">For Linux VMs you can use the *mdadm* utility to achieve the same.</span><span class="sxs-lookup"><span data-stu-id="e394c-169">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="e394c-170">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span><span class="sxs-lookup"><span data-stu-id="e394c-170">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="e394c-171">Storage account scalability targets</span><span class="sxs-lookup"><span data-stu-id="e394c-171">Storage account scalability targets</span></span>
<span data-ttu-id="e394c-172">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="e394c-172">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="e394c-173">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span><span class="sxs-lookup"><span data-stu-id="e394c-173">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="e394c-174">Total Account Capacity</span><span class="sxs-lookup"><span data-stu-id="e394c-174">Total Account Capacity</span></span> | <span data-ttu-id="e394c-175">Total Bandwidth for a Locally Redundant Storage Account</span><span class="sxs-lookup"><span data-stu-id="e394c-175">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="e394c-176">Disk capacity: 35TB</span><span class="sxs-lookup"><span data-stu-id="e394c-176">Disk capacity: 35TB</span></span><br /><span data-ttu-id="e394c-177">Snapshot capacity: 10 TB</span><span class="sxs-lookup"><span data-stu-id="e394c-177">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="e394c-178">Up to 50 gigabits per second for Inbound + Outbound</span><span class="sxs-lookup"><span data-stu-id="e394c-178">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="e394c-179">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="e394c-179">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="e394c-180">Disk caching policy</span><span class="sxs-lookup"><span data-stu-id="e394c-180">Disk caching policy</span></span>
<span data-ttu-id="e394c-181">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-181">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="e394c-182">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span><span class="sxs-lookup"><span data-stu-id="e394c-182">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="e394c-183">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span><span class="sxs-lookup"><span data-stu-id="e394c-183">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="e394c-184">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e394c-184">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="e394c-185">Location</span><span class="sxs-lookup"><span data-stu-id="e394c-185">Location</span></span>
<span data-ttu-id="e394c-186">Pick a location where Azure Premium Storage is available.</span><span class="sxs-lookup"><span data-stu-id="e394c-186">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="e394c-187">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span><span class="sxs-lookup"><span data-stu-id="e394c-187">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="e394c-188">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span><span class="sxs-lookup"><span data-stu-id="e394c-188">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="e394c-189">Other Azure VM configuration settings</span><span class="sxs-lookup"><span data-stu-id="e394c-189">Other Azure VM configuration settings</span></span>
<span data-ttu-id="e394c-190">When creating an Azure VM, you will be asked to configure certain VM settings.</span><span class="sxs-lookup"><span data-stu-id="e394c-190">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="e394c-191">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span><span class="sxs-lookup"><span data-stu-id="e394c-191">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="e394c-192">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span><span class="sxs-lookup"><span data-stu-id="e394c-192">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="e394c-193">Optimization</span><span class="sxs-lookup"><span data-stu-id="e394c-193">Optimization</span></span>
<span data-ttu-id="e394c-194">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-194">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="e394c-195">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span><span class="sxs-lookup"><span data-stu-id="e394c-195">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a><span data-ttu-id="e394c-196">Prepare and copy virtual hard disks (VHDs) to Premium Storage</span><span class="sxs-lookup"><span data-stu-id="e394c-196">Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="e394c-197">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-197">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="e394c-198">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span><span class="sxs-lookup"><span data-stu-id="e394c-198">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="e394c-199">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span><span class="sxs-lookup"><span data-stu-id="e394c-199">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="e394c-200">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e394c-200">Prerequisites</span></span>
<span data-ttu-id="e394c-201">To prepare the VHDs for migration, you'll need:</span><span class="sxs-lookup"><span data-stu-id="e394c-201">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="e394c-202">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-202">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="e394c-203">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span><span class="sxs-lookup"><span data-stu-id="e394c-203">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="e394c-204">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span><span class="sxs-lookup"><span data-stu-id="e394c-204">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="e394c-205">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e394c-205">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="e394c-206">A tool to upload the VHD file to the Storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-206">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="e394c-207">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="e394c-207">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="e394c-208">This guide describes copying your VHD using the AzCopy tool.</span><span class="sxs-lookup"><span data-stu-id="e394c-208">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="e394c-209">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-209">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="e394c-210">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span><span class="sxs-lookup"><span data-stu-id="e394c-210">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="e394c-211">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="e394c-211">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="e394c-212">You can use the Azure Import/Export service to copy data to a standard storage account only.</span><span class="sxs-lookup"><span data-stu-id="e394c-212">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="e394c-213">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-213">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="e394c-214">Note that Microsoft Azure only supports fixed size VHD files.</span><span class="sxs-lookup"><span data-stu-id="e394c-214">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="e394c-215">VHDX files or dynamic VHDs are not supported.</span><span class="sxs-lookup"><span data-stu-id="e394c-215">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="e394c-216">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e394c-216">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <a name="scenario1"></a><span data-ttu-id="e394c-217">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span><span class="sxs-lookup"><span data-stu-id="e394c-217">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="e394c-218">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e394c-218">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="e394c-219">The VM needs to be completely down to migrate a clean state.</span><span class="sxs-lookup"><span data-stu-id="e394c-219">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="e394c-220">There will be a downtime until the migration completes.</span><span class="sxs-lookup"><span data-stu-id="e394c-220">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="e394c-221">Step 1.</span><span class="sxs-lookup"><span data-stu-id="e394c-221">Step 1.</span></span> <span data-ttu-id="e394c-222">Prepare VHDs for migration</span><span class="sxs-lookup"><span data-stu-id="e394c-222">Prepare VHDs for migration</span></span>
<span data-ttu-id="e394c-223">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span><span class="sxs-lookup"><span data-stu-id="e394c-223">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="e394c-224">A generalized operating system image</span><span class="sxs-lookup"><span data-stu-id="e394c-224">A generalized operating system image</span></span>
* <span data-ttu-id="e394c-225">A unique operating system disk</span><span class="sxs-lookup"><span data-stu-id="e394c-225">A unique operating system disk</span></span>
* <span data-ttu-id="e394c-226">A data disk</span><span class="sxs-lookup"><span data-stu-id="e394c-226">A data disk</span></span>

<span data-ttu-id="e394c-227">Below we walk through these 3 scenarios for preparing your VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-227">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="e394c-228">Use a generalized Operating System VHD to create multiple VM instances</span><span class="sxs-lookup"><span data-stu-id="e394c-228">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="e394c-229">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span><span class="sxs-lookup"><span data-stu-id="e394c-229">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="e394c-230">This applies to a VHD that is on-premises or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="e394c-230">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="e394c-231">Sysprep removes any machine-specific information from the VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-231">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e394c-232">Take a snapshot or backup your VM before generalizing it.</span><span class="sxs-lookup"><span data-stu-id="e394c-232">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="e394c-233">Running sysprep will stop and deallocate the VM instance.</span><span class="sxs-lookup"><span data-stu-id="e394c-233">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="e394c-234">Follow steps below to sysprep a Windows OS VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-234">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="e394c-235">Note that running the Sysprep command will require you to shut down the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e394c-235">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="e394c-236">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="e394c-236">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="e394c-237">Open a Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e394c-237">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="e394c-238">Enter the following command to open Sysprep:</span><span class="sxs-lookup"><span data-stu-id="e394c-238">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="e394c-239">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="e394c-239">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="e394c-240">Sysprep will generalize the operating system and shut down the system.</span><span class="sxs-lookup"><span data-stu-id="e394c-240">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="e394c-241">For an Ubuntu VM, use virt-sysprep to achieve the same.</span><span class="sxs-lookup"><span data-stu-id="e394c-241">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="e394c-242">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span><span class="sxs-lookup"><span data-stu-id="e394c-242">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="e394c-243">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span><span class="sxs-lookup"><span data-stu-id="e394c-243">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="e394c-244">Use a unique Operating System VHD to create a single VM instance</span><span class="sxs-lookup"><span data-stu-id="e394c-244">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="e394c-245">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-245">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="e394c-246">A non-generalized VHD can be used to create a unique Azure VM instance.</span><span class="sxs-lookup"><span data-stu-id="e394c-246">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="e394c-247">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span><span class="sxs-lookup"><span data-stu-id="e394c-247">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="e394c-248">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-248">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="e394c-249">Register data disk VHD</span><span class="sxs-lookup"><span data-stu-id="e394c-249">Register data disk VHD</span></span>
<span data-ttu-id="e394c-250">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span><span class="sxs-lookup"><span data-stu-id="e394c-250">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="e394c-251">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span><span class="sxs-lookup"><span data-stu-id="e394c-251">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="e394c-252">Step 2.</span><span class="sxs-lookup"><span data-stu-id="e394c-252">Step 2.</span></span> <span data-ttu-id="e394c-253">Create the destination for your VHD</span><span class="sxs-lookup"><span data-stu-id="e394c-253">Create the destination for your VHD</span></span>
<span data-ttu-id="e394c-254">Create a storage account for maintaining your VHDs.</span><span class="sxs-lookup"><span data-stu-id="e394c-254">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="e394c-255">Consider the following points when planning where to store your VHDs:</span><span class="sxs-lookup"><span data-stu-id="e394c-255">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="e394c-256">The target Premium storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-256">The target Premium storage account.</span></span>
* <span data-ttu-id="e394c-257">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span><span class="sxs-lookup"><span data-stu-id="e394c-257">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="e394c-258">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span><span class="sxs-lookup"><span data-stu-id="e394c-258">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="e394c-259">Copy and save the storage account key of the destination storage account for the next stage.</span><span class="sxs-lookup"><span data-stu-id="e394c-259">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="e394c-260">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-260">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="copy-vhd-with-azcopy-or-powershell"></a><span data-ttu-id="e394c-261">Step 3.</span><span class="sxs-lookup"><span data-stu-id="e394c-261">Step 3.</span></span> <span data-ttu-id="e394c-262">Copy VHD with AzCopy or PowerShell</span><span class="sxs-lookup"><span data-stu-id="e394c-262">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="e394c-263">You will need to find your container path and storage account key to process either of these two options.</span><span class="sxs-lookup"><span data-stu-id="e394c-263">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="e394c-264">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span><span class="sxs-lookup"><span data-stu-id="e394c-264">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="e394c-265">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span><span class="sxs-lookup"><span data-stu-id="e394c-265">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="e394c-266">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span><span class="sxs-lookup"><span data-stu-id="e394c-266">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="e394c-267">Using AzCopy, you can easily upload the VHD over the Internet.</span><span class="sxs-lookup"><span data-stu-id="e394c-267">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="e394c-268">Depending on the size of the VHDs, this may take time.</span><span class="sxs-lookup"><span data-stu-id="e394c-268">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="e394c-269">Remember to check the storage account ingress/egress limits when using this option.</span><span class="sxs-lookup"><span data-stu-id="e394c-269">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="e394c-270">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span><span class="sxs-lookup"><span data-stu-id="e394c-270">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="e394c-271">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="e394c-271">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="e394c-272">Open Azure PowerShell and go to the folder where AzCopy is installed.</span><span class="sxs-lookup"><span data-stu-id="e394c-272">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="e394c-273">Use the following command to copy the VHD file from "Source" to "Destination".</span><span class="sxs-lookup"><span data-stu-id="e394c-273">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="e394c-274">Example:</span><span class="sxs-lookup"><span data-stu-id="e394c-274">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="e394c-275">Here are descriptions of the parameters used in the AzCopy command:</span><span class="sxs-lookup"><span data-stu-id="e394c-275">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="e394c-276">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-276">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="e394c-277">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-277">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="e394c-278">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span><span class="sxs-lookup"><span data-stu-id="e394c-278">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="e394c-279">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-279">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="e394c-280">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span><span class="sxs-lookup"><span data-stu-id="e394c-280">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="e394c-281">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="e394c-281">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="e394c-282">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span><span class="sxs-lookup"><span data-stu-id="e394c-282">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="e394c-283">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span><span class="sxs-lookup"><span data-stu-id="e394c-283">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="e394c-284">Use the following command on Azure PowerShell to copy VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-284">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="e394c-285">Replace the values in <> with corresponding values from your source and destination storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-285">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="e394c-286">To use this command, you must have a container called vhds in your destination storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-286">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="e394c-287">If the container doesn't exist, create one before running the command.</span><span class="sxs-lookup"><span data-stu-id="e394c-287">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="e394c-288">Example:</span><span class="sxs-lookup"><span data-stu-id="e394c-288">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a><span data-ttu-id="e394c-289">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span><span class="sxs-lookup"><span data-stu-id="e394c-289">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="e394c-290">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span><span class="sxs-lookup"><span data-stu-id="e394c-290">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="e394c-291">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-291">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="e394c-292">Step 1.</span><span class="sxs-lookup"><span data-stu-id="e394c-292">Step 1.</span></span> <span data-ttu-id="e394c-293">Export VHD to a local directory</span><span class="sxs-lookup"><span data-stu-id="e394c-293">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="e394c-294">Copy a VHD from AWS</span><span class="sxs-lookup"><span data-stu-id="e394c-294">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="e394c-295">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="e394c-295">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="e394c-296">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span><span class="sxs-lookup"><span data-stu-id="e394c-296">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="e394c-297">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span><span class="sxs-lookup"><span data-stu-id="e394c-297">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="e394c-298">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span><span class="sxs-lookup"><span data-stu-id="e394c-298">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="e394c-299">Download the VHD file from the S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="e394c-299">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="e394c-300">Select the VHD file, then **Actions** > **Download**.</span><span class="sxs-lookup"><span data-stu-id="e394c-300">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="e394c-301">Copy a VHD from other non-Azure cloud</span><span class="sxs-lookup"><span data-stu-id="e394c-301">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="e394c-302">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span><span class="sxs-lookup"><span data-stu-id="e394c-302">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="e394c-303">Copy the complete source path of the local directory where VHD is stored.</span><span class="sxs-lookup"><span data-stu-id="e394c-303">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premise"></a><span data-ttu-id="e394c-304">Copy a VHD from on-premise</span><span class="sxs-lookup"><span data-stu-id="e394c-304">Copy a VHD from on-premise</span></span>
<span data-ttu-id="e394c-305">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span><span class="sxs-lookup"><span data-stu-id="e394c-305">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="e394c-306">The source path could be a server location or file share.</span><span class="sxs-lookup"><span data-stu-id="e394c-306">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="e394c-307">Step 2.</span><span class="sxs-lookup"><span data-stu-id="e394c-307">Step 2.</span></span> <span data-ttu-id="e394c-308">Create the destination for your VHD</span><span class="sxs-lookup"><span data-stu-id="e394c-308">Create the destination for your VHD</span></span>
<span data-ttu-id="e394c-309">Create a storage account for maintaining your VHDs.</span><span class="sxs-lookup"><span data-stu-id="e394c-309">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="e394c-310">Consider the following points when planning where to store your VHDs:</span><span class="sxs-lookup"><span data-stu-id="e394c-310">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="e394c-311">The target storage account could be standard or premium storage depending on your application requirement.</span><span class="sxs-lookup"><span data-stu-id="e394c-311">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="e394c-312">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span><span class="sxs-lookup"><span data-stu-id="e394c-312">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="e394c-313">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span><span class="sxs-lookup"><span data-stu-id="e394c-313">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="e394c-314">Copy and save the storage account key of the destination storage account for the next stage.</span><span class="sxs-lookup"><span data-stu-id="e394c-314">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="e394c-315">We strongly recommend you moving all data for production workload to use premium storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-315">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="e394c-316">Step 3.</span><span class="sxs-lookup"><span data-stu-id="e394c-316">Step 3.</span></span> <span data-ttu-id="e394c-317">Upload the VHD to Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e394c-317">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="e394c-318">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e394c-318">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="e394c-319">Both options are provided here:</span><span class="sxs-lookup"><span data-stu-id="e394c-319">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="e394c-320">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span><span class="sxs-lookup"><span data-stu-id="e394c-320">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="e394c-321">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="e394c-321">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="e394c-322">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="e394c-322">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="e394c-323">Option 2: Using AzCopy to upload the .vhd file</span><span class="sxs-lookup"><span data-stu-id="e394c-323">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="e394c-324">Using AzCopy, you can easily upload the VHD over the Internet.</span><span class="sxs-lookup"><span data-stu-id="e394c-324">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="e394c-325">Depending on the size of the VHDs, this may take time.</span><span class="sxs-lookup"><span data-stu-id="e394c-325">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="e394c-326">Remember to check the storage account ingress/egress limits when using this option.</span><span class="sxs-lookup"><span data-stu-id="e394c-326">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="e394c-327">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span><span class="sxs-lookup"><span data-stu-id="e394c-327">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="e394c-328">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="e394c-328">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="e394c-329">Open Azure PowerShell and go to the folder where AzCopy is installed.</span><span class="sxs-lookup"><span data-stu-id="e394c-329">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="e394c-330">Use the following command to copy the VHD file from "Source" to "Destination".</span><span class="sxs-lookup"><span data-stu-id="e394c-330">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="e394c-331">Example:</span><span class="sxs-lookup"><span data-stu-id="e394c-331">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="e394c-332">Here are descriptions of the parameters used in the AzCopy command:</span><span class="sxs-lookup"><span data-stu-id="e394c-332">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="e394c-333">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span><span class="sxs-lookup"><span data-stu-id="e394c-333">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="e394c-334">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-334">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="e394c-335">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span><span class="sxs-lookup"><span data-stu-id="e394c-335">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="e394c-336">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-336">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="e394c-337">**/BlobType: page:** Specifies that the destination is a page blob.</span><span class="sxs-lookup"><span data-stu-id="e394c-337">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="e394c-338">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span><span class="sxs-lookup"><span data-stu-id="e394c-338">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="e394c-339">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="e394c-339">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="e394c-340">Other options for uploading a VHD</span><span class="sxs-lookup"><span data-stu-id="e394c-340">Other options for uploading a VHD</span></span>
<span data-ttu-id="e394c-341">You can also upload a VHD to your storage account using one of the following means:</span><span class="sxs-lookup"><span data-stu-id="e394c-341">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="e394c-342">Azure Storage Copy Blob API</span><span class="sxs-lookup"><span data-stu-id="e394c-342">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="e394c-343">Azure Storage Explorer Uploading Blobs</span><span class="sxs-lookup"><span data-stu-id="e394c-343">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="e394c-344">Storage Import/Export Service REST API Reference</span><span class="sxs-lookup"><span data-stu-id="e394c-344">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="e394c-345">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span><span class="sxs-lookup"><span data-stu-id="e394c-345">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="e394c-346">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span><span class="sxs-lookup"><span data-stu-id="e394c-346">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="e394c-347">Import/Export can be used to copy to a standard storage account.</span><span class="sxs-lookup"><span data-stu-id="e394c-347">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="e394c-348">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e394c-348">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a><span data-ttu-id="e394c-349">Create Azure VMs using Premium Storage</span><span class="sxs-lookup"><span data-stu-id="e394c-349">Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="e394c-350">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span><span class="sxs-lookup"><span data-stu-id="e394c-350">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="e394c-351">The data disk VHD can be attached to the VM once it is created.</span><span class="sxs-lookup"><span data-stu-id="e394c-351">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="e394c-352">A sample migration script is provided at the end of this section.</span><span class="sxs-lookup"><span data-stu-id="e394c-352">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="e394c-353">This simple script does not match all scenarios.</span><span class="sxs-lookup"><span data-stu-id="e394c-353">This simple script does not match all scenarios.</span></span> <span data-ttu-id="e394c-354">You may need to update the script to match with your specific scenario.</span><span class="sxs-lookup"><span data-stu-id="e394c-354">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="e394c-355">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="e394c-355">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="e394c-356">Checklist</span><span class="sxs-lookup"><span data-stu-id="e394c-356">Checklist</span></span>
1. <span data-ttu-id="e394c-357">Wait until all the VHD disks copying is complete.</span><span class="sxs-lookup"><span data-stu-id="e394c-357">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="e394c-358">Make sure Premium Storage is available in the region you are migrating to.</span><span class="sxs-lookup"><span data-stu-id="e394c-358">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="e394c-359">Decide the new VM series you will be using.</span><span class="sxs-lookup"><span data-stu-id="e394c-359">Decide the new VM series you will be using.</span></span> <span data-ttu-id="e394c-360">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span><span class="sxs-lookup"><span data-stu-id="e394c-360">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="e394c-361">Decide the exact VM size you will use.</span><span class="sxs-lookup"><span data-stu-id="e394c-361">Decide the exact VM size you will use.</span></span> <span data-ttu-id="e394c-362">VM size needs to be large enough to support the number of data disks you have.</span><span class="sxs-lookup"><span data-stu-id="e394c-362">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="e394c-363">E.g.</span><span class="sxs-lookup"><span data-stu-id="e394c-363">E.g.</span></span> <span data-ttu-id="e394c-364">if you have 4 data disks, the VM must have 2 or more cores.</span><span class="sxs-lookup"><span data-stu-id="e394c-364">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="e394c-365">Also, consider processing power, memory and network bandwidth needs.</span><span class="sxs-lookup"><span data-stu-id="e394c-365">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="e394c-366">Create a Premium Storage account in the target region.</span><span class="sxs-lookup"><span data-stu-id="e394c-366">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="e394c-367">This is the account you will use for the new VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-367">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="e394c-368">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span><span class="sxs-lookup"><span data-stu-id="e394c-368">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="e394c-369">Prepare your application for downtime.</span><span class="sxs-lookup"><span data-stu-id="e394c-369">Prepare your application for downtime.</span></span> <span data-ttu-id="e394c-370">To do a clean migration, you have to stop all the processing in the current system.</span><span class="sxs-lookup"><span data-stu-id="e394c-370">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="e394c-371">Only then you can get it to consistent state which you can migrate to the new platform.</span><span class="sxs-lookup"><span data-stu-id="e394c-371">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="e394c-372">Downtime duration will depend on the amount of data in the disks to migrate.</span><span class="sxs-lookup"><span data-stu-id="e394c-372">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="e394c-373">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span><span class="sxs-lookup"><span data-stu-id="e394c-373">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="e394c-374">Register your VHD</span><span class="sxs-lookup"><span data-stu-id="e394c-374">Register your VHD</span></span>
<span data-ttu-id="e394c-375">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span><span class="sxs-lookup"><span data-stu-id="e394c-375">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="e394c-376">Follow steps below depending on your VHD's scenario.</span><span class="sxs-lookup"><span data-stu-id="e394c-376">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="e394c-377">Generalized Operating System VHD to create multiple Azure VM instances</span><span class="sxs-lookup"><span data-stu-id="e394c-377">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="e394c-378">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span><span class="sxs-lookup"><span data-stu-id="e394c-378">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="e394c-379">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span><span class="sxs-lookup"><span data-stu-id="e394c-379">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="e394c-380">Provide the complete container URL where VHD was copied to.</span><span class="sxs-lookup"><span data-stu-id="e394c-380">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="e394c-381">Copy and save the name of this new Azure VM Image.</span><span class="sxs-lookup"><span data-stu-id="e394c-381">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="e394c-382">In the example above, it is *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="e394c-382">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="e394c-383">Unique Operating System VHD to create a single Azure VM instance</span><span class="sxs-lookup"><span data-stu-id="e394c-383">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="e394c-384">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span><span class="sxs-lookup"><span data-stu-id="e394c-384">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="e394c-385">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span><span class="sxs-lookup"><span data-stu-id="e394c-385">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="e394c-386">Provide the complete container URL where VHD was copied to.</span><span class="sxs-lookup"><span data-stu-id="e394c-386">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="e394c-387">Copy and save the name of this new Azure OS Disk.</span><span class="sxs-lookup"><span data-stu-id="e394c-387">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="e394c-388">In the example above, it is *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="e394c-388">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="e394c-389">Data disk VHD to be attached to new Azure VM instance(s)</span><span class="sxs-lookup"><span data-stu-id="e394c-389">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="e394c-390">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span><span class="sxs-lookup"><span data-stu-id="e394c-390">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="e394c-391">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span><span class="sxs-lookup"><span data-stu-id="e394c-391">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="e394c-392">Provide the complete container URL where VHD was copied to.</span><span class="sxs-lookup"><span data-stu-id="e394c-392">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="e394c-393">Copy and save the name of this new Azure Data Disk.</span><span class="sxs-lookup"><span data-stu-id="e394c-393">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="e394c-394">In the example above, it is *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="e394c-394">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="e394c-395">Create a Premium Storage capable VM</span><span class="sxs-lookup"><span data-stu-id="e394c-395">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="e394c-396">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-396">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="e394c-397">You will be using the operating system image or operating system disk name that you registered.</span><span class="sxs-lookup"><span data-stu-id="e394c-397">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="e394c-398">Select the VM type from the Premium Storage tier.</span><span class="sxs-lookup"><span data-stu-id="e394c-398">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="e394c-399">In example below, we are using the *Standard_DS2* VM size.</span><span class="sxs-lookup"><span data-stu-id="e394c-399">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="e394c-400">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span><span class="sxs-lookup"><span data-stu-id="e394c-400">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="e394c-401">Follow the step by step PowerShell cmdlets below to create the new VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-401">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="e394c-402">First, set the common parameters:</span><span class="sxs-lookup"><span data-stu-id="e394c-402">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="e394c-403">First, create a cloud service in which you will be hosting your new VMs.</span><span class="sxs-lookup"><span data-stu-id="e394c-403">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="e394c-404">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span><span class="sxs-lookup"><span data-stu-id="e394c-404">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="e394c-405">Generalized Operating System VHD to create multiple Azure VM instances</span><span class="sxs-lookup"><span data-stu-id="e394c-405">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="e394c-406">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span><span class="sxs-lookup"><span data-stu-id="e394c-406">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="e394c-407">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span><span class="sxs-lookup"><span data-stu-id="e394c-407">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="e394c-408">Unique Operating System VHD to create a single Azure VM instance</span><span class="sxs-lookup"><span data-stu-id="e394c-408">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="e394c-409">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span><span class="sxs-lookup"><span data-stu-id="e394c-409">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="e394c-410">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span><span class="sxs-lookup"><span data-stu-id="e394c-410">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="e394c-411">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span><span class="sxs-lookup"><span data-stu-id="e394c-411">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="e394c-412">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span><span class="sxs-lookup"><span data-stu-id="e394c-412">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="e394c-413">Attach data disk</span><span class="sxs-lookup"><span data-stu-id="e394c-413">Attach data disk</span></span>
<span data-ttu-id="e394c-414">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-414">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="e394c-415">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span><span class="sxs-lookup"><span data-stu-id="e394c-415">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="e394c-416">In example below the caching policy is set to *ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="e394c-416">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="e394c-417">There may be additional steps necessary to support your application that is not be covered by this guide.</span><span class="sxs-lookup"><span data-stu-id="e394c-417">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="e394c-418">Checking and plan backup</span><span class="sxs-lookup"><span data-stu-id="e394c-418">Checking and plan backup</span></span>
<span data-ttu-id="e394c-419">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span><span class="sxs-lookup"><span data-stu-id="e394c-419">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="e394c-420">All the settings, including the striped volumes, would be present in the new VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-420">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="e394c-421">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span><span class="sxs-lookup"><span data-stu-id="e394c-421">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <a name="a-sample-migration-script"></a><span data-ttu-id="e394c-422">A sample migration script</span><span class="sxs-lookup"><span data-stu-id="e394c-422">A sample migration script</span></span>
<span data-ttu-id="e394c-423">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span><span class="sxs-lookup"><span data-stu-id="e394c-423">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="e394c-424">Following is a sample script that automates the migration of a VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-424">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="e394c-425">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span><span class="sxs-lookup"><span data-stu-id="e394c-425">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="e394c-426">You may need to update the script to match with your specific scenario.</span><span class="sxs-lookup"><span data-stu-id="e394c-426">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="e394c-427">The assumptions are:</span><span class="sxs-lookup"><span data-stu-id="e394c-427">The assumptions are:</span></span>

* <span data-ttu-id="e394c-428">You are creating classic Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="e394c-428">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="e394c-429">Your source OS Disks and source Data Disks are in same storage account and same container.</span><span class="sxs-lookup"><span data-stu-id="e394c-429">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="e394c-430">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span><span class="sxs-lookup"><span data-stu-id="e394c-430">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="e394c-431">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="e394c-431">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="e394c-432">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span><span class="sxs-lookup"><span data-stu-id="e394c-432">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="e394c-433">The automation script is provided below.</span><span class="sxs-lookup"><span data-stu-id="e394c-433">The automation script is provided below.</span></span> <span data-ttu-id="e394c-434">Replace text with your information and update the script to match with your specific scenario.</span><span class="sxs-lookup"><span data-stu-id="e394c-434">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="e394c-435">Using the existing script does not preserve the network configuration of your source VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-435">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="e394c-436">You will need to re-config the networking settings on your migrated VMs.</span><span class="sxs-lookup"><span data-stu-id="e394c-436">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check the Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a><span data-ttu-id="e394c-437">Optimization</span><span class="sxs-lookup"><span data-stu-id="e394c-437">Optimization</span></span>
<span data-ttu-id="e394c-438">Your current VM configuration may be customized specifically to work well with Standard disks.</span><span class="sxs-lookup"><span data-stu-id="e394c-438">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="e394c-439">For instance, to increase the performance by using many disks in a striped volume.</span><span class="sxs-lookup"><span data-stu-id="e394c-439">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="e394c-440">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span><span class="sxs-lookup"><span data-stu-id="e394c-440">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="e394c-441">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span><span class="sxs-lookup"><span data-stu-id="e394c-441">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="e394c-442">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span><span class="sxs-lookup"><span data-stu-id="e394c-442">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="e394c-443">Preparation</span><span class="sxs-lookup"><span data-stu-id="e394c-443">Preparation</span></span>
1. <span data-ttu-id="e394c-444">Complete the Simple Migration as described in the earlier section.</span><span class="sxs-lookup"><span data-stu-id="e394c-444">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="e394c-445">Optimizations will be performed on the new VM after the migration.</span><span class="sxs-lookup"><span data-stu-id="e394c-445">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="e394c-446">Define the new disk sizes needed for the optimized configuration.</span><span class="sxs-lookup"><span data-stu-id="e394c-446">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="e394c-447">Determine mapping of the current disks/volumes to the new disk specifications.</span><span class="sxs-lookup"><span data-stu-id="e394c-447">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="e394c-448">Execution steps</span><span class="sxs-lookup"><span data-stu-id="e394c-448">Execution steps</span></span>
1. <span data-ttu-id="e394c-449">Create the new disks with the right sizes on the Premium Storage VM.</span><span class="sxs-lookup"><span data-stu-id="e394c-449">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="e394c-450">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span><span class="sxs-lookup"><span data-stu-id="e394c-450">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="e394c-451">Do this for all the current volumes that need to map to a new disk.</span><span class="sxs-lookup"><span data-stu-id="e394c-451">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="e394c-452">Next, change the application settings to switch to the new disks, and detach the old volumes.</span><span class="sxs-lookup"><span data-stu-id="e394c-452">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="e394c-453">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="e394c-453">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="e394c-454">Application migrations</span><span class="sxs-lookup"><span data-stu-id="e394c-454">Application migrations</span></span>
<span data-ttu-id="e394c-455">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span><span class="sxs-lookup"><span data-stu-id="e394c-455">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="e394c-456">Please refer to respective application documentation.</span><span class="sxs-lookup"><span data-stu-id="e394c-456">Please refer to respective application documentation.</span></span> <span data-ttu-id="e394c-457">E.g.</span><span class="sxs-lookup"><span data-stu-id="e394c-457">E.g.</span></span> <span data-ttu-id="e394c-458">typically databases can be migrated through backup and restore.</span><span class="sxs-lookup"><span data-stu-id="e394c-458">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e394c-459">Next steps</span><span class="sxs-lookup"><span data-stu-id="e394c-459">Next steps</span></span>
<span data-ttu-id="e394c-460">See the following resources for specific scenarios for migrating virtual machines:</span><span class="sxs-lookup"><span data-stu-id="e394c-460">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="e394c-461">Migrate Azure Virtual Machines between Storage Accounts</span><span class="sxs-lookup"><span data-stu-id="e394c-461">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="e394c-462">Create and upload a Windows Server VHD to Azure.</span><span class="sxs-lookup"><span data-stu-id="e394c-462">Create and upload a Windows Server VHD to Azure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="e394c-463">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span><span class="sxs-lookup"><span data-stu-id="e394c-463">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="e394c-464">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e394c-464">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="e394c-465">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span><span class="sxs-lookup"><span data-stu-id="e394c-465">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="e394c-466">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e394c-466">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="e394c-467">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="e394c-467">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="e394c-468">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span><span class="sxs-lookup"><span data-stu-id="e394c-468">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx



