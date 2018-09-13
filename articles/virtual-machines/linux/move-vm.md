---
title: Move a Linux VM in Azure| Microsoft Docs
description: Move a Linux VM to another Azure subscription or resource group in the Resource Manager deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 4fd19a6ee4e5f7285dbb338d9e4c7bd3c0572d12
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553907"
---
# <a name="move-a-linux-vm-to-another-subscription-or-resource-group"></a><span data-ttu-id="b4c23-103">Move a Linux VM to another subscription or resource group</span><span class="sxs-lookup"><span data-stu-id="b4c23-103">Move a Linux VM to another subscription or resource group</span></span>
<span data-ttu-id="b4c23-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b4c23-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="b4c23-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span><span class="sxs-lookup"><span data-stu-id="b4c23-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="b4c23-106">You cannot move Managed Disks at this time.</span><span class="sxs-lookup"><span data-stu-id="b4c23-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="b4c23-107">New resource IDs are created as part of the move.</span><span class="sxs-lookup"><span data-stu-id="b4c23-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="b4c23-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span><span class="sxs-lookup"><span data-stu-id="b4c23-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

## <a name="use-the-azure-cli-to-move-a-vm"></a><span data-ttu-id="b4c23-109">Use the Azure CLI to move a VM</span><span class="sxs-lookup"><span data-stu-id="b4c23-109">Use the Azure CLI to move a VM</span></span>
<span data-ttu-id="b4c23-110">To successfully move a VM, you need to move the VM and all its supporting resources.</span><span class="sxs-lookup"><span data-stu-id="b4c23-110">To successfully move a VM, you need to move the VM and all its supporting resources.</span></span> <span data-ttu-id="b4c23-111">Use the **azure group show** command to list all the resources in a resource group and their IDs.</span><span class="sxs-lookup"><span data-stu-id="b4c23-111">Use the **azure group show** command to list all the resources in a resource group and their IDs.</span></span> <span data-ttu-id="b4c23-112">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span><span class="sxs-lookup"><span data-stu-id="b4c23-112">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="b4c23-113">To move a VM and its resources to another resource group, use the **azure resource move** CLI command.</span><span class="sxs-lookup"><span data-stu-id="b4c23-113">To move a VM and its resources to another resource group, use the **azure resource move** CLI command.</span></span> <span data-ttu-id="b4c23-114">The following example shows how to move a VM and the most common resources it requires.</span><span class="sxs-lookup"><span data-stu-id="b4c23-114">The following example shows how to move a VM and the most common resources it requires.</span></span> <span data-ttu-id="b4c23-115">We use the **-i** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span><span class="sxs-lookup"><span data-stu-id="b4c23-115">We use the **-i** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="b4c23-116">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter to specify the destination subscription.</span><span class="sxs-lookup"><span data-stu-id="b4c23-116">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter to specify the destination subscription.</span></span>

<span data-ttu-id="b4c23-117">If you are working from the Command Prompt on a Windows computer, you need to add a **$** in front of the variable names when you declare them.</span><span class="sxs-lookup"><span data-stu-id="b4c23-117">If you are working from the Command Prompt on a Windows computer, you need to add a **$** in front of the variable names when you declare them.</span></span> <span data-ttu-id="b4c23-118">This isn't needed in Linux.</span><span class="sxs-lookup"><span data-stu-id="b4c23-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="b4c23-119">You are asked to confirm that you want to move the specified resource.</span><span class="sxs-lookup"><span data-stu-id="b4c23-119">You are asked to confirm that you want to move the specified resource.</span></span> <span data-ttu-id="b4c23-120">Type **Y** to confirm that you want to move the resources.</span><span class="sxs-lookup"><span data-stu-id="b4c23-120">Type **Y** to confirm that you want to move the resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="b4c23-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4c23-121">Next steps</span></span>
<span data-ttu-id="b4c23-122">You can move many different types of resources between resource groups and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b4c23-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="b4c23-123">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b4c23-123">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

