---
title: Frequently Asked Questions (FAQ) about Azure IaaS VM Disks | Microsoft Docs
description: Frequently asked questions about Azure IaaS VM disks and premium disks (managed and unmanaged)
services: storage
documentationcenter: ''
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: robinsh
ms.openlocfilehash: 1a462b8d557ad23bda912ddf9431195a8cfe909e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563657"
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="cb70f-103">Frequently Asked Questions about Azure IaaS VM Disks and managed and unmanaged premium disks</span><span class="sxs-lookup"><span data-stu-id="cb70f-103">Frequently Asked Questions about Azure IaaS VM Disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="cb70f-104">In this article, we'll visit some of the frequently asked questions about Managed Disks and Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="cb70f-104">In this article, we'll visit some of the frequently asked questions about Managed Disks and Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="cb70f-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="cb70f-105">Managed Disks</span></span>

<span data-ttu-id="cb70f-106">**What is Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="cb70f-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span><span class="sxs-lookup"><span data-stu-id="cb70f-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="cb70f-108">For more information, please see the [Managed Disks Overview](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cb70f-108">For more information, please see the [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="cb70f-109">**If I create a standard managed disk from an existing VHD that was 80 GB in size, how much will that cost me?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-109">**If I create a standard managed disk from an existing VHD that was 80 GB in size, how much will that cost me?**</span></span>

<span data-ttu-id="cb70f-110">A standard managed disk created from an 80 GB VHD will be treated as the next available premium disk size, which is an S10 disk.</span><span class="sxs-lookup"><span data-stu-id="cb70f-110">A standard managed disk created from an 80 GB VHD will be treated as the next available premium disk size, which is an S10 disk.</span></span> <span data-ttu-id="cb70f-111">You will be charged as per the S10 disk pricing.</span><span class="sxs-lookup"><span data-stu-id="cb70f-111">You will be charged as per the S10 disk pricing.</span></span> <span data-ttu-id="cb70f-112">Please check the [pricing page](https://azure.microsoft.com/pricing/details/storage) for details.</span><span class="sxs-lookup"><span data-stu-id="cb70f-112">Please check the [pricing page](https://azure.microsoft.com/pricing/details/storage) for details.</span></span>

<span data-ttu-id="cb70f-113">**Are there any transaction costs for standard managed disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="cb70f-114">Yes, you are charged for each transaction.</span><span class="sxs-lookup"><span data-stu-id="cb70f-114">Yes, you are charged for each transaction.</span></span> <span data-ttu-id="cb70f-115">Please check the [pricing page] (https://azure.microsoft.com/pricing/details/storage) for details.</span><span class="sxs-lookup"><span data-stu-id="cb70f-115">Please check the [pricing page] (https://azure.microsoft.com/pricing/details/storage) for details.</span></span>

<span data-ttu-id="cb70f-116">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-116">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="cb70f-117">You are charged based on the provisioned capacity of the disk.</span><span class="sxs-lookup"><span data-stu-id="cb70f-117">You are charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="cb70f-118">Please check the [pricing page](https://azure.microsoft.com/pricing/details/storage) for details.</span><span class="sxs-lookup"><span data-stu-id="cb70f-118">Please check the [pricing page](https://azure.microsoft.com/pricing/details/storage) for details.</span></span>

<span data-ttu-id="cb70f-119">**How is pricing of premium managed disks different than unmanaged disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-119">**How is pricing of premium managed disks different than unmanaged disks?**</span></span>

<span data-ttu-id="cb70f-120">The pricing of premium managed disks is the same as unmanaged premium disks.</span><span class="sxs-lookup"><span data-stu-id="cb70f-120">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="cb70f-121">**Can I change the storage account type (Standard/Premium) of my managed disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-121">**Can I change the storage account type (Standard/Premium) of my managed disks?**</span></span>

<span data-ttu-id="cb70f-122">Yes.</span><span class="sxs-lookup"><span data-stu-id="cb70f-122">Yes.</span></span> <span data-ttu-id="cb70f-123">You can change the storage account type of your managed disks using the Azure portal, PowerShell, or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cb70f-123">You can change the storage account type of your managed disks using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="cb70f-124">**Is there a way I can copy or export a managed disk to a private storage account?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-124">**Is there a way I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="cb70f-125">Yes, you can export your managed disks using the Azure portal, PowerShell, or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cb70f-125">Yes, you can export your managed disks using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="cb70f-126">**Can I use a VHD file in an Azure storage account to create a managed disk in a different subscriptions?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-126">**Can I use a VHD file in an Azure storage account to create a managed disk in a different subscriptions?**</span></span>

<span data-ttu-id="cb70f-127">No.</span><span class="sxs-lookup"><span data-stu-id="cb70f-127">No.</span></span>

<span data-ttu-id="cb70f-128">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-128">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="cb70f-129">No.</span><span class="sxs-lookup"><span data-stu-id="cb70f-129">No.</span></span>

<span data-ttu-id="cb70f-130">**Will there be any scale limitations for customers using managed disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-130">**Will there be any scale limitations for customers using managed disks?**</span></span>

<span data-ttu-id="cb70f-131">Managed Disks eliminates the limits associated with storage accounts.</span><span class="sxs-lookup"><span data-stu-id="cb70f-131">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="cb70f-132">However, the number of managed disks per subscription is limited to 2000 by default.</span><span class="sxs-lookup"><span data-stu-id="cb70f-132">However, the number of managed disks per subscription is limited to 2000 by default.</span></span> <span data-ttu-id="cb70f-133">This can be increased by calling support.</span><span class="sxs-lookup"><span data-stu-id="cb70f-133">This can be increased by calling support.</span></span>

<span data-ttu-id="cb70f-134">**Can I take an incremental snapshot of a managed disk?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="cb70f-135">No.</span><span class="sxs-lookup"><span data-stu-id="cb70f-135">No.</span></span> <span data-ttu-id="cb70f-136">The current Snapshot capability makes a full copy of a managed disk.</span><span class="sxs-lookup"><span data-stu-id="cb70f-136">The current Snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="cb70f-137">However, we are planning to support incremental snapshots in the future.</span><span class="sxs-lookup"><span data-stu-id="cb70f-137">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="cb70f-138">**Can VMs in an Availability Set consist of a mixture of managed and unmanaged disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-138">**Can VMs in an Availability Set consist of a mixture of managed and unmanaged disks?**</span></span>

<span data-ttu-id="cb70f-139">No, the VMs in an Availability Set must use either all managed or all unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="cb70f-139">No, the VMs in an Availability Set must use either all managed or all unmanaged disks.</span></span> <span data-ttu-id="cb70f-140">When creating an Availability Set, you can choose which type of disks you want to use.</span><span class="sxs-lookup"><span data-stu-id="cb70f-140">When creating an Availability Set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="cb70f-141">**Is Managed Disks the default option in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-141">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="cb70f-142">Not currently, but it will become the default in the future.</span><span class="sxs-lookup"><span data-stu-id="cb70f-142">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="cb70f-143">**Can I create an empty managed disk?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-143">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="cb70f-144">Yes, you can create an empty disk.</span><span class="sxs-lookup"><span data-stu-id="cb70f-144">Yes, you can create an empty disk.</span></span> <span data-ttu-id="cb70f-145">A managed disk can be created independently of a VM, i.e., without attaching it to a VM.</span><span class="sxs-lookup"><span data-stu-id="cb70f-145">A managed disk can be created independently of a VM, i.e., without attaching it to a VM.</span></span>

<span data-ttu-id="cb70f-146">**What is the supported fault domain count for Availability Sets using Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-146">**What is the supported fault domain count for Availability Sets using Managed Disks?**</span></span>

<span data-ttu-id="cb70f-147">The supported fault domain count is 2 or 3 for Availability Sets using Managed Disks depending on the region in which it is located.</span><span class="sxs-lookup"><span data-stu-id="cb70f-147">The supported fault domain count is 2 or 3 for Availability Sets using Managed Disks depending on the region in which it is located.</span></span>

<span data-ttu-id="cb70f-148">**How is the standard storage account for diagnostics set up?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-148">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="cb70f-149">You set up a private storage account for VM diagnostics.</span><span class="sxs-lookup"><span data-stu-id="cb70f-149">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="cb70f-150">In the future, we plan to switch diagnostics to Managed Disks as well.</span><span class="sxs-lookup"><span data-stu-id="cb70f-150">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="cb70f-151">**What kind of RBAC support do we have for Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-151">**What kind of RBAC support do we have for Managed Disks?**</span></span>

<span data-ttu-id="cb70f-152">Managed Disks supports three key default roles:</span><span class="sxs-lookup"><span data-stu-id="cb70f-152">Managed Disks supports three key default roles:</span></span>

1.  <span data-ttu-id="cb70f-153">Owner: Can manage everything, including access.</span><span class="sxs-lookup"><span data-stu-id="cb70f-153">Owner: Can manage everything, including access.</span></span>

2.  <span data-ttu-id="cb70f-154">Contributor: Can manage everything except access.</span><span class="sxs-lookup"><span data-stu-id="cb70f-154">Contributor: Can manage everything except access.</span></span>

3.  <span data-ttu-id="cb70f-155">Reader: Can view everything, but can't make changes.</span><span class="sxs-lookup"><span data-stu-id="cb70f-155">Reader: Can view everything, but can't make changes.</span></span>

<span data-ttu-id="cb70f-156">**Is there a way I can copy or export a managed disk to a private storage account?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-156">**Is there a way I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="cb70f-157">You can get a read-only shared access signature (SAS) URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span><span class="sxs-lookup"><span data-stu-id="cb70f-157">You can get a read-only shared access signature (SAS) URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="cb70f-158">**Can I create a copy of my managed disk?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-158">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="cb70f-159">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span><span class="sxs-lookup"><span data-stu-id="cb70f-159">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="cb70f-160">**Is unmanaged disks still supported?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-160">**Is unmanaged disks still supported?**</span></span>

<span data-ttu-id="cb70f-161">Yes, we support both managed and unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="cb70f-161">Yes, we support both managed and unmanaged disks.</span></span> <span data-ttu-id="cb70f-162">However, we recommend you start using managed disks for new workloads and migrate your current workloads to Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="cb70f-162">However, we recommend you start using managed disks for new workloads and migrate your current workloads to Managed Disks.</span></span>

<span data-ttu-id="cb70f-163">**If I create a disk of size 128 GB and then increase the size to 130 GB will I be charged for the next disk size (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-163">**If I create a disk of size 128 GB and then increase the size to 130 GB will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="cb70f-164">Yes.</span><span class="sxs-lookup"><span data-stu-id="cb70f-164">Yes.</span></span>

<span data-ttu-id="cb70f-165">**Can I create the LRS, GRS, and ZRS Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-165">**Can I create the LRS, GRS, and ZRS Managed Disks?**</span></span>

<span data-ttu-id="cb70f-166">Azure Managed Disks currently only supports locally-redundant storage (LRS).</span><span class="sxs-lookup"><span data-stu-id="cb70f-166">Azure Managed Disks currently only supports locally-redundant storage (LRS).</span></span>

## <a name="managed-disks-and-port-8443"></a><span data-ttu-id="cb70f-167">Managed Disks and port 8443</span><span class="sxs-lookup"><span data-stu-id="cb70f-167">Managed Disks and port 8443</span></span>

<span data-ttu-id="cb70f-168">**Why do customers have to unblock outbound traffic on port 8443 for VMs using Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-168">**Why do customers have to unblock outbound traffic on port 8443 for VMs using Azure Managed Disks?**</span></span>

<span data-ttu-id="cb70f-169">The Azure VM Agent uses port 8443 to report the status of each VM extension to the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="cb70f-169">The Azure VM Agent uses port 8443 to report the status of each VM extension to the Azure platform.</span></span> <span data-ttu-id="cb70f-170">Without this port being unblocked, the VM agent won't be able to report the status of any VM extension.</span><span class="sxs-lookup"><span data-stu-id="cb70f-170">Without this port being unblocked, the VM agent won't be able to report the status of any VM extension.</span></span> <span data-ttu-id="cb70f-171">For more information about the VM agent, please see [Azure Virtual Machine Agent overview](../virtual-machines/windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="cb70f-171">For more information about the VM agent, please see [Azure Virtual Machine Agent overview](../virtual-machines/windows/agent-user-guide.md).</span></span>

<span data-ttu-id="cb70f-172">**What happens if a VM is deployed with extensions and the port is not unblocked?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-172">**What happens if a VM is deployed with extensions and the port is not unblocked?**</span></span>

<span data-ttu-id="cb70f-173">The deployment will result in an error.</span><span class="sxs-lookup"><span data-stu-id="cb70f-173">The deployment will result in an error.</span></span> 

<span data-ttu-id="cb70f-174">**What happens if a VM is deployed with no extensions and the port is not unblocked?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-174">**What happens if a VM is deployed with no extensions and the port is not unblocked?**</span></span>

<span data-ttu-id="cb70f-175">There will be no impact on the deployment.</span><span class="sxs-lookup"><span data-stu-id="cb70f-175">There will be no impact on the deployment.</span></span> 

<span data-ttu-id="cb70f-176">**What happens if an extension is installed on a VM which is already provisioned and running and the VM does not have port 8443 unblocked?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-176">**What happens if an extension is installed on a VM which is already provisioned and running and the VM does not have port 8443 unblocked?**</span></span>

<span data-ttu-id="cb70f-177">The extension won't be successfully deployed.</span><span class="sxs-lookup"><span data-stu-id="cb70f-177">The extension won't be successfully deployed.</span></span> <span data-ttu-id="cb70f-178">The status of the extension will be unknown.</span><span class="sxs-lookup"><span data-stu-id="cb70f-178">The status of the extension will be unknown.</span></span> 

<span data-ttu-id="cb70f-179">**What happens if an ARM template is used to provision multiple VMs with port 8443 blocked -- one VM with extensions and a second VM dependent on the first VM?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-179">**What happens if an ARM template is used to provision multiple VMs with port 8443 blocked -- one VM with extensions and a second VM dependent on the first VM?**</span></span>

<span data-ttu-id="cb70f-180">The first VM will show as a failed deployment because the extensions were not successfully deployed.</span><span class="sxs-lookup"><span data-stu-id="cb70f-180">The first VM will show as a failed deployment because the extensions were not successfully deployed.</span></span> <span data-ttu-id="cb70f-181">The second VM will not be deployed.</span><span class="sxs-lookup"><span data-stu-id="cb70f-181">The second VM will not be deployed.</span></span> 

<span data-ttu-id="cb70f-182">**Will this requirement of the port being unblocked apply to all VM extensions?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-182">**Will this requirement of the port being unblocked apply to all VM extensions?**</span></span>

<span data-ttu-id="cb70f-183">Yes.</span><span class="sxs-lookup"><span data-stu-id="cb70f-183">Yes.</span></span>

<span data-ttu-id="cb70f-184">**Do both inbound and outbound connections on port 8443 have to be unblocked?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-184">**Do both inbound and outbound connections on port 8443 have to be unblocked?**</span></span>

<span data-ttu-id="cb70f-185">No.</span><span class="sxs-lookup"><span data-stu-id="cb70f-185">No.</span></span> <span data-ttu-id="cb70f-186">Only outbound connections on port 8443 have to be unblocked.</span><span class="sxs-lookup"><span data-stu-id="cb70f-186">Only outbound connections on port 8443 have to be unblocked.</span></span> 

<span data-ttu-id="cb70f-187">**Is having outbound connections on port 8443 being unblocked required for the entire lifetime of the VM?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-187">**Is having outbound connections on port 8443 being unblocked required for the entire lifetime of the VM?**</span></span>

<span data-ttu-id="cb70f-188">Yes.</span><span class="sxs-lookup"><span data-stu-id="cb70f-188">Yes.</span></span>

<span data-ttu-id="cb70f-189">**Does having this port unblocked affect the performance of the VM?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-189">**Does having this port unblocked affect the performance of the VM?**</span></span>

<span data-ttu-id="cb70f-190">No.</span><span class="sxs-lookup"><span data-stu-id="cb70f-190">No.</span></span>

<span data-ttu-id="cb70f-191">**Is there an estimated date for this issue to be fixed so I no longer have to unblock port 8443?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-191">**Is there an estimated date for this issue to be fixed so I no longer have to unblock port 8443?**</span></span>

<span data-ttu-id="cb70f-192">Yes, by the end of May 2017.</span><span class="sxs-lookup"><span data-stu-id="cb70f-192">Yes, by the end of May 2017.</span></span>

## <a name="premium-disks--both-managed-and-unmanaged"></a><span data-ttu-id="cb70f-193">Premium Disks – both managed and unmanaged</span><span class="sxs-lookup"><span data-stu-id="cb70f-193">Premium Disks – both managed and unmanaged</span></span>

<span data-ttu-id="cb70f-194">**If a VM uses a size series that supports Premium storage, such as a DSv2, can I attach both premium and standard data disks?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-194">**If a VM uses a size series that supports Premium storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="cb70f-195">Yes.</span><span class="sxs-lookup"><span data-stu-id="cb70f-195">Yes.</span></span>

<span data-ttu-id="cb70f-196">**Can I attach both premium and standard data disks to a size series that does not support Premium storage, such as D, Dv2, G or F series?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-196">**Can I attach both premium and standard data disks to a size series that does not support Premium storage, such as D, Dv2, G or F series?**</span></span>

<span data-ttu-id="cb70f-197">No.</span><span class="sxs-lookup"><span data-stu-id="cb70f-197">No.</span></span> <span data-ttu-id="cb70f-198">You can only attach standard data disks to VMs that do not use a size series that supports Premium storage.</span><span class="sxs-lookup"><span data-stu-id="cb70f-198">You can only attach standard data disks to VMs that do not use a size series that supports Premium storage.</span></span>

<span data-ttu-id="cb70f-199">**If I create a premium data disk from an existing VHD that was 80 GB in size, how much will that cost me?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-199">**If I create a premium data disk from an existing VHD that was 80 GB in size, how much will that cost me?**</span></span>

<span data-ttu-id="cb70f-200">A premium data disk created from 80 GB VHD will be treated as the next available premium disk size, which is a P10 disk.</span><span class="sxs-lookup"><span data-stu-id="cb70f-200">A premium data disk created from 80 GB VHD will be treated as the next available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="cb70f-201">You will be charged as per the P10 disk pricing.</span><span class="sxs-lookup"><span data-stu-id="cb70f-201">You will be charged as per the P10 disk pricing.</span></span>

<span data-ttu-id="cb70f-202">**Are there transaction costs when using Premium Storage?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-202">**Are there transaction costs when using Premium Storage?**</span></span>

<span data-ttu-id="cb70f-203">There is a fixed cost for each disk size which comes provisioned with specific limits on IOPS and throughput.</span><span class="sxs-lookup"><span data-stu-id="cb70f-203">There is a fixed cost for each disk size which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="cb70f-204">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span><span class="sxs-lookup"><span data-stu-id="cb70f-204">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="cb70f-205">Please check the [pricing page](https://azure.microsoft.com/pricing/details/storage) for details.</span><span class="sxs-lookup"><span data-stu-id="cb70f-205">Please check the [pricing page](https://azure.microsoft.com/pricing/details/storage) for details.</span></span>

<span data-ttu-id="cb70f-206">**What are the limits for IOPS and throughput that can I get from the disk cache?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-206">**What are the limits for IOPS and throughput that can I get from the disk cache?**</span></span>

<span data-ttu-id="cb70f-207">The combined limits for cache and local SSD for a DS series are 4000 IOPS per core and 33 MB per second per core.</span><span class="sxs-lookup"><span data-stu-id="cb70f-207">The combined limits for cache and local SSD for a DS series are 4000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="cb70f-208">The GS series offers 5000 IOPS per core and 50 MB per second per core.</span><span class="sxs-lookup"><span data-stu-id="cb70f-208">The GS series offers 5000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="cb70f-209">**Is the local SSD supported for Managed Disks VMs?**</span><span class="sxs-lookup"><span data-stu-id="cb70f-209">**Is the local SSD supported for Managed Disks VMs?**</span></span>

<span data-ttu-id="cb70f-210">The local SSD is temporary storage that is included with a managed disks VM.</span><span class="sxs-lookup"><span data-stu-id="cb70f-210">The local SSD is temporary storage that is included with a managed disks VM.</span></span> <span data-ttu-id="cb70f-211">There is no extra cost for this temporary storage.</span><span class="sxs-lookup"><span data-stu-id="cb70f-211">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="cb70f-212">It is recommended that you do not use this local SSD for storing your application data as it is not persisted in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="cb70f-212">It is recommended that you do not use this local SSD for storing your application data as it is not persisted in Azure Blob storage.</span></span>

## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="cb70f-213">What if my question isn't answered here?</span><span class="sxs-lookup"><span data-stu-id="cb70f-213">What if my question isn't answered here?</span></span>

<span data-ttu-id="cb70f-214">If your question isn't listed here, let us know and we'll help you find an answer.</span><span class="sxs-lookup"><span data-stu-id="cb70f-214">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="cb70f-215">You can post a question at the end of this article in the comments or in the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata) to engage with the Azure Storage team and other community members about this article.</span><span class="sxs-lookup"><span data-stu-id="cb70f-215">You can post a question at the end of this article in the comments or in the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata) to engage with the Azure Storage team and other community members about this article.</span></span>

<span data-ttu-id="cb70f-216">To make a feature request, please submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="cb70f-216">To make a feature request, please submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>