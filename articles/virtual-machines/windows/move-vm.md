---
title: Move a Windows VM resource in Azure | Microsoft Docs
description: Move a Windows VM to another Azure subscription or resource group in the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2017
ms.author: cynthn
ms.openlocfilehash: b35fc321428694674e3992d26db6ff9c55b11de9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797620"
---
# <a name="move-a-windows-vm-to-another-azure-subscription-or-resource-group"></a><span data-ttu-id="bb82d-103">Move a Windows VM to another Azure subscription or resource group</span><span class="sxs-lookup"><span data-stu-id="bb82d-103">Move a Windows VM to another Azure subscription or resource group</span></span>
<span data-ttu-id="bb82d-104">This article walks you through how to move a Windows VM between resource groups or subscriptions.</span><span class="sxs-lookup"><span data-stu-id="bb82d-104">This article walks you through how to move a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="bb82d-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want to move it to your company's subscription to continue your work.</span><span class="sxs-lookup"><span data-stu-id="bb82d-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want to move it to your company's subscription to continue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="bb82d-106">You cannot move Managed Disks at this time.</span><span class="sxs-lookup"><span data-stu-id="bb82d-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="bb82d-107">New resource IDs are created as part of the move.</span><span class="sxs-lookup"><span data-stu-id="bb82d-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="bb82d-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span><span class="sxs-lookup"><span data-stu-id="bb82d-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-to-move-a-vm"></a><span data-ttu-id="bb82d-109">Use Powershell to move a VM</span><span class="sxs-lookup"><span data-stu-id="bb82d-109">Use Powershell to move a VM</span></span>

<span data-ttu-id="bb82d-110">To move a virtual machine to another resource group, you need to make sure that you also move all of the dependent resources.</span><span class="sxs-lookup"><span data-stu-id="bb82d-110">To move a virtual machine to another resource group, you need to make sure that you also move all of the dependent resources.</span></span> <span data-ttu-id="bb82d-111">To use the Move-AzureRMResource cmdlet, you need the ResourceId of each of the resources.</span><span class="sxs-lookup"><span data-stu-id="bb82d-111">To use the Move-AzureRMResource cmdlet, you need the ResourceId of each of the resources.</span></span> <span data-ttu-id="bb82d-112">You can get a list of the ResourceId's using the [Get-AzureRMResource](/powershell/module/azurerm.resources/get-azurermresource) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bb82d-112">You can get a list of the ResourceId's using the [Get-AzureRMResource](/powershell/module/azurerm.resources/get-azurermresource) cmdlet.</span></span>

```azurepowershell-interactive
 Get-AzureRMResource -ResourceGroupName <sourceResourceGroupName> | Format-table -Property ResourceId 
```

<span data-ttu-id="bb82d-113">To move a VM we need to move multiple resources.</span><span class="sxs-lookup"><span data-stu-id="bb82d-113">To move a VM we need to move multiple resources.</span></span> <span data-ttu-id="bb82d-114">We can use the output of Get-AzureRMResource to create a comma separated list of the ResourceIds and pass that to [Move-AzureRMResource](/powershell/module/azurerm.resources/move-azurermresource) to move them to the destination.</span><span class="sxs-lookup"><span data-stu-id="bb82d-114">We can use the output of Get-AzureRMResource to create a comma separated list of the ResourceIds and pass that to [Move-AzureRMResource](/powershell/module/azurerm.resources/move-azurermresource) to move them to the destination.</span></span> 

```azurepowershell-interactive

Move-AzureRmResource -DestinationResourceGroupName "<myDestinationResourceGroup>" `
    -ResourceId <myResourceId,myResourceId,myResourceId>
```
    
<span data-ttu-id="bb82d-115">To move the resources to different subscription, include the **-DestinationSubscriptionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="bb82d-115">To move the resources to different subscription, include the **-DestinationSubscriptionId** parameter.</span></span> 

```azurepowershell-interactive
Move-AzureRmResource -DestinationSubscriptionId "<myDestinationSubscriptionID>" `
    -DestinationResourceGroupName "<myDestinationResourceGroup>" `
    -ResourceId <myResourceId,myResourceId,myResourceId>
```


<span data-ttu-id="bb82d-116">You will be asked to confirm that you want to move the specified resources.</span><span class="sxs-lookup"><span data-stu-id="bb82d-116">You will be asked to confirm that you want to move the specified resources.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb82d-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb82d-117">Next steps</span></span>
<span data-ttu-id="bb82d-118">You can move many different types of resources between resource groups and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="bb82d-118">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="bb82d-119">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="bb82d-119">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

