---
title: Create a copy of an Azure Managed Disk for back up | Microsoft Docs
description: Learn how to create a copy of an Azure Managed Disk to use for back up or troubleshooting disk issues.
documentationcenter: ''
author: cwatsonMSFT
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: a759502172de07412268e139e8e31d61e1e7d46f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669991"
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="d5cfe-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span><span class="sxs-lookup"><span data-stu-id="d5cfe-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="d5cfe-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="d5cfe-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="d5cfe-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="d5cfe-107">For more information about Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d5cfe-107">For more information about Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="d5cfe-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="d5cfe-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d5cfe-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d5cfe-109">Before you begin</span></span>
<span data-ttu-id="d5cfe-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="d5cfe-111">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-111">Run the following command to install it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="d5cfe-112">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="d5cfe-112">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>

## <a name="copy-the-vhd-with-a-snapshot"></a><span data-ttu-id="d5cfe-113">Copy the VHD with a snapshot</span><span class="sxs-lookup"><span data-stu-id="d5cfe-113">Copy the VHD with a snapshot</span></span>
<span data-ttu-id="d5cfe-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span></span>

### <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="d5cfe-115">Use Azure portal to take a snapshot</span><span class="sxs-lookup"><span data-stu-id="d5cfe-115">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="d5cfe-116">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5cfe-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d5cfe-117">Starting in the upper left, click **New** and search for **snapshot**.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-117">Starting in the upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="d5cfe-118">In the Snapshot blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-118">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="d5cfe-119">Enter a **Name** for the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-119">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="d5cfe-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="d5cfe-121">Select an Azure datacenter Location.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="d5cfe-122">For **Source disk**, select the Managed Disk to snapshot.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-122">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="d5cfe-123">Select the **Account type** to use to store the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-123">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="d5cfe-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="d5cfe-125">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-125">Click **Create**.</span></span>

### <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="d5cfe-126">Use PowerShell to take a snapshot</span><span class="sxs-lookup"><span data-stu-id="d5cfe-126">Use PowerShell to take a snapshot</span></span>
<span data-ttu-id="d5cfe-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span></span> 

1. <span data-ttu-id="d5cfe-128">Set some parameters.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="d5cfe-129">Replace the parameter values:</span><span class="sxs-lookup"><span data-stu-id="d5cfe-129">Replace the parameter values:</span></span>
  -  <span data-ttu-id="d5cfe-130">"myResourceGroup" with the VM's resource group.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-130">"myResourceGroup" with the VM's resource group.</span></span>
  -  <span data-ttu-id="d5cfe-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="d5cfe-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span></span>
  -  <span data-ttu-id="d5cfe-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span></span>

2. <span data-ttu-id="d5cfe-134">Get the VHD disk to be copied.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-134">Get the VHD disk to be copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="d5cfe-135">Create the snapshot configurations.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-135">Create the snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="d5cfe-136">Take the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-136">Take the snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="d5cfe-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="d5cfe-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="d5cfe-139">Premium Managed Disks are more expensive than Standard.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="d5cfe-140">So be sure you really need Premium before using that parameter.</span><span class="sxs-lookup"><span data-stu-id="d5cfe-140">So be sure you really need Premium before using that parameter.</span></span>


