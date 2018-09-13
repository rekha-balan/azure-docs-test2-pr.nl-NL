---
title: Move a Windows VM resource in Azure | Microsoft Docs
description: Move a Windows VM to another Azure subscription or resource group in the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: fc68ac2e2c471d60e82ba2bb1b53595f6b9a2326
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555548"
---
# <a name="move-a-windows-vm-to-another-azure-subscription-or-resource-group"></a><span data-ttu-id="3d6b5-103">Move a Windows VM to another Azure subscription or resource group</span><span class="sxs-lookup"><span data-stu-id="3d6b5-103">Move a Windows VM to another Azure subscription or resource group</span></span>
<span data-ttu-id="3d6b5-104">This article walks you through how to move a Windows VM between resource groups or subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-104">This article walks you through how to move a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="3d6b5-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want to move it to your company's subscription to continue your work.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want to move it to your company's subscription to continue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="3d6b5-106">You cannot move Managed Disks at this time.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="3d6b5-107">New resource IDs are created as part of the move.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="3d6b5-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-to-move-a-vm"></a><span data-ttu-id="3d6b5-109">Use Powershell to move a VM</span><span class="sxs-lookup"><span data-stu-id="3d6b5-109">Use Powershell to move a VM</span></span>
<span data-ttu-id="3d6b5-110">To move a virtual machine to another resource group, you need to make sure that you also move all of the dependent resources.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-110">To move a virtual machine to another resource group, you need to make sure that you also move all of the dependent resources.</span></span> <span data-ttu-id="3d6b5-111">To use the Move-AzureRMResource cmdlet, you need the resource name and the type of resource.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-111">To use the Move-AzureRMResource cmdlet, you need the resource name and the type of resource.</span></span> <span data-ttu-id="3d6b5-112">You can get both from the Find-AzureRMResource cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-112">You can get both from the Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="3d6b5-113">To move a VM we need to move multiple resources.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-113">To move a VM we need to move multiple resources.</span></span> <span data-ttu-id="3d6b5-114">We can just create separate variables for each resource and then list them.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="3d6b5-115">This example includes most of the basic resources for a VM, but you can add more as needed.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-115">This example includes most of the basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="3d6b5-116">To move the resources to different subscription, include the **-DestinationSubscriptionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-116">To move the resources to different subscription, include the **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="3d6b5-117">You will be asked to confirm that you want to move the specified resources.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-117">You will be asked to confirm that you want to move the specified resources.</span></span> <span data-ttu-id="3d6b5-118">Type **Y** to confirm that you want to move the resources.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-118">Type **Y** to confirm that you want to move the resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d6b5-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d6b5-119">Next steps</span></span>
<span data-ttu-id="3d6b5-120">You can move many different types of resources between resource groups and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3d6b5-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="3d6b5-121">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="3d6b5-121">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

