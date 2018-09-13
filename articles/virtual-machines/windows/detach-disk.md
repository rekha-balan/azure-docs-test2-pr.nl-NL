---
title: Detach a data disk from a Windows VM - Azure| Microsoft Docs
description: Detach a data disk from a virtual machine in Azure using the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2018
ms.author: cynthn
ms.openlocfilehash: 0c00130a50ea5091432095d38978c16d509c5839
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800389"
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="e8ebc-103">How to detach a data disk from a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="e8ebc-103">How to detach a data disk from a Windows virtual machine</span></span>

<span data-ttu-id="e8ebc-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="e8ebc-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="e8ebc-106">If you detach a disk it is not automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="e8ebc-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="e8ebc-108">For more information, see [Pricing and Billing when using Premium Storage](premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="e8ebc-108">For more information, see [Pricing and Billing when using Premium Storage](premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="e8ebc-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>


## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="e8ebc-110">Detach a data disk using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8ebc-110">Detach a data disk using PowerShell</span></span>

<span data-ttu-id="e8ebc-111">You can *hot* remove a data disk using PowerShell, but make sure nothing is actively using the disk before detaching it from the VM.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-111">You can *hot* remove a data disk using PowerShell, but make sure nothing is actively using the disk before detaching it from the VM.</span></span>

<span data-ttu-id="e8ebc-112">In this example, we remove the disk named **myDisk** from the VM **myVM** in the **myResourceGroup** resource group.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-112">In this example, we remove the disk named **myDisk** from the VM **myVM** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="e8ebc-113">First you remove the disk using the [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-113">First you remove the disk using the [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk) cmdlet.</span></span> <span data-ttu-id="e8ebc-114">Then, you update the state of the virtual machine, using the [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm) cmdlet, to complete the process of removing the data disk.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-114">Then, you update the state of the virtual machine, using the [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm) cmdlet, to complete the process of removing the data disk.</span></span>

```azurepowershell-interactive
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "myDisk"
Update-AzureRmVM -ResourceGroupName "myResourceGroup" -VM $VirtualMachine
```

<span data-ttu-id="e8ebc-115">The disk stays in storage but is no longer attached to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-115">The disk stays in storage but is no longer attached to a virtual machine.</span></span>


## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="e8ebc-116">Detach a data disk using the portal</span><span class="sxs-lookup"><span data-stu-id="e8ebc-116">Detach a data disk using the portal</span></span>

1. <span data-ttu-id="e8ebc-117">In the left menu, select **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-117">In the left menu, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="e8ebc-118">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-118">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="e8ebc-119">In the virtual machine pane, select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-119">In the virtual machine pane, select **Disks**.</span></span>
4. <span data-ttu-id="e8ebc-120">At the top of the **Disks** pane, select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-120">At the top of the **Disks** pane, select **Edit**.</span></span>
5. <span data-ttu-id="e8ebc-121">In the **Disks** pane, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-121">In the **Disks** pane, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="e8ebc-122">After the disk has been removed, click **Save** on the top of the pane.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-122">After the disk has been removed, click **Save** on the top of the pane.</span></span>
6. <span data-ttu-id="e8ebc-123">In the virtual machine pane, click **Overview** and then click the **Start** button at the top of the pane to restart the VM.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-123">In the virtual machine pane, click **Overview** and then click the **Start** button at the top of the pane to restart the VM.</span></span>

<span data-ttu-id="e8ebc-124">The disk stays in storage but is no longer attached to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8ebc-124">The disk stays in storage but is no longer attached to a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8ebc-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8ebc-125">Next steps</span></span>
<span data-ttu-id="e8ebc-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e8ebc-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

