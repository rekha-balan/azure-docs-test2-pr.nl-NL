---
title: Move a Linux VM in Azure| Microsoft Docs
description: Move a Linux VM to another Azure subscription or resource group in the Resource Manager deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 12/14/2017
ms.author: cynthn
ms.openlocfilehash: 68010d543532ea3f6b1f3b5ed07b2652b5007627
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774923"
---
# <a name="move-a-linux-vm-to-another-subscription-or-resource-group"></a><span data-ttu-id="c238b-103">Move a Linux VM to another subscription or resource group</span><span class="sxs-lookup"><span data-stu-id="c238b-103">Move a Linux VM to another subscription or resource group</span></span>
<span data-ttu-id="c238b-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c238b-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="c238b-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span><span class="sxs-lookup"><span data-stu-id="c238b-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="c238b-106">You cannot move Managed Disks at this time.</span><span class="sxs-lookup"><span data-stu-id="c238b-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="c238b-107">New resource IDs are created as part of the move.</span><span class="sxs-lookup"><span data-stu-id="c238b-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="c238b-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span><span class="sxs-lookup"><span data-stu-id="c238b-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

## <a name="use-the-azure-cli-to-move-a-vm"></a><span data-ttu-id="c238b-109">Use the Azure CLI to move a VM</span><span class="sxs-lookup"><span data-stu-id="c238b-109">Use the Azure CLI to move a VM</span></span>


<span data-ttu-id="c238b-110">Before you can move your VM using the CLI, you need to make sure the source and destination subscriptions exist within the same tenant.</span><span class="sxs-lookup"><span data-stu-id="c238b-110">Before you can move your VM using the CLI, you need to make sure the source and destination subscriptions exist within the same tenant.</span></span> <span data-ttu-id="c238b-111">To check that both subscriptions have the same tenant ID, use [az account show](/cli/azure/account#az_account_show).</span><span class="sxs-lookup"><span data-stu-id="c238b-111">To check that both subscriptions have the same tenant ID, use [az account show](/cli/azure/account#az_account_show).</span></span>

```azurecli-interactive
az account show --subscription mySourceSubscription --query tenantId
az account show --subscription myDestinationSubscription --query tenantId
```
<span data-ttu-id="c238b-112">If the tenant IDs for the source and destination subscriptions are not the same, you must contact [support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) to move the resources to a new tenant.</span><span class="sxs-lookup"><span data-stu-id="c238b-112">If the tenant IDs for the source and destination subscriptions are not the same, you must contact [support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) to move the resources to a new tenant.</span></span>

<span data-ttu-id="c238b-113">To successfully move a VM, you need to move the VM and all its supporting resources.</span><span class="sxs-lookup"><span data-stu-id="c238b-113">To successfully move a VM, you need to move the VM and all its supporting resources.</span></span> <span data-ttu-id="c238b-114">Use the [az resource list](/cli/azure/resource#az_resource_list) command to list all the resources in a resource group and their IDs.</span><span class="sxs-lookup"><span data-stu-id="c238b-114">Use the [az resource list](/cli/azure/resource#az_resource_list) command to list all the resources in a resource group and their IDs.</span></span> <span data-ttu-id="c238b-115">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span><span class="sxs-lookup"><span data-stu-id="c238b-115">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span></span>

```azurecli-interactive
az resource list --resource-group "mySourceResourceGroup" --query "[].{Id:id}" --output table
```

<span data-ttu-id="c238b-116">To move a VM and its resources to another resource group, use [az resource move](/cli/azure/resource#az_resource_move).</span><span class="sxs-lookup"><span data-stu-id="c238b-116">To move a VM and its resources to another resource group, use [az resource move](/cli/azure/resource#az_resource_move).</span></span> <span data-ttu-id="c238b-117">The following example shows how to move a VM and the most common resources it requires.</span><span class="sxs-lookup"><span data-stu-id="c238b-117">The following example shows how to move a VM and the most common resources it requires.</span></span> <span data-ttu-id="c238b-118">Use the **-ids** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span><span class="sxs-lookup"><span data-stu-id="c238b-118">Use the **-ids** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span></span>

```azurecli-interactive
vm=/subscriptions/mySourceSubscriptionID/resourceGroups/mySourceResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
nic=/subscriptions/mySourceSubscriptionID/resourceGroups/mySourceResourceGroup/providers/Microsoft.Network/networkInterfaces/myNIC
nsg=/subscriptions/mySourceSubscriptionID/resourceGroups/mySourceResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNSG
pip=/subscriptions/mySourceSubscriptionID/resourceGroups/mySourceResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIPAddress
vnet=/subscriptions/mySourceSubscriptionID/resourceGroups/mySourceResourceGroup/providers/Microsoft.Network/virtualNetworks/myVNet
diag=/subscriptions/mySourceSubscriptionID/resourceGroups/mySourceResourceGroup/providers/Microsoft.Storage/storageAccounts/mydiagnosticstorageaccount
storage=/subscriptions/mySourceSubscriptionID/resourceGroups/mySourceResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageacountname    

az resource move \
    --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag \
    --destination-group "myDestinationResourceGroup"
```

<span data-ttu-id="c238b-119">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId** parameter to specify the destination subscription.</span><span class="sxs-lookup"><span data-stu-id="c238b-119">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId** parameter to specify the destination subscription.</span></span>

<span data-ttu-id="c238b-120">If you are asked to confirm that you want to move the specified resource.</span><span class="sxs-lookup"><span data-stu-id="c238b-120">If you are asked to confirm that you want to move the specified resource.</span></span> <span data-ttu-id="c238b-121">Type **Y** to confirm that you want to move the resources.</span><span class="sxs-lookup"><span data-stu-id="c238b-121">Type **Y** to confirm that you want to move the resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="c238b-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="c238b-122">Next steps</span></span>
<span data-ttu-id="c238b-123">You can move many different types of resources between resource groups and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c238b-123">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="c238b-124">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c238b-124">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

