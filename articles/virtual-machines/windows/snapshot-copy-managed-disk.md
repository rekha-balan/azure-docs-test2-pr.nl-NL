---
title: Create a snapshot of a VHD in Azure | Microsoft Docs
description: Learn how to create a copy of an Azure VM to use as a back up or for troubleshooting issues.
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 04/10/2018
ms.author: cynthn
ms.openlocfilehash: 7cd7cd05b5a23b64d811d6ae9ffd9784cf67bf15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804627"
---
# <a name="create-a-snapshot"></a><span data-ttu-id="b0a49-103">Create a snapshot</span><span class="sxs-lookup"><span data-stu-id="b0a49-103">Create a snapshot</span></span>

<span data-ttu-id="b0a49-104">Take a snapshot of an OS or data disk VHD for backup or to troubleshoot VM issues.</span><span class="sxs-lookup"><span data-stu-id="b0a49-104">Take a snapshot of an OS or data disk VHD for backup or to troubleshoot VM issues.</span></span> <span data-ttu-id="b0a49-105">A snapshot is a full, read-only copy of a VHD.</span><span class="sxs-lookup"><span data-stu-id="b0a49-105">A snapshot is a full, read-only copy of a VHD.</span></span> 

## <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="b0a49-106">Use Azure portal to take a snapshot</span><span class="sxs-lookup"><span data-stu-id="b0a49-106">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="b0a49-107">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0a49-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b0a49-108">Starting in the upper left, click **Create a resource** and search for **snapshot**.</span><span class="sxs-lookup"><span data-stu-id="b0a49-108">Starting in the upper left, click **Create a resource** and search for **snapshot**.</span></span>
3. <span data-ttu-id="b0a49-109">In the Snapshot blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0a49-109">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="b0a49-110">Enter a **Name** for the snapshot.</span><span class="sxs-lookup"><span data-stu-id="b0a49-110">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="b0a49-111">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span><span class="sxs-lookup"><span data-stu-id="b0a49-111">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="b0a49-112">Select an Azure datacenter Location.</span><span class="sxs-lookup"><span data-stu-id="b0a49-112">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="b0a49-113">For **Source disk**, select the Managed Disk to snapshot.</span><span class="sxs-lookup"><span data-stu-id="b0a49-113">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="b0a49-114">Select the **Account type** to use to store the snapshot.</span><span class="sxs-lookup"><span data-stu-id="b0a49-114">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="b0a49-115">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span><span class="sxs-lookup"><span data-stu-id="b0a49-115">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="b0a49-116">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0a49-116">Click **Create**.</span></span>

## <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="b0a49-117">Use PowerShell to take a snapshot</span><span class="sxs-lookup"><span data-stu-id="b0a49-117">Use PowerShell to take a snapshot</span></span>

<span data-ttu-id="b0a49-118">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0a49-118">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="b0a49-119">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="b0a49-119">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="b0a49-120">This article requires the AzureRM module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="b0a49-120">This article requires the AzureRM module version 5.7.0 or later.</span></span> <span data-ttu-id="b0a49-121">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="b0a49-121">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="b0a49-122">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b0a49-122">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="b0a49-123">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a49-123">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

<span data-ttu-id="b0a49-124">Set some parameters.</span><span class="sxs-lookup"><span data-stu-id="b0a49-124">Set some parameters.</span></span> 

 ```azurepowershell-interactive
$resourceGroupName = 'myResourceGroup' 
$location = 'eastus' 
$vmName = 'myVM'
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="b0a49-125">Get the VM.</span><span class="sxs-lookup"><span data-stu-id="b0a49-125">Get the VM.</span></span>

 ```azurepowershell-interactive
$vm = get-azurermvm `
   -ResourceGroupName $resourceGroupName `
   -Name $vmName
```

<span data-ttu-id="b0a49-126">Create the snapshot configuration.</span><span class="sxs-lookup"><span data-stu-id="b0a49-126">Create the snapshot configuration.</span></span> <span data-ttu-id="b0a49-127">In this example, we are going to snapshot the OS disk.</span><span class="sxs-lookup"><span data-stu-id="b0a49-127">In this example, we are going to snapshot the OS disk.</span></span>

 ```azurepowershell-interactive
$snapshot =  New-AzureRmSnapshotConfig `
   -SourceUri $vm.StorageProfile.OsDisk.ManagedDisk.Id `
   -Location $location `
   -CreateOption copy
```
   
> [!NOTE]
> <span data-ttu-id="b0a49-128">If you would like to store your snapshot in zone-resilient storage, you need to create it in a region that supports [availability zones](../../availability-zones/az-overview.md) and include the `-SkuName Standard_ZRS` parameter.</span><span class="sxs-lookup"><span data-stu-id="b0a49-128">If you would like to store your snapshot in zone-resilient storage, you need to create it in a region that supports [availability zones](../../availability-zones/az-overview.md) and include the `-SkuName Standard_ZRS` parameter.</span></span>   

   
<span data-ttu-id="b0a49-129">Take the snapshot.</span><span class="sxs-lookup"><span data-stu-id="b0a49-129">Take the snapshot.</span></span>

```azurepowershell-interactive
New-AzureRmSnapshot `
   -Snapshot $snapshot `
   -SnapshotName $snapshotName `
   -ResourceGroupName $resourceGroupName 
```




## <a name="next-steps"></a><span data-ttu-id="b0a49-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0a49-130">Next steps</span></span>

<span data-ttu-id="b0a49-131">Create a virtual machine from a snapshot by creating a managed disk from a snapshot and then attaching the new managed disk as the OS disk.</span><span class="sxs-lookup"><span data-stu-id="b0a49-131">Create a virtual machine from a snapshot by creating a managed disk from a snapshot and then attaching the new managed disk as the OS disk.</span></span> <span data-ttu-id="b0a49-132">For more information, see the [Create a VM from a snapshot](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) sample.</span><span class="sxs-lookup"><span data-stu-id="b0a49-132">For more information, see the [Create a VM from a snapshot](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) sample.</span></span>
