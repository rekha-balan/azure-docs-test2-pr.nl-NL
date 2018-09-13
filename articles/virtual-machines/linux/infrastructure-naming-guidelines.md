---
title: Azure infrastructure naming guidelines - Linux | Microsoft Docs
description: Learn about the key design and implementation guidelines for naming in Azure infrastructure services.
documentationcenter: ''
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7fe737fd879b9e794c668323679c69b459650c4d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556144"
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="f38ac-103">Azure infrastructure naming guidelines for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="f38ac-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="f38ac-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span><span class="sxs-lookup"><span data-stu-id="f38ac-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="f38ac-105">Implementation guidelines for naming conventions</span><span class="sxs-lookup"><span data-stu-id="f38ac-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="f38ac-106">Decisions:</span><span class="sxs-lookup"><span data-stu-id="f38ac-106">Decisions:</span></span>

* <span data-ttu-id="f38ac-107">What are your naming conventions for Azure resources?</span><span class="sxs-lookup"><span data-stu-id="f38ac-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="f38ac-108">Tasks:</span><span class="sxs-lookup"><span data-stu-id="f38ac-108">Tasks:</span></span>

* <span data-ttu-id="f38ac-109">Define the affixes to use across your resources to maintain consistency.</span><span class="sxs-lookup"><span data-stu-id="f38ac-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="f38ac-110">Define storage account names given the requirement for them to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="f38ac-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="f38ac-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span><span class="sxs-lookup"><span data-stu-id="f38ac-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="f38ac-112">Naming conventions</span><span class="sxs-lookup"><span data-stu-id="f38ac-112">Naming conventions</span></span>
<span data-ttu-id="f38ac-113">You should have a good naming convention in place before creating anything in Azure.</span><span class="sxs-lookup"><span data-stu-id="f38ac-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="f38ac-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span><span class="sxs-lookup"><span data-stu-id="f38ac-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="f38ac-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span><span class="sxs-lookup"><span data-stu-id="f38ac-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="f38ac-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, you need to be able to scale for teams working together in Azure.</span><span class="sxs-lookup"><span data-stu-id="f38ac-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, you need to be able to scale for teams working together in Azure.</span></span>

<span data-ttu-id="f38ac-117">Agree on a set of naming conventions up front.</span><span class="sxs-lookup"><span data-stu-id="f38ac-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="f38ac-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span><span class="sxs-lookup"><span data-stu-id="f38ac-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="f38ac-119">Affixes</span><span class="sxs-lookup"><span data-stu-id="f38ac-119">Affixes</span></span>
<span data-ttu-id="f38ac-120">As you look to define a naming convention, one decision is whether the affix is at:</span><span class="sxs-lookup"><span data-stu-id="f38ac-120">As you look to define a naming convention, one decision is whether the affix is at:</span></span>

* <span data-ttu-id="f38ac-121">The beginning of the name (prefix)</span><span class="sxs-lookup"><span data-stu-id="f38ac-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="f38ac-122">The end of the name (suffix)</span><span class="sxs-lookup"><span data-stu-id="f38ac-122">The end of the name (suffix)</span></span>

<span data-ttu-id="f38ac-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span><span class="sxs-lookup"><span data-stu-id="f38ac-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="f38ac-124">Rg-WebApp (prefix)</span><span class="sxs-lookup"><span data-stu-id="f38ac-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="f38ac-125">WebApp-Rg (suffix)</span><span class="sxs-lookup"><span data-stu-id="f38ac-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="f38ac-126">Affixes can refer to different aspects that describe the particular resources.</span><span class="sxs-lookup"><span data-stu-id="f38ac-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="f38ac-127">The following table shows some examples typically used.</span><span class="sxs-lookup"><span data-stu-id="f38ac-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="f38ac-128">Aspect</span><span class="sxs-lookup"><span data-stu-id="f38ac-128">Aspect</span></span> | <span data-ttu-id="f38ac-129">Examples</span><span class="sxs-lookup"><span data-stu-id="f38ac-129">Examples</span></span> | <span data-ttu-id="f38ac-130">Notes</span><span class="sxs-lookup"><span data-stu-id="f38ac-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f38ac-131">Environment</span><span class="sxs-lookup"><span data-stu-id="f38ac-131">Environment</span></span> |<span data-ttu-id="f38ac-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="f38ac-132">dev, stg, prod</span></span> |<span data-ttu-id="f38ac-133">Depending on the purpose and name of each environment.</span><span class="sxs-lookup"><span data-stu-id="f38ac-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="f38ac-134">Location</span><span class="sxs-lookup"><span data-stu-id="f38ac-134">Location</span></span> |<span data-ttu-id="f38ac-135">usw (West US), use (East US 2)</span><span class="sxs-lookup"><span data-stu-id="f38ac-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="f38ac-136">Depending on the region of the datacenter or the region of the organization.</span><span class="sxs-lookup"><span data-stu-id="f38ac-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="f38ac-137">Azure component, service, or product</span><span class="sxs-lookup"><span data-stu-id="f38ac-137">Azure component, service, or product</span></span> |<span data-ttu-id="f38ac-138">Rg for resource group, VNet for virtual network</span><span class="sxs-lookup"><span data-stu-id="f38ac-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="f38ac-139">Depending on the product for which the resource provides support.</span><span class="sxs-lookup"><span data-stu-id="f38ac-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="f38ac-140">Role</span><span class="sxs-lookup"><span data-stu-id="f38ac-140">Role</span></span> |<span data-ttu-id="f38ac-141">db, app, web</span><span class="sxs-lookup"><span data-stu-id="f38ac-141">db, app, web</span></span> |<span data-ttu-id="f38ac-142">Depending on the role of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f38ac-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="f38ac-143">Instance</span><span class="sxs-lookup"><span data-stu-id="f38ac-143">Instance</span></span> |<span data-ttu-id="f38ac-144">01, 02, 03, etc.</span><span class="sxs-lookup"><span data-stu-id="f38ac-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="f38ac-145">For resources that have more than one instance.</span><span class="sxs-lookup"><span data-stu-id="f38ac-145">For resources that have more than one instance.</span></span> <span data-ttu-id="f38ac-146">For example, load balanced web servers in a cloud service.</span><span class="sxs-lookup"><span data-stu-id="f38ac-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="f38ac-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span><span class="sxs-lookup"><span data-stu-id="f38ac-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="f38ac-148">Dates</span><span class="sxs-lookup"><span data-stu-id="f38ac-148">Dates</span></span>
<span data-ttu-id="f38ac-149">It is often important to determine the date of creation from the name of a resource.</span><span class="sxs-lookup"><span data-stu-id="f38ac-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="f38ac-150">We recommend the YYYYMMDD date format.</span><span class="sxs-lookup"><span data-stu-id="f38ac-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="f38ac-151">This format ensures that not only is the full date is recorded, but also that two resources whose names differ only on the date are sorted alphabetically and chronologically.</span><span class="sxs-lookup"><span data-stu-id="f38ac-151">This format ensures that not only is the full date is recorded, but also that two resources whose names differ only on the date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="f38ac-152">Naming resources</span><span class="sxs-lookup"><span data-stu-id="f38ac-152">Naming resources</span></span>
<span data-ttu-id="f38ac-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span><span class="sxs-lookup"><span data-stu-id="f38ac-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="f38ac-154">These rules should apply to all types of resources, for example:</span><span class="sxs-lookup"><span data-stu-id="f38ac-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="f38ac-155">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="f38ac-155">Subscriptions</span></span>
* <span data-ttu-id="f38ac-156">Accounts</span><span class="sxs-lookup"><span data-stu-id="f38ac-156">Accounts</span></span>
* <span data-ttu-id="f38ac-157">Storage accounts</span><span class="sxs-lookup"><span data-stu-id="f38ac-157">Storage accounts</span></span>
* <span data-ttu-id="f38ac-158">Virtual networks</span><span class="sxs-lookup"><span data-stu-id="f38ac-158">Virtual networks</span></span>
* <span data-ttu-id="f38ac-159">Subnets</span><span class="sxs-lookup"><span data-stu-id="f38ac-159">Subnets</span></span>
* <span data-ttu-id="f38ac-160">Availability sets</span><span class="sxs-lookup"><span data-stu-id="f38ac-160">Availability sets</span></span>
* <span data-ttu-id="f38ac-161">Resource groups</span><span class="sxs-lookup"><span data-stu-id="f38ac-161">Resource groups</span></span>
* <span data-ttu-id="f38ac-162">Virtual machines</span><span class="sxs-lookup"><span data-stu-id="f38ac-162">Virtual machines</span></span>
* <span data-ttu-id="f38ac-163">Endpoints</span><span class="sxs-lookup"><span data-stu-id="f38ac-163">Endpoints</span></span>
* <span data-ttu-id="f38ac-164">Network security groups</span><span class="sxs-lookup"><span data-stu-id="f38ac-164">Network security groups</span></span>
* <span data-ttu-id="f38ac-165">Roles</span><span class="sxs-lookup"><span data-stu-id="f38ac-165">Roles</span></span>

<span data-ttu-id="f38ac-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span><span class="sxs-lookup"><span data-stu-id="f38ac-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="f38ac-167">Computer names</span><span class="sxs-lookup"><span data-stu-id="f38ac-167">Computer names</span></span>
<span data-ttu-id="f38ac-168">When you create a virtual machine (VM), Azure requires a VM name of up to 64 characters that is used for the resource name.</span><span class="sxs-lookup"><span data-stu-id="f38ac-168">When you create a virtual machine (VM), Azure requires a VM name of up to 64 characters that is used for the resource name.</span></span> <span data-ttu-id="f38ac-169">Azure uses the same name for the operating system installed in the VM.</span><span class="sxs-lookup"><span data-stu-id="f38ac-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="f38ac-170">However, these names might not always be the same.</span><span class="sxs-lookup"><span data-stu-id="f38ac-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="f38ac-171">If a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span><span class="sxs-lookup"><span data-stu-id="f38ac-171">If a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="f38ac-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span><span class="sxs-lookup"><span data-stu-id="f38ac-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="f38ac-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span><span class="sxs-lookup"><span data-stu-id="f38ac-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="f38ac-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span><span class="sxs-lookup"><span data-stu-id="f38ac-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="f38ac-175">Storage account names</span><span class="sxs-lookup"><span data-stu-id="f38ac-175">Storage account names</span></span>
<span data-ttu-id="f38ac-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span><span class="sxs-lookup"><span data-stu-id="f38ac-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="f38ac-177">For unmanaged disks, storage accounts have special rules governing their names.</span><span class="sxs-lookup"><span data-stu-id="f38ac-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="f38ac-178">You can only use lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="f38ac-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="f38ac-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f38ac-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="f38ac-180">Additionally, the storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span><span class="sxs-lookup"><span data-stu-id="f38ac-180">Additionally, the storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="f38ac-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span><span class="sxs-lookup"><span data-stu-id="f38ac-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="f38ac-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f38ac-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="f38ac-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f38ac-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="f38ac-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f38ac-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="f38ac-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="f38ac-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

