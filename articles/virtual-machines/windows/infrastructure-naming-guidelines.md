---
title: Azure infrastructure naming guidelines - Windows | Microsoft Docs
description: Learn about the key design and implementation guidelines for naming in Azure infrastructure services.
documentationcenter: ''
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0100475d574722b169bb91ac59a50dab07e80b6f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551793"
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="4f00e-103">Azure infrastructure naming guidelines for Windows VMs</span><span class="sxs-lookup"><span data-stu-id="4f00e-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="4f00e-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span><span class="sxs-lookup"><span data-stu-id="4f00e-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="4f00e-105">Implementation guidelines for naming conventions</span><span class="sxs-lookup"><span data-stu-id="4f00e-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="4f00e-106">Decisions:</span><span class="sxs-lookup"><span data-stu-id="4f00e-106">Decisions:</span></span>

* <span data-ttu-id="4f00e-107">What are your naming conventions for Azure resources?</span><span class="sxs-lookup"><span data-stu-id="4f00e-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="4f00e-108">Tasks:</span><span class="sxs-lookup"><span data-stu-id="4f00e-108">Tasks:</span></span>

* <span data-ttu-id="4f00e-109">Define the affixes to use across your resources to maintain consistency.</span><span class="sxs-lookup"><span data-stu-id="4f00e-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="4f00e-110">Define storage account names given the requirement for them to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="4f00e-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="4f00e-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span><span class="sxs-lookup"><span data-stu-id="4f00e-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="4f00e-112">Naming conventions</span><span class="sxs-lookup"><span data-stu-id="4f00e-112">Naming conventions</span></span>
<span data-ttu-id="4f00e-113">You should have a good naming convention in place before creating anything in Azure.</span><span class="sxs-lookup"><span data-stu-id="4f00e-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="4f00e-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span><span class="sxs-lookup"><span data-stu-id="4f00e-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="4f00e-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span><span class="sxs-lookup"><span data-stu-id="4f00e-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="4f00e-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, when a team needs to work on a project on Azure, that model does not scale well.</span><span class="sxs-lookup"><span data-stu-id="4f00e-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, when a team needs to work on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="4f00e-117">Agree on a set of naming conventions up front.</span><span class="sxs-lookup"><span data-stu-id="4f00e-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="4f00e-118">There are some considerations regarding naming conventions that cut across this set of rules.</span><span class="sxs-lookup"><span data-stu-id="4f00e-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="4f00e-119">Affixes</span><span class="sxs-lookup"><span data-stu-id="4f00e-119">Affixes</span></span>
<span data-ttu-id="4f00e-120">As you look to define a naming convention, one decision comes whether the affix is at:</span><span class="sxs-lookup"><span data-stu-id="4f00e-120">As you look to define a naming convention, one decision comes whether the affix is at:</span></span>

* <span data-ttu-id="4f00e-121">The beginning of the name (prefix)</span><span class="sxs-lookup"><span data-stu-id="4f00e-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="4f00e-122">The end of the name (suffix)</span><span class="sxs-lookup"><span data-stu-id="4f00e-122">The end of the name (suffix)</span></span>

<span data-ttu-id="4f00e-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span><span class="sxs-lookup"><span data-stu-id="4f00e-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="4f00e-124">Rg-WebApp (prefix)</span><span class="sxs-lookup"><span data-stu-id="4f00e-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="4f00e-125">WebApp-Rg (suffix)</span><span class="sxs-lookup"><span data-stu-id="4f00e-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="4f00e-126">Affixes can refer to different aspects that describe the particular resources.</span><span class="sxs-lookup"><span data-stu-id="4f00e-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="4f00e-127">The following table shows some examples typically used.</span><span class="sxs-lookup"><span data-stu-id="4f00e-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="4f00e-128">Aspect</span><span class="sxs-lookup"><span data-stu-id="4f00e-128">Aspect</span></span> | <span data-ttu-id="4f00e-129">Examples</span><span class="sxs-lookup"><span data-stu-id="4f00e-129">Examples</span></span> | <span data-ttu-id="4f00e-130">Notes</span><span class="sxs-lookup"><span data-stu-id="4f00e-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4f00e-131">Environment</span><span class="sxs-lookup"><span data-stu-id="4f00e-131">Environment</span></span> |<span data-ttu-id="4f00e-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="4f00e-132">dev, stg, prod</span></span> |<span data-ttu-id="4f00e-133">Depending on the purpose and name of each environment.</span><span class="sxs-lookup"><span data-stu-id="4f00e-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="4f00e-134">Location</span><span class="sxs-lookup"><span data-stu-id="4f00e-134">Location</span></span> |<span data-ttu-id="4f00e-135">usw (West US), use (East US 2)</span><span class="sxs-lookup"><span data-stu-id="4f00e-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="4f00e-136">Depending on the region of the datacenter or the region of the organization.</span><span class="sxs-lookup"><span data-stu-id="4f00e-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="4f00e-137">Azure component, service, or product</span><span class="sxs-lookup"><span data-stu-id="4f00e-137">Azure component, service, or product</span></span> |<span data-ttu-id="4f00e-138">Rg for resource group, VNet for virtual network</span><span class="sxs-lookup"><span data-stu-id="4f00e-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="4f00e-139">Depending on the product for which the resource provides support.</span><span class="sxs-lookup"><span data-stu-id="4f00e-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="4f00e-140">Role</span><span class="sxs-lookup"><span data-stu-id="4f00e-140">Role</span></span> |<span data-ttu-id="4f00e-141">sql, ora, sp, iis</span><span class="sxs-lookup"><span data-stu-id="4f00e-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="4f00e-142">Depending on the role of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="4f00e-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="4f00e-143">Instance</span><span class="sxs-lookup"><span data-stu-id="4f00e-143">Instance</span></span> |<span data-ttu-id="4f00e-144">01, 02, 03, etc.</span><span class="sxs-lookup"><span data-stu-id="4f00e-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="4f00e-145">For resources that have more than one instance.</span><span class="sxs-lookup"><span data-stu-id="4f00e-145">For resources that have more than one instance.</span></span> <span data-ttu-id="4f00e-146">For example, load balanced web servers in a cloud service.</span><span class="sxs-lookup"><span data-stu-id="4f00e-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="4f00e-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span><span class="sxs-lookup"><span data-stu-id="4f00e-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="4f00e-148">Dates</span><span class="sxs-lookup"><span data-stu-id="4f00e-148">Dates</span></span>
<span data-ttu-id="4f00e-149">It is often important to determine the date of creation from the name of a resource.</span><span class="sxs-lookup"><span data-stu-id="4f00e-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="4f00e-150">We recommend the YYYYMMDD date format.</span><span class="sxs-lookup"><span data-stu-id="4f00e-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="4f00e-151">This format ensures that not only the full date is recorded, but also that two resources whose names differ only on the date is sorted alphabetically and chronologically at the same time.</span><span class="sxs-lookup"><span data-stu-id="4f00e-151">This format ensures that not only the full date is recorded, but also that two resources whose names differ only on the date is sorted alphabetically and chronologically at the same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="4f00e-152">Naming resources</span><span class="sxs-lookup"><span data-stu-id="4f00e-152">Naming resources</span></span>
<span data-ttu-id="4f00e-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span><span class="sxs-lookup"><span data-stu-id="4f00e-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="4f00e-154">These rules should apply to all types of resources, for example:</span><span class="sxs-lookup"><span data-stu-id="4f00e-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="4f00e-155">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="4f00e-155">Subscriptions</span></span>
* <span data-ttu-id="4f00e-156">Accounts</span><span class="sxs-lookup"><span data-stu-id="4f00e-156">Accounts</span></span>
* <span data-ttu-id="4f00e-157">Storage accounts</span><span class="sxs-lookup"><span data-stu-id="4f00e-157">Storage accounts</span></span>
* <span data-ttu-id="4f00e-158">Virtual networks</span><span class="sxs-lookup"><span data-stu-id="4f00e-158">Virtual networks</span></span>
* <span data-ttu-id="4f00e-159">Subnets</span><span class="sxs-lookup"><span data-stu-id="4f00e-159">Subnets</span></span>
* <span data-ttu-id="4f00e-160">Availability sets</span><span class="sxs-lookup"><span data-stu-id="4f00e-160">Availability sets</span></span>
* <span data-ttu-id="4f00e-161">Resource groups</span><span class="sxs-lookup"><span data-stu-id="4f00e-161">Resource groups</span></span>
* <span data-ttu-id="4f00e-162">Virtual machines</span><span class="sxs-lookup"><span data-stu-id="4f00e-162">Virtual machines</span></span>
* <span data-ttu-id="4f00e-163">Endpoints</span><span class="sxs-lookup"><span data-stu-id="4f00e-163">Endpoints</span></span>
* <span data-ttu-id="4f00e-164">Network security groups</span><span class="sxs-lookup"><span data-stu-id="4f00e-164">Network security groups</span></span>
* <span data-ttu-id="4f00e-165">Roles</span><span class="sxs-lookup"><span data-stu-id="4f00e-165">Roles</span></span>

<span data-ttu-id="4f00e-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span><span class="sxs-lookup"><span data-stu-id="4f00e-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="4f00e-167">Computer names</span><span class="sxs-lookup"><span data-stu-id="4f00e-167">Computer names</span></span>
<span data-ttu-id="4f00e-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up to 15 characters which is used for the resource name.</span><span class="sxs-lookup"><span data-stu-id="4f00e-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up to 15 characters which is used for the resource name.</span></span> <span data-ttu-id="4f00e-169">Azure uses the same name for the operating system installed in the VM.</span><span class="sxs-lookup"><span data-stu-id="4f00e-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="4f00e-170">However, these names might not always be the same.</span><span class="sxs-lookup"><span data-stu-id="4f00e-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="4f00e-171">In case a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span><span class="sxs-lookup"><span data-stu-id="4f00e-171">In case a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="4f00e-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span><span class="sxs-lookup"><span data-stu-id="4f00e-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="4f00e-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span><span class="sxs-lookup"><span data-stu-id="4f00e-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="4f00e-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span><span class="sxs-lookup"><span data-stu-id="4f00e-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="4f00e-175">Storage account names</span><span class="sxs-lookup"><span data-stu-id="4f00e-175">Storage account names</span></span>
<span data-ttu-id="4f00e-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span><span class="sxs-lookup"><span data-stu-id="4f00e-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="4f00e-177">For unmanaged disks, storage accounts have special rules governing their names.</span><span class="sxs-lookup"><span data-stu-id="4f00e-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="4f00e-178">You can only use lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="4f00e-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="4f00e-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4f00e-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="4f00e-180">Additionally, the storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span><span class="sxs-lookup"><span data-stu-id="4f00e-180">Additionally, the storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="4f00e-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span><span class="sxs-lookup"><span data-stu-id="4f00e-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="4f00e-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="4f00e-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="4f00e-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="4f00e-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="4f00e-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="4f00e-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f00e-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f00e-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

