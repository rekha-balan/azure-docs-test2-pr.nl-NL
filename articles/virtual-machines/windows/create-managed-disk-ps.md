---
title: Create a managed disk from a VHD in Azure| Microsoft Docs
description: Create a managed disk from a VHD that is currently in an Azure storage account, using the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 9ac1c37fcca239a816bcf660ce288a90d0a9f1d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670734"
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="6b63e-103">Create managed disks from unmanaged disks in a storage account</span><span class="sxs-lookup"><span data-stu-id="6b63e-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="6b63e-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="6b63e-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="6b63e-105">You can also crate an empty disk that can be used as a new data disk for a VM.</span><span class="sxs-lookup"><span data-stu-id="6b63e-105">You can also crate an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="6b63e-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="6b63e-106">Before you begin</span></span>
<span data-ttu-id="6b63e-107">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="6b63e-107">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="6b63e-108">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="6b63e-108">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="6b63e-109">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="6b63e-109">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="6b63e-110">Create a managed disk from a VHD in an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="6b63e-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="6b63e-111">In the example we create a disk from a VHD as managed disk and assign it to the parameter **$disk1** to use later.</span><span class="sxs-lookup"><span data-stu-id="6b63e-111">In the example we create a disk from a VHD as managed disk and assign it to the parameter **$disk1** to use later.</span></span> 

<span data-ttu-id="6b63e-112">The managed disk will be created in the **West-US** location, in a resource group named **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6b63e-112">The managed disk will be created in the **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="6b63e-113">The disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded to a storage account named **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="6b63e-113">The disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded to a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="6b63e-114">The managed disk will be created in premium locally-redundant storage (LRS).</span><span class="sxs-lookup"><span data-stu-id="6b63e-114">The managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="6b63e-115">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span><span class="sxs-lookup"><span data-stu-id="6b63e-115">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="6b63e-116">Set some parameters</span><span class="sxs-lookup"><span data-stu-id="6b63e-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="6b63e-117">Create the data disk.</span><span class="sxs-lookup"><span data-stu-id="6b63e-117">Create the data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="6b63e-118">Create an empty data disk as a managed disk</span><span class="sxs-lookup"><span data-stu-id="6b63e-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="6b63e-119">In the example we create an empty data disk as managed disk and assign it to the parameter **$dataDisk2** to use later.</span><span class="sxs-lookup"><span data-stu-id="6b63e-119">In the example we create an empty data disk as managed disk and assign it to the parameter **$dataDisk2** to use later.</span></span> <span data-ttu-id="6b63e-120">An empty data disk will need to be initialized logging in to the VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached to a running VM.</span><span class="sxs-lookup"><span data-stu-id="6b63e-120">An empty data disk will need to be initialized logging in to the VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached to a running VM.</span></span>

<span data-ttu-id="6b63e-121">The empty data disk will be created in the **West Central US** location, in a resource group named **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6b63e-121">The empty data disk will be created in the **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="6b63e-122">The disk will be named **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="6b63e-122">The disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="6b63e-123">The empty disk will be created in premium locally-redundant storage (LRS).</span><span class="sxs-lookup"><span data-stu-id="6b63e-123">The empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="6b63e-124">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span><span class="sxs-lookup"><span data-stu-id="6b63e-124">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="6b63e-125">The disk size in this example is 128GB, but you should choose a size that meets the needs of any applications running on your VM.</span><span class="sxs-lookup"><span data-stu-id="6b63e-125">The disk size in this example is 128GB, but you should choose a size that meets the needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="6b63e-126">Set some parameters</span><span class="sxs-lookup"><span data-stu-id="6b63e-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="6b63e-127">Create the data disk.</span><span class="sxs-lookup"><span data-stu-id="6b63e-127">Create the data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="6b63e-128">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6b63e-128">Next Steps</span></span>   
- <span data-ttu-id="6b63e-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b63e-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>