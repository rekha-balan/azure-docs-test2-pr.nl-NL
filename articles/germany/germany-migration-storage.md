---
title: Migration from Azure Germany storage resources to global Azure
description: This article provides help for migrating storage resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 7a856290962d0c699a34e020852462604fe253d7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969006"
---
# <a name="migration-from-azure-germany-storage-resources-to-global-azure"></a><span data-ttu-id="ccf4e-103">Migration from Azure Germany storage resources to global Azure</span><span class="sxs-lookup"><span data-stu-id="ccf4e-103">Migration from Azure Germany storage resources to global Azure</span></span>

<span data-ttu-id="ccf4e-104">This article will provide you some help for the migration of Azure Storage resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-104">This article will provide you some help for the migration of Azure Storage resources from Azure Germany to global Azure.</span></span>

## <a name="blobs"></a><span data-ttu-id="ccf4e-105">Blobs</span><span class="sxs-lookup"><span data-stu-id="ccf4e-105">Blobs</span></span>

<span data-ttu-id="ccf4e-106">AzCopy is a free tool to help you copy blobs, files, and tables.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-106">AzCopy is a free tool to help you copy blobs, files, and tables.</span></span> <span data-ttu-id="ccf4e-107">AzCopy works from Azure to Azure, from on-premise to Azure and from Azure to on-premise.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-107">AzCopy works from Azure to Azure, from on-premise to Azure and from Azure to on-premise.</span></span> <span data-ttu-id="ccf4e-108">Use AzCopy for your migration to copy blobs directly between Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-108">Use AzCopy for your migration to copy blobs directly between Azure Germany to global Azure.</span></span>

<span data-ttu-id="ccf4e-109">If you have non-managed disks for your source VM, use AzCopy to copy the `.vhd` files to the target environment.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-109">If you have non-managed disks for your source VM, use AzCopy to copy the `.vhd` files to the target environment.</span></span> <span data-ttu-id="ccf4e-110">Otherwise, you need some steps in advance, see [recommendations for Managed Disks](#managed-disks) further down.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-110">Otherwise, you need some steps in advance, see [recommendations for Managed Disks](#managed-disks) further down.</span></span>

<span data-ttu-id="ccf4e-111">Here's a short example how AzCopy works, for a complete reference look at the [AzCopy documentation](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="ccf4e-111">Here's a short example how AzCopy works, for a complete reference look at the [AzCopy documentation](../storage/common/storage-use-azcopy.md).</span></span>

<span data-ttu-id="ccf4e-112">AzCopy uses the terms *Source* and *Dest*, expressed as URIs.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-112">AzCopy uses the terms *Source* and *Dest*, expressed as URIs.</span></span> <span data-ttu-id="ccf4e-113">URIs for Azure Germany always have this format:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-113">URIs for Azure Germany always have this format:</span></span>

```http
https://<storageaccountname>.blob.core.cloudapi.de/<containername>/<blobname>
```

<span data-ttu-id="ccf4e-114">and for global Azure:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-114">and for global Azure:</span></span>

```http
https://<storageaccountname>.blob.core.windows.net/<containername>/<blobname>
```

<span data-ttu-id="ccf4e-115">You get the three parts (*storageaccountname*, *containername*, *blobname*) for the URI from the portal, with PowerShell, or with CLI.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-115">You get the three parts (*storageaccountname*, *containername*, *blobname*) for the URI from the portal, with PowerShell, or with CLI.</span></span> <span data-ttu-id="ccf4e-116">The name of the blob can be part of the URI or given as a pattern, like *vm121314.vhd*.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-116">The name of the blob can be part of the URI or given as a pattern, like *vm121314.vhd*.</span></span>

<span data-ttu-id="ccf4e-117">You also need the storage account keys to access the storage account.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-117">You also need the storage account keys to access the storage account.</span></span> <span data-ttu-id="ccf4e-118">Get them from the portal, PowerShell, or CLI.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-118">Get them from the portal, PowerShell, or CLI.</span></span> <span data-ttu-id="ccf4e-119">For example:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-119">For example:</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name <saname> -ResourceGroupName <rgname>
```

<span data-ttu-id="ccf4e-120">As always, you need only one of the two keys available for each storage account.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-120">As always, you need only one of the two keys available for each storage account.</span></span>

<span data-ttu-id="ccf4e-121">Example:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-121">Example:</span></span>
<span data-ttu-id="ccf4e-122">URI part</span><span class="sxs-lookup"><span data-stu-id="ccf4e-122">URI part</span></span> | <span data-ttu-id="ccf4e-123">example value</span><span class="sxs-lookup"><span data-stu-id="ccf4e-123">example value</span></span>
-------- | --------------
<span data-ttu-id="ccf4e-124">Source storageAccount</span><span class="sxs-lookup"><span data-stu-id="ccf4e-124">Source storageAccount</span></span> | `migratetest`
<span data-ttu-id="ccf4e-125">Source container</span><span class="sxs-lookup"><span data-stu-id="ccf4e-125">Source container</span></span> | `vhds`
<span data-ttu-id="ccf4e-126">Source blob</span><span class="sxs-lookup"><span data-stu-id="ccf4e-126">Source blob</span></span> | `vm-121314.vhd`
<span data-ttu-id="ccf4e-127">Target storageAccount</span><span class="sxs-lookup"><span data-stu-id="ccf4e-127">Target storageAccount</span></span> | `migratetarget`
<span data-ttu-id="ccf4e-128">Target container</span><span class="sxs-lookup"><span data-stu-id="ccf4e-128">Target container</span></span> | `targetcontainer`

<span data-ttu-id="ccf4e-129">This command copies a virtual hard disk from Azure Germany to global Azure (keys are shortened for better readability):</span><span class="sxs-lookup"><span data-stu-id="ccf4e-129">This command copies a virtual hard disk from Azure Germany to global Azure (keys are shortened for better readability):</span></span>

```cmd
azcopy -v /source:https://migratetest.blob.core.cloudapi.de/vhds /sourcekey:"0LN...w==" /dest:https://migratetarget.blob.core.windows.net/targetcontainer /DestKey:"o//ucDi5TN...w==" /Pattern:vm-121314.vhd
```

To get a consistent copy of the VHD, shutdown the VM before copying and plan some downtime. <span data-ttu-id="ccf4e-131">When copied, [follow these instructions](../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to rebuild your VM in the target environment.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-131">When copied, [follow these instructions](../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to rebuild your VM in the target environment.</span></span>

### <a name="links"></a><span data-ttu-id="ccf4e-132">Links</span><span class="sxs-lookup"><span data-stu-id="ccf4e-132">Links</span></span>

- [<span data-ttu-id="ccf4e-133">AzCopy Documentation</span><span class="sxs-lookup"><span data-stu-id="ccf4e-133">AzCopy Documentation</span></span>](../storage/common/storage-use-azcopy.md)
- [<span data-ttu-id="ccf4e-134">Create VM from restored disks</span><span class="sxs-lookup"><span data-stu-id="ccf4e-134">Create VM from restored disks</span></span>](../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks)















## <a name="disks"></a><span data-ttu-id="ccf4e-135">Disks</span><span class="sxs-lookup"><span data-stu-id="ccf4e-135">Disks</span></span>

<span data-ttu-id="ccf4e-136">Azure Managed Disks simplifies disk management for Azure IaaS VMs by managing the storage accounts associated with the VM disk.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-136">Azure Managed Disks simplifies disk management for Azure IaaS VMs by managing the storage accounts associated with the VM disk.</span></span> <span data-ttu-id="ccf4e-137">Since you don't have direct access to the `.vhd`, you can't directly use tools like AzCopy (see [Storage Migration](#blobs) to copy your files.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-137">Since you don't have direct access to the `.vhd`, you can't directly use tools like AzCopy (see [Storage Migration](#blobs) to copy your files.</span></span> <span data-ttu-id="ccf4e-138">The workaround is to first export the managed disk by getting a temporary SAS URI and to download or copy it with this information.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-138">The workaround is to first export the managed disk by getting a temporary SAS URI and to download or copy it with this information.</span></span> <span data-ttu-id="ccf4e-139">Here's a short example how to get the SAS URI and what to do with it:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-139">Here's a short example how to get the SAS URI and what to do with it:</span></span>

### <a name="step-1-get-sas-uri"></a><span data-ttu-id="ccf4e-140">Step 1: Get SAS URI</span><span class="sxs-lookup"><span data-stu-id="ccf4e-140">Step 1: Get SAS URI</span></span>

- <span data-ttu-id="ccf4e-141">Go to the portal, search for your managed disk (in the same resource group as your VM, the resource type is "Disk").</span><span class="sxs-lookup"><span data-stu-id="ccf4e-141">Go to the portal, search for your managed disk (in the same resource group as your VM, the resource type is "Disk").</span></span>
- <span data-ttu-id="ccf4e-142">In the `Overview`, look for the `Export` button in the top ribbon, and click it (you have to shut down and deallocate your VM first, or unattach it).</span><span class="sxs-lookup"><span data-stu-id="ccf4e-142">In the `Overview`, look for the `Export` button in the top ribbon, and click it (you have to shut down and deallocate your VM first, or unattach it).</span></span>
- <span data-ttu-id="ccf4e-143">Define a time when the URI expires (default is 3600 seconds)</span><span class="sxs-lookup"><span data-stu-id="ccf4e-143">Define a time when the URI expires (default is 3600 seconds)</span></span>
- <span data-ttu-id="ccf4e-144">Generate URL (should only take a few seconds)</span><span class="sxs-lookup"><span data-stu-id="ccf4e-144">Generate URL (should only take a few seconds)</span></span>
- <span data-ttu-id="ccf4e-145">Copy the URL (displayed only once)</span><span class="sxs-lookup"><span data-stu-id="ccf4e-145">Copy the URL (displayed only once)</span></span>

### <a name="step-2-azcopy"></a><span data-ttu-id="ccf4e-146">Step 2: AzCopy</span><span class="sxs-lookup"><span data-stu-id="ccf4e-146">Step 2: AzCopy</span></span>

<span data-ttu-id="ccf4e-147">Examples on how to use AzCopy are provided further up this article at [Blob Migration](#blobs).</span><span class="sxs-lookup"><span data-stu-id="ccf4e-147">Examples on how to use AzCopy are provided further up this article at [Blob Migration](#blobs).</span></span> <span data-ttu-id="ccf4e-148">Use it (or an other tool) to copy the disk directly from your source environment to the target environment.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-148">Use it (or an other tool) to copy the disk directly from your source environment to the target environment.</span></span> <span data-ttu-id="ccf4e-149">For AzCopy, you have to split the URI into the base URI and the SAS part starting with the character "?".</span><span class="sxs-lookup"><span data-stu-id="ccf4e-149">For AzCopy, you have to split the URI into the base URI and the SAS part starting with the character "?".</span></span> <span data-ttu-id="ccf4e-150">If this is the SAS URI the portal provides:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-150">If this is the SAS URI the portal provides:</span></span>

```http
https://md-kp4qvrzhj4j5.blob.core.cloudapi.de/r0pmw4z3vk1g/abcd?sv=2017-04-17&sr=b&si=22970153-4c56-47c0-8cbb-156a24b6e4b5&sig=5Hfu0qMw9rkZf6mCjuCE4VMV6W3IR8FXQSY1viji9bg%3D>
```

<span data-ttu-id="ccf4e-151">The source parameters for AzCopy would be:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-151">The source parameters for AzCopy would be:</span></span>

```cmd
/source:"https://md-kp4qvrzhj4j5.blob.core.cloudapi.de/r0pmw4z3vk1g/abcd"
```

<span data-ttu-id="ccf4e-152">and</span><span class="sxs-lookup"><span data-stu-id="ccf4e-152">and</span></span>

```cmd
/sourceSAS:" ?sv=2017-04-17&sr=b&si=22970153-4c56-47c0-8cbb-156a24b6e4b5&sig=5Hfu0qMw9rkZf6mCjuCE4VMV6W3IR8FXQSY1viji9bg%3D"
```

<span data-ttu-id="ccf4e-153">And the complete command line:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-153">And the complete command line:</span></span>

```cmd
azcopy -v /source:"https://md-kp4qvrzhj4j5.blob.core.cloudapi.de/r0pmw4z3vk1g/abcd" /sourceSAS:"?sv=2017-04-17&sr=b&si=22970153-4c56-47c0-8cbb-156a24b6e4b5&sig=5Hfu0qMw9rkZf6mCjuCE4VMV6W3IR8FXQSY1viji9bg%3D" /dest:"https://migratetarget.blob.core.windows.net/targetcontainer/newdisk.vhd" /DestKey:"o//ucD... Kdpw=="
```

### <a name="step-3-create-a-new-managed-disk-in-the-target-environment"></a><span data-ttu-id="ccf4e-154">Step 3: Create a new managed disk in the target environment</span><span class="sxs-lookup"><span data-stu-id="ccf4e-154">Step 3: Create a new managed disk in the target environment</span></span>

<span data-ttu-id="ccf4e-155">There are several options to create a new managed disk, for example via portal:</span><span class="sxs-lookup"><span data-stu-id="ccf4e-155">There are several options to create a new managed disk, for example via portal:</span></span>

- <span data-ttu-id="ccf4e-156">In the portal, select `New` > `Managed Disk` > `Create`.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-156">In the portal, select `New` > `Managed Disk` > `Create`.</span></span>
- <span data-ttu-id="ccf4e-157">Give the new disk a name</span><span class="sxs-lookup"><span data-stu-id="ccf4e-157">Give the new disk a name</span></span>
- <span data-ttu-id="ccf4e-158">select a resource group as usual</span><span class="sxs-lookup"><span data-stu-id="ccf4e-158">select a resource group as usual</span></span>
- <span data-ttu-id="ccf4e-159">Under `Source type`, select *Storage blob* and either copy the destination URI from the AzCopy command, or browse to select.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-159">Under `Source type`, select *Storage blob* and either copy the destination URI from the AzCopy command, or browse to select.</span></span>
- <span data-ttu-id="ccf4e-160">If you copied an OS disk, choose the OS type, otherwise click `Create`.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-160">If you copied an OS disk, choose the OS type, otherwise click `Create`.</span></span>

### <a name="step-4-create-the-vm"></a><span data-ttu-id="ccf4e-161">Step 4: create the VM</span><span class="sxs-lookup"><span data-stu-id="ccf4e-161">Step 4: create the VM</span></span>

<span data-ttu-id="ccf4e-162">Again, there are various ways to create a VM with this new managed disk.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-162">Again, there are various ways to create a VM with this new managed disk.</span></span>

<span data-ttu-id="ccf4e-163">In the portal, select the disk and click `Create VM` at the top ribbon.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-163">In the portal, select the disk and click `Create VM` at the top ribbon.</span></span> <span data-ttu-id="ccf4e-164">Define the other parameters of your VM as usual.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-164">Define the other parameters of your VM as usual.</span></span>

<span data-ttu-id="ccf4e-165">For PowerShell follow [this article](../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create a VM from a restored disk.</span><span class="sxs-lookup"><span data-stu-id="ccf4e-165">For PowerShell follow [this article](../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create a VM from a restored disk.</span></span>

### <a name="links"></a><span data-ttu-id="ccf4e-166">Links</span><span class="sxs-lookup"><span data-stu-id="ccf4e-166">Links</span></span>

- <span data-ttu-id="ccf4e-167">Export to disk [via API](/rest/api/compute/disks/grantaccess.md) by getting a SAS URI</span><span class="sxs-lookup"><span data-stu-id="ccf4e-167">Export to disk [via API](/rest/api/compute/disks/grantaccess.md) by getting a SAS URI</span></span> 
- <span data-ttu-id="ccf4e-168">Create a managed disk [via API](/rest/api/compute/disks/createorupdate.md#create_a_managed_disk_by_importing_an_unmanaged_blob_from_a_different_subscription) from an unmanaged blob</span><span class="sxs-lookup"><span data-stu-id="ccf4e-168">Create a managed disk [via API](/rest/api/compute/disks/createorupdate.md#create_a_managed_disk_by_importing_an_unmanaged_blob_from_a_different_subscription) from an unmanaged blob</span></span>
