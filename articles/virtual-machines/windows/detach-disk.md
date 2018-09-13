---
title: Detach a data disk from a Windows VM - Azure| Microsoft Docs
description: Learn to detach a data disk from a virtual machine in Azure using the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 0c7dc17935b720a55b998c5267fd35dfd3233fd1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549484"
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="3f048-103">How to detach a data disk from a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="3f048-103">How to detach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="3f048-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span><span class="sxs-lookup"><span data-stu-id="3f048-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="3f048-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span><span class="sxs-lookup"><span data-stu-id="3f048-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="3f048-106">If you detach a disk it is not automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="3f048-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="3f048-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span><span class="sxs-lookup"><span data-stu-id="3f048-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="3f048-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="3f048-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="3f048-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span><span class="sxs-lookup"><span data-stu-id="3f048-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="3f048-110">Detach a data disk using the portal</span><span class="sxs-lookup"><span data-stu-id="3f048-110">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="3f048-111">In the portal hub, select **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="3f048-111">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="3f048-112">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span><span class="sxs-lookup"><span data-stu-id="3f048-112">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="3f048-113">In the virtual machine blade, select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="3f048-113">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="3f048-114">At the top of the **Disks** blade, select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="3f048-114">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="3f048-115">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/detach-disk/detach.png) detach button.</span><span class="sxs-lookup"><span data-stu-id="3f048-115">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="3f048-116">After the disk has been removed, click Save on the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="3f048-116">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="3f048-117">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span><span class="sxs-lookup"><span data-stu-id="3f048-117">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>



<span data-ttu-id="3f048-118">The disk remains in storage but is no longer attached to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3f048-118">The disk remains in storage but is no longer attached to a virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="3f048-119">Detach a data disk using PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f048-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="3f048-120">In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f048-120">In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="3f048-121">The command stores the virtual machine in the **$VirtualMachine** variable.</span><span class="sxs-lookup"><span data-stu-id="3f048-121">The command stores the virtual machine in the **$VirtualMachine** variable.</span></span> 

<span data-ttu-id="3f048-122">The second command removes the data disk named DataDisk3 from the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3f048-122">The second command removes the data disk named DataDisk3 from the virtual machine.</span></span> 

<span data-ttu-id="3f048-123">The final command updates the state of the virtual machine to complete the process of removing the data disk.</span><span class="sxs-lookup"><span data-stu-id="3f048-123">The final command updates the state of the virtual machine to complete the process of removing the data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" 
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="3f048-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="3f048-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f048-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f048-125">Next steps</span></span>
<span data-ttu-id="3f048-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3f048-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>


